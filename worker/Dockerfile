FROM spark-base:3.2.3-hadoop3.2

LABEL maintainer="Akmal Masud <akmalmasud96@gmail.com>"

COPY worker.sh /
COPY spark-env.sh /spark/conf/

ENV SPARK_WORKER_WEBUI_PORT 8081
ENV SPARK_WORKER_LOG /spark/logs
ENV SPARK_MASTER "spark://spark-master:7077"
ENV CORES=8
ENV MEMORY=16G

EXPOSE 8081
RUN chmod +x /spark/conf/spark-env.sh

CMD ["/bin/bash", "/worker.sh"]
