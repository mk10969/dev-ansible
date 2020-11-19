FROM centos:centos7.7.1908

SHELL [ "/bin/bash", "-c"]

ENV container docker
# RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [$1 == systemd-tmpfiles-setup.service ] || rm -fr $1; done); \

RUN \cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
    && echo 'LANG="ja_JP.UTF-8"' > /etc/localtime \
    && yum -y install openssh openssh-clients sshpass python3 sudo vim less telnet nc screen tcpdump strace net-tools iproute bind-utils \
    && yum clean all

CMD [ "/bin/bash" ]
