FROM ubuntu:12.04

ENV USER ubuntu
ENV PASSWORD ubuntu
ENV ROOTPASSWORD root

# Run upgrades
RUN echo deb http://us.archive.ubuntu.com/ubuntu/ precise universe multiverse >> /etc/apt/sources.list;\
  echo deb http://us.archive.ubuntu.com/ubuntu/ precise-updates main restricted universe >> /etc/apt/sources.list;\
  echo deb http://security.ubuntu.com/ubuntu precise-security main restricted universe >> /etc/apt/sources.list;\
  echo udev hold | dpkg --set-selections;\
  echo initscripts hold | dpkg --set-selections;\
  echo upstart hold | dpkg --set-selections;\
  apt-get update;\
  apt-get -y upgrade

# Install ssh
RUN apt-get install -y openssh-server && mkdir /var/run/sshd
RUN echo "root:${ROOTPASSWORD}" |chpasswd

# Install packages
RUN apt-get install -y sudo git curl

# Add user
RUN useradd $USER && adduser $USER sudo && echo "${USER}:${PASSWORD}" |chpasswd && mkdir /home/$USER && chown -R $USER /home/$USER && chsh -s /bin/bash $USER

EXPOSE 22
CMD    /usr/sbin/sshd -D
