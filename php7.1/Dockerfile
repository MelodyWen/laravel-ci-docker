FROM ubuntu:16.04
MAINTAINER chenjiawen <604989282@qq.com>

#######################
# 第一部分 设置环境参数 #
######################
ENV PHP_VERSION=7.1

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
    && apt-get -y install net-tools iputils-ping

# 3.2 安装nginx服务
RUN apt-get -y install nginx

# 3.3 安装php-7.1
RUN apt-get -y install php$PHP_VERSION \
    && apt-get -y install php$PHP_VERSION-fpm \
    && apt-get -y install  mcrypt php$PHP_VERSION-mcrypt php$PHP_VERSION-mysql \
    && apt-get -y install php$PHP_VERSION-curl php$PHP_VERSION-gd \
    && apt-get -y install php$PHP_VERSION-dom php$PHP_VERSION-mbstring \
    && apt-get -y install php$PHP_VERSION-pgsql php$PHP_VERSION-sqlite3 \
    && apt-get -y install php$PHP_VERSION-apcu php$PHP_VERSION-mcrypt \
    && apt-get -y install php$PHP_VERSION-imap php$PHP_VERSION-memcached \
    && apt-get -y install php$PHP_VERSION-readline php$PHP_VERSION-xdebug \
    && apt-get -y install php$PHP_VERSION-xml php$PHP_VERSION-zip \
    && apt-get -y install php$PHP_VERSION-intl php$PHP_VERSION-bcmath \
    && apt-get -y install php$PHP_VERSION-soap

# 3.6 安装node lts 8.11.3
WORKDIR /root
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs

#######################################
# 第四部分 安装 其他上层应用，并且优化应用 #
#######################################
# 4.1 安装 composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://packagist.laravel-china.org \
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

EXPOSE 22

CMD ["/etc/init.d/ssh", "start","-D"]