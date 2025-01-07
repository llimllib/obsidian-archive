---
created: 2025-01-07T14:25:20.675Z
updated: 2025-01-07T14:25:20.675Z
---
http://thredds.northwestknowledge.net:8080/thredds/terraclimate_aggregated.html

Contains freely-available high resolution climate data.

To download the data for the [bivariate map of North America](https://observablehq.com/d/de1419e02bc65596), I:

- got a bounding box for North America
	- lat: 6.6/83.3
	- lon: -178.2/-49
- for each datatype of `ppt` (precipitation), `tmax` (high temp), `tmin` (low temp)
	- downloaded the data for that bounding box from this URL:

`http://thredds.northwestknowledge.net:8080/thredds/ncss/agg_terraclimate_${datatype}_1958_CurrentYear_GLOBE.nc?var=${datatype}&south=${LAT_MIN}&north=${LAT_MAX}&west=${LON_MIN}&east=${LON_MAX}&disableProjSubset=on&addLatLon=true&horizStride=1&accept=netcdf`

Which returns a [netcdf](https://www.unidata.ucar.edu/software/netcdf/) file which can be opened by https://www.npmjs.com/package/netcdfjs or similar libraries in other languages.

I haven't found a proper full description of the data set.

That data is aggregate data from 1958-current; you can also get individual years. For example, here is the netCDF file containing the `tmin` data for 1982:

`http://thredds.northwestknowledge.net:8080/thredds/fileServer/TERRACLIMATE_ALL/data/TerraClimate_tmin_1982.nc`