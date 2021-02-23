FROM centos:centos7.7.1908

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


RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
    && echo 'LANG="ja_JP.UTF-8"' > /etc/localtime \
    && yum -y install openssh openssh-clients sshpass python3 sudo vim less telnet nc screen tcpdump strace net-tools iproute bind-utils \
    && yum clean all

# CMD [ "/bin/bash" ]
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]