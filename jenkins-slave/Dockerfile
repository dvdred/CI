FROM ubuntu:16.04
MAINTAINER dvd.red@gmail.com
ENV DEBIAN_FRONTEND noninteractive

# Make sure the package repository is up to date.
RUN apt-get update && apt-get -y upgrade && apt-get install -y wget git openssh-server openjdk-8-jdk && apt clean all
RUN sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd
RUN mkdir -p /var/run/sshd

# Add user jenkins to the image
RUN adduser --quiet jenkins && echo "jenkins:jenkins" | chpasswd

RUN mkdir /home/jenkins/.m2

ADD settings.xml /home/jenkins/.m2/

RUN chown -R jenkins:jenkins /home/jenkins/.m2/ 

RUN apt-get install -y maven && apt clean all
#http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/jdk-8u151-linux-x64.tar.gz
ENV java_version 1.8.0_151
ENV filename jdk-8u151-linux-x64.tar.gz
ENV downloadlink http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/$filename
# download java, accepting the license agreement
RUN wget --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" -O /tmp/$filename $downloadlink && mkdir /opt/java-oracle && tar -zxf /tmp/$filename -C /opt/java-oracle/ && rm -f /tmp/$filename
ENV MAVEN_HOME /opt/maven
ENV JAVA_HOME /opt/java-oracle/jdk$java_version/bin/java

# Standard SSH port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
