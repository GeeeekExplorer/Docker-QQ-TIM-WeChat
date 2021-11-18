FROM ubuntu
ARG USER=docker
COPY preferences /etc/apt/preferences
RUN ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
 && apt update && apt install --no-install-recommends -y sudo ca-certificates gnupg locales \
 && locale-gen zh_CN.UTF-8 \
 && sed -i 's/http:\/\/archive.ubuntu.com/https:\/\/mirrors.nju.edu.cn/g' /etc/apt/sources.list \
 && sed -i 's/http:\/\/security.ubuntu.com/https:\/\/mirrors.nju.edu.cn/g' /etc/apt/sources.list \
 && echo "deb https://community-packages.deepin.com/deepin/ apricot main contrib non-free"  > /etc/apt/sources.list.d/deepin.list \
 && echo "deb https://community-store-packages.deepin.com/appstore eagle appstore" >> /etc/apt/sources.list.d/deepin.list \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 425956BB3E31DF51 1C30362C0A53D5BB \
 && echo "$USER ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers \
 && useradd -m $USER
RUN dpkg --add-architecture i386 \
 && apt update && apt upgrade -y \
 && apt install --no-install-recommends -y com.qq.im.deepin com.qq.weixin.deepin \
 && rm -rf /var/lib/apt/lists/*
USER $USER
WORKDIR /home/$USER
RUN cp /opt/apps/com.qq.im.deepin/files/run.sh qq.sh \
 && cp /opt/apps/com.qq.weixin.deepin/files/run.sh wechat.sh
