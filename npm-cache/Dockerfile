FROM node:10-alpine

RUN apk add --no-cache \
      openssl \
      python2
      
RUN npm cache add grpc@1.12.4 \
      grpc@1.13.0  \
      node-gyp  \
      isexe  \
      which  

RUN npm config set unsafe-perm true && \ 
    npm install pm2@latest -g && \
    pm2 install typescript

WORKDIR /var/www

CMD ["pm2-runtime", "src/server.ts","--error","/root/.pm2/logs/${LOG_PATH}-error.log","--output","/root/.pm2/logs/${LOG_PATH}-output.log"]