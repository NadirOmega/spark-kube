# base image= openjdk-8-jdk
#TO DO USE REDHAT AS DEFAULT IMG
FROM java:openjdk-8-jdk

# define spark and hadoop versions
ENV HADOOP_VERSION=2.7.3
ENV SPARK_VERSION=2.2.1

#signe layer for both hadoop and spark 
# download and install hadoop & Spark 
RUN mkdir -p /spark-nad && \
    cd /spark-nad && curl http://archive.apache.org/dist/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz | \
        tar -zx hadoop-${HADOOP_VERSION}/lib/native && \
    ln -s hadoop-${HADOOP_VERSION} hadoop && \
    echo Hadoop OK && \ 
     #Begin spark install 
    curl http://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop2.7.tgz | \
    tar -zx && \
    ln -s spark-${SPARK_VERSION}-bin-hadoop2.7 spark && \
    echo Spark OK

#OLD when using two layers
# download and install spark
#RUN mkdir -p /spark-nad && \
#    cd /spark-nad && \
#    curl http://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop2.7.tgz | \
#        tar -zx && \
#    ln -s spark-${SPARK_VERSION}-bin-hadoop2.7 spark && \
#    echo Spark OK


#Add spark default env 
ENV PATH $PATH:/spark-nad/spark/bin
# add scripts and update spark default config
ADD common.sh spark-master spark-worker /
# We have to  add a spark-default cfg 
ADD spark-defaults.conf /spark-nad/spark/conf/spark-defaults.conf

