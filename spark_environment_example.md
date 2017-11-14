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

# Example: Optional file transfer and environment configuration

You can upload files as needed and create a script to configure
environment variables while you develop and test your application.

You can upload your application files to the Spark cluster as part of
the spark-submit.sh script, or you can use the Analytics for Apache
Spark File Transfer service. In this example, you upload application and
supporting files, and create a script that configures the Analytics for
Apache Spark service to use the specified files.

Restriction: The maximum file size that you can upload using the
spark-submit.sh script or the file transfer commands is 200 MB.

To transfer files and configure the environment:

1.  Upload your application JAR files, and any other supporting files,
    using the curl command. The syntax to upload a file is:

    ```
    curl \
        -X PUT \
        -k \
        -u ${tenant_id}:${tenant_secret} \
        -H "X-Spark-service-instance-id: ${instance_id}" \
        --data-binary "@${path_to_local_file}" \
        ${cluster_master_url}/tenant/data/${path_to_remote_file}
    ```

    For example:

    ```
    curl \
        -X PUT \
        -k \
        -u sa80-b8cffa2153a41f-42a9cf195d79:f1f442df-a27e-40c7-9623-b04ef0a86a05 \
        -H "X-Spark-service-instance-id: 18728f7e-b4e9-42a7-ba80-b8cffa2153a4" \
        --data-binary "@/my/path/to/local/file.txt" \
        https://169.53.43.71/tenant/data/my/path/to/remote/file.txt
    ```

2.  Create a script that configures the Analytics for Apache Spark
    service to use the specified files. For example, create a file
    `spark-submit-environment.sh` by running the following command:

    ```
    cat <<EOT > ~/spark-submit-environment.sh
    export SS_APP_MAIN_UPLOAD=false
    export SS_FILES_UPLOAD=false
    export SS_JARS_UPLOAD=false
    export SS_LOG_ENABLE=false
    EOT
    ```

    In this example, the variables are:

      - **SS\_APP\_JAR\_UPLOAD=**   
        The default value is true, in which case the application JAR
        file is uploaded to the cluster when you run the spark-submit.sh
        script. Set the value to false if you already uploaded the
        application JAR file.

      - **SS\_FILES\_UPLOAD=**   
        The default value is true, in which case the files specified in
        `--files` are uploaded to the cluster when you run the
        spark-submit.sh script. Set the value to false if you already
        uploaded the files and file paths in the `--files` options are the file paths on the cluster.

      - **SS\_JARS\_UPLOAD=**  
        The default value is true, in which case the files specified in
        the `--jars` option are uploaded to the cluster when you run the
        spark-submit.sh script. Set the value to false if you already
        uploaded the JAR files and the JAR file paths specified in the
        `--jars` option are the JAR file paths on the cluster.

      - **SS\_LOG\_ENABLE=**  
        The default value is true, in which case the log is created. Set
        the value to false to view all log entries in the terminal
        without saving them to a log file.

3.  Export the environment variables by running the following command:
    `source~/spark-submit-environment.sh` in your local shell where you
    run the spark-submit.sh script.

4.  View the current status of the environment variables by running the
    grep command. For example:

    ```
    set| grep SS_
    # SS_APP_JAR_MOVE=false# SS_FILES_MOVE=false
    ```
