FROM centos:centos7.9.2009

SHELL [ "/bin/bash", "-c"]

### centosでは、systemctlが、container内で無効化になっているので有効化。
### https://hub.docker.com/_/centos?tab=description
### systemd-user-session.service が消えるとsshdが起動できないので退避。
ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    mv /lib/systemd/system/multi-user.target.wants/systemd-user-sessions.service /var/tmp/systemd-user-sessions.service; \
    rm -f /lib/systemd/system/multi-user.target.wants/*;\
    rm -f /etc/systemd/system/*.wants/*;\
    rm -f /lib/systemd/system/local-fs.target.wants/*; \
    rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /lib/systemd/system/basic.target.wants/*;\
    rm -f /lib/systemd/system/anaconda.target.wants/*;\
    mv  /var/tmp/systemd-user-sessions.service /lib/systemd/system/multi-user.target.wants/systemd-user-sessions.service;

### https://qiita.com/yuki2006/items/6cea8c352e38f047b52a#comment-8e863c71962008035d0d
# RUN yum -y reinstall glibc-common
# RUN localedef -v -c -i ja_JP -f UTF-8 ja_JP.UTF-8; echo "";
# ENV LANG=ja_JP.UTF-8
RUN rm -f /etc/localtime
RUN ln -fs /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

RUN yum -y install openssh openssh-clients sshpass python3 sudo vim less telnet nc screen tcpdump strace net-tools iproute bind-utils \
    && yum clean all

# CMD [ "/bin/bash" ]
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]