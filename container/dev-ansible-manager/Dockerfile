FROM dev-ansible-base:latest

SHELL ["/bin/bash", "-c"]

RUN pip3 install ansible

RUN groupadd -g 1010 ansible-manager \
    && useradd -g 1010 -u 1010 -m -s /bin/bash ansible-manager \
    && mkdir -p /var/log/ansible \
    && chown ansible-manager: /var/log/ansible \
    && mkdir -p /home/ansible-manager/.ssh \
    && chmod 700 /home/ansible-manager/.ssh \
    && ln -s /opt/ansible /home/ansible-manager/ansible

# ssh 公開鍵配布
COPY --chown=ansible-manager:ansible-manager id_rsa /home/ansible-manager/.ssh/id_rsa
RUN chmod 600 /home/ansible-manager/.ssh/id_rsa

CMD ["/usr/sbin/init"]
