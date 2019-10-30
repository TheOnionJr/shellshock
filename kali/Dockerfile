FROM kalilinux/kali-linux-docker

RUN apt update
RUN apt -y dist-upgrade
RUN apt -y autoremove
RUN apt -y clean

#Installing tools
RUN apt install -y kali-linux-web
