- ## nginx 配置

  ```sh
  vim /etc/nginx/nginx.conf
  ```

  ```text
  #是否启动gzip压缩,on代表启动,off代表开启
  gzip  on;
  
  #需要压缩的常见静态资源
  gzip_types text/plain application/javascript   application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png;
  
  #由于nginx的压缩发生在浏览器端而微软的ie6很坑爹,会导致压缩后图片看不见所以该选
  项是禁止ie6发生压缩
  gzip_disable "MSIE [1-6]\.";
  
  #如果文件大于1k就启动压缩
  gzip_min_length 1k;
  
  #以16k为单位,按照原始数据的大小以4倍的方式申请内存空间,一般此项不要修改
  gzip_buffers 4 16k;
  
  #压缩的等级,数字选择范围是1-9,数字越小压缩的速度越快,消耗cpu就越大
  gzip_comp_level 2;
  
  #引导的在/etc/nginx/conf.d目录下所有后缀为.conf的子配置文件
  include /etc/nginx/conf.d/*.conf;
  ```

  ```sh
  nginx -t
  
  nginx -s reload
  ```