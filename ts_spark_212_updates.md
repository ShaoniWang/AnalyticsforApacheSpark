---

copyright:
  years: 2017
lastupdated: "2018-01-09"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# What you need to consider when upgrading to Spark 2.1.2

If you upgraded to Spark 2.1.2, you need to consider the following implementation changes:

- [Use of the `@keyword_only` decorator](#use-of-the- @keyword_only-decorator)
- [Connectivity property values](#connectivity-property-values)
- [Provide the `driver` option when accessing data in a database source](#provide-the-driver-option-when-accessing-data-in-a-database-source) 

## Use of the `@keyword_only` decorator
The implementation of the `keyword_only` decorator was changed for Spark 2.1.2. When you upgrade to Spark 2.1.2, all the classes in your code using the `@keyword_only` decorator need to be changed. For an example of the code changes that are required, see this [Stack Overflow question](https://stackoverflow.com/questions/45189191/custom-algorithm-in-pyspark-mllib-function-object-has-no-attribute-input-kw).

## Connectivity property values
The data source connectivity properties are now case-sensitive so that the data source can handle them as-is. For example, the schema name in `currentSchema` is case-sensitive, and must be specified in uppercase characters. If your Spark programs that do not specify the `currentSchema` JDBC  connection property value in uppercase, you will get an `SQLCODE=-204` error. For more information about the supported values for Db2 properties for example, see the [common properties documentation for Db2]( https://www.ibm.com/support/knowledgecenter/en/SSEPEK_10.0.0/java/src/tpc/imjcc_r0052607.html).  

## Provide the `driver` option when accessing data in a database source

To avoid an error message stating that no suitable driver could be  found when accessing data in a database source, for example, `java.sql.SQLException: No suitable driver`, provide the `driver` option with your user credentials. For example, to access Db2 data:
```
properties = {
   'jdbcurl': 'JDBCURL',
   'user': 'USER',
   'password': 'PASSWORD',
   'driver': 'com.ibm.db2.jcc.DB2Driver'
}
```
