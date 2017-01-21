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
ENV java_version 1.8.0_11 
ENV filename jdk-8u11-linux-x64.tar.gz 
ENV downloadlink http://download.oracle.com/otn-pub/java/jdk/8u11-b12/$filename 
# download java, accepting the license agreement 
RUN wget --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" -O /tmp/$filename $downloadlink 
# unpack java 
RUN mkdir /opt/java-oracle && tar -zxf /tmp/$filename -C /opt/java-oracle/

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
