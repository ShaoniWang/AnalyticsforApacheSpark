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

# Using IBM Cloud Object Storage

You can use IBM Cloud Object Storage to store the data you want to work
with in your applications. Data stored in IBM Cloud Object Storage is
encrypted and distributed across geographies making it highly durable
and available.


Apache Spark uses an object storage connector to access data in an
object store. However, these existing Hadoop open source connectors are
designed to work with file systems rather than object stores and
therefore perform many operations that are not native to object stores.
To overcome these limitations, IBM has created Stocator, a high
performance connector to object storage for Apache Spark. The connector
to IBM Cloud Object Storage in Analytics for Apache Spark is based on
Stocator technology. Note that the connector to Cloud Object Storage is
a beta release.



To provision IBM Cloud Object Storage in which to store data to use in
your Spark application:

1.  Open [IBM Cloud Object
    Storage](https://www.ibm.com/cloud-computing/bluemix/cloud-object-storage "(Opens in a new tab or window)")
    and subscribe to the IBM Cloud Object Storage cross region service.
    Note that a free tier of 25 GB can be obtained by entering an appropriate promotion code.
2.  After the Cloud Object Storage service is provisioned, you can view the details of your storage service.
    1.  Click **Infrastructure \> Storage \> Object  Storage** and select the service you provisioned. The total storage and bandwidth capacity is displayed.

    2.  You must create at least one bucket in which to store your data.

        For details, see [Storing and retrieving
        data](https://ibm-public-cos.github.io/crs-docs/storing-and-retrieving-objects "(Opens in a new tab or window)").  Alternatively, you can create a bucket and add data to the bucket by using REST APIs. For details, see [REST
        APIs](https://ibm-public-cos.github.io/crs-docs/about-compatibility-api "(Opens in a new tab or window)").
3.  To access the newly created bucket from your application, you need the service account credentials.
    1.  Click **Access & Permissions** on the service account page.
    2.  Click **Access Keys** on the storage account details page. You need to remember the access key and the secret key.
4.  Create your application that uses data stored in IBM Cloud Object Storage and run it by using spark-submit.
    1.  Begin your application by enabling the Stocator storage connector to access the data in the IBM Cloud Object Storage service.

        You can use `ibmos2spark` to interact with your Cloud Object Storage. The lib initializes Hadoop configurations. It also provides a function that returns the URL that can be used to fetch a file from your Cloud Object Storage.

        The following example shows you how to define the endpoint and include the IBM Cloud Object Storage credentials:
        ```
        import ibmos2spark

        credentials = {
          'endpoint': 'https://s3-api.objectstorage.softlayer.net/',  
          # just an example. Your url might be different
          'access_key': '',
          'secret_key': ''
        }

        cos = ibmos2spark.CloudObjectStorage(sc, credentials)  #sc is the SparkContext instance

        bucket_name = 'my_bucket'
        file_name = 'myText.txt'
        ```

        Note:

          - The endpoint should be the private endpoint for Dallas.
          - The access key and secret key are the service credential
            values you obtained in an earlier step.
          - To access data in IBM Cloud Object Storage, you need Spark 2.0 or higher.

    2.  Now that the credentials and endpoint are set up, you can access your data.

        The following example shows you how to fetch your data from Cloud Object Storage.

        Notice that the URI for the input data set use the `s3d` prefix.
        This indicates that the Cloud Object Storage connector is to be used to access the data in Cloud Object Storage.

        ```
        # Example fetching file from Cloud Object Storage
        # Input: a text file
        file_url = cos.url(file_name, bucket_name)
        # file_url will be "s3d://my_bucket.service/myText.txt"
        inputDataset = sc.textFile(inputDataset)
        ```

    3.  Submit the application.
