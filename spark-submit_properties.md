---

copyright:
  years: 2017
lastupdated: "2017-09-21"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Properties and variables for the spark-submit.sh script

The Analytics for Apache Spark spark-submit.sh script supports a subset
of Apache Spark spark-submit configuration properties and environment
variables.

For additional descriptions of the following supported settings, see
[Spark 1.6.0
configuration](https://spark.apache.org/docs/1.6.0/configuration.html "(Opens in a new tab or window)")
or [Spark 2.0
configuration](https://spark.apache.org/docs/2.0.0-preview/configuration.html "(Opens in a new tab or window)").

## Configuration properties

You can use any of the following properties to configure how the
spark-submit.sh script interacts with the Analytics for Apache Spark
service after the `--conf` argument. In some cases the value is passed
through as-is, in other cases the value is modified to conform to the
needs of Analytics for Apache Spark.

| Property                                                                    | Source        | Set by:                 | Usage, modification                                                                                            |
| :-------------------------------------------------------------------------- | :------------ | :---------------------- | :------------------------------------------------------------------------------------------------------------- |
| `spark.service.tenant_id`                                                    | Spark service | User or spark-submit.sh | Used for tenant service authentication. Required if you run the spark-submit script without the `--vcap` option. |
| `spark.service.tenant_secret`                                                | Spark service | User or spark-submit.sh | Used for tenant service authentication. Required if you run the spark-submit script without the `--vcap` option. |
| `spark.service.instance_id`                                                  | Spark service | User or spark-submit.sh | Used for tenant service authentication. Required if you run the spark-submit script without the `--vcap` option. |
| `spark.service.spark_version`                                                | Spark service | User                    | Spark 1.6.0 and Spark 2.0.x. Required when you run the spark-submit script.                                    |
| `spark.jars`                                                                  | Apache Spark  | User or spark-submit.sh | List of comma separated JAR files, each JAR file is a relative path to the `<tenant-home>/data` directory.         |
| `spark.submit.pyFiles`                                                        |               | User or spark-submit.sh | List of comma separated Python files, each file is a relative path to the `<tenant-home>/data` directory.          |
| `spark.driver.extraClassPath`                                                 | Apache Spark  | Spark service           | Set to `./data/libs/*`                                                                                          |
| `spark.driver.extraLibraryPath`                                               | Apache Spark  | Spark service           | Set to `./data/libs/*`                                                                                          |
| `spark.executor.extraClassPath`                                               | Apache Spark  | Spark service           | Set to `./data/libs/*`                                                                                          |
| `spark.executor.extraLibraryPath`                                             | Apache Spark  | Spark service           | Set to `./data/libs/*`                                                                                          |
| User-defined properties that begin with `spark.service.user.*``               | User          | User                    | Passed through to Spark master unchanged.                                                                      |
| All other `spark.*` properties or properties that do not begin with `spark.*` |               |                         | Removed.                                                                                                       |

Table 1. Configuration properties for the spark-submit.sh script

## Environment variables

You can specify environment variables to configure how the
spark-submit.sh script interacts with the Analytics for Apache Spark
service. However, the variables are not allowed to begin with `SPARK_`.
