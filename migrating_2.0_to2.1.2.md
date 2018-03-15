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

# Migrating from Spark 2.0 to Spark 2.1.2

When you upgrade from using Spark 2.0 to Spark 2.1.2, you might need to modify the code in your applications. Refer to the following [documentation](./ts_spark_212_updates.html#what-you-need-to-consider-when-upgrading-to-spark-2-1-2) to learn about what to consider when upgrading your applications to run in Spark 2.1.2.

Follow the instructions in the following sections to start using Spartk 2.1.2.

## Using Spark through IBM Watson Studio

In {{site.data.keyword.DSX_short}}, you can select which Spark service to  use when your notebooks are run. For information on how to switch the Spark service of a  notebook, see [Change the Spark service used by a notebook](https://dataplatform.ibm.com/docs/content/analyze-data/change-spark-service.html?context=wdp).

## Using the `spark-submit.sh`  script

The version of Spark that is used by the `spark-submit.sh`script  is controlled by the `--conf spark.service.spark_version` option. Setting the value to `2.1` will direct the `spark-submit.sh` script to use Spark 2.1.2.

For example:
```
./spark-submit.sh
--vcap ./vcap.json
--conf spark.service.spark_version=2.1
--class org.apache.spark.examples.SparkPi
sparkpi_2.10-1.0.jar ```

For details on using the `spark-submit.sh` script, see [Running a Spark application using spark-submit](./using_spark-submit.html#running-a-spark-application-using-the-spark-submit-sh-script).

## Using Spark Interactive API

When you use the Spark Interactive API service and want to migrate to Spark 2.1.2, you need to modify the kernel names to specify the Spark 2.1 variants. For example, change:
 - `python2-spark20` to `python2-spark21`
 - `python3-spark20` to `python3-spark21`
 - `scala-spark20` to `scala-spark21`
 - `r-spark20` to `r-spark21`

See [using the Spark Interactive API service](./spark_interactive_api.html#spark-interactive-api) to learn more about running applications by using the Spark Interactive API.
