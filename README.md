# NYC Tenants Rights & Community Organization Service Area Boundaries
Polygon boundaries representing estimates of service / catchment areas of tenants rights and community organizations in NYC that operate at the neighborhood level. 

Please <a href="mailto:chrishenrick@gmail.com">get in touch</a> if you have organizations to add to this dataset, suggestions, or corrections to be made!

Data is available in GeoJSON and ESRI Shapefile format.

## Data Sources:
This dataset was created from a list of tenants rights organizations I compiled for NYC which includes orgs listed in the [DHCR Community Based Housing Organizations list](https://github.com/clhenrick/DHCR_Community_Based_Housing_Orgs). 

The polygon boundaries are sourced from multiple datasources for NYC neighborhoods, zipcode tabulation areas, community district boundaries, as well as boundaries I drew from scratch. For organizations that serve multiple neighborhoods the polygons were dissolved / joined. 

- [Pediacities NYC Neighborhoods](http://nyc.pediacities.com/New_York_City_Neighborhoods)
- [NYC Planning Neighborhood Tabulation Areas](http://www.nyc.gov/html/dcp/html/bytes/dwn_nynta.shtml)
- [NYC Zipcode Tabulation Areas](http://catalog.opendata.city/dataset/nyc-zip-code-tabulation-areas)
- [NYC Community District boundaries](http://www.nyc.gov/html/dcp/html/bytes/districts_download_metadata.shtml)

## Notes
There is a lot of overlap in the polygon boundaries. Using PostGIS with a "point in polygon" query will return all organizations that overlap for that specific point. This can be done easily with the data hosted in [CartoDB](http://cartodb.com) by opening the dataset and pasting in the following `SQL` code into CartoDB's SQL Panel. Note that the coordinates for a point must be in the order of lon, lat (x, y).

```
SELECT * FROM nyc_tenants_rights_service_areas
where 
ST_Intersects(
  ST_GeomFromText(
   'Point(-73.982557 40.724435)', 4326
  ),
  nyc_tenants_rights_service_areas.the_geom    
);
```
Or by using `ST_Contains`:

```
SELECT * FROM nyc_tenants_rights_service_areas
where 
st_contains(
  nyc_tenants_rights_service_areas.the_geom,
  ST_GeomFromText(
   'Point(-73.917104 40.694827)', 4326
  )      
);
```

## License
This data is licensed under a [Creative Commons Attribution-NonCommericial](https://creativecommons.org/licenses/by-nc/3.0/us/) license.