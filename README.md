# Data Ingestion using Kafka and its Ecosystem to create a Dashboard

## Project Objective

In this project the objective is to build a real-time data pipeline levaraging Kafka and its ecosystem including kafka Connect and Kafka REST Proxy. The data pipeline combines data from multiple sources which include a Postgres database containing stations data, live weather data served through a REST endpoint and arrivals and turnstile events data and feeds into a dashboard which shows public transit status in real-time. 

## Data Pipeline Architecture

A high-level architectural representation of the data pipeline is shown in the figure below. Various components of the Kafka ecosystem are shown such as kafka Connect and Kafka REST Proxy.

![Image of datapipeline architecture](https://github.com/MRazaKazmi/kafka-data-ingestion-public-transit/blob/master/data_pipeline_architecture.png)


## Project Implementation 

Step 1: Create Kafka Producers

There are three Kafka Producers loading data into the Kafka cluster. First, arrivals and turnstile events are loaded into Kafka using functionality provided by the Kafka Producer base class and using the confluent-kafka library.

Next, a REST Proxy Producer emits live weather data via REST Proxy and puts into Kafka.

Finally, the Kafka Connect Producer uses the JDBC source connector to connect to Postgres and extract data from the stations table. 


Step 2: Configure Stream Processors

Two stream processors are used: Faust and KSQL.

Faust stream processing is used to transform raw stations data ingested using Kafka Connect. KSQL is used to create two tables: a turnstile table and a turnstile summary table containing an aggregated view of turnstile data by station

Step 3: Create Kafka Consumers

There are 4 Kafka Consumers which consume the data in the webserver to provide real-time updates on public transit status to commuters. 

