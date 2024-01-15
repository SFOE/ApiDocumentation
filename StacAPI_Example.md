# Spatial Temporal Asset Catalog API (STAC API)
The geospatial datasets of the Swiss Federal Office of Energy (SFOE) are available via the STAC API.
The STAC API is a "dataset based" download service providing access to packaged geospatial data and related metadata.
Here we show you some examples how to query the STAC-API:

## General information
* [General information on the STAC-API](https://www.geo.admin.ch/en/geo-services/geo-services/download-services/stac-api.html)
* [Detailled documentation of the STAC-API](https://data.geo.admin.ch/api/stac/static/spec/v0.9/api.html)
* [STAC Specification](https://stacspec.org/)
* [Plugin to read data directly in QGIS using STAC-API ](https://kartoza.com/blog/qgis/qgis-stac-api-plugin)

*Note: Use [GeoAdmin API](https://nrohrbach.github.io/ApiDocumentation/GeoAdminAPI/) if you want to query objects within a dataset.*

## Available datasets
You will find all available datasets of the Federal Spatial Data Infrastructure FSDI [here](https://data.geo.admin.ch/browser/index.html#/?t=collections).

## Example queries

### Get the description of a dataset
Use the [GET collections](https://data.geo.admin.ch/api/stac/static/spec/v0.9/api.html#operation/getCollections) endpoint.

E.G [Get the details of the dataset "Wind Energy Plants](https://data.geo.admin.ch/api/stac/v0.9/collections/ch.bfe.windenergieanlagen):
```
https://data.geo.admin.ch/api/stac/v0.9/collections/ch.bfe.windenergieanlagen
```

### Get the available download possibilities of a dataset
Use the [GET features](https://data.geo.admin.ch/api/stac/static/spec/v0.9/api.html#operation/getFeatures) endpoint.

E.G [Get the all downloads of the dataset "Wind Energy Plants](https://data.geo.admin.ch/api/stac/v0.9/collections/ch.bfe.windenergieanlagen/items):
```
https://data.geo.admin.ch/api/stac/v0.9/collections/ch.bfe.windenergieanlagen/items
```

### Get all datasets published within a time period
Use the [GET search](https://data.geo.admin.ch/api/stac/static/spec/v0.9/api.html#operation/getSearchSTAC) endpoint.

E.G [Get the all dataset acquired after 2022-02-01](https://data.geo.admin.ch/api/stac/v0.9/search?datetime=2022-02-01/..):
```
https://data.geo.admin.ch/api/stac/v0.9/search?datetime=2022-02-01/..
```
Time intervalls can be expressed as followed:
* A date-time: "2018-02-12T23:20:50Z"
* A closed interval: "2018-02-12T00:00:00Z/2018-03-18T12:31:12Z"
* Open intervals: "2018-02-12T00:00:00Z/.." or "../2018-03-18T12:31:12Z"
 

