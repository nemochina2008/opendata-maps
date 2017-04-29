# opendata-maps


## notes & code used to convert shapefiles

inspect shape file properties:
```
ogrinfo -so -al CTRY_2013_GB_BGC.shp
```

use gdal to covert coordinate system:
```
ogr2ogr -t_srs EPSG:4326 CTRY_2013_GB_BGC_WGS84.shp CTRY_2013_GB_BGC.shp
```

use topojson to simply & convert format (hires / lores)
```
topojson -o CTRY_2013_GB_BGC_WGS84.topojson --id-property 'CTRY13CD' -q 1e5 --bbox CTRY_2013_GB_BGC_WGS84.shp
topojson -o CTRY_2013_GB_BGC_WGS84.topojson --id-property 'CTRY13CD' -q 1e5 -s 1e-9 --filter=small --bbox CTRY_2013_GB_BGC_WGS84.shp
```

parameters for simplification & quantization:

- for hires detail use small number: -s = simplication = 0.000000001 (1e-9) 
- for lores detail use large number: -q = quantization = 10000 (1e5)

see notes in gist for more details & sample R code for rendering shapefile / topojson:

- https://gist.github.com/andyjudson/1a1ba0bd85e8b41ba19f


## source shapefile repositories

ukgov:

- repository = http://geoportal.statistics.gov.uk
- license = [open government](http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)

ukgov.scotland [offline]

- repository = http://crtb.sedsh.gov.uk/spatialDataDownload/dload.asp
- license = [open government](http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)

usgov:

- repository = https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html
- license = [public domain](https://ask.census.gov/prweb/PRServletCustom/YACFBFye-rFIz_FoGtyvDRUGg1Uzu5Mn*/!STANDARD)

naturalearth:

- repository = http://www.naturalearthdata.com/
- license = [public domain](http://www.naturalearthdata.com/about/terms-of-use/)


## derived topojson metadata (tood)


|topojson|shapefile|transform|simplify|
|---|---|---|---|
|[ukgov/gbr_ctry_2013.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/gbr_ctry_2013.topojson)|[GBR Country Boundaries](http://geoportal.statistics.gov.uk/datasets?q=CTRY_Boundaries)|WGS84|-q 1e5 -s 1e-9|
||||
||||

