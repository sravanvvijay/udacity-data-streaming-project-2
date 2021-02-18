<h1>SF Crime Statistics with Kafka and Spark Streaming</h1>

<h2>Objective</h2>
<p>
In this project, you will be provided with a real-world dataset, extracted from Kaggle, on San Francisco crime incidents, and you will provide statistical analyses of the data using Apache Spark Structured Streaming. You will draw on the skills and knowledge you've learned in this course to create a Kafka server to produce data, and ingest data through Spark Structured Streaming.</p>

<h3>Directory Layout</h3>
<p>The project consists of directory, config and producer, kafka server.</p>
<p>
.config
.     server.properties
.     zookeeper.properties
.data_stream.py
.kafka_server.py
.police-department-calls-for-service.json
.producer_server.py
.radio_code.json
.README.md
.requirements.txt
.start.sh
</p> 

<h3>Running and Testing</h3>
This project requires creating topics, starting Zookeeper and Kafka server, and your Kafka bootstrap server. Use the commands below to start Zookeeper and Kafka server.

`/usr/bin/zookeeper-server-start config/zookeeper.properties`

`/usr/bin/kafka-server-start config/server.properties`
 Start producer_server.py and kafka_server.py to send police-department-calls-for-service.json into Kafka topic

`python kafka_server.py`
 Build the Kafka server

`kafka-console-consumer --topic <TOPIC_NAME> --bootstrap-server <PORT> --from-beginning`
 Run Apache Spark

`spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.3.4 --master local[*] data_stream.py`

<h3>Questions</h3>
<h4>Q1 - How did changing values on the SparkSession property parameters affect the throughput and latency of the data?</h4>
         These are the parameters inputRowsPerSecond and processedRowsPerSecond will create the impact

<h4>Q2 - What were the 2-3 most efficient SparkSession property key/value pairs? Through testing multiple variations on values, how can you tell these were the most optimal?</h4>
    We can follow SQL performance tuning and Tuning Spark to make hypertuning over the parameters spark.sql.shuffle.partitions, spark.streaming.kafka.maxRatePerPartition 
    and spark.default.parallelism

    "spark.default.parallelism" : 1200
    "spark.sql.shuffle.partitions":10
    "spark.streaming.kafka.maxRatePerPartition":10
