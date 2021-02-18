<h1>SF Crime Statistics with Kafka and Spark Streaming</h1>

<h2>Objective</h2>
<p>
In this project, you will be provided with a real-world dataset, extracted from Kaggle, on San Francisco crime incidents, and you will provide statistical analyses of the data using Apache Spark Structured Streaming. You will draw on the skills and knowledge you've learned in this course to create a Kafka server to produce data, and ingest data through Spark Structured Streaming.</p>

Directory Layout
The project consists of directory, config and producer, kafka server.

├── config
│   ├── server.properties
│   ├── zookeeper.properties
├── data_stream.py
├── kafka_server.py
├── police-department-calls-for-service.json
├── producer_server.py
├── radio_code.json
├── README.md
├── requirements.txt
└── start.sh

Running and Testing
This project requires creating topics, starting Zookeeper and Kafka server, and your Kafka bootstrap server. Use the commands below to start Zookeeper and Kafka server.

`/usr/bin/zookeeper-server-start config/zookeeper.properties`

`/usr/bin/kafka-server-start config/server.properties`
 Start producer_server.py and kafka_server.py to send police-department-calls-for-service.json into Kafka topic

`python kafka_server.py`
 Build the Kafka server

`kafka-console-consumer --topic <TOPIC_NAME> --bootstrap-server <PORT> --from-beginning`
 Run Apache Spark

`spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.3.4 --master local[*] data_stream.py`

Questions
Q1 - How did changing values on the SparkSession property parameters affect the throughput and latency of the data?
They will change the parameters inputRowsPerSecond and processedRowsPerSecond (i.e jobs completed much more quickly )

Q2 - What were the 2-3 most efficient SparkSession property key/value pairs? Through testing multiple variations on values, how can you tell these were the most optimal?
We can follow SQL performance tuning and Tuning Spark to make hypertuning over the parameters spark.sql.shuffle.partitions, spark.streaming.kafka.maxRatePerPartition and spark.default.parallelism

"spark.default.parallelism" : 1200
"spark.sql.shuffle.partitions":10
"spark.streaming.kafka.maxRatePerPartition":10
