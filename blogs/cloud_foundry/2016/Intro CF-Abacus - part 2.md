# Introduction to CF-Abacus - Part 2 of 3

## Architecture Overview

The CF-Abacus uses a pipeline architecture. The pipeline can be seen as containing six stages where each stage is responsible for processing, manipulating, saving, sorting, and reporting metering information. The following diagram illustrate the six stages which we elaborate on a bit more below.

[pic: CF-Abacus pipelining architecture diagram]

The six stages of the CF-Abacus pipeline comprises:

1. Resource provider: at this stage in the pipeline service providers connect to Abacus to pump usage information into the system. Two main resource providers exist, one are third party services, that is CF service brokers that expose services to a CF installation. And second, the CF runtime itself which provides information about application lifecycle for instance
2. Usage event collector: at this stage in the pipeline the various resource providers are configured and are providing events into the system. The job of this stage is to collect the usage information and store it and do some initial preprocessing of the data.
3. Metering: the core of the Abacus pipeline is the stage that applies the metering formulas to the usage data. The resulting computation is also stored in a database.
4. Accumulator: since usage data is a constant stream, it needs to be accumulated over time (days, weeks, and months) to make it useful for consumption. This stage does all accumulation processing.
5. Aggregator: while accumulated usage is more useful than individual usage, it’s even better when aggregated around logical identities, for instance organizations, spaces, applications, services, and users. In this stage the accumulation of the data around these known identities is performed.
6. Reporting: while usage information is useful when accumulated it’s even more useful when in a report format that spans time and potentially multiple identities. In the reporting stage we the Abacus system allow users to customize how the reported data is presented to Abacus users.

One of the main goals of this architecture is to allow flexibility and scaling. The flexibility goal is to enable the architecture to grow without major disruption to the system. That is new stages to the pipeline can be introduced somewhat easily. 

Scalability is achieved by allowing the design of each stage to independently scale. Because the system is partitioned logically into stages that connect to each other, by scaling each component we can achieve a overall more scalable pipeline by focusing on the stages that are slow and scale them to achieve the performance needed.

## Design Goals

To support our architecture decisions we opted to design the CF-Abacus project as a collection of micro services. In its most obvious decomposition, each stage of the Abacus pipeline is exposed as a micro service with a REST API that is backed by a database. Following common 12-factor application patterns, this design means that each stage can scale independently using classic horizontal replications.

Furthermore, the resulting micro services applications are easily deployable and maintained in a Cloud Foundry deployment. This means that CF-Abacus can enjoy the same scaling and maintenance lifecycle and workflow as any other applications running in CF. Using the platform to run some parts of the platform is the effective result.

Naturally, any discussion of 12-factor applications or micro service requires mentioning where the data is being kept and managed. This is no different. The various stages of the CF-Abacus pipeline require a database. And a database that scales to TB of data and that can easily be partitioned and sharded. Think of the resulting accumulated data for any one organization running 10s of apps over a year. The resulting data is large and will keep growing.

The design goal for CF-Abacus to deal with this database problem is two fold. First, assume that the database will be provided by a CF service. So each stage (micro service) creates and connects to the database service to accumulate, query, and process the collected data. The database is assumed to be any Couch-compliant database. So access to the database (once connected) is via the known open CouchDB APIs.

To deal with the challenges of an ever growing database footprint, the micro services automatically shard the database overtime partitions. This makes sense since the data flowing into the Abacus pipeline is always timestamped and more importantly the resulting access of the accumulated and reported data tends to be sensitive to the timespan it represents. For instance, as a user of Abacus for billing, that would typically be interested in the data for latest time period, a goal would be to make the data for more recent time periods be readily available.

## Implementation

To realize the architecture and design goals the team chose to use Node.js as their primary implementation language and application server. This choice makes sense when one considers that Node.js has excellent built-in libraries for creating Web APIs and first class connectors to CouchDB-like databases.

Since Node.js is also supported as a first class language in Cloud Foundry, with an active build pack release schedule that matches the Node community schedules, this choice is as good as any other language choices for implementation.

The resulting implementation is all contained in the CF-Abacus Github project with each of the six stages for the pipeline modularize into their own Node.js module each exposing their APIs and connecting to the database layer (CouchDB compliant). Each pipeline module can be pushed as an app into CF and thus independently scaled like other CF apps.
