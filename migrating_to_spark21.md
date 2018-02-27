---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-26"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Migrating from Spark 1.6 to Spark 2.1

Many fixes, enhancements and new features were added to Spark since Spark 1.6. To keep up with these changes, you might want to consider upgrading to Spark 2.1. The migration effort from Spark 1.6 is dependent upon the Apache Spark APIs your applications use.

Use the information at the following links to learn about the new functionality that was added and the changes that were made and then update your applications as needed to work with Spark 2.1.

- For high-level information about new features; changes, removals, and deprecations made to the Spark APIs; performance improvements and known issues, see: [Apache Spark 2.0.2](http://spark.apache.org/releases/spark-release-2-0-2.html).
- For a list of behavioral changes that Spark 2.0 introduces, see [Spark 2.0 Deprecations and removals](https://issues.apache.org/jira/browse/SPARK-11806).
- The Spark SQL and Spark ML projects have documented migration changes for Apache Spark 1.6 to 2.0. See the [Spark Machine Learning Library (MLlib) Guide](http://spark.apache.org/docs/2.0.2/ml-guide.html). Note that the Spark MLlib RDD-based APIs are in maintenance mode and consider how this might affect your applications.  
- The following Spark projects have not documented any migration actions:

  - [Spark Streaming](http://spark.apache.org/docs/2.0.2/streaming-programming-guide.html)
  - [Structured Streaming](http://spark.apache.org/docs/2.0.2/structured-streaming-programming-guide.html)
  - [GraphX](http://spark.apache.org/docs/2.0.2/graphx-programming-guide.html)

**Note:** If you are migrating your applications to Spark 2.1.2, see [What you need to consider when upgrading to Spark 2.1.2](./ts_spark_212_updates.html).
