---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-15"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Example: Creating an application using the Spark Interactive API service

Create a sample application that illustrates how to run sample Spark code against a Spark kernel by using the Spark Interactive API service.

The sample application creates the Spark kernel, runs simple Spark code against the kernel, checks the status and the results, and then drops the kernel.

To create a sample application that runs on a Linux system:

1.  Prepare the environment in which you run the sample application. Run the following commands to install the required Node packages:

    ```
    mkdir ~/spark-example
    cat <<EOT > ~/spark-example/package.json
    {
      "name": "spark-example",
      "version": "0.0.0",
      "private": true,
      "dependencies": {
        "jupyter-js-services": "^0.9.0",
        "ws": "^0.8.0",
        "xmlhttprequest": "^1.8.0"
      }
    }
    EOT
    cd ~/spark-example
    npm install
    ```

2.  Create the sample application file. Create a file named
    spark-interactive-demo.js and copy the following  content to the file. Adjust the `tenant_id`,  `tenant_secret`, `instance_id`, and `host`
    variable values to use the VCAP credentials of the Analytics for Apache Spark service that you have
    created.

    ```
    // Access variables with the VCAP information from your Spark service.
    var tenant_id ='sec6-61efb78ac97935-3e8888c56516';
    var tenant_secret ='9e7b8ff6-6c4b-43ec-9bf7-0550d17e820c';
    var instance_id ='dbd0901f-22ac-4486-9ec6-61eeb78ac979';
    var host ='spark.bluemix.net';

    // Client program variables.
    var xmlhttprequest =require('xmlhttprequest');
    var ws =require('ws');
    global.XMLHttpRequest=xmlhttprequest.XMLHttpRequest;
    global.WebSocket= ws;
    var jupyter =require('jupyter-js-services');
    var ajaxSettings = {
        user: tenant_id +'_'+ instance_id,
        password: tenant_secret
    };
    var url ='//'+ tenant_id +'_'+ instance_id +':'+ tenant_secret +'@'+ host +'/jupyter/v2'

    // Sample source code to run against the Spark kernel.
    var sourceToExecute =`
    import pyspark
    rdd = sc.parallelize(range(1000))
    sample = rdd.takeSample(False, 5)
    print(sample)`

    // Start a kernel.
    jupyter.startNewKernel({
        baseUrl:'https:'+ url,
        wsUrl:'wss:'+ url,
        name:'python2-spark21',
        ajaxSettings: ajaxSettings
    })

    // Run the sample source code against the kernel.
    .then((kernel) => {
        var future =kernel.execute({ code: sourceToExecute } );
        future.onDone= () => { process.exit(0); };
        future.onIOPub= (msg) => { console.log('Received message:', msg); };
    }).catch(req=> {
        console.log('Error starting new kernel:', req.xhr.statusText);
        process.exit(1);
    });
    ```

    For more information on jupyter-js-services, see
    [here](https://github.com/jupyterlab/services "(Opens in a new tab or window)").

3.  Run the sample application. Enter the following command to run the Node client:
    ```
    node ~/spark-example/spark-interactive-demo.js
    ```

    The sample Python code sourceToExecute that runs against the Spark  kernel takes 5 numbers and then displays them in the JSON output.
    Example:
    ```
    content: { text: '[882, 635, 978, 219, 773]\n', name: 'stdout' },
    ```
