
# Base image
FROM openjdk:11

# Define Spark and Hadoop versions
ENV SPARK_VERSION=3.2.0
ENV HADOOP_VERSION=3.3.1

# Download and install Hadoop
RUN mkdir -p /opt && \
    cd /opt && \
    curl -O https://archive.apache.org/dist/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz && \
    tar -xzf hadoop-${HADOOP_VERSION}.tar.gz && \
    rm hadoop-${HADOOP_VERSION}.tar.gz && \
    ln -s hadoop-${HADOOP_VERSION} hadoop && \
    echo "Hadoop ${HADOOP_VERSION} installed in /opt"

# Download and install Spark
RUN mkdir -p /opt && \
    cd /opt && \
    curl -O https://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop3.2.tgz && \
    tar -xzf spark-${SPARK_VERSION}-bin-hadoop3.2.tgz && \
    rm spark-${SPARK_VERSION}-bin-hadoop3.2.tgz && \
    ln -s spark-${SPARK_VERSION}-bin-hadoop3.2 spark && \
    echo "Spark ${SPARK_VERSION} installed in /opt"

# Add scripts and update Spark default config
ADD common.sh /common.sh
ADD spark-master /spark-master
ADD spark-worker /spark-worker
ADD spark-defaults.conf /opt/spark/conf/spark-defaults.conf

# Make the scripts executable
RUN chmod +x /common.sh /spark-master /spark-worker

# Update PATH
ENV PATH $PATH:/opt/spark/bin

