  
FROM alpine:latest

WORKDIR /asm-unicom/

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories
RUN apk add --no-cache tzdata nodejs npm
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

 # 复制代码
COPY . /asm-unicom/

RUN npm config set registry https://registry.npm.taobao.org
RUN npm install

RUN rm -rf /usr/local/bin/entrypoint.sh

COPY docker/entrypoint.sh /usr/local/bin

RUN chmod +x /usr/local/bin/entrypoint.sh

ENTRYPOINT ["entrypoint.sh"]
CMD ["crond"]
