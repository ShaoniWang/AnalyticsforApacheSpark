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

# Spark Interactive API

The Spark Interactive API is a web service that enables you to create
non-notebook web clients that can provision and use Jupyter kernels.

The Spark Interactive API incorporates [Jupyter Kernel
Gateway](https://github.com/jupyter/kernel_gateway "(Opens in a new tab or window)") into the Analytics for Apache Spark service offering.
Most of the Jupyter Kernel Gateway functionality that is supported by
the Spark Interactive API is documented in
[ReadTheDocs](https://jupyter-kernel-gateway.readthedocs.io/en/latest/ "(Opens in a new tab or window)")
and
[GitHub](https://github.com/jupyter/kernel_gateway "(Opens in a new tab or window)").

The difference between Jupyter Kernel Gateway and Spark Interactive API
is the need for additional URL segments, credentials to support
authorized authentication, and the exclusive use of the `https://`
protocol.

You do not have to install nor configure the Spark Interactive API
service when you deploy an Analytics for Apache Spark service. The
native Jupyter Kernel Gateway code is automatically deployed in the
Apache Spark service.

The Spark Interactive API service allows you to write applications that
run Spark code against a Spark context and to maintain this context for
as long as you need it.
