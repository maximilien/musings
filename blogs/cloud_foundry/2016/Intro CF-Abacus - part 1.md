# Introduction to CF-Abacus - Part 1 of 3

## Abstract

Project CF-Abacus is a scalable usage aggregation and metering engine for any CloudFoundry (CF) installation. The point of the project is to provide a complete turnkey solution that any CF vendor can use to enable their CF installation with usage metering and aggregation in a manner that will scale with number of users, organization, and services. This is achieved by following a micro-services pipeline architecture for the different stages of collection, metering, and aggregation, as well as supporting various backend database systems that can scale via sharding. Additionally, a key design point of CF-Abacus is to enable the various parts of the pipeline to be ran as applications on the CF installation, thereby benefiting from the easy management and scale-up and -down aspects of CF itself.

## Problem

CloudFoundry (CF) is designed to be a multiuser, multiplication operating system for any cloud. What this means is that out of the box, any CF installation is pretty much ready (assuming the necessary cloud resources are available) to serve 1000s of different users with 100s of applications each. Users can be grouped into organizations and these into spaces.

Naturally, for any decent size installation of CF, whether it be public, dedicated, or private, there will eventually be a need to understand and manage information about what applications are running for which user, what services they use, and more importantly what resources these applications and services are using at any point and time and over time.

Collecting, aggregating, manipulating such metering information (in it’s many formats and guises) constitute the core of what a metering engine needs to provide. The problem is essentially one of accounting. Pretty much collecting, aggregating, and computing events for apps, services, and build packs. However, the complexity of the metering problem comes when once considers  doing it at scale. 

Specifically, being able to provide a metering engine that can deal with 1000s of users and millions of applications and service instances. Second, being able to do it in soft-real time. This is important since, metering information is more useful the closer it is to when it is consumed. Finally, that information will grow so there is a need to manage the growth of the data while still allowing queries over time. To make matters a bit more complex the information being metered needs to be flexible. That is, some services might want to send API calls data, whereas another wants to meter KB transferred.

The CF-Abacus project is a solution to this problem that is tested at scale in the largest CloudFoundry deployment to date: IBM’s Bluemix.

## Scope

The scope of the CF-Abacus project is to provide a solution to the metering problem for any CF installation. Specifically we want to allow metering of:

1. Application usages. For instance the creation and deletion of an application, as well as other parts of the application lifecycle, such as restaging.
2. Buildpacks usages. For example, which build pack is used by each application and what version and for how long.
3. Service usages. For instance the number of instances of a service, how much data flows in and out of the service per application, etc.

Naturally, much of this information needs to be customizable by end users. Especially services data. So part of the scope is to have some of the data that flows in and out of Abacus to be customizable. So, for instance, one service might want to be metered by the ingress of data flowing into it where as another by the number of time it’s APIs are invoked. Both metering options need to be supported.

Finally, in scope is the ability to transform and manipulate the data out of Abacus. The ideal situation would be to enable clients of Abacus to treat it as a streaming database that can respond to queries snd thereby able to respond to a verity of questions that clients have of the metering data that it is processing.