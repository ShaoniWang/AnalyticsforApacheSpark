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

# Example: Running a Spark application with optional parameters

Run the example Spark application built with Scala.

Usage information for the spark-submit.sh script:

```
spark-submit.sh --vcap <vcap-file> --conf spark.service.spark_version=<spark version> [options] <app jar | python file> [app arguments]
```

```
spark-submit.sh --vcap <vcap-file> --conf spark.service.spark_version=<spark version> --kill [submission ID]
```

```
spark-submit.sh --vcap <vcap-file> --conf spark.service.spark_version=<spark version> --status [submission ID]
```

```
spark-submit.sh --help
```

```
spark-submit.sh --version
```

The vcap-file is a JSON file that contains Spark service credentials,
including `tenant_id`, `instance_id`, and `tenant_secret` values.

The `cluster_master_url` is the value of the `cluster_master_url` from the service credentials page.

Important: If you use optional parameters, for example `--conf` or
`--master`, the values that are specified on the command-line where you
run the spark-submit.sh script take precedence. For example, if you
provide values in a vcap.json file and additionally specify the `--master` option on the command-line, the value in `--master` takes precedence. Alternatively, if you specify a value for `tenant_id` in a  vcap.json file and also specify `--conf spark.service.tenant-id=YourID` on the command-line, the value in `--conf` on the command-line takes precedence.

| Option                      | Description                                                                                                                                                                                                  |
| :-------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--master MASTER_URL`       | `spark://<cluster-master-url>` The variable `cluster-master-url` is from Spark service instance credentials. You must set `--master` and `--conf` to the required settings in `VCAP_FILE` if you do not use the `--vcap` option. |
| `--vcap VCAP_FILE`           | File named vcap.json with the service credentials from your Spark  instance.                                                                                                                                  |
| `--deploy-mode DEPLOY_MODE` | `DEPLOY_MODE` must be "cluster".                                                                                                                                                                              |
| `--class CLASS_NAME`        | Your application's main class (for Java or Scala  applications).                                                                                                                                              |
| `--name NAME`                 | The name of your application.                                                                                                                                                                                |
| `--jars JARS`                | Comma-separated list of local JAR files to include on the driver and executor classpaths.                                                                                                                    |
| `--py-files PY_FILES`       | Comma-separated list of .zip, .egg, or .py files to place on the PYTHONPATH for Python applications.                                                                                                         |
| `--files FILES`              | Comma-separated list of files to be placed in the working directory of each executor.                                                                                                                        |
| `--conf PROP=VALUE`          | Arbitrary Spark configuration property. You must set `--master` and `--conf` to the required settings in `VCAP_FILE` if you do not use the `--vcap` option.                                                         |
| `--kill SUBMISSION_ID`      | If given, stops the specified driver.                                                                                                                                                                        |
| `--status SUBMISSION_ID`    | If given, requests the status of the specified driver.                                                                                                                                                       |
| `--help`                     | Print usage information.                                                                                                                                                                                     |
| `--version`                  | Print version of spark-submit.sh script.                                                                                                                                                                     |

Table 1. spark-submit.sh options

For more information about optional configuration properties, see
Properties and variables for the spark-submit.sh script.



1.  Create an instance of the Analytics for Apache Spark service.

2.  Create a copy of the vcap.json file or a mock vcap.json file. For
    example:

    ```
    {
      "credentials": {
        "tenant_id": "s1a9-7f40d9344b951f-42a9cf195d79",
        "tenant_id_full": "b404510b-d17a-43d2-b1a9-7f40d9344b95_9c09a3cb-7178-43f9-9e1f-42a9cf195d79",
        "cluster_master_url": "https://spark.bluemix.net",
        "instance_id": "b404510b-d17a-43d2-b1a9-7f40d9344b95",
        "tenant_secret": "8b2d72ad-8ac5-4927-a90c-9ca9edfad124",
        "plan":"ibm.SparkService.PayGoLite"
      }
    }
    ```

3.  Upload the files described in [Example: Optional file transfer and
    environment configuration](./spark_environment_example.html).

4.  Run the batch job. For example, run the following commands:

    ```
    export SS_LOCAL_SPARK_HOME=/home/local/spark
     /usr/local/spark-cli/sbin/spark-submit.sh \
        --vcap ~/vcap.json \
        --deploy-mode cluster \
        --conf spark.service.spark_version=1.6 \
        --class org.apache.spark.examples.SparkPi \
        my/path/to/remote/sparkpi_2.10-1.0.jar file://spark-submit_20160305165113.log
    ```

5.  View the results by using the stdout command. For example:

    ```
    cat stdout
    # no extra config
    # load default config from : /usr/local/src/spark160master/spark/profile/notebook
    # Pi is roughly 3.14nnn
    ```
