# nginx
configration

#nginx多站点配置

删除nginx目录下 sites-enabled和sites-available 的default文件

新建文件夹vhost
在这里放置站点配置文件
如 haoyun1991.com.conf eg：

<pre>

server {
    listen       80;
    server_name  ml.haoyun1991.com;


    #charset koi8-r;

    #access_log  logs/yourmall.access.log  main;

    location / {
        root   /home/www/ml.haoyun1991.com;
        index  index.html index.html;
    }

    error_page  404              /404.html;

    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /var/sites/yourmall;
    }

    location ~ \.php$ {
        root           /var/sites/yourmall;
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  /usr/local/nginx/html/$fastcgi_script_name;
        include        fastcgi_params;
    }

}

</pre>


配置nginx.conf

$ sudo vi /etc/nginx/nginx.conf
将虚拟目录的配置文件加入到”http {}“部分的末尾
<pre>
http {
    ...
    include /etc/nginx/vhost/*.conf;
}

</pre>



