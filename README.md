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
        root   /home/www/ml.haoyun1991.com;
    }

}

server {
    #ssl参数
    listen              443 ssl;
    server_name         kexifs.com;
    #证书文件
    ssl_certificate     /root/.acme.sh/kexifs.com/kexifs.com.cer;
    #私钥文件
    ssl_certificate_key /root/.acme.sh/kexifs.com/kexifs.com.key;
    ssl_protocols       TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers         HIGH:!aNULL:!MD5;
    #...

location / {
        root   /home/www/ml.haoyun1991.com;
        index  index.html index.html;
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



