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

# Requirement to use Spark Interactive API

To use the Spark Interactive API service, you must have an existing
instance of the Analytics for Apache Spark service.

With your Spark service credentials, you can make HTTP requests to the
Kernel Gateway by using the Spark Interactive API. To construct the HTTP
request to your Spark Interactive API instance, you need the following
Spark service credentials:

  - `tenant_id`
  - `tenant_secret`
  - `instance_id`
  - `cluster_master_url`

The HTTP request must:

1.  Use the HTTPS and WSS protocols.
2.  Prefix all Kernel Gateway APIs with `/jupyter/v2`.
3.  Use an HTTP header or conform to a required URL format.
      - HTTP header:

        `Authorization` HTTP header (in accordance with
        [RFC7235](https://tools.ietf.org/html/rfc7235 "(Opens in a new tab or window)"))
        with a value of `"Basic value"` where `value` is the base-64
        encoding of `"${tenant_id}_${instance_id}:${tenant_secret}"`

      - URL format:

        ```
        https://${tenant_id}_${instance_id}:${tenant_secret}@${cluster_master_url-host}/jupyter/v2/...
        ```

For example, if you make an HTTP request to the Spark Interactive API by
using a curl command, use the following command syntax:

```
 curl -v -X GET \
    -u ${tenant_id}_${instance_id}:${tenant_secret} \
    ${cluster_master_url}/jupyter/v2/api
```

The URL format that is used to access the Spark Interactive API allows
you to run the client program against the Kernel Gateway in the cluster
as well as a local instance of the Kernel Gateway that was launched with
the `--KernelGatewayApp.base_url=/jupyter/v2` parameter or the
`KG_BASE_URL=/jupyter/v2` environment variable.
