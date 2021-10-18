FROM ubuntu
ARG USER=docker
COPY preferences /etc/apt/preferences
RUN ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
 && apt update && apt install --no-install-recommends -y ca-certificates gnupg locales \
 && locale-gen zh_CN.UTF-8 \
 && sed -i 's/http:\/\/archive.ubuntu.com/https:\/\/mirrors.nju.edu.cn/g' /etc/apt/sources.list \
 && sed -i 's/http:\/\/security.ubuntu.com/https:\/\/mirrors.nju.edu.cn/g' /etc/apt/sources.list \
 && echo "deb https://community-packages.deepin.com/deepin/ apricot main contrib non-free"  > /etc/apt/sources.list.d/deepin.list \
 && echo "deb https://community-store-packages.deepin.com/appstore eagle appstore" >> /etc/apt/sources.list.d/deepin.list \
 && echo "deb https://d.store.deepinos.org.cn/ /" > /etc/apt/sources.list.d/spark.list \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 425956BB3E31DF51 0E41D354A29A440C 1C30362C0A53D5BB \
 && useradd -m $USER
RUN dpkg --add-architecture i386 \
 && apt update && apt upgrade -y \
 && apt install --no-install-recommends -y com.qq.tim.spark \
 && rm -rf /var/lib/apt/lists/*
USER $USER
WORKDIR /home/$USER
RUN cp /opt/apps/com.qq.tim.spark/files/run.sh tim.sh && ./tim.sh \
 && mkdir -p .deepinwine/Spark-TIM/drive_c/Program\ Files/Tencent/TIM/ \
 && ln -s ~/Tencent\ Files .deepinwine/Spark-TIM/drive_c/Program\ Files/Tencent/TIM/Users
 # && cp /opt/apps/com.qq.weixin.spark/files/run.sh wechat.sh