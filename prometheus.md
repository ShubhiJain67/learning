- opensource
- used for event monitoring and alerting
- written in GO

a multi-dimensional data model with time series data identified by metric name and key/value pairs
PromQL, a flexible query language to leverage this dimensionality
no reliance on distributed storage; single server nodes are autonomous
time series collection happens via a pull model over HTTP
pushing time series is supported via an intermediary gateway
targets are discovered via service discovery or static configuration
multiple modes of graphing and dashboarding support

Prometheus collects metrics from targets by scraping metrics HTTP endpoints. Since Prometheus exposes data in the same manner about itself, it can also scrape and monitor its own health.

Using Prometheus, you can monitor application metrics like throughput (TPS) and response times of the Kafka load generator (Kafka producer), Kafka consumer, and Cassandra client. Node exporter can be used for monitoring of host hardware and kernel metrics.

Grafana is only a visualization solution. Time series storage is not part of its core functionality. … The way Prometheus stores time series is the best by far (thanks to its dimensional model, which uses key-value tagging along the time series to better organize the data and offer strong query capabilities)

Prometheus stores its on-disk time series data under the directory specified by the flag storage. local. path . The default path is ./data (relative to the working directory), which is good to try something out quickly but most likely not what you want for actual operations.

Occasionally you will need to monitor components which cannot be scraped. The Prometheus Pushgateway allows you to push time series from short-lived service-level batch jobs to an intermediary job which Prometheus can scrape.

