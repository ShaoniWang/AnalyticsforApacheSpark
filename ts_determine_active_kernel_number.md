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

# Spark kernel limit reached when using the Spark Interactive API

Each Apache Spark instance can have a maximum of 10 active kernels. Once
that limit is reached, no new Spark kernels can be created.

## Symptoms

When you request a new kernel when using the Spark Interactive API and
the returned message states that the kernel limit was reached, you must
delete another active kernel before you can create a new kernel.

## Resolving the problem

You can monitor the number of active kernels when using the Spark
Interactive API to allow for the creation of a new kernel.

## Determining the number of active Spark kernels

To monitor the number of active kernels when using the Spark Interactive
API:

1.  Determine the number of active kernels by running the following
    command:

    ```
    https://${tenant_id}_${instance_id}:${tenant_secret}@spark.bluemix.net/jupyter/v2/api/kernels
    ```

    If the command returns the following response, the kernel limit was
    reached:

    ```
    {"message": "Resource Limit", "reason": "Payment Required"}
    ```

2.  If the kernel limit was reached, run the following curl command to
    delete another active kernel:

    ``` 
    curl -v -X DELETE \
        -u ${tenant_id}_${instance_id}:${tenant_secret} \
        https://spark.bluemix.net/jupyter/v2/api/kernels/${kernel_id}
    ```
