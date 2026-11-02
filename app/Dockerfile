FROM amazonlinux:2

RUN amazon-linux-extras install -y epel \
# php rep
&& yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm \
&& yum update -y 

# httpd
RUN yum install -y httpd \
libedit ncurses-compat-libs \
freetype \
libjpeg-turbo \
t1lib \ 
libXpm \ 
harfbuzz \ 
libtiff \ 
fontconfig \
libtool-ltdl \
libxslt \
libicu \
vim \
less \
git \
zip \
unzip \
libmemcached && \
# php5.5
yum install -y --enablerepo=remi,remi-php55 \
php55-php \
php55-php-mbstring \
php55-php-zip \
php55-php-gd \
php55-php-mysqlnd \
php55-php-pdo \
php55-php-pdo-dblib \
php55-php-pdo-firebird \
php55-php-xml \
php55-php-pecl-xdebug

RUN ln /usr/bin/php55 /usr/bin/php

# Postfix install
RUN yum install -y postfix cyrus-sasl cyrus-sasl-plain mailx telnet

ADD main.cf /etc/postfix/main.cf

# Apache configuration
ADD httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf
ADD httpd/conf.d/app.conf /etc/httpd/conf.d/app.conf

RUN systemctl enable httpd.service

RUN yum clean all && rm -rf /var/cache/yum/*

# Copy Composer from the official Composer image
COPY --from=composer:2.3.9 /usr/bin/composer /usr/bin/composer

# Ensure Apache runs in the foreground
CMD ["/usr/sbin/httpd", "-DFOREGROUND"]
