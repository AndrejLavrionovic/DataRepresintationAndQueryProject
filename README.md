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

The data is available through *http://www.tourism.ie/attractions/r/* URL address and using HTTP methods.

####GET method is used for retrieving data.

#####All attractions

With using http://www.tourism.ie/attractions/r/all URL address, data will be returned in json format with set of all object IDs.

An example of a response would be:
```json
[{1}, {2}, {3}, {4}, ..., {34}]
```
#####Data for specified attraction

To retrieve the data just from one line about only one attraction need to specify object id in the URL address. For example - if you want to get data about "Elphin Windmill" attraction with object ID - 22, URL will be
*http://www.tourism.ie/attraction/r/22.json*. Data will be returned in json format as an object with set of names and values, where name is column name and value is the data such as:

- *X*: map x coordinate,
- *Y*: map y coordinate,
- *OBJECTID*: object id specified in the url address,
- *Name*: attraction name,
- ...

Example of respond:

```json
{
  X: -8.20549189312339,
  Y: 53.8516852415384,
  OBJECTID: 22,
  Name: Elphin Windmill,
  Address: Elphin,
  Streetview_Link: http://apps.roscommoncoco.ie/GoogleStreetView/GoogleMapStreetView.html?Lat=53.8516852426549&amp;Lng=-8.20549189242993,
  WGS84Longitude: -8.20549189,
  WGS84Latitude: 53.8516852
}
```

#####Data specified by address

Also there is available to get data regarding the location (town address). To do that the URL address must by build with addition parameters - *http://www.tourism.ie/attractions/r/all?address=Roscommon*. Result of this query will be set of OBJECTIDs of all attractions that located in Rosscommon.

An example:

```json
[{19}, {24}, {25}, {27}]
```

####DELETE method

Using DELETE method app developer can remove record from dataset by specifieng object id in the URL address: *http://www.tourism.ie/attraction/r/all?OBJECTID=22*. To remove group of records need to specify their object ids in the URL address separated by '&' - *http://www.tourism.ie/attraction/r/all?OBJECTID=5&OBJECTID=22&OBJECTID=29*. To delete all records of attraction located in the same address need to specify location address in the URL. *http://www.tourism.ie/attraction/r/all?Address=Roscommon* will delete all attraction located in Roscommon.

Need to be very carefull to use DELETE method as incorect use can delete not proper record and even all if record is not specified. The same query is performed only once.

####POST method

With the POST method you can add new record to the dataset, that is POST to *http://www.tourism.ie/attractions/r/* creates a resources that lives under the */r* resource. As result the new record will be returned in json format:

```json
{
  X: -8.7584994947,
  Y: 53.7483984734,
  OBJECTID: 36,
  Name: New Attraction,
  Address: Roscommon,
  Streetview_Link: <google map link>,
  WGS84Longitude: -8.7584994947,
  WGS84Latitude: 53.7483984734
}
```

####PUT method

PUT is used to update record (by replacing it in dataset), thus the object id must be specified - *http://www.tourism.ie/attractions/r/<OBJECTID>*. For Example if you want to rename *Elphin Windmill* to *Elphin Old Windmill*, which has OBJECTID 22, you need to PUT request to *http://www.tourism.ie/attractions/r/22*. As result the modified record will be returned as an object:

```json
{
  X: -8.20549189312339,
  Y: 53.8516852415384,
  OBJECTID: 22,
  Name: Elphin Old Windmill,
  Address: Elphin,
  Streetview_Link: http://apps.roscommoncoco.ie/GoogleStreetView/GoogleMapStreetView.html?Lat=53.8516852426549&amp;Lng=-8.20549189242993,
  WGS84Longitude: -8.20549189,
  WGS84Latitude: 53.8516852
}
```

