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

# Using an external SoftLayer Object Storage account in Analytics for Apache Spark

To use data that you stored in Object Storage hosted on SoftLayer, you need the SoftLayer Object Storage account credentials.

To use the data in an existing external Object Storage instance in your application:

1.  Get the access authentication credentials for the existing Object Storage on SoftLayer.

    You need the following information from your external SoftLayer account:

    1.  The public authentication endpoint URL
    2.  Your user name and API Key (password)
    3.  A container name

2.  To configure access to the external Object Storage account and enable loading data from this Object Storage to your application, copy the following lines of code:

    ```
    !pip install --user ibmos2spark
    import ibmos2spark
    # Enter the credentials to your Softlayer Object Storage
    auth_url = 'xxx'
    tenant = 'xxx'
    username = 'xxx'
    password = 'xxx'
    # You can give it any name you like
    configuration_name = "my_softlayer_os"
    ```

    Enter the values for `auth_url`, `tenant`, `username`, and `password` from your SoftLayer account. The value of `configuration_name` can be any value you choose for your configuration.

3.  Invoke the Object Storage account function by running the following code in a cell:
    ```
    slos = ibmos2spark.softlayer2d(sc, configuration_name, auth_url, tenant, username, password)
    ```

    `sc` is the SparkContext instance.

4.  Load data from Object Storage as follows:

    ```
    data = sc.textFile(slos.url(container_name, object_name))
    ```

    `object_name` is the name of the file that you want to access from Object Storage and `container_name` is the name of its container. For example:

    ```
    data = sc.textFile(slos.url("ClimateDataForTutorial","2015.csv")
    ```
