### UBuntu16.04 安装letsencrypt 证书

### 安装 Certbot

Certbot 其实就是维护 Let's Encrypt 的 Package，在 Ubuntu 16.04 上，我们可以这样安装
```
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt-get update
$ sudo apt-get install python-certbot-nginx 
```

### 签发 SSL 证书

```
$ sudo certbot --nginx certonly
```
选择完毕之后，等待 SSL 生成完毕，就会有类似这样的输出：

```
IMPORTANT NOTES:
- Congratulations! Your certificate and chain have been saved at:
/etc/letsencrypt/live/iruach.com/fullchain.pem
Your key file has been saved at:
/etc/letsencrypt/live/iruach.com/privkey.pem
Your cert will expire on 2019-02-13. To obtain a new or tweaked
version of this certificate in the future, simply run certbot
again. To non-interactively renew *all* of your certificates, run
"certbot renew"
- Your account credentials have been saved in your Certbot
configuration directory at /etc/letsencrypt. You should make a
secure backup of this folder now. This configuration directory will
also contain certificates and private keys obtained by Certbot so
making regular backups of this folder is ideal.
- If you like Certbot, please consider supporting our work by:

Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
Donating to EFF:                    https://eff.org/donate-le
```
然后在上面的文字中，这个 /etc/letsencrypt/live/your-domain.com/fullchain.pem 路径很重要，就是你的 SSL 证书路径。

### 自动更新证书

因为 Let's Encrypt 签发的 SSL 证书有效期只有 90 天，所有在过期之前，我们需要自动更新 SSL 证书，而如果你使用最新的 certbot 的话，Let's Encrypt 会帮你添加自动更新的脚本到 /etc/cron.d 里，你只需要去检测一下这个命令是否生效就OK！

```
sudo certbot renew --dry-run
```

### 参考链接
1 [Ubuntu 16.04 配置 Let's Encrypt 实现站点 SSL](https://www.codecasts.com/blog/post/secure-nginx-with-let-s-encrypt-on-ubuntu-16-04)
2 [Nginx on Ubuntu 16.04 (xenial)](https://certbot.eff.org/lets-encrypt/ubuntuxenial-nginx)

