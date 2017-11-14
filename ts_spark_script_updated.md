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

# Older version of the spark-submit script not supported

The spark-submit.sh script was updated and contains a security fix that
does not permit submitting Spark jobs using scripts versions earlier
than version 1.0.5.

## Symptoms

When you start a Spark application by using an older version of the
spark-submit.sh script, the application will not run and you will see
the following error message in the spark-submit
log:

```
The version of spark-submit.sh you are using is no longer supported. Please upgrade to at least VERSION: 1.0.5.
```

## Resolving unsupported spark-submit script issues

To enable running Spark applications by using the spark-submit script:

1.  Check the script version that spark-submit is using by entering the
    following command:

    ```
    $ ./spark-submit.sh --version
    ```

    You need the script version 1.0.5, or later.

2.  If you are using an earlier version of the script, use the latest
    script from the following site:
    [https://spark.bluemix.net/batch/spark-submit.sh](https://spark.bluemix.net/batch/spark-submit.sh "(Opens in a new tab or window)").
