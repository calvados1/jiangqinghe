---
title: CentOS更新网站证书
link: CentOS_Update_Website_Certificate
catalog: true
lang: cn
tags:
  - 服务器
  - CentOS
categories:
  - [笔记,服务器]
date: 2024-10-29 09:34:30
---
# CentOS更新网站证书

### 1. 安装Certbot

如果你还没有安装Certbot，你需要先安装它。对于CentOS系统，可以通过以下命令安装Certbot和Nginx插件：

```
sudo yum install epel-release
sudo yum install certbot python2-certbot-nginx
```

### 2. 获取/更新Let's Encrypt证书

接下来，使用Certbot来获取或更新你的Let's Encrypt证书。Certbot可以自动配置Nginx以使用新证书。运行以下命令来自动更新你的Nginx配置以使用新的证书（如果你之前已经使用Certbot生成过证书，这个命令将自动尝试更新它们）：

```
sudo certbot --nginx -d heyiyuanqi.top -d www.heyiyuanqi.top
```

如果你想手动配置Nginx（不推荐，因为自动配置通常更安全、更简单），你可以仅获取证书，而不让Certbot修改你的Nginx配置：

```
sudo certbot certonly --webroot -w /var/www/html -d heyiyuanqi.top -d www.heyiyuanqi.top
```

在这个命令中，`-w /var/www/html` 应该替换为你的网站的实际根目录。

### 3. 确认Nginx配置（如果手动配置）

如果你选择手动配置Nginx，请确认你的Nginx配置文件（通常位于`/etc/nginx/nginx.conf`或`/etc/nginx/conf.d/your-site.conf`）已正确设置`ssl_certificate`和`ssl_certificate_key`指令以指向Certbot生成的证书和密钥：

```
ssl_certificate /etc/letsencrypt/live/heyiyuanqi.top/fullchain.pem;
ssl_certificate_key /etc/letsencrypt/live/heyiyuanqi.top/privkey.pem;
```

Certbot会自动更新这些路径指向最新的证书，因此通常不需要修改这些行，除非你的证书存放路径有所不同。

### 4. 检查Nginx配置并重载

在应用任何更改后，使用以下命令检查Nginx配置文件的语法是否正确：

```
sudo nginx -t
```

如果配置没有问题，重新加载Nginx以应用新的证书配置：

```
sudo systemctl reload nginx
```

或者，如果你的系统使用的是较旧的服务管理系统，可以使用：

```
sudo service nginx reload
```

### 5. 设置自动续订

Let's Encrypt的证书有效期为90天，因此建议设置自动续订。Certbot通常会在安装时自动安装一个定时任务或系统服务来处理续订。你可以通过运行以下命令测试自动续订是否正常工作：

```
sudo certbot renew --dry-run
```

按照这些步骤操作，你应该能够成功更新CentOS系统上Nginx的Let's Encrypt证书。如果在过程中遇到任何问题，可以查看Certbot的官方文档或搜索相关错误信息获取帮助。