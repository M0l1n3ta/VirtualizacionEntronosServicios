FROM alpine:latest

LABEL maintainer emilio-jose.roldan-navarro@sogeti.com

RUN apk add --no-cache \
    bash \
    ca-certificates \
    curl \
    python \
    py-pip \
    py-setuptools \
    rsync \
    openssh \
	nano
	


RUN sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
  && echo "root:r@meses2" | chpasswd \
  && rm -rf /var/cache/apk/*
 

RUN sed -ie 's/#Port 22/Port 22/g' /etc/ssh/sshd_config

RUN sed -ir 's/#HostKey \/etc\/ssh\/ssh_host_rsa_key/HostKey \/etc\/ssh\/ssh_host_rsa_key/g' /etc/ssh/sshd_config
RUN sed -ir 's/#HostKey \/etc\/ssh\/ssh_host_dsa_key/HostKey \/etc\/ssh\/ssh_host_dsa_key/g' /etc/ssh/sshd_config
RUN sed -ir 's/#HostKey \/etc\/ssh\/ssh_host_ecdsa_key/HostKey \/etc\/ssh\/ssh_host_ecdsa_key/g' /etc/ssh/sshd_config
RUN sed -ir 's/#HostKey \/etc\/ssh\/ssh_host_ed25519_key/HostKey \/etc\/ssh\/ssh_host_ed25519_key/g' /etc/ssh/sshd_config


RUN ssh-keygen -t rsa -b 4096 -f /etc/ssh/ssh_host_rsa_key -N ''
RUN ssh-keygen -t rsa -b 4096 -f  /etc/ssh/ssh_host_ecdsa_key -N ''
RUN ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key -N ''

EXPOSE 22

CMD ["/usr/sbin/sshd","-D"]
