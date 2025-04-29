# Welcome to SciCat Operator's Manual

## Overview

Getting SciCat up and running at your site should be rather straight forward for a test deployment. However turning into a production ready system may involve a bit more work, because different existing systems will need to be interfaced to SciCat.

## Understanding the Components

For the subsequent sections it will be useful to have a "helicopter" overview of the various components that need to play together seamlessly. The following diagram shows these components and also shows potentially existing components at your site, that you would likely want to interface to SciCat. The specific diagram reflects essentially the situation at PSI as of Sept. 2020. Of course your situation may look different. The diagram should therefore be seen as an example, which you need to adapt to your situation.

![ToDo: Updated schematic view of SciCat components](img/DacatDataflowV3.png)

## Up-to-date operator's information
Generally, the [**scicatlive**](https://www.scicatproject.org/scicatlive/latest/) documentation contains an up-to-date information how to set up and run the system ```SciCat``` interfacing it with various external, site-specific services. For troublshooting issues, please refer [the User's Guide](../troubleshoot/index.md).

## Backend
At the heart of the SciCat architecture there is the **REST API server**. This is a NodeJS application that uses the nestjs framework to generate RESTful APIs from JSON files that define these models Users, Datasets, Instruments, Proposals and Instruments. Following the Swagger/OpenAPI format SDKs can be generated in almost any language. You can explore the backend APIs directly via the [Swagger](../swagger/index.md) interface.

The persistence layer behind this API server is a **MongoDB** instance, i.e an open source, NoSQL, document-based database solution. The API server handles all the bi-directional communication from the REST interface to the database.

These two components together comprise the "backend" of the architecture.

### Configuration of the backend
There is one central place where one has a handle on how the backend is configured in SciCat: the [dotenv](../backendconfig/index.md) file.

### Example: How to integrate to OIDC using keycloak

Integration with an identity provider, Keycloak, can be done using Open ID Connect, a protocol for authentication.
See [scicatlive manual](https://www.scicatproject.org/scicatlive/latest/services/backend/services/keycloak/) for more information on integration setup in SciCat backend.

## Frontend

To the REST server an arbitrary number of "clients" (frontends) can be connected. One of the most important clients is the web based GUI frontend. This allows to communicate with the data catalog in a user friendly way. It is based on the Angular (9+) technology and uses ngrx to communicate with the SciCat API and provide a searchable interface for datasets, as well as the option to carry out actions (i.e. archiving).

In addition to the GUI other clients exist, such as command line (CLI) clients (example exist written in GO and Python) or desktop based GUI applications based on Qt. The CLI tools are especially useful for automated workflows, e.g. to get the data into the data catalog. This process is termed "ingestion" of the data. But they can also be used to add the data manually, especially for derived data, since this part of the workflow is often not possible to automate, in particular in truly experimental setups.

### Configuration of the frontend

To start a local instance of the frontend follow the recipe: install requirements, esp. angular, git clone the [code](https://github.com/SciCatProject/frontend), go the the directory and run "npm run start". Then you can launch it by entering "localhost:4200".

### How to include site-specific logos
See [here](https://github.com/SciCatProject/frontend/blob/master/SITE-LOGO-CONFIGURATION.md) for example procedure how to include your logo.

### Messaging infractructure

SciCat strength is to intergrate into almost any existing infrastructure because **messaging systems** can be easily interfaced to SciCat that take over the communication to other services and systems.

In particular RabbitMQ (used at PSI) and Apache Kafka are in use. Such systems can e.g. be used to interface to an tape archive system. To add the specific business logic you can e.g. add your own scripting layer. At PSI however a Node-RED based solution proved to be a stable and flexible platform for this purpose. Node-RED is a A NodeJS based visual programming tool to handle flows of data from one source to another. The following shows the Nod-RED flow used for communicating job requests to the PSI archive system.

![Node-RED](img/job-assembler.png)


### Different entry points to SciCat

One can ususally see SciCat datasets that is the metadata of data taken. It will be possible to sort according to samples, proposals, instruments and published data. Integration and generalisation of these entry points to the catalogue is currently in development. Another strength of SciCat is that it provides a publishing server.

#### Publishing Server

In order to publish data you need to run a landing page server and you need to assign DOIs to your published data. Since the API server may be operated in an intranet, with no access to the internet the following architecture was chosen at PSI:

An OAI-PMH server is running in a DMZ connected to a local Mongo instance. At publication time the data from SciCat is pushed to the external OAI-PMH server. From this server the landing page server can fetch the information about the published data. Also external DOI systems connect to this OAI-PMH server to synchronize the data with the world wide DOI system.

If a user wants to download the full datasets of the published data, the data is copied from the internal file server to a https file server (acting as a cache file server) , which subsequently allows anonymous download of the data.

### Underlying Infrastructure of SciCat as a Service

You may or may not run the infrastructure as part of a Kubernetes cluster. E.g. at PSI the API server, the GUI application, RabbitMQ and the Node-RED instances are all deployed to a Kubernetes cluster, whereas the Mongo DB ist kept outside Kubernetes. Kubernetes is not necessary to have, but can simplify operations. Likewise "helm charts" or similar tools for managing software applications as a service. <!--Also, the separation into internet and intranet zones can be defined as required -- OK HOW??. You can, of course, operate the whole infrastructure directly in internet accessible servers, if security policies permit.-->

## Who uses SciCat?

Traditionally there were PSI, ESS and MaxIV that developed and deploy SciCat. More institutions joined the efforts and have pushed its development and many deploy photon and neutron labs in Europe and world-wide, see our project's for [all facilities](https://www.scicatproject.org/#facilities), contributors and users of SciCat.

Below is a list of their documentation with more details on their deployment.

* ESS - European Spallation Source
* [PSI - Paul-Scherrer-Institute](../sites/PSI/index.md)
* MAXIV 
* RFI
* ALS 
* SOLEIL
* [DESY](../sites/DESY/index.md)


