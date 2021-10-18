FROM archlinux:base-devel
ARG USER=docker
RUN ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
 && echo "Server = https://mirrors.nju.edu.cn/archlinux/\$repo/os/\$arch" > /etc/pacman.d/mirrorlist \
 && sed -i '/\[community\]/!{p;d;};n;n;a [multilib]\nInclude = /etc/pacman.d/mirrorlist\n' /etc/pacman.conf \
 && sed -i '/\[multilib\]/!{p;d;};n;n;a [archlinuxcn]\nServer = https://mirrors.ustc.edu.cn/archlinuxcn/\$arch\n' /etc/pacman.conf \
 && pacman-key --init && pacman -Syu --noconfirm && pacman -S --noconfirm archlinuxcn-keyring \
 && pacman -S --noconfirm yay \
 && echo "%wheel ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers \
 && useradd -m -G wheel $USER
USER $USER
WORKDIR /home/$USER
RUN yay -S --noconfirm wqy-zenhei deepin-wine-tim
RUN cp /opt/apps/com.qq.office.deepin/files/run.sh tim.sh \
 && sed -i 's/env LC_ALL=zh_CN.UTF-8 //g' tim.sh \
 && yes | yay -Scc
 # && cp /opt/apps/com.qq.weixin.deepin/files/run.sh wechat.sh \
