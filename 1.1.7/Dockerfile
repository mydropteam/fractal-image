FROM node:8

# Installation of PHP and usefull extensions
# Needed for the twig template engine
RUN
RUN apt-get install -y --no-install-recommends \
    php7 \
    php7-dev \
    php7-common \
    php7-apcu \
    php7-bcmath \
    php7-xmlwriter \
    php7-ctype \
    php7-curl \
    php7-exif \
    php7-fileinfo \
    php7-iconv \
    php7-imagick \
    php7-intl \
    php7-json \
    php7-mbstring \
    php7-opcache \
    php7-openssl \
    php7-pcntl \
    php7-mysqlnd \
    php7-pdo \
    php7-pdo_mysql \
    php7-pdo_pgsql \
    php7-phar \
    php7-posix \
    php7-session \
    php7-xml \
    php7-simplexml \
    php7-mcrypt \
    php7-xsl \
    php7-zip \
    php7-zlib \
    php7-dom \
    php7-redis \
    php7-fpm \
    php7-tidy \
    php7-tokenizer \
    bash \
    openssh \
    curl \
    wget \
    rsync \
    sshpass \
    python \
    g++ \
    make \
    gifsicle \
    libpng-dev \
    optipng \
    && rm -rf /var/cache/* /tmp/*

# Installation of Composer
RUN cd /usr/src && curl -sS http://getcomposer.org/installer | php
RUN cd /usr/src && mv composer.phar /usr/bin/composer

# Installation of Twig
RUN composer require twig/twig:~2.0

# Creation of the Fractal project directories
RUN mkdir -p /opt/project \
&& mkdir -p /opt/project/components \
&& mkdir -p /opt/project/docs \
&& mkdir -p /opt/project/build \
&& mkdir -p /opt/project/assets

# Installation of Gulp.
RUN npm install --global gulp-cli

# the package.json file
COPY config/package.json /opt/project/package.json

# The project directory
WORKDIR /opt/project/

# Installation of Fractal and Gulp as dependency
# RUN npm install && npm cache clean --force \
# && npm install --save @frctl/fractal \
RUN npm install --save @frctl/fractal \
&& npm i -g @frctl/fractal \
&& npm install --save @frctl/twig \
&& npm install --save-dev gulp

# ENV PATH /opt/project/fractal/node_modules/.bin:$PATH

# the fractal.js file
COPY config/fractal.js /opt/project/fractal.js

# the gulpfile.js file
COPY config/fractal.js /opt/project/gulpfile.js

# the component example files
COPY config/example /opt/project/components/example

# We set the node user as owner of the project module.
RUN chown -R node:node /opt/project

# Expose 3000 for the node.js server, 3002 for the BrowserSync
EXPOSE 3000 3002

# The project volume
VOLUME /opt/project
