FROM jenkins
USER root
# this is a non-interactive automated build - avoid some warning messages
ENV DEBIAN_FRONTEND noninteractive 
# update dpkg repositories
RUN apt-get update 
# install wget 
RUN apt-get install -y wget
# get maven 3.2.2 
RUN wget --no-verbose -O /tmp/apache-maven-3.3.9-bin.tar.gz http://archive.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
# install maven 
RUN tar xzf /tmp/apache-maven-3.3.9-bin.tar.gz -C /opt/
RUN ln -s /opt/apache-maven-3.3.9 /opt/maven
RUN ln -s /opt/maven/bin/mvn /usr/local/bin
RUN rm -f /tmp/apache-maven-3.3.9.tar.gz
# set shell variables for java installation 
#http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/jdk-8u151-linux-x64.tar.gz
ENV java_version 1.8.0_151
ENV filename jdk-8u151-linux-x64.tar.gz
ENV downloadlink http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/$filename
# download java, accepting the license agreement
RUN wget --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" -O /tmp/$filename $downloadlink && mkdir /opt/java-oracle && tar -zxf /tmp/$filename -C /opt/java-oracle/ && rm -f /tmp/$filename
ENV JAVA_HOME /opt/java-oracle/jdk$java_version/bin/java

###
# Fix for https://github.com/dvdred/CI/issues/1
ARG JENKINS_UID
ARG JENKINS_GID
ARG JAVA_OPTS
RUN echo $JENKINS_UID $JENKINS_GID $JAVA_OPTS
RUN groupmod -g ${JENKINS_GID} jenkins
RUN usermod -u ${JENKINS_UID} -g ${JENKINS_GID} jenkins
###
USER $JENKINS_UID
ENV MAVEN_HOME /opt/maven
#CMD ["/bin/tini", "--", "/usr/local/bin/jenkins.sh"]
