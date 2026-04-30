# Welcome to SciCat Users Guide

Scicat, a scientific metadata catalogue, allows you to explore your datasets through their metadata. SciCat has mechanisms to interact with the related datasets through its flexible integration with most storage systems.

SciCat is a data management tool accompanying some critical steps during the entire data life cycle which are: getting an overview of datasets for data analysis, for re-analysis, for publishing datasets, and in particular for publication. 

Advantages of SciCat:

* It can be integrated to almost any other service that has REST APIs. Therefore, site-specific applications can be easily integrated. 
* The Data Model of SciCat forsees a schemaless fields for quite different use cases. This concept has been implemented for the main class, Datasets, but is extended to function in the same way for the other classes e.g. Proposlas, Samples, Intstruments and Published Data.
* Its components are based on OpenSource software projects and state of the art technologies using MongoDB as backbone database, nestjs as backend basis. 

In the past 5 years (since about 2020) SciCat has undergone major improvements in key areas for better user experience and re-structuring to meet the various different needs of photon science labs. The collaboration has grown and governance will be soon established.

## How to run SciCat
More detailed information on how to run scicat, see [scicatlive documentation](https://www.scicatproject.org/scicatlive/latest/). For more details on how to ingest, setup and deploy information from SciCat, see the [operator's guide](../operator-guide/index.md). 

## How to use SciCat
Once metadata is ingested into SciCat, the user can login and view, edit the metadata, list, filter and make a selection of interesting datasets using also scientific metadata. There are four main areas of SciCat where metadata can be explored:

1. [Datasets](../datasets/index.md): Metadata in SciCat is ideally sorted according to a dataset. It can have several associated files attached which have the same metadata like a thumbnail or most common image files.
2. [Proposals](../proposals.md): are used to link datasets to the proposal under which beamtime was granted.
3. [Instruments](../instruments.md): Instruments is a library of instruments available at your institute, which can be linked to datasets.
4. [Samples](../samples.md): Here you can add metadata describing a physical sample which can be linked to it’s experimental use captured in datasets. 

For many the SciCat datasets are the entry point to the catalogue, but soon it will be possible to start with samples or published data records (registered metadata sets).
You can just browse what's in the catalogue for any published datasets. Else one can list all datasets that I either own or have access to. Here is how to find more on how to proceed:

## How-Tos for Users (Quick-links)

* [Login](../login/index.md)
* Search and find your data, see [Datasets How to query](../datasets/index.md#how-to-query-datasets)
*   How to change some fields after ingestion
*   How to view history of changes to a dataset
*   How to [group and tag datasets](../datasets/grouping_tagging_ds.md).
*   How to group and tag grouped datasets

## A few more How-To's for users and site-admins
* Where to find the version of the deployed SciCat Frontend? Check [here](../about/operatorHowTos.md).



