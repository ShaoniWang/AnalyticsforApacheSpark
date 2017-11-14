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

# Example: Creating a Spark application

Learn how to create a Spark application that uses the SparkPi.scala
sample code shipped with spark-1.6.3-bin-hadoop2.6.tgz package.

Sample Scala code is included in the spark-1.6.3-bin-hadoop2.6.tgz
package, which you can download from
[here](https://www.apache.org/dist/spark/spark-1.6.3/spark-1.6.3-bin-hadoop2.6.tgz "(Opens in a new tab or window)").

While you create and test your application, you might want to run
several tests that use the Analytics for Apache Spark environment. In
that case, you can upload files or JAR files as needed by using file
transfer commands and environment variables. See [Example: Optional file
transfer and environment configuration](./spark_environment_example.html).

1.  Determine if you already have the Scala compiler installed by
    running the following command: `sbt help`. If the Scala compiler is
    not installed, follow the instructions on the Scala website at
    [http://www.scala-sbt.org/release/tutorial/Installing-sbt-on-Linux.html](http://www.scala-sbt.org/release/tutorial/Installing-sbt-on-Linux.html "(Opens in a new tab or window)").

2.  Copy the sample Scala application to a local workspace. For example:

    ```
    mkdir -p ~/spark-submit-example/project
    mkdir -p ~/spark-submit-example/src/main/scala
    cp /opt/spark/examples/src/main/scala/org/apache/spark/examples/SparkPi.scala ~/spark-submit-example/src/main/scala/SparkPi.scala
    ```

3.  Create a new file, `~/spark-submit-example/build.sbt` with the
    following contents:

    ```
    name := "SparkPi"

      version := "1.0"

      scalaVersion := "2.10.4"

      libraryDependencies += "org.apache.spark" %% "spark-core" % "1.6.0"

      resolvers += "Akka Repository" at "http://repo.akka.io/releases/"
    ```

    Important: The blank lines are required.

4.  Create a new file, `~/spark-submit-example/project/build.properties`,
    by running the following command:

    ```
    cat <<EOT > ~/spark-submit-example/project/build.properties
    sbt.version=0.13.2
    EOT
    ```

5.  Verify that your directory structure looks like the following
    example:

    ```
    +-- build.sbt
    +-- project
    |   +-- build.properties
    +-- src
    +-- main
    +-- scala
        +-- SparkPi.scala
    ```

6.  Build the JAR file. For example, run the following commands:

    ```
    cd ~/spark-submit-example
    sbt package
    ```

    The resulting application JAR file is
    `~/spark-submit-example/target/scala-2.10/sparkpi\_2.10-1.0.jar`.

## What to do next

Run the application using the spark-submit.sh script which you
downloaded in your local shell. For more information, see [Example:
Running a Spark application with optional parameters](./spark_submit_example.html).
