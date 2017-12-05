FROM node:8

# Creation of the application directory
RUN mkdir -p /opt/app/fractal

WORKDIR /opt/app/fractal

# Installation of Fractal
RUN npm install && npm cache clean --force && npm install --save @frctl/fractal && npm i -g @frctl/fractal

ENV PATH /opt/apt/fractal/node_modules/.bin:$PATH

# Expose 3000 for the node.js server, 3002 for the BrowserSync
EXPOSE 3000 3002

# The application volume
VOLUME /opt/app/fractal

CMD ["gulp"]

CMD [ "fractal", "start --sync" ]
