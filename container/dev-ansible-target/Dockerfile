FROM dev-ansible-base:latest

SHELL ["/bin/bash", "-c"]

RUN yum -y install openssh-server rsyslog logrotate rpm-cron \
    && yum clean all


RUN ssh-keygen -b 2048 -t rsa -N "" -f /etc/ssh/ssh_host_rsa_key \
    && ssh-keygen -b 256 -t ecdsa -N "" -f /etc/ssh/ssh_host_ecdsa_key \
    && ssh-keygen -b 1024 -t ed25519 -N "" -f /etc/ssh/ssh_host_ed25519_key \
    && systemctl enable sshd.service \
    && groupadd -g 1002 rmt_op \
    && useradd -g 1002 -u 1002 -m -s /bin/bash rmt_op \
    && mkdir -p /home/rmt_op/.ssh \
    && chown rmt_op: /home/rmt_op/.ssh \
    && chmod 700 /home/rmt_op/.ssh \
    && echo 'rmt_op        ALL=(ALL)       NOPASSWD: ALL ' > /etc/sudoers.d/010_rmt_op_nopassword


# ssh 秘密鍵配布
COPY --chown=rmt_op:rmt_op authorized_keys /home/rmt_op/.ssh/authorized_keys
RUN chmod 644 /home/rmt_op/.ssh/authorized_keys

CMD ["/usr/sbin/init"]
