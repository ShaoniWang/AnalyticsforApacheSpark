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

# Running a Spark application using the spark-submit.sh script

You can bring your own Apache Spark application and run it on the
Analytics for Apache Spark service.

Running your own Apache Spark application on the Analytics for Apache
Spark service lets you take advantage of powerful on-demand processing
in the cloud. And you can load your own data into an object store in
{{site.data.keyword.Bluemix_notm}} for fast, cost-effective access.

**Tip:** Follow this procedure when your application JAR file is stable and
no more testing is required. If you are still developing and testing
your application, see the procedures in [Example: Running a Spark
application with optional parameters](./spark_submit_example.html) and [Example: Optional file transfer and environment configuration](./spark_environment_example.html).

The spark-submit.sh script performs the following functions:

  - Runs the Apache Spark spark-submit command with the provided
    parameters.
  - Uploads JAR files and the application JAR file to the Spark cluster.
  - Calls the Spark master with the path to the application file.
  - Periodically checks the Spark master for job status.
  - Downloads the job stdout and stderr files to your local file system.

**Restriction:**

To run a Spark application using the spark-submit.sh script:

1.  Create your application. Be sure to test and debug your application
    locally before submitting it to the Analytics for Apache Spark
    service with the spark-submit.sh script. For more information see
    [Example: Creating a Spark application](./spark_app_example.html).

2.  Create an instance of the Analytics for Apache Spark service on {{site.data.keyword.Bluemix_notm}}, and record the credentials from the Service Credentials page.

3.  Copy the service credentials from your Spark instance to a file
    named vcap.json in the directory where you plan to run the
    spark-submit.sh script. For example:

    ```
    {
        "credentials": {
        "tenant_id": "s1a9-7f40d9344b951f-42a9cf195d79",
        "tenant_id_full": "b404510b-d17a-43d2-b1a9-7f40d9344b95_9c09a3cb-7178-43f9-9e1f-42a9cf195d79",
        "cluster_master_url": "https://169.54.219.20:8443/",
        "instance_id": "b404510b-d17a-43d2-b1a9-7f40d9344b95",
        "tenant_secret": "8b2d72ad-8ac5-4927-a90c-9ca9edfad124",
        "plan":"ibm.SparkService.PayGoLite"
      }
    }
    ```

    **Restriction:** If you run your application on a Analytics for Apache
    Spark service instance that was provisioned for working on notebooks
    with an {{site.data.keyword.objectstoragefull}} instance and you want to use a different Object Storage account with the service instance, do not use `spark` as the configname in the Swift URI
    ("swift2d://containername.configname/filename.csv").

    For example: Instead of
    `sc.textFile("swift2d://notebooks.spark/2015\_small.csv”)`, use
    `sc.textFile("swift2d://notebooks.keystone/2015\_small.csv”)`.

4.  To run your applications, use the Analytics for Apache Spark
    spark-submit.sh script, which you can get from the following site
    [https://spark.bluemix.net/batch/spark-submit.sh](https://spark.bluemix.net/batch/spark-submit.sh "(Opens in a new tab or window)").

5.  Run the spark-submit.sh script in your local shell. For example:

    ```
    ./spark-submit.sh \
    --vcap ./vcap.json \
    --deploy-mode cluster \
    --conf spark.service.spark_version=1.6 \
    --class org.apache.spark.examples.SparkPi \
    spark-examples-1.6.0-hadoop2.6.0.jar
    file://spark-submit_20160305165113.log
    ```

    The generated log file lists the steps taken by the spark-submit.sh
    script and is located in the folder where you run the script. For
    more information about the script parameters, see [Example: Running a Spark application with optional parameters](./spark_submit_example.html).

    You can check the status of the job by running the spark-submit.sh
    script with the `--status` parameter. For example:

    ```
    ./spark-submit.sh  
     --vcap ./vcap.json \
     --conf spark.service.spark_version=1.6 \
     --status driver--20160322155455-0085-189c0f50-3621-4465-ab51-7d162be4f6a3
    ```

    The status of the running job is queried continuously until the job
    status indicates `finished`, `error`, or `failed`. You can use CTRL-C to stop the running job with status polling. Selecting `Yes` cancels the job on the cluster immediately. Selecting `No` enables you to select either `Yes` to stop polling and return for further user action, or `No` to continue running your job and polling the status until the job finishes.

    You can cancel a running job by running the spark-submit.sh script
    with the `--kill` parameter. For example:

    ```
    ./spark-submit.sh  
     --vcap ./vcap.json \
     --conf spark.service.spark_version=1.6 \
     --kill driver--20160322155455-0085-189c0f50-3621-4465-ab51-7d162be4f6a3
    ```

    You can find the submission ID (driver value) in the stdout log
    file.

    **Restriction:** If you signed up for the Lite PayGo plan (formerly
    referred to as the Personal PayGo plan), you can run only one
    spark-submit job at a time.

## Results

Log files stdout and stderr are written to the cluster. The log file
names include a timestamp to identify each file. The timestamp is
identical for all output from each time you run the spark-submit.sh
script. For example: stdout_1458677079521707955 or
stderr_1458677079521707955.

You can access the stdout log file on the cluster by running the
following command:

```
 curl \
   -X GET \
   -u <tenant_id>:<tenant_secret> \
   -H 'X-Spark-service-instance-id: <instance_id>' \
   https://169.54.219.20/tenant/data/workdir/<submission-id>/stdout

```

For example:

```
curl \
   -X GET \
   -u s1a9-7f40d9344b951f-42a9cf195d79:8b2d72ad-8ac5-4927-a90c-9ca9edfad124 \
   -H 'X-Spark-service-instance-id: b404510b-d17a-43d2-b1a9-7f40d9344b95'\
   https://169.54.219.20/tenant/data/workdir/driver-20160322155455-0085-189c0f50-3621-4465-ab51-7d162be4f6a3/stdout
```

## What to do next

You can track the current execution of your running application and see
the details of previously run jobs on the Spark job history UI by
clicking **Job History** on the Analytics for Apache Spark service console.
