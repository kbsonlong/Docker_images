FROM centos
MAINTAINER <Email:kbsonlong@gmail.com Blog:www.along.party>
RUN yum install -y -q openssh-server net-tools python-setuptools && easy_install supervisor
RUN ssh-keygen -q -t rsa -b 2048 -f /etc/ssh/ssh_host_rsa_key -N ''
RUN ssh-keygen -q -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key -N ''
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_ed25519_key  -N ''
RUN sed -i "s/UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config
RUN sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config
RUN echo 'root:kbsonlong' |chpasswd
RUN echo_supervisord_conf |grep -v '^;' | sed -e '/^$/d' | sed  's/nodaemon=false/nodaemon=true/g'  > /etc/supervisord.conf
RUN echo -e "\n[program:sshd]\ncommand=/usr/sbin/sshd -D" >>/etc/supervisord.conf
EXPOSE 22
CMD ["/usr/bin/supervisord"]
