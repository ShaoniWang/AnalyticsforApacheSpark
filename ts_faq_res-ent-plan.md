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

# FAQ: How is the Reserved Enterprise Plan Spark service instance configured?

## Is the provisioned Spark cluster shared with other users? How is the multi-tenant cluster managed to avoid impact on workloads?

The Spark Service cluster is a shared multi-tenant cluster. Reserved
Enterprise Plan tenants have a claim on their resources, and priority
over Personal-Free Plan tenants in the following ways:

1.  Reserved Enterprise plan tenants have priority over Personal-Free
    plan tenants in resources, job scheduling, and so on.
2.  Reserved Enterprise Plan tenants have their own job scheduling,
    separate from Personal-Free Plan tenants. This means faster
    performance, with no contention or conflict with Personal-Free Plan
    tenants.
3.  Using cloud services ensures that sufficient capacity is available
    to all tenants, such that in practice a reallocation of resources
    should rarely be required.

Reserved Enterprise Plan tenants each get a Spark cluster with
guaranteed capacity – memory and CPU cores – as follows:

  - Reserved Enterprise Plan tenants get 16 GB driver memory. The
    language runtimes also get memory on top of this. For example,
    Python runtime gets 48 GB of memory.
  - Each Spark job can run at most 150 Spark tasks in parallel, with a
    minimum of 2 GB data partitions per task.
  - This can translate into 150 executors each with 1 task at 6 GB of
    memory each. In practice, you can get tens of executors, each
    running at most 3 Spark tasks, each with at least 2 GB of memory.
  - You can run many Spark jobs concurrently, each with the above
    reserved resources at their disposal.
