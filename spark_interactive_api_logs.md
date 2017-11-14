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

# Accessing the Spark Interactive API logs

You can monitor the Spark Interactive API log files in a Python notebook
in Analytics for Apache Spark.

To access and monitor the Spark Interactive API log files for errors:

1.  On the {{site.data.keyword.Bluemix_notm}} dashboard, click your  Analytics for Apache Spark service and select to work with notebooks.
2.  Click NEW NOTEBOOK to create a new blank Python notebook.
3.  In the new notebook, run the following commands in a code cell:
      - To view your home directory, run:

        ``` pre codeblock
        !ls -l ${HOME}
        ```

      - To view the list of available log files, run:

        ``` pre codeblock
        !cat ${HOME}/kgateway-stdout.log
        ```

      - To view the last bootstrap log, use the last line in
        kgateway-stdout.log. For example:

        ``` pre codeblock
        !cat ${HOME}/kgateway/logs/bootstrap-20160726_195538.log
        ```

      - To view a list of the Kernel Gateway logs, run the following
        command:

        ``` pre codeblock
        !ls -latr ${HOME}/kgateway/logs
        ```

      - To view the contents of a more recent log file, run the
        following command with the name of a log file that appears at
        the bottom of the list of log files. For example:

        ``` pre codeblock
        !cat ${HOME}/kgateway/logs/jupyter-20160726_195538.log
        ```
