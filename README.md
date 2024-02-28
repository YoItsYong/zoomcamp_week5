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