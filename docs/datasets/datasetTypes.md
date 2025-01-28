# Datasets Types

A new feature was introduced: instead of only providing ```raw``` and ```derived``` custom dataset types are now available, e.g. for the proposed dataset collections (hierarchical grouping). Control of which types are allowed should be on the site administration side and be configurable, see also [PR](https://github.com/SciCatProject/scicat-backend-next/pull/1532). 


## How is this new dataset type used?
Add any type into a separate JSON named ```datasetTypes.json```.

## Changes made

* configuration: add new datasetTypes field and support to read in a json file for custom datasest types (either by env variable or default location "datasetTypes.json")
* add support for custom dataset types in dataset schema
* dataset controller: update endpoints and validation methods to accept custom dataset types.

## Examples of usage

Abstract layer of dataset types, e.g. type ```collection``` defined with more, other or less properties or information per dataset. Can be tailored to site-specific adoptions.

