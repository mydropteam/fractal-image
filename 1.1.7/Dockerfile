FROM node:8

# Creation of the project directories
RUN mkdir -p /opt/project \
&& mkdir -p /opt/project/components \
&& mkdir -p /opt/project/docs \
&& mkdir -p /opt/project/build \
&& mkdir -p /opt/project/assets

# Installation of Gulp.
RUN npm install --global gulp-cli

# the package.json file
COPY config/package.json /opt/project/package.json

# We set the node user as owner of the project module.
WORKDIR /opt/
RUN chown -R node:node ./project

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

# Expose 3000 for the node.js server, 3002 for the BrowserSync
EXPOSE 3000 3002

# The project volume
VOLUME /opt/project
