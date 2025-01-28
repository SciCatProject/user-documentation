# Datasets
Datasets can include several files which e.g. comprise a self-contained measurement - which is fully customizeable during ingestion of meta data. Users can search, view, list the meta data of a dataset. 

To group and tag datasets is depicted [here](grouping_tagging_ds.md). Datasets can also be issued to be published: either removing the restricted view or triggering the process of obtaining a DOI for the selected datasets, see [old description](Publishing.md).


### How to query datasets


## Dataset file listing
Here is the view of files belonging to a dataset: Below the PID on the top, one finds the tab **Datafiles**:
![list](img/dataset_details_filelist.png)



## Dataset attachments
What kind of attachement can be saved? Will they be searchable? Can also other formats be attached than pngs?

On the dataset details page, you can click on the Attachments tab
![Choose an image file, must be under 16 MB limit](img/dataset_attachments_PSI.png)

Simply follow the instructions to upload an image. The size is restricted to be below 16 MB.

## View raw JSON data

Scientific meta data is shown in JSON under its section and looks like this:
![img](img/dataset_details_rawJSON.png)

## Get raw JSON data

One can also get the JSON file via the swagger API. If set up, one can directly access the API endpoints of SciCat backend. Usually the address is in the form: ```my-scicat-instance.country/explorer```, swagger is accessible via the explorer. One needs to authenticate by copying the token from the GUI into the field **authorize**, then find the dataset of interest, by trying it out it will display you dataset and you can download it in JSON format.

## Edit Scientific meta data
// WARNING: this is the old text! 
If enabled, fields in the scientific metadata can be modified and edited by the owner of the data by hitting the "Edit" Icon. The user can add,remove or change metadata fields, every change will create a new record in the databse with it's history.

![Image edit metadata](img/editMetadata.png)


## New developments on dataset types
Generalize datatypes to remove restrictions of ```raw``` and ```derived``` types (difference was a set of dataset properties).

[datasetTypes](datasetTypes.md)