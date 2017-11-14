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

# Running a Spark application by using the Spark Interactive API

To use the Spark Interactive API, you first must deploy an instance of
the Analytics for Apache Spark service.

Spark Interactive API is automatically deployed with the Analytics for
Apache Spark service.

To run a Spark application by using the Spark Interactive API:

1.  Create an Analytics for Apache Spark service:

      - Deploy Analytics for Apache Spark using the web interface:
        1.  Sign into [{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net "(Opens in a new tab or window)").
        2.  Click **Catalog** and in Services for Data and Analytics, choose `Apache Spark`.
        3.  Create an Apache Spark service and record the service
            credentials from the Service Credentials page.
      - Deploy Analytics for Apache Spark using the Cloud Foundry cf
        command:
        1.  Log into {{site.data.keyword.Bluemix_notm}} as           follows:

            ```
            cf login -a https://api.ng.bluemix.net -u ${username} -p ${password} -o ${organization} -s ${space}
            ```

        2.  Find the name of your Apache Spark service by entering:

            ```
            cf marketplace | grep spark
            ```

            Choose a service from the service column.

        3.  Find the service plan for the service you chose by entering:

            ```
            cf marketplace -s ${service_name}
            ```

            For example:

            ```
            cf marketplace -s spark
            ```

        4.  Create an Analytics for Apache Spark
            service:

            ```
            cf create-service ${service_name} ${service_plan} ${my_service_name}
            ```

            where `${my\_service\_name}` is a name of your choosing. For example:

            ```
            cf create-service spark ibm.SparkService.PayGoLite example_spark_service
            ```

        5.  Retrieve the Analytics for Apache Spark service credentials:

            1.  Create a Spark service key by using the following
                command:

                ```
                cf create-service-key ${my_service_name} ${my_service_key_name}
                ```

                where `${my\_service\_key\_name}` is a name of your
                choosing. For example:

                ```
                cf create-service-key example_spark_service example_spark_service_key
                ```

            2.  Retrieve the service key in the following way:

                ```
                cf service-key ${my_service_name} ${my_service_key_name}
                ```

                For example:

                ```
                cf service-key example_spark_service example_spark_service_key
                ```

            Example of service credentials:

            ```
            {  
              "cluster_master_url": "https://spark.bluemix.net",  
              "instance_id": "3d1c7867-a20f-4ee7-8c3a-870379666242",  
              "plan": "ibm.SparkService.PayGoLite",  
              "tenant_id": "sc3a-8703796662421f-42a9cf195d79",   
              "tenant_id_full": "3d1c7867-a20f-4ee7-8c3a-870379666242_9c09a3cb-7178-43f9-9e1f-42a9cf195d79",  
              "tenant_secret": "2869d797-0473-4a4f-85a9-c96078491765"
            }
            ```

2.  Access the Spark Interactive API.

    Make an HTTP request to the kernel gateway in a curl command:

      - By using the Authorization HTTP header:

        ```
        curl -v -X GET \
          -u ${tenant_id}_${instance_id}:${tenant_secret} \
          ${cluster_master_url}/jupyter/v2/api
        ```

        For example:

        ```
        curl -v -X GET \
            -u sc3a-8703796662421f-42a9cf195d79_3d1c7867-a20f-4ee7-8c3a-870379666242:2869d797-0473-4a4f-85a9-c96078491765 \
            https://spark.bluemix.net/jupyter/v2/api
        ```

      - Or by using the following URL structure:

        ```
        curl -v -X GET \
          https://${tenant_id}_${instance_id}:${tenant_secret}@${hostname}/jupyter/v2/api
        ```

        For example:

        ```
        curl -v -X GET \
            https://sc3a-8703796662421f-42a9cf195d79_3d1c7867-a20f-4ee7-8c3a-870379666242:2869d797-0473-4a4f-85a9-c96078491765@spark.bluemix.net/jupyter/v2/api
        ```

    You can find the OpenAPI (Swagger) specification of the Spark
    Interactive API at `${cluster_master_url}/api-docs/interactive/swagger.yaml`.

    Alternatively, you can open a browser at
    [https://spark.bluemix.net/api-docs/interactive/swagger.yaml](https://spark.bluemix.net/api-docs/interactive/swagger.yaml "(Opens in a new tab or window)").

3.  Use the Spark Interactive API.

    The Jupyter Kernel Gateway provides code samples in
    [https://github.com/jupyter/kernel\_gateway\_demos](https://github.com/jupyter/kernel_gateway_demos "(Opens in a new tab or window)").

    1.  Run the following commands using the Spark service credentials
        that you retrieved through the Spark service key.

        For
        example:

        ```
        export SPARK_INTERACTIVE_USERNAME=sc3a-8703796662421f-42a9cf195d79
        export SPARK_INTERACTIVE_PASSWORD=2869d797-0473-4a4f-85a9-c96078491765
        export SPARK_INTERACTIVE_INSTANCE_ID=3d1c7867-a20f-4ee7-8c3a-870379666242
        export SPARK_INTERACTIVE_HOST=spark.bluemix.net
        ```

    2.  After the commands have completed, run the following commands
        without making any
        modifications:

        ```
        export BASE_GATEWAY_HTTP_URL=https://${SPARK_INTERACTIVE_USERNAME}_${SPARK_INTERACTIVE_INSTANCE_ID}:${SPARK_INTERACTIVE_PASSWORD}@${SPARK_INTERACTIVE_HOST}/jupyter/v2
        export BASE_GATEWAY_WS_URL=wss://${SPARK_INTERACTIVE_USERNAME}_${SPARK_INTERACTIVE_INSTANCE_ID}:${SPARK_INTERACTIVE_PASSWORD}@${SPARK_INTERACTIVE_HOST}/jupyter/v2
        export BASE_GATEWAY_USERNAME=${SPARK_INTERACTIVE_USERNAME}_${SPARK_INTERACTIVE_INSTANCE_ID}
        export BASE_GATEWAY_PASSWORD=${SPARK_INTERACTIVE_PASSWORD}
        ```

    3.  Run the following command to get the demo
        programs:

        ```
        git clone https://github.com/jupyter/kernel_gateway_demos.git ~/kernel_gateway_demos
        ```

    4.  Modify the node demo program to match the Spark service kernel
        names `python2-spark20`, `scala-spark20`, and `r-spark20`:

        ```
        sed -i.$(date +'%s') \
          -e s/"kernelName: 'python'"/"kernelName: 'python2-spark20'"/g \
          -e s/"kernelName: 'scala'"/"kernelName: 'scala-spark20'"/g \
          -e s/"kernelName: 'ir'"/"kernelName: 'r-spark20'"/g \
          ~/kernel_gateway_demos/node_client_example/src/client.js
        ```

    5.  Run the demo Python client:

        ```
        cd ~/kernel_gateway_demos/python_client_example/src
        python client.py --lang="python2-spark20"
        ```

    6.  Install the prerequisites for the demo node client:

        ```
        cd ~/kernel_gateway_demos/node_client_example/src
        npm install
        ```

    7.  Run the demo node client:

        ```
        cd ~/kernel_gateway_demos/node_client_example/src
        # Node client running "python"
        DEMO_LANG=python node client.js
        # Node client running "scala"
        DEMO_LANG=scala node client.js
        # Node client running "R"
        DEMO_LANG=r node client.js
        ```
