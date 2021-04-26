FROM debian:jessie-slim

# 添加国内源
ADD sources.list /etc/apt/ 
# file 
# g++ 
# gcc 
# perl 
# curl 
# make 
# build-essential 基本构建软件包的信息性列表
# libcurl3 易于使用的客户端URL传输库（OpenSSL风格）
#autoconf 自动配置脚本生成器
# ca-certificates 通用CA证书
# libssl-dev 安全套接字层工具箱-开发文件 libssl1.0.0 
# freetds-dev MS SQL和Sybase客户端库（静态库和标头）
# firebird-dev Firebird的开发文件-基于InterBase 6.0代码的RDBMS 
# libpq-dev libpq5的头文件（PostgreSQL库） PostgreSQL C客户端库 
# libmhash-dev 用于加密哈希和消息认证的库 
# libc-client-dev IMAP（Internet消息访问协议）是一种访问保存在（可能是共享的）邮件服务器上的电子消息的方法。
# libcurl4-gnutls-dev libcurl的开发文件和文档（GnuTLS风格 
# libcunit1-ncurses-dev C单元测试库（ncurses）-开发文件 
# libmysql++-dev MySQL C ++库绑定（开发） libmysql ++ 3v5
# libkrb5-dev MIT Kerberos的标题和开发库 krb5-multidev
# libaprutil1-dev Apache可移植运行时实用程序库-开发标题 
# libpcre3-dev Perl 5兼容的正则表达式库-开发文件 
# libxml2-dev GNOME XML库的开发文件  
# libbz2-dev 高质量块排序文件压缩器库-开发 
# libxslt-dev XSLT 1.0处理库-开发套件 
# libtidy-dev HTML语法检查器和重新格式化-开发 
# libzip-dev 用于读取，创建和修改zip存档的库（开发 
# libpng-dev PNG库-开发 
# libjpeg-dev 独立JPEG组的JPEG运行时库（依赖包） 
# libmcrypt-dev 解/加密库开发文件 
# libreadline-dev GNU readline和历史记录库，开发文件
# libsnmp-dev SNMP（简单网络管理协议）开发文件 
# libpspell-dev 具有pspell支持的应用程序的开发文件
# unixodbc-dev UNIX的ODBC库（开发文件 unixodbc
# zlib1g-dev  压缩库-开发 zlib1g
RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends \
      autoconf \ 
      file \
      g++ \
      gcc \
      perl \
      curl \
      make \
      build-essential \
      ca-certificates \
      libssl-dev \
      freetds-dev \
      firebird-dev \
      libaprutil1-dev \
      libpq-dev \
      libmhash-dev \
      libncurses-dev \
      libcurl4-gnutls-dev \
      libcunit1-ncurses \
      libmysql++-dev \
      libkrb5-dev \
      libpcre3-dev \
      libxml2 \
      libbz2-dev \
      libxslt-dev \
      libtidy-dev \
      libzip-dev  \
      libpng-dev \
      libmcrypt-dev \
      libreadline-dev \
      libsnmp-dev  \
      libc-client-dev \
      libpspell-dev \
      unixodbc-dev && \
      apt-get clean && \
      rm -r /var/lib/apt/lists/* && \
      ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \ 
      ln -s /usr/lib/libc-client.so.2007e.0 /usr/lib/x86_64-linux-gnu/libc-client.a && \
      ln -s /usr/local/lib/libiconv.so.2 /usr/lib/ && \
      mkdir -p /var/www/html && chmod -R 777 /var/www/html/ 


ENV VERSION_APACHE 2.4.46
ENV VERSION_PHP 5.6.40
ENV PHP_INI_DIR /usr/src/php-$VERSION_PHP


ADD libiconv-1.15.tar.gz /usr/src/
RUN cd /usr/src/libiconv-1.15 && \
      ./configure --prefix=/usr/local/ && \
      make && make install && \
      rm -rf /usr/src/libiconv-1.15
      

#https://archive.apache.org/dist/httpd/
 ADD httpd-$VERSION_APACHE.tar.gz /usr/src/
 RUN cd /usr/src/httpd-$VERSION_APACHE && \
      ./configure --enable-mods-shared="all" \
      --enable-so \
      --enable-rewrite \
      --enable-headers  \
      --enable-log_config \
      --enable-logio \
      --enable-prefork \
      --enable-http_core \
      --enable-so \
      --enable-actions \
      --enable-alias \
      --enable-autoindex \
      --enable-cache \
      --enable-cgi \
      --enable-deflate \
      --enable-dir \
      --enable-env \
      --enable-expires \
      --enable-geoip \
      --enable-mime \
      --enable-negotiation \
      --enable-setenvif  \
      --enable-status \
      --enable-authz_host && \
      make && make install && \
      rm -rf /usr/src/httpd-$VERSION_APACHE

ADD httpd.conf /usr/local/apache2/conf/

#https://www.php.net/distributions/
ADD php-$VERSION_PHP.tar.gz /usr/src/
COPY php.ini /usr/src/php-$VERSION_PHP/
RUN cd /usr/src/php-$VERSION_PHP && \
      ./configure --prefix=/usr/local/php --with-config-file-path="$PHP_INI_DIR" --with-libdir=/lib/x86_64-linux-gnu \
      --enable-shared \
      --enable-mbstring \
      --with-bcmath \
      --with-bz2 \
      --with-calendar \
      --with-com_dotnet \
      --with-ctype \
      --with-curl \
      --with-date \
      --with-dba \
      --with-dom \    
      --with-fdf \
      --with-filter \
      --with-ftp \
      --with-gd \
      --with-gettext \
      --with-hash \
      --with-iconv\
      --with-imap \
      --with-imap-ssl \
      --with-kerberos \
      --with-interbase \
      --with-json \
      --with-ldap \
      --with-libxml \
      --with-mbstring \
      --with-mcrypt \
      --with-mhash \
      --with-mime_magic \
      --with-mssql \
      --with-mysql \
      --with-mysqli \      
      --with-ncurses \
      --with-odbc \
      --with-openssl \
      --with-pcntl \
      --with-pcre \
      --with-pdo \
      --with-pdo_dblib \
      --with-pdo_firebird \
      --with-pdo_mysql \
      --with-pdo_odbc=unixODBC,/usr \
      --with-pdo_pgsql \
      --with-pdo_sqlite \
      --with-pgsql \
      --with-posix \
      --with-pspell \
      --with-readline \
      --with-reflection \
      --with-session \
      --with-shmop \
      --with-simplexml \
      --with-skeleton \
      --with-snmp \
      --with-soap \
      --with-sockets \
      --enable-sql \
      --with-sqlite \
      --with-standard \
      --with-sybase \
      --with-sysvmsg \
      --with-sysvsem \
      --with-sysvshm \
      --with-tidy \
      --with-tokenizer \
      --with-wddx \
      --with-xml \
      --with-xmlreader \
      --with-xmlrpc \
      --with-xmlwriter \
      --with-xsl \
      --with-zip \
      --with-zlib \
      --without-pear \
      --disable-phar \
      --with-apxs2=/usr/local/apache2/bin/apxs && \
      make clean && make ZEND_EXTRA_LIBS='-liconv' && make install && \
      rm -rf /usr/src/php-$VERSION_PHP

WORKDIR /var/www/html
COPY apache2-foreground /usr/local/bin/
COPY phpinfo.php /var/www/html
EXPOSE 80
CMD ["apache2-foreground"]
 
