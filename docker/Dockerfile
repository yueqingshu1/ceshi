FROM alpine:latest

ARG KEY="-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAACmFlczI1Ni1jdHIAAAAGYmNyeXB0AAAAGAAAABA0ygQZc6
r2ZgAhVbHys1ZtAAAAEAAAAAEAAAAzAAAAC3NzaC1lZDI1NTE5AAAAILcUft0K85KquyiJ
Bv/QrpQGSnV+YOKNH1rvCEuRM+NjAAAAoHdF78ukQw7RIXa0NaGnnU7W1lLD2OvqZJQWzO
47t6g5DnisBkfTHpcJYLSB5/kzwQb5SAnLuu0rf4OjrVPp6KiA4w1uh8yIlstJDYKzYf+s
1eze746ecFOTeWour2XY89BJGBtzoSZcR1c5IPKJ9PNnHVDjioT3NffL6JYLPqOmSyADn9
atATiCOHVQ2rbwYHzN3YSsTZaGi71SvYw76cg=
-----END OPENSSH PRIVATE KEY-----"

ENV REPO_URL=git@github.com:yueqingshu1/ceshi.git \
    REPO_BRANCH=main

WORKDIR /asm-unicom/

RUN apk update
RUN apk upgrade
RUN apk add --no-cache tzdata git nodejs moreutils npm curl jq openssh-client
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositoriesRUN 
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN mkdir -p /root/.ssh
RUN echo -e $KEY > /root/.ssh/id_rsa
RUN chmod 600 /root/.ssh/id_rsa
RUN ssh-keyscan github.com > /root/.ssh/known_hosts
RUN git clone -b $REPO_BRANCH $REPO_URL /asm-unicom

 # 复制代码
#COPY . /asm-unicom/

RUN npm config set registry https://registry.npm.taobao.org
RUN npm install

RUN rm -rf /usr/local/bin/entrypoint.sh
COPY docker/entrypoint.sh /usr/local/bin
RUN chmod +x /usr/local/bin/entrypoint.sh

ENTRYPOINT ["entrypoint.sh"]
CMD ["crond"]

