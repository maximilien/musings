# Introduction to CF-Abacus - Part 3 of 3

CF-Abacus team: [Jean-Sebastien Delfino](https://github.com/jsdelfino) (IBM), [Saravanakumar Srinivasan](https://github.com/sasrin) "Assk" (Independent), [Benjamin Cheng](https://github.com/BetaFood) (IBM), [Hristo Lliev](https://github.com/hsiliev) (SAP), [Georgi Sabev](https://github.com/georgethebeatle) (SAP), [Kevin Yudhiswara](https://github.com/KRuelY) (IBM), [Piotr Przybylski](https://github.com/piotrprzybylski) (IBM), and [Rajkiran Balasubramanian](https://github.com/rajkiranrbala) (IBM)

## Introduction

In part 1 and part 2 of this series we introduced the metering problem that CF-Abacus solves as well as giving a complete overview of its architecture and design. In the last part we discuss future directions and conclude with the next steps. We also provide various references that all parties interested with CF-Abacus can use to become more active in the project.

## Future Directions

While the current CF-Abacus implementation has come a long way to implement a scalable, reliable, and modular metering pipeline for any Cloud Foundry installation, it’s not without some shortcomings. Three primary areas of improvements are identifiable:

1. User friendliness. A big part of the Abacus configuration and setup is enabling the service providers to plug in their usage data into the pipeline. This on-boarding process has typically been manual with configuration files exchanged via emails to administrators. In order to support scaling there is clearly a need to enable some level of self-onboarding mechanism for services. Additionally, the current reporting API is primarily REST. A user interface that displays typical reporting information would allow first time users of Abacus to be inspired and use it as a starting point for their own user interface.

2. Pluggable data layer. Any metering pipeline has to process a constant flow of information. The resulting data, even for a small installation of CF can be enormous and hard to deal with, especially over time. The database layer needs to be therefore managed for scale and resiliency. By allowing the database layer to be pluggable via BOSH release, we can hopefully achieve a system that scales but also be deployed along side the CF installation. The team is investigating adding MongoDB support as well as a comprehensive BOSH release for CouchDB itself.

3. Error correction. Much of the any usage data needs to be accurate in order to be processable. What we mean is that any errors in IDs (e.g., organizational, application, service) that is wrong will result in the usage information not being counted or accumulated. Since the Abacus system is designed to be scalable and support heterogenous providers, such erroneous usage information are more common in real deployment of Abacus. As such, a process to identify, select, and correct usage that are in error is needed for the system as a whole.

The team is currently working on solutions to the three problems and limitations identified above.

## Conclusion


As we venture into making Cloud Foundry the default open operating system for the cloud, usage information that can help deployers of CF better bill and manage the resource usage of their installation is becoming more and more important. The CF-Abacus project is a solution to proofing an open metering engine for any CF installation. The engine was created with a micro-services architecture designed as a pipeline of six stages. Each  of the pipeline stages can be deployed and scaled as a CF application and exposes its own APIs and talks to its own slice of the database. Since extracting the core CF-Abacus project from IBM’s Bluemix deployment of CloudFoundry we have created a small but active team around the project. With contributors from SAP we were able to add and work on new features such as self-on-boarding as well as expand the realizable DBs that can be used for a real deployment of Abacus. Additionally, we are working to also make Abacus more user friendly and reliable by giving easy means for correcting erroneous usage data and displaying reports.

Join the CF-Abacus team by “kicking the tires” from our Github project page and joining the discussion on our Gitter.im cf-abacus channel.

## References

* CF-Abacus Github [project](https://github.com/cloudfoundry-incubator/cf-abacus)
* CF-Abacus [docs](https://github.com/cloudfoundry-incubator/cf-abacus/tree/master/doc): [README](https://github.com/cloudfoundry-incubator/cf-abacus/blob/master/README.md), [FAQs](https://github.com/cloudfoundry-incubator/cf-abacus/blob/master/doc/faq.md), and [API design](https://github.com/cloudfoundry-incubator/cf-abacus/blob/master/doc/api.md) information
* CF-Abacus [Slack](https://abacusdev-slack.mybluemix.net/) and [Gitter](https://gitter.im/cloudfoundry-incubator/cf-abacus?utm_source=badge) channels