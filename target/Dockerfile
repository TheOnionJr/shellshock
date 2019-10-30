FROM ubuntu:18.04

MAINTAINER Sander L Berntsen <sander.loken@gmail.com>

#Apt
RUN apt-get update
RUN apt-get install -y build-essential
RUN apt-get install -y wget
RUN apt-get install -y tar
RUN apt-get install -y apache2 && apt-get clean && rm -rf /var/lib/apt/lists/*

#ENV
ENV APACHE_RUN_USER  www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR   /var/log/apache2
ENV APACHE_PID_FILE  /var/run/apache2/apache2.pid
ENV APACHE_RUN_DIR   /var/run/apache2
ENV APACHE_LOCK_DIR  /var/lock/apache2
ENV APACHE_LOG_DIR   /var/log/apache2

#RUN
RUN mkdir -p $APACHE_RUN_DIR
RUN mkdir -p $APACHE_LOCK_DIR
RUN mkdir -p $APACHE_LOG_DIR

COPY resources/index.html /var/www/html

EXPOSE 80

#Creating shellshock vulnerability
RUN wget https://ftp.gnu.org/gnu/bash/bash-4.3.tar.gz
RUN tar -xvf bash-4.3.tar.gz
RUN /bash-4.3/configure && make
RUN ln -s /bash-4.3/bash bash_shellshock

RUN mkdir /var/www/html/cgi-bin
COPY resources/script.cgi /var/www/html/cgi-bin

#Start apache
CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]
