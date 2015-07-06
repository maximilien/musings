# CloudFoundry Services Keys and Sample Go Service Broker

![credit: blog.trustmyroot.com](http://blog.trustmyroot.com/wp-content/uploads/2015/06/Cloud-Encryption.jpeg)

# Introduction

The CloudFoundry (CF) platform-as-a-service (PaaS) has an extensible model via CF services wherein new service providers can easily be added and enable their service instance in any CF installation. These services appear into the CF marketplace and can then easily be, discovered, bound to (connected to), and used by any user running a CF application.

While powerful, the binding model for CF applications to services was also a bit restrictive. In particular it meant that CF services could only be used with CF applications and a service's lifecycle could not easily survive the applications they were bound to. 

In this post we will introduce and discuss `CF Services Keys` which is a new feature added to CF that resolves this issue. We will describe an example broker that makes use of this new feature as well as two additional new features of the CF services architecture: `Async Service Provisioning` and `Arbitrary Service Parameters`. We will also describe a [new sample service broker](https://github.com/cloudfoundry-samples/go_service_broker), written in [Golang](https://golang.org/), that we have implemented that illustrates the use of these new features.

# Use cases

Besides restricting the lifecycle of a CF service to a CF application, the current CF services architecture also caused some problems when trying to address specific service use cases.

For instance, with the popularity of Docker, there has been an increasing interest by cloud users in using that container platform. In particular, users are wanting to experiment setting up their own Docker files and running applications. However, these application still need to connect to exisisting services, so having them bind to a CF service is complicated since there may not be an easy way to run these docker applications as CF applications.

Additionally, there has been various discussions for the need to share a service instance with multiple applications. For instance, enterprise users may have many applications for one data source (a database) that is exposed as a service. One application can be given read-only access to the service instance while another application has limited read-write access, while an admin application could have full access. In all of these cases, the current CF service model does nothing to facilitate this division of access since all applications accessing the service instance need to bind resulting in the same access.

Finally, another major issue with the current architecture was how to revoke or renew access to a service instance without having the application rebind to the service. For instance, the service credential information may have been updated applying new enterprise security rules and therefore requiring all applications bound to it to get new credentials. In the current model this meant that all applications needed to rebind and be restaged to get the new credentials, a cumbersome proposition.

# Overview

To address the issues mentioned above and many more, this IBM team worked with Pivotal to create a new service endpoint called: `/service_keys` which decouples the process of accessing and managing access to a service with the service instance itself and the applications that bind to it.

The new endpoint acts like anything else in CF and CloudCountroller in that it is a REST endpoint giving CRUD (create, read, update, and delete) access to a new resource, this one called: ServiceKey. Think of it as exposing access to credential information for a service instance. 

Using the credentials any CF API agent (a CF application, CLI, curl, etc) can perform lifecycle operations to manage service credentials. Using these credentials or service keys, the agent can then access and use the service (that is bind to it).

# Service Keys

As we mentioned the new Service Key feature is added as a new resource which essentially externalizes the old service binding operation, except it does not require an application to be called or manipulated. Like other CF Cloud Controller (CC) resources, this one has the typical CRUD operations (except update, but includes listing) which we describe and give example of below.

## Create

Creating a new Service Key means calling an HTTP POST operation on the new `/service_keys` endpoint using an already created service instance. So for example:

```json
POST /v2/service_keys

{
  "service_instance_guid": "4c0025a1-46b7-4843-97a9-1a406e4ae950", 
  "name": "key-1",
  "parameters": {}
}
```
In the HTTP body, the `service_instance_guid` and `name` is required, the optional `parameters` is an arbitrary JSON object to pass along to the service broker.

Assuming the current user agent is properly authenticated and the service instance GUID is valid then the result can be a new Service Key such as:

```json
201 Created

{
  "metadata": {
    "guid": "d323f959-73bb-4fd8-b2b7-164677a4650c",    
    "url": "/v2/service_keys/d323f959-73bb-4fd8-b2b7-164677a4650c",    
    "created_at": "2015-06-25T10:06:45Z",
    "updated_at": null
  },
  "entity": {
    "name": "key-1",
    "service_instance_guid": "4c0025a1-46b7-4843-97a9-1a406e4ae950",
    "credentials": {
      "user": "admin",
      "password": "mysecret"
    },
    "service_instance_url": "/v2/service_instances/4c0025a1-46b7-4843-97a9-1a406e4ae950"
  }
}
````

## Retrieve

Retrieving a Service Key can be done through an HTTP GET operation on the `/service_keys` endpoint by using an service key GUID or on the `/service_instances` endpoint with the service instance's GUID and service key name. So for example:

```
GET /v2/service_keys/d323f959-73bb-4fd8-b2b7-164677a4650c
```
or:

```
GET /v2/service_instances/4c0025a1-46b7-4843-97a9-1a406e4ae950/service_keys?q=name:key-1
```

If the request is successfully processed, the response code and body will be like:

```json
200 OK

{
  "metadata": {
    "guid": "d323f959-73bb-4fd8-b2b7-164677a4650c",
    "url": "/v2/service_keys/d323f959-73bb-4fd8-b2b7-164677a4650c",
    "created_at": "2015-06-25T10:06:45Z",
    "updated_at": null
  },
  "entity": {
    "name": "key-1",
    "service_instance_guid": "4c0025a1-46b7-4843-97a9-1a406e4ae950",
    "credentials": {
      "user": "admin",
      "password": "mysecret" 
    },
    "service_instance_url": "/v2/service_instances/4c0025a1-46b7-4843-97a9-1a406e4ae950"
  }
}
```

If the current user has [Space Manager or Space Auditor](https://docs.cloudfoundry.org/concepts/roles.html) priviledge, a response code `404 Not Found` will be returned.

## List

As a developer or admin user, Service Keys can be retrieved by HTTP GET operation on the `/service_keys` endpoint without any parameter. But Space Manager and Auditor user can't retrieve the Service Keys which means 0 results will be returned.

```
GET /v2/service_keys
```

If the Service Keys are successfully retuned, the result will be like:

```json
{
  "total_results": 1,
  "total_pages": 1,
  "prev_url": null,
  "next_url": null,
  "resources": [
    {
      "metadata": {
        "guid": "d323f959-73bb-4fd8-b2b7-164677a4650c",
        "url": "/v2/service_keys/d323f959-73bb-4fd8-b2b7-164677a4650c",
        "created_at": "2015-06-25T10:06:46Z",
        "updated_at": null
      },
      "entity": {
        "name": "name-52",
        "service_instance_guid": "4c0025a1-46b7-4843-97a9-1a406e4ae950",
        "credentials": {
          "creds-key-19": "creds-val-19"
        },
        "service_instance_url": "/v2/service_instances/4c0025a1-46b7-4843-97a9-1a406e4ae950"
      }
    },
    [...],
  ]
}
``` 

## Delete

A Service Key can be deleted by using HTTP DELETE opeartion on `/service_keys` endpoint. Currently Space Manager and Auditor are not authorized to perform delete operation. Only Admin and Space Developer have this permission.

```
DELETE /v2/service_keys/d323f959-73bb-4fd8-b2b7-164677a4650c
```
If the delete operation succeeds, The response code will be:

```
204 No Content
```

# Example Service Broker

Based on the implementation for `/service_keys` mentioned above, we created a new service broker which supports this new feature. This service broker is written in Golang and is designed to provide AWS virtual machine manipulation service. Future infrastructure-as-a-service, e.g., SoftLayer or OpenStack, may also be supported in the future.

This new service broker essentially provides AWS virtual machine as a service and different types of the virtual machine can be requested. For instance, `t2.micro` or `t2.small`, which are treated as different service plans. By using this service broker, a user can create/delete virtual machines in the AWS environment by treating them as service instances. 

In addition, the service broker also support the CRUD operations of service keys. When creating a service key for a virtual machine, the service broker will generate an SSH key pair, inject the public key into the remote virtual machine and return the private key as the service key.  

We recorded a video demo of how to use this new service broker to manipulate service keys. Readers who is interested in this new feature, please find this video at: <a>https://www.youtube.com/watch?v=V5uzLcPQPmo</a>

We have contributed this service broker to CloudFoundry community, now the source code is put in the CloudFoundry samples repository, at: [https://github.com/cloudfoundry-samples/go_service_broker](https://github.com/cloudfoundry-samples/go_service_broker)

# Async and arbitrary parameters

Besides service key, Pivotal service team and IBM CloudFoundry development team also developed two other new features for CloudFoundry services: Service Async and Service Arbitrary Parameters.

## Service Async Provisioning

In previous CloudFoundry releases, when creating a service instance, there was a limitation to how long the broker could take to create the service instance and to have it ready for use. Typically this was limited to 60 seconds. Otherwise, the creation of the service instance would fail. This limitation blocked the ability for large services from being added into CloudFoundry. For example, some large database service, used for analytics, may take a long time to create. 

To resolve this issue, the CF Service APIs team implemented a new mechanism for service instance creation, named Service Async Provisioning. This new mechanism changed the service creation process from a synchronized process to a asynchrornous process. This new feature defines a new response for service broker who supports async service creation. Service broker now can respond that the service instance creation is 'in progress' and CloudFoundry will immediately respond the user without waiting for the service instance to be ready. 

After the immediate response from the CloudFoundry to the end user, CloudFoundry will then launch a backend process to poll the service instance status information from the service broker, until the service broker replies that the service instance is 'created successfully'. During the creation process of a service instance, end user can always use the 'cf service service-instance-name' command to check the creation status of a service instance. 

Since virtual machines on AWS and other infrastructure-as-a-service clouds may take more than 60 seconds to be ready for use, we used this new async feature in the Go service broker mentioned above. We have recorded a video demo using this Go service broker, please find the video on Youtube

[![Sample Golang Broker: Async Provisioning](http://img.youtube.com/vi/Ij5KSKrAq9Q/0.jpg)](http://www.youtube.com/watch?v=Ij5KSKrAq9Q)

## Service Arbitrary Parameters

In previous CloudFoundry, when creating a service instance, there was no way to configure the created service instance or pass some launch parameters to the service instance. Some work around to resolve this issue was to provide different service instance configurations, by providing different service plans from the service broker. However, in some of the situations, we would need to write a lot of different service plans in the service catalog for different config options combinations, which poluted the catalog and degraded the experience of end-users.

To resolve this issue, the CF Service APIs team has implemented a new command option to help pass arbitrary parameters when creating service instances. By providing a new command option '-p' with an arbitrary JSON string in the CloudFoundry cli command `$cf create service`, now CF can pass the JSON string parameter to the service broker and service broker will parse the json string and configure the service instance according to the content of the JSON parameter.

Our Go service broker also make use of this new arbitrary service parameters feature in order to pass the type (size) of the virtual machine to provision. We also have recorded a video demo using this feature in our Go service broker, please find the video on Youtube:

[![Sample Golang Broker: Arbitrary Parameters](http://img.youtube.com/vi/Qc3bZljGscs/0.jpg)](http://www.youtube.com/watch?v=Qc3bZljGscs)

# Conclusion

Working closely with Pivotal over the month of March and April we were able to improve the current CF services architecture to externalize the CF service credentials. This new feature opens a series of new use cases in how CF services can be used. The new feature remains backward compatible with existing brokers since they are able to easily implement the `/service_keys` broker APIs with their old service binding (just without an 'app_id' parameter). This means that old brokers should be able to quickly support service keys and open the door for a whole new class of CF service users, such as Docker applications. 

And to help accelerate the usage of this new feature, we have also created a new Service Broker in Golang that takes advantage of the new CF services features, including Service Keys, Service Async, and Arbritrary Parameters. The broker essentially exposes the creation and management of infrastructure-as-a-service virtual machines as a CF service. Using this new broker you can easily create new VMs (regarless of how long they take) and access ssh keys for these VMs. The broker is now part of the CF samples and supports creating AWS VMs.
