# nginx

## 常用反向代理配置

```nginx
server {
    listen 80;
    server_name example.com;

    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

修改配置后先检查再重载：

```bash
sudo nginx -t
sudo systemctl reload nginx
```

HTTPS 证书应使用自动续期机制；不要把私钥放入仓库。

## 静态文件部署

```nginx
server {
    listen 80;
    server_name example.com;
    root /var/www/site;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

## 常用命令

```bash
sudo systemctl status nginx
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
sudo nginx -s reload
```

## 经验总结

1. 每次修改先执行 `nginx -t`，配置错误时不要直接 reload。
2. SPA 部署需要 `try_files` 回退到 `index.html`，否则刷新子路由会 404。
3. 代理 WebSocket 时需额外设置 `Upgrade` 和 `Connection` 请求头。
