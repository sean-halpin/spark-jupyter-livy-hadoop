FROM alpine:latest

RUN apk --update add make automake gcc g++ subversion \
    curl tar bash python3-dev openjdk8 nss libc6-compat && \
    ln -s /lib64/ld-linux-x86-64.so.2 /lib/ld-linux-x86-64.so.2

RUN apk add cmd:pip3

RUN curl -L https://ftp.heanet.ie/mirrors/www.apache.org/dist/spark/spark-3.1.1/spark-3.1.1-bin-hadoop2.7.tgz -o spark-3.1.1-bin-hadoop2.7.tgz

RUN tar -xzf spark-3.1.1-bin-hadoop2.7.tgz && \
    mv spark-3.1.1-bin-hadoop2.7 /spark && \
    rm spark-3.1.1-bin-hadoop2.7.tgz && \
    pip3 install --upgrade pip && \
    pip3 install numpy pandas && \
    mkdir /etc/conf.d/hadoop

ENV SPARK_HOME="/spark"
ENV PYSPARK_PYTHON="/usr/bin/python3"
ENV PYSPARK_DRIVER_PYTHON="jupyter"
ENV PYSPARK_DRIVER_PYTHON_OPTS="notebook"
ENV JAVA_HOME="/usr/lib/jvm/java-1.8-openjdk"
ENV HADOOP_CONF_DIR="/etc/conf.d/hadoop"

COPY start-master.sh /start-master.sh
COPY start-worker.sh /start-worker.sh
COPY ./conf/ /etc/conf.d/hadoop
