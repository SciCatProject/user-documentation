# Welcome to SciCat Operator's Guide

## Overview
SciCat is a flexible metadata catalogue designed to be easily interfaced in to most existing infrastructure. The following guide will introduce the configuration required to integrate SciCat into common technologies.

How to ingest metadata, set SciCat up to deploy it is best covered by understanding its core systems, backend and frontend, its features, configurations, and what else one could do to fully exploit all of SciCat's capabilities.

SciCat consists of a backend application, that is connected to the database - a MongoDB - and a frontend client exposing database content through a GUI to a user. At large scale facilities SciCat handles about 30 PB of data. 

## Features 

SciCat covers these core aspects in a flexible way:

1. Searchable metadata fields, most common and highly specific ones. SciCat was developed by the PaNoSc community and has been successfully used more widely. This is because SciCat is highly configurable.
2. Provision of unique persistent identifiers not only for the internal catalogue, but also connecting to the global DOI system through e.g. ready pathway to publication via [DataCite](https://datacite.org/). 

SciCat is an open source project can can be developed in accordance with our [license](https://github.com/SciCatProject/scicat-backend-next?tab=BSD-3-Clause-1-ov-file#readme).

## Dataset ingestion
You find here a pythonic way of metadata ingestion using SciCats API based on the PySciCat client:
See this [how-to-ingest doc](https://www.scicatproject.org/pyscicat/howto/ingest.html) to get started. 

Another example that uses Jupyter Notebook in SciCatLive (see below) can be found [here]([https://github.com/SciCatProject/scicatlive/blob/main/services/jupyter/config/notebooks/pyscicat.ipynb) which includes how to authenticate, create a dataset, add datablocks and upload an attachement.

## Up-to-date operator's information
Generally, the [**scicatlive**](https://www.scicatproject.org/scicatlive/latest/) documentation contains an up-to-date information how to set up and run the system ```SciCat``` interfacing it with various external, site-specific services. For troublshooting issues, please refer [the User's Guide](../troubleshoot/index.md).

## Backend
At the heart of the SciCat architecture there is the **REST API server**. This is a NodeJS application that uses the nestjs framework to generate RESTful APIs from JSON files that define these models Users, Datasets, Instruments, Proposals and Instruments. Following the Swagger/OpenAPI format SDKs can be generated in almost any language. You can explore the backend APIs directly via the [Swagger](../swagger/index.md) interface.

The persistence layer behind this API server is a **MongoDB** instance, i.e an open source, NoSQL, document-based database solution. The API server handles all the bi-directional communication from the REST interface to the database.

These two components together comprise the "backend" of the architecture.

### Configuration of the backend
There is one central place where one has a handle on how the backend is configured in SciCat: the [dotenv](../backendconfig/index.md) file.


### Example: How to connect your scicat to an external service
One useful feature of SciCat is to be able to connect your scicat to some external service via "SciCat jobs". Traditionally there were three fixed types, a job to archive, to retrieve and to publish, visible from the GUI through the respective buttons. Since recently (summer 2025) there are in total 9 types available. How to use them for your site, start with this documentation [here](../backendconfig/jobs.md) for admins. For now, stick to the developers documentation directly in the [code repo](https://github.com/SciCatProject/documentation/blob/master/Development/v4.x/backend/configuration/jobconfig.md).


### Example: How to integrate to OIDC using keycloak

Integration with an identity provider, Keycloak, can be done using Open ID Connect, a protocol for authentication.
See [scicatlive manual](https://www.scicatproject.org/scicatlive/latest/services/backend/services/keycloak/) for more information on integration setup in SciCat backend.

## Frontend

To the REST server an arbitrary number of "clients" (frontends) can be connected. One of the most important clients is the web based GUI frontend. This allows to communicate with the data catalog in a user friendly way. It is based on the Angular (9+) technology and uses ngrx to communicate with the SciCat API and provide a searchable interface for datasets, as well as the option to carry out actions (i.e. archiving).

In addition to the GUI other clients exist, such as command line (CLI) clients (example exist written in GO and Python) or desktop based GUI applications based on Qt. The CLI tools are especially useful for automated workflows, e.g. to get the data into the data catalog. This process is termed "ingestion" of the data. But they can also be used to add the data manually, especially for derived data, since this part of the workflow is often not possible to automate, in particular in truly experimental setups.

### Start up a frontend client

To start a local instance of the frontend follow the recipe: install requirements, esp. angular, git clone the [code](https://github.com/SciCatProject/frontend), go the the directory and run "npm run start". Then you can launch it by entering "localhost:4200".

### Configuration of the frontend
[Jays Link](https://github.com/SciCatProject/scicat-backend-next/pull/2306/files) Find [here](../frontendconfig/index.md) a guide of the frontend configuration.

### How to include site-specific logos
See [here](https://github.com/SciCatProject/frontend/blob/master/SITE-LOGO-CONFIGURATION.md) for example procedure how to include your logo.

### Messaging infractructure

SciCat strength is to intergrate into almost any existing infrastructure because **messaging systems** can be easily interfaced to SciCat that take over the communication to other services and systems.

A detailed description of jobs in for the new backend can be found [here](https://github.com/SciCatProject/documentation/blob/master/Development/v4.x/backend/configuration/jobconfig.md).


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


