最近在项目中经常用到UITableView中的cell中带有UITextField或UITextView的情况，然后在这种场景下，当我们点击屏幕较下方的cell进行编辑时，这时候键盘弹出来会出现遮挡待输入的cell，导致我们无法很方便地查看到我们输入的内容，这样的体验是非常不好的。这个问题在之前我们的随笔iOS学习——键盘弹出遮挡输入框问题解决方案中也有讲过对应的解决方案，但是该方案在最近的应用中还有点小问题，我们在这里重新进行处理好。

### 一 主控制器为UITableViewController或其子类

　　首先，有一个很简单的解决方案，就是将我们的控制器换成UITableViewController或其子类，UITableViewController中的cell当有键盘弹出的时候表单整体会自动进行上移，我们需要编辑的区域正好可以在键盘的上方，这样我们正好也可以看到我们编辑的内容，方便我们进行修改和调整具体内容。

　　但是，如果我们的整体布局并不是只有一个UITableView，或者我们在项目中需要用到MBProgressHUD框架时，我们可能就不能直接将我们的控制器设置成UITableViewController或其子类，因为MBProgressHUD框架在UITableViewController和UICollectionViewController中显示会存在一些bug，在GitHub中的MBProgressHUD框架官方文档中就有提到要避免将HUD添加到具有复杂视图层次结构的某些UIKit视图（如UITableView或UICollectionView），UITableViewController和UICollectionViewController中的self.view实际上就是对应的UITableView或UICollectionView，所以会出现一些莫名其妙的bug，显示不出来或者显示的位置不对。



### 二 主控制器为UIViewController或其子类
　　其实最开始我就是用的UITableViewController，结果要提示的要提示的tips总是显示不设定的位置上，后来才得以发现的这个bug，我也很无奈，我们的项目汇总因为用到了MBProgressHUD框架，所以只能是用UIViewController上布局一个UITableView来实现，这样我们再self.view上布局MBProgressHUD时才避开了UITableView或UICollectionView，然后就都没问题了。言归正传，下面就说回到我们要解决的问题，在UITableView的cell中，系统自带的UITableViewCell的格式没有自带UITextField或UITextView这种可以编辑的区域的，而这种类型的cell在我们的项目开发包中经常要用到，所以我们就需要对这类cell进行封装和自定义。

#### 2.1 UITextField或UITextView点击之后的详细流程

　　在对cell进行封装和自定义的时候，我们需要考虑我们的UITextField或UITextView从点击编辑框到结束编辑的整个过程是怎么样的，在这个过程中我们需要回传什么信息，才能保证我们的可以对我们控制器中的tableview进行控制。下面的流程就是UITextField或UITextView在整个编辑过程中的详细流程步骤：

在成为第一响应者之前，文本框调用其代理的textFieldShouldBeginEditing:  方法来允许或阻止其第一响应者，并控制是否对文本框进行输入
成为第一响应者，对应的相应事件就是系统调用键盘（自动弹出），并且系统会根据需要发出`UIKeyboardWillShowNotification` 和`UIKeyboardDidShowNotification的Notification`通知，而如果此时系统中有其他的输入视图是可视的，则系统会发出 `UIKeyboardWillChangeFrameNotification`和`UIKeyboardDidChangeFrameNotification`的通知
系统调用代理的 textFieldDidBeginEditing:  方法，并且发出`UITextFieldTextDidBeginEditingNotification`的通知，此时光标已经在text field中定位了，键盘也已经弹出来了，接下来可以进行输入了
在输入信息过程中，当前文本内容改变就会调用，textField:shouldChangeCharactersInRange:replacementString: 方法，并且会发出`UITextFieldTextDidChangeNotification`的通知。此外，当用户点击【clear/清除】按键时调用 textFieldShouldClear: 方法清除内容，当用户点击【return/完成】按键时调用 textFieldShouldReturn: 方法，注意：UITextViewDelegate没有对应清除和完成方法，所以我们不能调用textFieldShouldClear: 方法和 textFieldShouldReturn： 方法实现【clear/清除】和【return/完成】按键的效果 
在文本框输入即将结束，即即将注销第一响应者时，系统会调用 textFieldShouldEndEditing: 方法
文本框注销第一响应者，对应的响应时间就是系统收回键盘，并且在隐藏键盘时会发出 `UIKeyboardWillHideNotification`和`UIKeyboardDidHideNotification`的通知
最后，系统调用 textFieldDidEndEditing:  方法结束输入，并发出`UITextFieldTextDidEndEditingNotification`的通知。

#### 2.2 自定义包含UITextField的UITableViewCell

　　首先，我们在点击编辑区域的时候，获取到当前编辑区域相对屏幕的位置，这样方便我们判断整个tableview是否需要上移以及需要上移多少比较合适。当然，我们自定义的cell中的UITextField或UITextView的代理设为cell自己，具体实现如下：
　　
　　
　　
```
#import <UIKit/UIKit.h>

typedef void(^ContentEditResultBlock)(NSString *contentString);
typedef void(^ContentStartEditBlock)(CGRect frameToView);

@interface BasicCell : UITableViewCell

@property (copy, nonatomic) NSString *title;        //左侧标题栏
@property (copy, nonatomic) NSString *placeHolder;  //没有内容时的提示
@property (copy, nonatomic) NSString *content;      //内容
@property (assign, nonatomic) BOOL isForbidEdit;    //是否允许编辑
@property (assign, nonatomic) BOOL isHiddenLine;    //是否隐藏分割线
//编辑结束时的回调
@property (copy, nonatomic) ContentEditResultBlock contentEditResultBlock;
//编辑开始时的回调
@property (copy, nonatomic) ContentStartEditBlock contentStartEditBlock;

@end

```

 　　在这里，我们定义了两个回调block，分别在编辑区域开始编辑(textFieldDidBeginEditing: )和结束编辑(textFieldDidEndEditing: )的时候调用，开始编辑的时候返回当前cell相对屏幕的位置方便我们控制是否上移tableview，结束编辑时返回我们编辑框的内容方便进行记录。具体实现的代码如下：
 　　
 　```

  1 #import "BasicCell.h"
  2 @interface BasicCell () <UITextFieldDelegate>
  3 @property (strong, nonatomic) UILabel *titleLabel;          //标题栏
  4 @property (strong, nonatomic) UITextField *contentField;    //内容栏
  5 @property (strong, nonatomic) UIView *lineView;             //分割线
  6 
  7 @end
  8 
  9 @implementation CJMeetingReplyBasicCell
 10 
 11 - (instancetype)initWithStyle:(UITableViewCellStyle)style reuseIdentifier:(NSString *)reuseIdentifier{
 12     self = [super initWithStyle:style reuseIdentifier:reuseIdentifier];
 13     CGFloat fontSize = 16.0f;
 14     if (IS_IPHONE_5 || IS_IPHONE_5S) {
 15         fontSize = 15.0f;
 16     } else {
 17         fontSize = 16.0f;
 18     }
 19     //标题栏 配置
 20     _titleLabel = [[UILabel alloc] init];
 21     _titleLabel.font = FONT(fontSize);
 22     _titleLabel.textColor = kGrayFontColor;
 23     //内容栏 配置
 24     _contentField = [[UITextField alloc] init];
 25     _contentField.font = FONT(fontSize);
 26     _contentField.textColor = kBlackFontColor;
 27     _contentField.textAlignment = NSTextAlignmentRight;
 28     _contentField.returnKeyType = UIReturnKeyDone;
 29     _contentField.delegate = self;
 30     //分割线 配置
 31     _lineView = [[UIView alloc] init];
 32     _lineView.backgroundColor = kLineColor;
 33     //添加到 cell中
 34     [self addSubview:_titleLabel];
 35     [self addSubview:_contentField];
 36     [self addSubview:_lineView];
 37     //布局
 38     WEAKSELF
 39     CGFloat ratio = 230.0f/375.0f;
 40     [_titleLabel mas_makeConstraints:^(MASConstraintMaker *make) {
 41         make.top.bottom.mas_equalTo(weakSelf).mas_offset(0.0f);
 42         make.left.mas_equalTo(weakSelf).mas_offset(15.0f);
 43         make.right.mas_equalTo(weakSelf.mas_left).mas_offset((1-ratio-0.02)*ZYAppWidth);
 44     }];
 45     [_contentField mas_makeConstraints:^(MASConstraintMaker *make) {
 46         make.top.bottom.mas_equalTo(weakSelf).mas_offset(0.0f);
 47         make.left.mas_equalTo(weakSelf.mas_right).mas_offset(-(ratio*ZYAppWidth));
 48         make.right.mas_equalTo(weakSelf).mas_offset(-15.0f);
 49     }];
 50     [_lineView mas_makeConstraints:^(MASConstraintMaker *make) {
 51         make.left.mas_equalTo(weakSelf).mas_offset(15.0f);
 52         make.right.mas_equalTo(weakSelf).mas_offset(0.0f);
 53         make.bottom.mas_equalTo(weakSelf).mas_offset(0.0f);
 54         make.height.mas_equalTo(0.5f);
 55     }];
 56     
 57     return self;
 58 }
 59 
 60 - (void)setTitle:(NSString *)title{
 61     self.titleLabel.text = title;
 62 }
 63 
 64 - (void)setContent:(NSString *)content{
 65     self.contentField.text = content;
 66 }
 67 
 68 - (void)setPlaceHolder:(NSString *)placeHolder{
 69     self.contentField.placeholder = placeHolder;
 70 }
 71 
 72 - (void)setIsForbidEdit:(BOOL)isForbidEdit{
 73     self.contentField.enabled = !isForbidEdit;
 74 }
 75 
 76 - (void)setIsHiddenLine:(BOOL)isHiddenLine{
 77     self.lineView.hidden = isHiddenLine;
 78 }
 79 
 80 #pragma mark -- UITextField代理
 81 - (void)textFieldDidBeginEditing:(UITextField *)textField{
 82     CGRect frame = [textField convertRect:textField.frame toView:nil];
 83     if (_contentStartEditBlock) {
 84         _contentStartEditBlock(frame);
 85     }
 86 }
 87 
 88 - (void)textFieldDidEndEditing:(UITextField *)textField{
 89     NSString *contentString = textField.text;
 90     if (_contentEditResultBlock) {
 91         _contentEditResultBlock(contentString);
 92     }
 93 }
 94 
 95 #pragma mark - textField delegate
 96 - (BOOL)textFieldShouldReturn:(UITextField *)textField {
 97     [textField resignFirstResponder];
 98     return YES;
 99 }
100 
101 @end
```

#### 2.3 对自定义cell的应用

　　我们在对tableview的上移进行调整时，我们需要知道当前编辑的cell相对屏幕的位置，然后才能判断是否需要上移tableview以及上移多少。所以我们在cell的编辑区域开始编辑(textFieldDidBeginEditing: )，需要回传自身的位置，就是通过block将当前cell相对屏幕的frame回传到我们的主控制器。
　　
```
- (void)textFieldDidBeginEditing:(UITextField *)textField{
    //获取当前cell相对屏幕的位置
    CGRect frame = [textField convertRect:textField.frame toView:nil];
    if (_contentStartEditBlock) {
        _contentStartEditBlock(frame);
    }
}
```
 　　主控制器中对自定义cell的应用，首先，我们再主控制器中定义几个属性来保存我们键盘弹出时tableview的contentOffset以及当前编辑cell的frame，然后在应用自定义cell时设定我们的两个回调block，当开始编辑时，通过回调block回传的frame参数设置对应的editFrame。具体代码如下：
```
@interface ViewController ()<UITableViewDelegate, UITableViewDataSource>

@property (strong, nonatomic) UITableView *tableView;
@property (strong, nonatomic) NSMutableArray<NSMutableArray<CellInfoModel *> *> *cellInfoForParts;
//保存当前编辑cell的frame
@property (assign, nonatomic) CGRect editFrame;
//保存键盘弹出前tableview的contentOffset,方便我们在键盘收起时将tableview进行还原程原先的位置
@property (assign, nonatomic) CGPoint lastContentOffset;

@end

```
下面是应用自定义cell的代码：

```
#pragma mark - Table view data source
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {
    //当前行的数据模型
    CellInfoModel *cellModel = _cellInfoForParts[indexPath.section][indexPath.row];
    BasicCell *cell = [tableView dequeueReusableCellWithIdentifier:@"BasicCell"];
    if (!cell) {
        cell = [[BasicCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"BasicCell"];
    }
    cell.title = cellModel.title;
    cell.content = [self getInfo:cellModel.propName];
    cell.placeHolder = cellModel.placeHolder;
    cell.isForbidEdit = cellModel.isForbidEdit;
    cell.selectionStyle = cellModel.selectionStyle;
    WEAKSELF
    cell.contentEditResultBlock = ^(NSString *contentString) {
        //编辑完成后的处理，一般是数据保存
        NSLog(@"result %@", contentString);
    };
    cell.contentStartEditBlock = ^(CGRect frameToView) {
        weakSelf.editFrame = frameToView;
    };
    return cell;
}

```
#### 2.4 键盘的弹出和收起

　　在前面的2.1的UITextField或UITextView点击之后的详细流程分析中我们知道，在点击文本之后弹出键盘时会发送一个UIKeyboardWillShowNotification的通知，在编辑结束之后收起键盘时则也会发送一个UIKeyboardWillHideNotification的通知，所以我们通过监听这两个通知，来采取对应的行动。那么，首先我们需要对对应的通知进行注册，然后设置在监听到对应的通知之后应该采取的行动和措施。

注册通知的方法：

```
#pragma mark notification 通知管理
/**
 *    @brief    通知注册
 *    @return
 */
- (void)registNotification
{
    //弹出键盘的通知
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(keyboardWillShow:) name:UIKeyboardWillShowNotification object:nil];
    //收起键盘的通知
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(keyboardWillHide:) name:UIKeyboardWillHideNotification object:nil];
}
 弹出键盘对应的操作，如果有遮挡，我们通过修改tableview的contentOffset来实现tableview的上移：

#pragma mark --键盘弹出收起管理
-(void)keyboardWillShow:(NSNotification *)note{
    CGRect frame = _editFrame;
    //保存键盘弹出前tableview的contentOffset偏移
    self.lastContentOffset = self.tableView.contentOffset;
    //获取键盘高度
    NSDictionary *info = [note userInfo];
    CGSize kbSize = [[info objectForKey:UIKeyboardFrameEndUserInfoKey] CGRectValue].size;
    //判断键盘弹出是否会遮挡当前编辑cell，frame.size.height是当前编辑cell的高度
    CGFloat offSet = frame.origin.y + frame.size.height - (self.view.frame.size.height - kbSize.height);
    //将试图的Y坐标向上移动offset个单位，以使线面腾出开的地方用于软键盘的显示
    if (offSet > 0.01) {
        WEAKSELF
        //有遮挡时，tableview需要的偏移量应该是在原先的基础上再往上上移的，这里我们默认增加10个单位的空白
        offSet += self.lastContentOffset.y + 10;
        [UIView animateWithDuration:0.1 animations:^{
            weakSelf.tableView.contentOffset = CGPointMake(0, offSet);
        }];
    }
}

```

收起键盘的操作，和弹出键盘相对，弹出键盘时我们保存了弹出键盘之前tableview的contentOffset的偏移量，所以，在收起键盘后，我们将tableview的contentOffset值设为弹出之前的值就可以了，回到键盘弹出之前的状态了。

```
-(void)keyboardWillHide:(NSNotification *)note{
    WEAKSELF
    [UIView animateWithDuration:0.1 animations:^{
        weakSelf.tableView.contentOffset = weakSelf.lastContentOffset;
    }];
}
```