---

copyright:
  years: 2017
lastupdated: "2017-05-31"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with Compose Enterprise
{: #getting-started-with-compose-enterprise}

{{site.data.keyword.composeEnterprise_full}} for Bluemix pairs the needs of the enterprises with the agility of a cloud database service, offering database-as-a-service on dedicated physical machines. In this way, {{site.data.keyword.composeEnterprise}} provides the security and isolation required by enterprise level applications.

{{site.data.keyword.composeEnterprise}} creates a single-tenant cluster, offering you dedicated networking and performance for your database deployments. After the cluster has been created, any database created through one of the other Compose database services that are offered by Bluemix can be provisioned into it.

Complete these steps to get started with {{site.data.keyword.composeEnterprise}}:

## Provisioning a Compose Enterprise service instance
{: provisioning-compose-enterprise}

You can provision a new {{site.data.keyword.composeEnterprise}} instance using the Bluemix console or the command line.

### Provisioning a Compose Enterprise service instance from the Bluemix console

[Create a {{site.data.keyword.composeEnterprise}} instance](https://console.bluemix.net/catalog/services/compose-enterprise/), ensuring that you complete all the fields.

**Notes:**
- The name of your {{site.data.keyword.composeEnterprise}} cluster can have a maximum length of 19 characters, and can contain only alphanumeric characters.
- Choose a *Cloud Provider Region* from the available regions. The location that you select is the SoftLayer data center in which the Compose instance will be deployed.

### Provisioning a Compose Enterprise service instance from the command line

1. Download and install the [Cloud Foundry CLI](https://github.com/cloudfoundry/cli) tool
2. Provision an instance of the service with `cf create-service`:

  ```
  cf create-service service_name service_plan service_instance -c start_command
  ```

  <dl>
    <dt>service_name</dt>
    <dd>
    The name of the Bluemix service you want to create an instance of. The value must be `compose-enterprise`.
    </dd>
    <dt>service_plan</dt>
    <dd>
    The pricing plan for the new service. The value must be `Enterprise`.
    </dd>
    <dt>service_instance</dt>
    <dd>
    The name of the new Compose database service that you want to provision.
    </dd>
    <dt>-c start_command</dt>
    <dd>
    The start_command contains the details of the {{site.data.keyword.composeEnterprise}} cluster that you want to provision. It is formatted as an array and can contain the following values:
      <dl>
        <dt>contact_name (required)</dt>
        <dd>
        The name of the owner of the {{site.data.keyword.composeEnterprise}} cluster
        </dd>
        <dt>contact_phone (required)</dt>
        <dd>
        A contact telephone number for the {{site.data.keyword.composeEnterprise}} cluster owner
        </dd>
        <dt>contact_email (required)</dt>
        <dd>
        An email address for the {{site.data.keyword.composeEnterprise}} cluster owner
        </dd>
        <dt>provider_region (required)</dt>
        <dd>
        The SoftLayer datacenter in which you want the {{site.data.keyword.composeEnterprise}} instance to be deployed. Valid values are: 'amsterdam', 'chennai', 'dallas', 'frankfurt', 'hong kong', 'houston', 'london', 'melbourne', 'milan', 'montreal', 'oslo', 'paris', 'queretaro', 'san jose', 'sao paulo', 'seattle', 'seoul', 'singapore', 'sydney', 'tokyo', 'toronto', 'washington dc'. Choose the location closest to the address on the order, for example Dallas or London.
        </dd>
        <dt>cluster_name (optional)</dt>
        <dd>
        Choose a name for your provisioned {{site.data.keyword.composeEnterprise}} cluster. The maximum length is 19 characters, and can contain only alphanumeric characters.
        </dd>
        <dt>notes (optional)</dt>
        <dd>
        Add any notes relating to your cluster, for example 'Bare Metal'.
        </dd>
      </dl>
    </dd>
  </dl>

Sample cf create-service usage:

```
cf create-service compose-enterprise Enterprise myComposeEnterpriseServiceName -c '{"contact_name": "myName", "contact_phone": "888-888-8888", "contact_email": "myEmail@ibm.com", "provider_region": "dallas", "cluster_name": "myClusterName123", "notes": "Bare Metal" }'
```

When your {{site.data.keyword.composeEnterprise}} Cluster is available, you will be able to provision Compose Bluemix databases into the cluster and enjoy the benefits of auto-scaling databases with encryption at rest and in motion within an isolated cluster.

## Provisioning a Compose Bluemix database into Compose Enterprise
{: #provisioning-database-into-compose-enterprise}

You can provision a Compose Bluemix database into a {{site.data.keyword.composeEnterprise}} cluster when you create a new database from any of the existing Compose database Bluemix services. You can use the Bluemix console or the command line.

### Provisioning a new database into a Compose Enterprise cluster from the Bluemix console

If you have already created a {{site.data.keyword.composeEnterprise}} cluster using Bluemix, you can specify that your new Compose Bluemix database is provisioned into the cluster. Select the name of the {{site.data.keyword.composeEnterprise}} cluster from the list of available locations in the *Select Location for Deployment* drop-down when you are creating the new Compose Bluemix database service instance.

### Provisioning a database into a Compose Enterprise cluster from the command line

To create a new instance of a Compose database service and provision it into a {{site.data.keyword.composeEnterprise}} cluster:

1. Download and install the [Cloud Foundry CLI](https://github.com/cloudfoundry/cli) tool
2. Provision a database with `cf create-service`:

  ```
  cf create-service service_name service_plan service_instance -c start_command
  ```

  <dl>
    <dt>service_name (required)</dt>
    <dd>
    The name of the Compose database service. The value must be one of the following: [compose-for-elasticsearch](https://console.bluemix.net/catalog/services/compose-for-elasticsearch), [compose-for-etcd](https://console.bluemix.net/catalog/services/compose-for-etcd), [compose-for-mongodb](https://console.bluemix.net/catalog/services/compose-for-mongodb), [compose-for-myqsl](https://console.bluemix.net/catalog/services/compose-for-mysql), [compose-for-postgresql](https://console.bluemix.net/catalog/services/compose-for-postgresql), [compose-for-rabbitmq](https://console.bluemix.net/catalog/services/compose-for-rabbitmq),
    [compose-for-redis](https://console.bluemix.net/catalog/services/compose-for-redis), [compose-for-rethinkdb](https://console.bluemix.net/catalog/services/compose-for-rethinkdb), [compose-for-scylladb](https://console.bluemix.net/catalog/services/compose-for-scylladb)
    </dd>
    <dt>service_plan (required)</dt>
    <dd>
    The pricing plan for the new service. The value must be `Enterprise`.
    </dd>
    <dt>service_instance (required)</dt>
    <dd>
    The name of the new Compose Database service that you want to provision.
    </dd>
    <dt>-c start_command (required)</dt>
    <dd>
    The start_command is formatted as an array. It can contain the following values:
      <dl>
        <dt>cluster_id (required)</dt>
        <dd>The Cluster ID of your {{site.data.keyword.composeEnterprise}} cluster. You can find this value in the dashboard of your {{site.data.keyword.composeEnterprise}} service instance.
        </dd>
      </dl>
    </dd>
  </dl>

Sample cf create-service usage:

```
cf create-service compose-for-elasticsearch Enterprise myComposeForEnterpriseService -c '{"cluster_id": "123456781234567812345678"}'
```
