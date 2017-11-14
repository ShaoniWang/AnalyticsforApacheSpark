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

# Example: Specifying a file path as input to the Spark application

If the input to your Spark application includes a file path, you must make this known when you run the spark-submit.sh script by using the `file://` prefix.

You must use the `file://` identifier because each tenant on the Spark cluster has a separate space and this identifier indicates that the path must be modified by the Spark  service to point to the file in the tenant's space.

To start an application that includes a file path:

Run the spark-submit.sh script with the `file://`  identifier. For example:

```
   ~/spark-submit.sh \
   --vcap ~/vcap.json \
   --deploy-mode cluster \
   --conf spark.service.spark_version=1.6 \
   --files /my/path/to/local/TwoWords.txt \
   --class org.apache.spark.examples.JavaWordCount \
   ~/spark-examples_2.10-1.6.0.jar file://TwoWords.txt
```

The local file `/my/path/to/local/TwoWords.txt` is uploaded to the tenant's space. When `spark-examples_2.10-1.6.0.jar` runs, it is passed the absolute path to TwoWords.txt as a parameter.

If you use the Analytics for Apache Spark File Transfer service to upload a file before running the spark-submit.sh script, you must specify the URL path segment `my/path/to/remote/` in both the curl command
and the spark-submit.sh script.

For example, upload the file using the curl command:

```
    curl -X PUT -k \
    -u s024-ad54206e4b441f-42a9cf195d79:6865d083-06b6-4028-84c1-4a54645d187f \
    -H "X-Spark-service-instance-id: c7b01e91-3d75-4a1e-a024-ad54206e4b44" \
    --data-binary "@/my/path/to/local/TwoWords.txt" \
    https://169.54.219.20/tenant/data/my/path/to/remote/TwoWords.txt
```

Then run the spark-submit.sh script:

```
   ~/spark-submit.sh \
   --vcap ~/vcap.json \
   --deploy-mode cluster \
   --conf spark.service.spark_version=1.6 \
   --class org.apache.spark.examples.JavaWordCount \
   ~/spark-examples_2.10-1.6.0.jar file://my/path/to/remote/TwoWords.txt
```
