# zoomcamp_week5

export JAVA_HOME="/workspaces/zoomcamp_week5/spark/jdk-11.0.2"
export PATH="${JAVA_HOME}/bin:${PATH}"

export SPARK_HOME="/workspaces/zoomcamp_week5/spark/spark-3.3.2-bin-hadoop3"
export PATH="${SPARK_HOME}/bin:${PATH}"

export PYTHONPATH="${SPARK_HOME}/python/:$PYTHONPATH"
export PYTHONPATH="${SPARK_HOME}/python/lib/py4j-0.10.9.5-src.zip:$PYTHONPATH"

nano .bashrc
source .bashrc
which java
which pyspark

echo $JAVA_HOME
echo $SPARK_HOME
echo $PYTHONPATH

gsutil -m cp -r pq/ gs://week5_nytaxi/pq
/workspaces/zoomcamp_week5/spark/data/google-cloud-sdk/bin/gsutil cp gs://hadoop-lib/gcs/gcs-connector-hadoop3-2.2.5.jar gcs-connector-hadoop3-2.2.5.jar

<!-- 5.6.2 Running Local Spark Cluster -->
python 06_spark_sql.py \
    --input_green=data/pq/green/2020/*/ \
    --input_yellow=data/pq/yellow/2020/*/ \
    --output=data/report-2020

./sbin/start-master.sh
./sbin/stop-master.sh
./sbin/stop-worker.sh
./sbin/start-worker.sh spark://codespaces-3a7421:7077

URL="spark://codespaces-3a7421:7077"
spark-submit \
    --master="${URL}" \
    06_spark_sql.py \
        --input_green=data/pq/green/2021/*/ \
        --input_yellow=data/pq/yellow/2021/*/ \
        --output=data/report/report-2021


<!-- 5.6.3 -->
./data/google-cloud-sdk/bin/gsutil cp 06_spark_sql.py gs://week5_nytaxi/code/06_spark_sql.py


--input_green=gs://week5_nytaxi/pq/green/2021/*/ \
--input_yellow=gs://week5_nytaxi/pq/yellow/2021/*/ \
--output=gs://week5_nytaxi/report/report-2021

week5-cluster
gs://week5_nytaxi/code/06_spark_sql.py

--input_green=gs://week5_nytaxi/pq/green/2021/*/
--input_yellow=gs://week5_nytaxi/pq/yellow/2021/*/
--output=gs://week5_nytaxi/report/report-2021

./data/google-cloud-sdk/bin/gcloud dataproc jobs submit pyspark \
    --cluster=week5-cluster \
    --region=us-central1 \
    gs://week5_nytaxi/code/06_spark_sql.py \
    -- \
        --input_green=gs://week5_nytaxi/pq/green/2020/*/ \
        --input_yellow=gs://week5_nytaxi/pq/yellow/2020/*/ \
        --output=gs://week5_nytaxi/report/report-2020

<!-- 5.6.4 -->

./data/google-cloud-sdk/bin/gsutil cp 06_spark_sql_bq.py gs://week5_nytaxi/code/06_spark_sql_bq.py

./data/google-cloud-sdk/bin/gcloud dataproc jobs submit pyspark \
    --cluster=week5-cluster \
    --region=us-central1 \
    --jars=gs://spark-lib/bigquery/spark-bigquery-latest_2.12.jar \
    gs://week5_nytaxi/code/06_spark_sql_bq.py \
    -- \
        --input_green=gs://week5_nytaxi/pq/green/2020/*/ \
        --input_yellow=gs://week5_nytaxi/pq/yellow/2020/*/ \
        --output=week5_trips_data.reports-2020