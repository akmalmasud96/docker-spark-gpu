FROM spark-base:3.2.3-hadoop3.2

LABEL maintainer="Akmal Masud <akmalmasud96@gmail.com>"

ENV SPARK_MASTER_NAME spark-master
ENV SPARK_MASTER_PORT 7077

COPY submit.sh /

CMD ["/bin/bash", "/submit.sh"]
