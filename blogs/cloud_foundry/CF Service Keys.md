# CloudFoundry Services Keys

# Introduction
The CloudFoundry (CF) platform-as-a-service (PaaS) has an extensible model via CF services wherein new service providers can easily be added and enable their service instance in any CF installation. These services appear into the CF marketplace and can easily be bound to (connected to) by any user running a CF application.

While powerful, the binding model for CF applications to services is also restrictive. In particular it means that CF services can only be used with CF applications and their lifecycle cannot easily survive the applications they are bound to. In this post we will discuss Services Keys which is a new feature added to CF that resolves this issue. We will describe an example broker that makes use of this new feature as well as two additional new feature to the CF services architecture: async provisioning and arbitraty parameters.

# Use cases

Besides restricting the lifecycle of a CF service to a CF application, the current CF services architecture caused some problems when trying to address some specific use cases.

For instance, with the popularity of Docker, there has been an increasing interest by CF users in using that container platform. In particular, users are wanting to experiment setting up their own Docker files and running applications. However, these application still need to connect to some service, so having them bind to a CF service is complicated since there may not be an easy way to run these docker application as CF applications.

Additionally, there has been various discussions for the need to share a service instance with multiple applications. For instance, some enterprise users may have many applications for one data source that is exposed as a service. One application can be given read-only access to the service instance database while another application has limited read-write access, while an admin application could have full access. In all of these cases, the current CF service model does nothing to facilitate this division of access since all applications accessing the service instance need to bind resulting in the same access.

Finally, another major issue with the current architecture was how to revoke or renew access to a service instance without having the application rebind to the service. For instance, the service credential information may have been updated with new enterprise rules and therefore require all application bound to it to get new credentials. In the current model this means that all applications need to rebind and be restaged to get the new credentials, a cumbersome proposition.

# Overview

To address the issues above and many more, this IBM team worked with Pivotal to create a new service endpoint called: Service Keys which decouples the process of accessing and managing access to a service with the service instance itself and the applications that bind to it.

The new endpoint acts like anything else in CF and CloudCountroller in that it is a REST endpoint giving CRUD (create, read, update, and delete) access to a new resource, this one called: ServiceKey. Think of it as exposing access to credential information for a service instance. Using the credentials any CF API agent (a CF application, CLI, curl, etc) can perform lifecycle operations to access service credentials. Using these credentials or service keys, the agent can then access and use the service (that is bind to it).

# Service Keys

As we mentioned the new Service Key feature is added as a new resource which essentially externalizes the old service binding operation, except it does not require an application to be called or manipulated. Like other CF Cloud Controller (CC) resources, this one has the typical CRUD operations which we describe and give example of below.

## Create

Creating a new Service Key means calling an HTTP POST operation on the new service_keys endpoint using an already created service instance. So for example:

```
POST /v2/service_keys

{
  "service_instance_guid": "4c0025a1-46b7-4843-97a9-1a406e4ae950", 
  "name": "key-1",
  "parameters": {}
}
```
In the HTTP body, the `service_instance_guid` and `name` is required, the optional `parameters` is an arbitrary JSON object to pass along to the service broker.

Assuming the current user agent is properly authenticated and the service instance GUID is valid then the result can be a new Service Key such as:

```
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

## Read
Retrieving a Service Key can be done through an HTTP GET operation on the service_keys endpoint by using an service key GUID or on service_instances endpoint with service_instances GUID and service key name. So for example:

```
GET /v2/service_keys/d323f959-73bb-4fd8-b2b7-164677a4650c
```
or:

```
GET /v2/service_instances/4c0025a1-46b7-4843-97a9-1a406e4ae950/service_keys?q=name:key-1
```

If the request is successfully processed, the response code and body will be like:

```
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
      "password": "mysecret"    },
    "service_instance_url": "/v2/service_instances/4c0025a1-46b7-4843-97a9-1a406e4ae950"
  }
}
```

If the current user is Space Manager or Space Auditor, a response code `404 Not Found` will be returned.

## List
As a developer or admin user, Service Keys can be retrieved by HTTP GET operation on the service_keys endpoint without any parameter. But Space Manager and Auditor user can't retrieve the Service Keys which means 0 results will be returned.

```
GET /v2/service_keys
```

If the Service Keys are successfully retuned, the result will be like:

```
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
    }
  ]
}
``` 

## Delete

The Service Key can be deleted by using HTTP DELETE opeartion on service_keys endpoint. Currently Space Manager and Auditor are not authorized to perform delete operation. Only Admin and Space Developer have this permission.

```
DELETE /v2/service_keys/d323f959-73bb-4fd8-b2b7-164677a4650c
```
If the delete operation succeeds, The response code will be:

```
204 No Content
```

# Example broker

[TODO: describe the example Go service broker, include links to video and Github]

# Async and arbitrary parameters

[TODO: mention briefly that the example Go service broker also uses the Async and Arbitrary parameter features. Add links to the documentation for these features]

# Conclusion

Working closely with Pivotal over the month of March and April we were able to improve the current CF services architecture to externalize the CF service credentials. This new feature opens a series of new use cases in how CF services can be used. The new feature remains backward compatible with existing brokers since they are able to easily implement the ServiceKey broker APIs with their old service binding (just without an app_id). This means that old brokers should be able to quickly support service keys and open the door for a whole new class of CF service users, such as Docker applications.
