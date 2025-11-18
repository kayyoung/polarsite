# VPS 部署指南

## 🚀 快速部署到您的VPS

### 1. 准备工作

确保您的VPS已安装：
- Nginx
- Git (可选)
- SSL证书 (推荐使用Let's Encrypt)

### 2. 上传文件到VPS

#### 方法A: 使用SCP上传
```bash
# 从本地上传到VPS
scp -r /var/www/polarsite user@your-vps-ip:/var/www/

# 设置权限
ssh user@your-vps-ip "sudo chown -R www-data:www-data /var/www/polarsite && sudo chmod -R 755 /var/www/polarsite"
```

#### 方法B: 使用Git克隆
```bash
# 在VPS上创建目录
sudo mkdir -p /var/www/polarsite
sudo chown $USER:$USER /var/www/polarsite

# 克隆项目 (如果有Git仓库)
cd /var/www/polarsite
git clone your-repo-url .
```

#### 方法C: 直接下载
```bash
# 在VPS上下载文件
sudo mkdir -p /var/www/polarsite
cd /var/www/polarsite

# 使用wget下载压缩包 (如果有提供)
wget https://your-domain.com/polarsite.zip
unzip polarsite.zip
rm polarsite.zip

# 设置权限
sudo chown -R www-data:www-data /var/www/polarsite
sudo chmod -R 755 /var/www/polarsite
```

### 3. 配置Nginx

创建站点配置文件：

```bash
sudo nano /etc/nginx/sites-available/polarsite
```

添加以下配置：

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name your-domain.com www.your-domain.com;
    
    # 重定向到HTTPS
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name your-domain.com www.your-domain.com;
    
    root /var/www/polarsite;
    index index.html;
    
    # SSL配置
    ssl_certificate /path/to/your/certificate.crt;
    ssl_certificate_key /path/to/your/private.key;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    
    # 安全头
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header Referrer-Policy "no-referrer-when-downgrade" always;
    add_header Content-Security-Policy "default-src 'self' http: https: data: blob: 'unsafe-inline'" always;
    
    # 压缩
    gzip on;
    gzip_vary on;
    gzip_min_length 1024;
    gzip_types text/plain text/css text/xml text/javascript application/javascript application/xml+rss application/json;
    
    # 缓存静态资源
    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }
    
    # 主页面
    location = / {
        try_files /index.html =404;
    }
    
    # 工具页面
    location / {
        try_files $uri $uri/ $uri.html =404;
    }
    
    # 禁止访问隐藏文件
    location ~ /\. {
        deny all;
    }
}
```

启用站点：
```bash
sudo ln -s /etc/nginx/sites-available/polarsite /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

### 4. 获取SSL证书 (Let's Encrypt)

```bash
# 安装Certbot
sudo apt update
sudo apt install certbot python3-certbot-nginx

# 获取证书
sudo certbot --nginx -d your-domain.com -d www.your-domain.com

# 自动续期
crontab -e
# 添加: 0 12 * * * /usr/bin/certbot renew --quiet
```

### 5. 域名配置

在您的域名提供商处添加DNS记录：

```
A     your-domain.com     YOUR_VPS_IP
A     www.your-domain.com YOUR_VPS_IP
```

### 6. 防火墙配置

```bash
# UFW (Ubuntu)
sudo ufw allow 'Nginx Full'
sudo ufw enable

# 或者 iptables
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```

### 7. 测试部署

访问您的域名：
- https://your-domain.com (主站)
- https://your-domain.com/pdf.html (PDF转换器)
- https://your-domain.com/image.html (图片处理器)

### 8. 性能优化

#### 启用Brotli压缩
```bash
sudo apt install nginx-module-brotli
```

在Nginx配置中添加：
```nginx
brotli on;
brotli_comp_level 6;
brotli_types text/plain text/css application/javascript application/json image/svg+xml;
```

#### 优化文件权限
```bash
sudo find /var/www/polarsite -type f -exec chmod 644 {} \;
sudo find /var/www/polarsite -type d -exec chmod 755 {} \;
```

### 9. 监控和维护

#### 检查Nginx状态
```bash
sudo systemctl status nginx
sudo nginx -t
```

#### 查看访问日志
```bash
tail -f /var/log/nginx/access.log
tail -f /var/log/nginx/error.log
```

#### 更新SSL证书
```bash
sudo certbot renew --dry-run
```

### 10. 故障排除

#### 权限问题
```bash
sudo chown -R www-data:www-data /var/www/polarsite
sudo chmod -R 755 /var/www/polarsite
```

#### SELinux问题 (CentOS/RHEL)
```bash
sudo setsebool -P httpd_can_network_connect 1
sudo restorecon -Rv /var/www/polarsite
```

#### 端口占用
```bash
sudo lsof -i :80
sudo lsof -i :443
```

### 11. 高级配置

#### 设置HTTP/2
已在上面的配置中包含，确保Nginx版本 >= 1.9.5

#### 启用OCSP Stapling
```nginx
ssl_stapling on;
ssl_stapling_verify on;
ssl_trusted_certificate /path/to/your/certificate.crt;
```

#### HSTS (HTTP Strict Transport Security)
```nginx
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
```

---

## 📊 部署验证清单

- [ ] 网站可通过HTTPS访问
- [ ] 所有工具页面正常加载
- [ ] 文件上传功能正常
- [ ] 语言切换功能正常
- [ ] 深色模式切换正常
- [ ] 移动端适配正常
- [ ] SSL证书有效
- [ ] 安全头正确设置
- [ ] 压缩功能启用
- [ ] 缓存策略生效

---

## 🔧 常用命令

```bash
# 重启Nginx
sudo systemctl restart nginx

# 检查配置
sudo nginx -t

# 查看状态
sudo systemctl status nginx

# 查看日志
sudo tail -f /var/log/nginx/error.log

# 更新证书
sudo certbot renew

# 文件权限修复
sudo chown -R www-data:www-data /var/www/polarsite
```

---

© 2025 Polarsite Toolkit - VPS Deployment Guide
