FROM ubuntu:16.04
MAINTAINER chenjiawen <604989282@qq.com>

#######################
# 第一部分 设置环境参数 #
######################
ENV PHP_VERSION_5_6=5.6
ENV PHP_VERSION_7_0=7.0
ENV PHP_VERSION_7_1=7.1
ENV PHP_VERSION_7_2=7.2

##########################################
# 第二步 更换阿里镜像apt源 并且 初始化ubuntu #
##########################################

# 2.1 换源
COPY ./sources-ali.list /etc/apt/sources.list

# 2.2 Update Package List and System Packages
RUN apt-get update && apt-get -y upgrade

# 2.3 Force Locale  and timezone
RUN apt-get install -y language-pack-en-base \
    && locale-gen en_US.UTF-8 \
    && LC_ALL="en_US.UTF-8" \
    && LC_CTYPE="en_US.UTF-8" \
    && LANG="en_US.UTF-8" \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# 2.3 Install Some PPAs
RUN apt-get install -y software-properties-common \
    && LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php

################################
# 第三部分 install application  #
################################
# 3.1 安装基础包
RUN apt-get update \
    && apt-get -y install openssh-server vim git wget unzip curl \
    && apt-get -y install net-tools iputils-ping \
    && apt-get -y install build-essential dos2unix gcc libmcrypt4 libpcre3-dev make \
    && apt-get -y install python2.7-dev python-pip re2c supervisor unattended-upgrades whois libnotify-bin

# 3.2 安装nginx服务
RUN apt-get -y install nginx

# 3.3 安装php-5.6
RUN apt-get -y install php$PHP_VERSION_5_6 \
    && apt-get -y install php$PHP_VERSION_5_6-fpm \
    && apt-get -y install  mcrypt php$PHP_VERSION_5_6-mcrypt php$PHP_VERSION_5_6-mysql \
    && apt-get -y install php$PHP_VERSION_5_6-curl php$PHP_VERSION_5_6-gd \
    && apt-get -y install php$PHP_VERSION_5_6-dom php$PHP_VERSION_5_6-mbstring \
    && apt-get -y install php$PHP_VERSION_5_6-pgsql php$PHP_VERSION_5_6-sqlite3 \
    && apt-get -y install php$PHP_VERSION_5_6-apcu php$PHP_VERSION_5_6-mcrypt \
    && apt-get -y install php$PHP_VERSION_5_6-imap php$PHP_VERSION_5_6-memcached \
    && apt-get -y install php$PHP_VERSION_5_6-readline php$PHP_VERSION_5_6-xdebug \
    && apt-get -y install php$PHP_VERSION_5_6-xml php$PHP_VERSION_5_6-zip \
    && apt-get -y install php$PHP_VERSION_5_6-intl php$PHP_VERSION_5_6-bcmath \
    && apt-get -y install php$PHP_VERSION_5_6-soap

# 3.4 安装php-7.0
RUN apt-get -y install php$PHP_VERSION_7_0 \
    && apt-get -y install php$PHP_VERSION_7_0-fpm \
    && apt-get -y install  mcrypt php$PHP_VERSION_7_0-mcrypt php$PHP_VERSION_7_0-mysql \
    && apt-get -y install php$PHP_VERSION_7_0-curl php$PHP_VERSION_7_0-gd \
    && apt-get -y install php$PHP_VERSION_7_0-dom php$PHP_VERSION_7_0-mbstring \
    && apt-get -y install php$PHP_VERSION_7_0-pgsql php$PHP_VERSION_7_0-sqlite3 \
    && apt-get -y install php$PHP_VERSION_7_0-apcu php$PHP_VERSION_7_0-mcrypt \
    && apt-get -y install php$PHP_VERSION_7_0-imap php$PHP_VERSION_7_0-memcached \
    && apt-get -y install php$PHP_VERSION_7_0-readline php$PHP_VERSION_7_0-xdebug \
    && apt-get -y install php$PHP_VERSION_7_0-xml php$PHP_VERSION_7_0-zip \
    && apt-get -y install php$PHP_VERSION_7_0-intl php$PHP_VERSION_7_0-bcmath \
    && apt-get -y install php$PHP_VERSION_7_0-soap

# 3.4 安装php-7.1
RUN apt-get -y install php$PHP_VERSION_7_1 \
    && apt-get -y install php$PHP_VERSION_7_1-fpm \
    && apt-get -y install  mcrypt php$PHP_VERSION_7_1-mcrypt php$PHP_VERSION_7_1-mysql \
    && apt-get -y install php$PHP_VERSION_7_1-curl php$PHP_VERSION_7_1-gd \
    && apt-get -y install php$PHP_VERSION_7_1-dom php$PHP_VERSION_7_1-mbstring \
    && apt-get -y install php$PHP_VERSION_7_1-pgsql php$PHP_VERSION_7_1-sqlite3 \
    && apt-get -y install php$PHP_VERSION_7_1-apcu php$PHP_VERSION_7_1-mcrypt \
    && apt-get -y install php$PHP_VERSION_7_1-imap php$PHP_VERSION_7_1-memcached \
    && apt-get -y install php$PHP_VERSION_7_1-readline php$PHP_VERSION_7_1-xdebug \
    && apt-get -y install php$PHP_VERSION_7_1-xml php$PHP_VERSION_7_1-zip \
    && apt-get -y install php$PHP_VERSION_7_1-intl php$PHP_VERSION_7_1-bcmath \
    && apt-get -y install php$PHP_VERSION_7_1-soap

# 3.5 安装php-7.2
RUN apt-get -y install php$PHP_VERSION_7_2 \
    && apt-get -y install php$PHP_VERSION_7_2-fpm \
    && apt-get -y install php$PHP_VERSION_7_2-mysql \
    && apt-get -y install php$PHP_VERSION_7_2-curl php$PHP_VERSION_7_2-gd \
    && apt-get -y install php$PHP_VERSION_7_2-dom php$PHP_VERSION_7_2-mbstring \
    && apt-get -y install php$PHP_VERSION_7_2-pgsql php$PHP_VERSION_7_2-sqlite3 \
    && apt-get -y install php$PHP_VERSION_7_2-apcu \
    && apt-get -y install php$PHP_VERSION_7_2-imap php$PHP_VERSION_7_2-memcached \
    && apt-get -y install php$PHP_VERSION_7_2-readline php$PHP_VERSION_7_2-xdebug \
    && apt-get -y install php$PHP_VERSION_7_2-xml php$PHP_VERSION_7_2-zip \
    && apt-get -y install php$PHP_VERSION_7_2-intl php$PHP_VERSION_7_2-bcmath \
    && apt-get -y install php$PHP_VERSION_7_2-soap

# 3.6 安装node lts 8.11.3
WORKDIR /root
RUN wget https://nodejs.org/dist/v8.11.3/node-v8.11.3.tar.gz \
    && tar zxvf node-v8.11.3.tar.gz

WORKDIR /root/node-v8.11.3
RUN ./configure && make && make install
WORKDIR /root
RUN rm -rf node-v8.11.3*

#######################################
# 第四部分 安装 其他上层应用，并且优化应用 #
#######################################
# 4.1 安装 composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && printf "\nexport PATH=~/.composer/vendor/bin:\$PATH" | tee -a ~/.bash_profile

# 4.2 安装 yarn
RUN apt-get -y install apt-transport-https  \
    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -  \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update && apt-get -y install yarn

# 4.3 安装 laravel/envoy
RUN composer global require laravel/envoy \
    && mkdir -p /root/bin/composer-project

WORKDIR /root/bin/composer-project

RUN composer require mr-jiawen/laravel-envoy \
    && echo "@servers(['web' => 'root@localhost'])" | tee -a Envoy.blade.php \
    && echo "@import('vendor/mr-jiawen/laravel-envoy/bootstrap.blade.php')" | tee -a Envoy.blade.php

WORKDIR /root
# 4.3 挂载匿名数据卷
#VOLUME /builds

EXPOSE 22

CMD ["/etc/init.d/ssh", "start","-D"]