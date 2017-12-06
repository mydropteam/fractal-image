FROM node:8

# Creation of the project directories
RUN mkdir -p /opt/project \
&& mkdir -p /opt/project/components \
&& mkdir -p /opt/project/docs \
&& mkdir -p /opt/project/build \
&& mkdir -p /opt/project/assets

# The project directory
WORKDIR /opt/project

# Installation of Fractal
RUN npm install && npm cache clean --force \
&& npm install --save @frctl/fractal \
&& npm i -g @frctl/fractal \
&& npm install --save @frctl/twig

ENV PATH /opt/project/fractal/node_modules/.bin:$PATH

# the fractal.js file
COPY config/fractal.js /opt/project/fractal.js

# the package.json file
# COPY config/package.json /opt/project/package.json

# the component example files
COPY config/example /opt/project/components/example

# Expose 3000 for the node.js server, 3002 for the BrowserSync
EXPOSE 3000 3002

# The project volume
VOLUME /opt/project
