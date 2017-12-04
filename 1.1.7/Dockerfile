FROM node:8

RUN mkdir -p /opt/app/fractal

WORKDIR /opt/app/fractal

RUN npm install && npm cache clean --force && npm install --save @frctl/fractal && npm i -g @frctl/fractal

ENV PATH /opt/apt/fractal/node_modules/.bin:$PATH

EXPOSE 3000

CMD ["gulp"]

CMD [ "fractal", "start" ]
