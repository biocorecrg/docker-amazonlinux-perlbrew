FROM biocorecrg/amazonlinux-perlbrew-pyenv:2023

RUN yum update -y
RUN dnf install -y java-21-amazon-corretto java-21-amazon-corretto-devel maven-local-amazon-corretto21

ENV JAVA_HOME=/usr/lib/jvm/java-21-openjdk

# Clean cache
RUN yum clean all
