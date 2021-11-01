FROM public.ecr.aws/f1n8f8j1/openjdk:8-jdk-slim

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get -qq update && \
    apt-get -qq upgrade -y && \
    apt-get -qq install -y git wget gnupg curl

RUN wget -q https://dlcdn.apache.org/maven/maven-3/3.8.3/binaries/apache-maven-3.8.3-bin.tar.gz -P /tmp && \
    tar xf /tmp/apache-maven-3.8.3-bin.tar.gz -C /opt && \
    ln -s /opt/apache-maven-3.8.3 /opt/maven

RUN echo "deb https://repo.scala-sbt.org/scalasbt/debian all main" | tee /etc/apt/sources.list.d/sbt.list && \
    echo "deb https://repo.scala-sbt.org/scalasbt/debian /" | tee /etc/apt/sources.list.d/sbt_old.list && \
    curl -sL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | apt-key add && \
    apt-get -qq update

RUN  apt-get -qq install sbt && \
    apt-get -qq install -y r-base

RUN     apt install -y python && \
    apt install -y python3 python3-pip
    # We remove ensurepip since it adds no functionality since pip is
    # installed on the image and it just takes up 1.6MB on the image
RUN  rm -r /usr/lib/python*/ensurepip && \
    pip install --upgrade pip setuptools

ENV M2_HOME=/opt/maven
ENV MAVEN_HOME=/opt/maven
ENV PATH=${PATH}:${M2_HOME}/bin
