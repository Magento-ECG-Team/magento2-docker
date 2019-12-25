FROM ubuntu:latest
ARG ROOTPASS
WORKDIR /var/www/magento

RUN apt -q -y update && apt install -q -y openssh-server
RUN mkdir /var/run/sshd
RUN echo "root:${ROOTPASS}" | chpasswd
RUN sed -i 's/\#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
RUN echo "cd /var/www/magento" >> /root/.profile

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]