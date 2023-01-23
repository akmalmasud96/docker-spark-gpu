FROM nvidia/cuda:11.7.0-devel-ubuntu20.04

LABEL maintainer="Akmal Masud <akmalmasud96@gmail.com>"

ENV ENABLE_INIT_DAEMON false
ENV INIT_DAEMON_BASE_URI http://identifier/init-daemon
ENV INIT_DAEMON_STEP spark_master_init

ENV BASE_URL=https://archive.apache.org/dist/spark/
ENV SPARK_VERSION=3.2.3
ENV HADOOP_VERSION=3.2

COPY wait-for-step.sh /
COPY execute-step.sh /
COPY finish-step.sh /

RUN apt-get update --yes && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
      net-tools \
      netcat \
      gnupg \
      libsnappy-dev \
      wget \
      && rm -rf /var/lib/apt/lists/*

#COPY bde-spark.css /css/org/apache/spark/ui/static/timeline-view.css
RUN apt-get update --yes && \
    apt-get install --yes --no-install-recommends \
    "openjdk-8-jre-headless" \
    ca-certificates-java && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

ADD https://raw.githubusercontent.com/guilhem/apt-get-install/master/apt-get-install /usr/bin/
RUN chmod +x /usr/bin/apt-get-install

RUN apt-get-install -y curl \
      && chmod +x *.sh \
      && wget ${BASE_URL}/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
      && tar -xvzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
      && mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} spark \
      && rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
      #&& cd /css \
      #&& jar uf /spark/jars/spark-core_2.11-${SPARK_VERSION}.jar org/apache/spark/ui/static/timeline-view.css \
      && cd /

#Give permission to execute scripts
RUN chmod +x /wait-for-step.sh && chmod +x /execute-step.sh && chmod +x /finish-step.sh

RUN apt-get-install -y python3 python3-setuptools python3-pip
# Fix the value of PYTHONHASHSEED
# Note: this is needed when you use Python 3.3 or greater
ENV PYTHONHASHSEED 1
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/