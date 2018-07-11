FROM node:10-alpine

RUN echo -e "Host *\n\tStrictHostKeyChecking no\n" >>/root/.ssh/config && echo "nameserver 119.29.29.29" >>/etc/resolv.conf

RUN echo "172.217.161.144  storage.googleapis.com" >>/etc/hosts && cat /etc/hosts

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories

RUN apk update && apk --no-cache add tzdata ca-certificates wget && \
    cp -r -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN apk add --no-cache \
      openssl
      
RUN npm cache add grpc@1.12.4

RUN npm config set unsafe-perm true && \ 
    npm install pm2@latest -g && \
    pm2 install typescript

WORKDIR /var/www

CMD ["pm2-runtime", "src/server.ts","--error","/root/.pm2/logs/${LOG_PATH}-error.log","--output","/root/.pm2/logs/${LOG_PATH}-output.log"]