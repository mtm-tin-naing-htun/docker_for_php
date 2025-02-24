FROM amazonlinux:2023

RUN yum update -y \
# httpd
&& yum install -y httpd \
libedit ncurses-compat-libs \
# php
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
procps \
libxml2 \
php8.3.x86_64 \
php8.3-bcmath.x86_64 \
php8.3-cli.x86_64 \
php8.3-common.x86_64 \
php8.3-devel.x86_64 \
php8.3-gd.x86_64 \
php8.3-fpm.x86_64 \
php8.3-mbstring.x86_64 \
php8.3-pdo.x86_64 \
php8.3-xml.x86_64 \
php8.3-mysqlnd.x86_64 \
php8.3-intl.x86_64 \
php8.3-intl.x86_64 \
php-pear.noarch \
php8.3-zip.x86_64
RUN yum install -y php8.3-devel php-pear libzip libzip-devel \
    && pecl install zip

# postfix
ADD main.cf /etc/postfix/main.cf
RUN chown -R root:root /etc/postfix/ \
&& chmod 644 /etc/postfix/main.cf

# apache conf
ADD httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf
ADD httpd/conf.d/app.conf /etc/httpd/conf.d/app.conf

ENV APACHE_LOG_DIR /var/log/httpd
# systemctl
RUN systemctl enable httpd.service

RUN yum clean all && rm -rf /var/cache/yum/*

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
