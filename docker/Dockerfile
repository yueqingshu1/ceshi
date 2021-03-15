FROM alpine:latest

WORKDIR /AutoSignMachine/

RUN set -ex \
 && sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories \
 && apk add --no-cache tzdata nodejs npm \
 && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \

 # 复制代码
 && cp . /AutoSignMachine/ \

 && npm install --registry https://registry.npm.taobao.org \

 && rm -rf /usr/local/bin/entrypoint.sh \

 && cp docker/entrypoint.sh /usr/local/bin \

 && chmod +x /usr/local/bin/entrypoint.sh

ENTRYPOINT ["entrypoint.sh"]
CMD ["crond"]

