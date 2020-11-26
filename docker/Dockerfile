# base image= openjdk-8-jdk

FROM java:openjdk-8-jdk

# define spark and hadoop versions
ENV HADOOP_VERSION=2.7.3
ENV SPARK_VERSION=2.2.1
ENV HADOOP_URL= http://archive.apache.org/dist/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz
ENV SPARK_URL = http://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop2.7.tgz
# download and install hadoop
RUN mkdir -p /opt && cd /opt && curl ${HADOOP_URL} | \
    tar -zx hadoop-${HADOOP_VERSION}/lib/native && ln -s hadoop-${HADOOP_VERSION} hadoop 
   

# download and install spark
RUN mkdir -p /opt && cd /opt &&  curl ${SPARK_URL} | \
        tar -zx && ln -s spark-${SPARK_VERSION}-bin-hadoop2.7 spark 

# add scripts and update spark default config
ADD common.sh spark-master spark-worker /
ADD spark-defaults.conf /opt/spark/conf/spark-defaults.conf
ENV PATH $PATH:/opt/spark/bin
