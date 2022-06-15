FROM php:7.3-fpm
# 更新安装依赖包和PHP核心拓展
RUN  sed -i s@/deb.debian.org/@/mirrors.163.com/@g /etc/apt/sources.list
RUN  apt-get clean
RUN apt-get update && apt-get install -y \
       git \
       libfreetype6-dev \
       libjpeg62-turbo-dev \
       libpng-dev \
       zlib1g-dev \
       libxml2-dev \
       libbz2-dev \
       libzip-dev \
       supervisor \
   && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
   && docker-php-ext-install -j$(nproc) gd \
       && docker-php-ext-install zip \
       && docker-php-ext-install pdo_mysql \
       && docker-php-ext-install opcache \
       && docker-php-ext-install mysqli \
       && docker-php-ext-install mbstring \
       && docker-php-ext-install bz2 \
       && docker-php-ext-install soap \
	   && pecl install -o -f redis \
	   && rm -rf /tmp/pear \
	   && docker-php-ext-enable redis \
	   && docker-php-ext-install bcmath \
       && rm -r /var/lib/apt/lists/*
# 安装 Composer
ENV COMPOSER_HOME /root/composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ENV PATH $COMPOSER_HOME/vendor/bin:$PATH