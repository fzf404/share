> 强大的反向代理工具

## 安装

```nginx
# 更新软件源
apt update
# 安装nginx
apt install nginx

# 配置文件
/etc/nginx/sites-available/
/etc/nginx/sites-eable/
```



## 返回字符串

```nginx
# 一个服务
server {
    	# 监听80端口
        listen 80 default_server;
        listen [::]:80 default_server;
    
    	# 默认静态页目录
        root /var/www/html;

        # 默认请求文件
        index index.html index.htm index.nginx-debian.html;

        server_name _;

        location / {
                try_files $uri $uri/ =404;
        }
    
    	# 监听/fzf404路径
        location /fzf404 {
        		# 返回类型为html
                default_type text/html;
        		# http状态码 返回字符串
                return 200 "here's fzf404's home";
        }
}

```

## 搭建服务

```nginx
# 新建目录
mkdir -p /www/website

# nginx配置
root /www/website/;
location /2048/ {
	try_files $uri $uri/ =404;
}
```

