# Tourism Attractons API

###Overview

This API is designed for other software developers so that thay can design their products. Its use the dataset downloaded from [data.gov.ie](https://data.gov.ie/dataset/roscommon-tourism-attractions11457) web source.

###About the data

Dataset provide the data about Tourism Attractions in Ireland Co. Roscommon.

| Dataset Characteristics | Description |
|-------------------|--------------------------|
| Dataset Publisher | Roscommon County Council |
| Dataset language |English |
| Spatial Projection |Web Mercator|
|Date of Creation|2011|
|Update Frequency|As Required|
| Last modified | 29/10/2015|

Roscommon County Council provides this information with the understanding that it is not guaranteed to be accurate, correct or complete. Roscommon County Council accepts no liability for any loss or damage suffered by those using this data for any purpose.

The dataset is downloaded as a csv (Comma Separated Values) format file. It contains 35 rows of data including header (1st row). There are 7 values in each line:

- **X** and **Y** - map coordinates;
- **OBJECTID** -  object id;
- **Name** - name of the Attraction;
- **Address** - town where attraction is locating;
- **Streetview_Link** - link to the Google Map Location with a propriate Attraction;
- **WGS84Longitude** and **WGS84Latitude** - same as *X* and *Y*;

### Design

The data is available through http://www.tourism.ie/attractions/r/ URL address and using HTTP methods.

####GET method is used for retrieving data.

#####All attractions

With using http://www.tourism.ie/attractions/r/all URL address, data will be returned in json format with set of all object IDs.

An example of a response would be:
```json
[{1}, {2}, {3}, {4}, ..., {34}]
```

