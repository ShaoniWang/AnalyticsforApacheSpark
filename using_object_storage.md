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

# Using Object Storage accessed through the Swift API

You can use {{site.data.keyword.objectstoragefull}} to store the data you want
to work with in your applications.


{{site.data.keyword.objectstoragefull}} provides you with access to a fully provisioned Swift Object Storage service to manage your data files.
Swift provides a fully distributed, API-accessible storage platform. You
can use it directly in your applications or for backups, making it ideal
for cost effective, scale-out storage.



To provision Swift Object Storage to use in your Spark application to
store data files:

1.  Open the {{site.data.keyword.Bluemix_notm}} dashboard, select **Create service** and then **Services > Storage**.
2.  Click **Object Storage**, select a service plan and create an Object
    Storage instance.
3.  To access Object Storage in your application, you need the Object
    Storage account credentials. To obtain the Object Storage
    credentials:
    1.  Open the {{site.data.keyword.Bluemix_notm}} Dashboard and select **Storage**.
    2.  Select the Object Storage service you just created and copy the
        service credentials which you can view on the Service
        credentials tab.

## Results

If you want to access data in your applications in existing Object
Storage, follow the instructions in the following topics:

  - [Using an existing {{site.data.keyword.Bluemix_notm}} Object Storage account in IBM Analytics for Apache Spark](./reusing_existing_bluemix_object_storage.html).
  - [Using an external SoftLayer Object Storage account in IBM Analytics
    for Apache
    Spark](./ReusingObjectStorageOnExternalSoftLayer.html).
