FROM biocorecrg/amazonlinux-perlbrew-pyenv23

# File Author / Maintainer
MAINTAINER Toni Hermoso Pulido <toni.hermoso@crg.eu>
MAINTAINER Luca Cozzuto <lucacozzuto@gmail.com> 

ARG JAVA_VERSION=1.8.0
ARG MAVEN_VERSION=3.3.9

ENV JAVA_HOME /usr/lib/jvm/java-openjdk

# Install Redis
RUN yum update -y
# Install Java
RUN yum install -y java-$JAVA_VERSION-openjdk java-$JAVA_VERSION-openjdk-devel
# Install maven

RUN cd /usr/local; curl --fail --silent --show-error --location --remote-name https://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz

RUN cd /usr/local; tar zxf apache-maven-$MAVEN_VERSION-bin.tar.gz
RUN cd /usr/local; rm apache-maven-$MAVEN_VERSION-bin.tar.gz
RUN cd /usr/local; ln -s /usr/local/apache-maven-$MAVEN_VERSION/bin/mvn /usr/local/bin/mvn

# Clean cache
RUN yum clean all

