FROM node:8

# Installation of PHP and usefull extensions
# Needed for the twig template engine
RUN deb http://packages.dotdeb.org jessie all
RUN deb-src http://packages.dotdeb.org jessie all
RUN wget https://www.dotdeb.org/dotdeb.gpg \
&& apt-key add dotdeb.gpg
RUN apt-get update
RUN apt-get install apache2 \
libapache2-mod-php7.0 \
php7.0-cli \
php7.0-apcu \
php7.0-mcrypt \
php7.0-intl \
php7.0-mysql \
php7.0-curl \
php7.0-gd \
php7.0-soap \
php7.0-xml \
php7.0-zip \
&& a2enmod rewrite

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
