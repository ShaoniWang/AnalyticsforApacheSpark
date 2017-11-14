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

# Using an existing {{site.data.keyword.Bluemix_notm}} Object Storage account in Analytics for Apache Spark

To use data that you stored in a container in an existing Object Storage instance on {{site.data.keyword.Bluemix_notm}}, you need the Object Storage account credentials.

To use the data in an existing Object Storage instance on {{site.data.keyword.Bluemix_notm}} in your Spark application:

1.  Get the access authentication credentials for the existing Object Storage on {{site.data.keyword.Bluemix_notm}}.

  To get this information, select the existing Object Storage instance on the {{site.data.keyword.Bluemix_notm}} dashboard, click **Service credentials**, select the
  container, and view it's credentials. You can copy the credentials verbatim.

2.  To access this existing Object Storage account in  {{site.data.keyword.Bluemix_notm}} and load data to your application, copy the following lines of code, including the Object Storage credentials. For example:

    ```
    !pip install --user ibmos2spark
    import ibmos2spark
    credentials = {
     "auth_url": "https://identity.open.softlayer.com",
     "project": "object_storage_698ca8c5_5310_47bf_9001_xxx",
     "projectId": "0f4bc004asdadfadf669f4c018e9c8873axxx",
     "region": "dallas",
     "userId": "495e1205ed3048a7a2a96c8acd56xxx",
     "username": "Admin_c57a5faeeb30c6a39b08911bf1613c5ef5exxx",
     "password": "UHM(Dadsjfadfadsfpaxxx",
     "domainId": "9a41e4a2e07542f19cd46c8e83cxxx",
     "domainName": "760xxx"}

    # Invoke the Object Storage account
    bmos = ibmos2spark.bluemix(sc, credentials, "json")
    ```
    `sc` is the SparkContext instance.

3.  Load data from the existing Object Storage as follows:

    ```
    data = sc.textFile(bmos.url(container_name, object_name))
    ```
    `object_name` is the name of the file that you want to access from Object Storage and `container_name` is the name of its container. For example:

    ```
    data = sc.textFile(bmos.url("ClimateDataForTutorial","2015.csv"))
    ```
