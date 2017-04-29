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
- disclaimer = Contains National Statistics data © Crown copyright and database right. Contains OS data © Crown copyright and database right.

ukgov.scotland [offline]:

- repository = http://crtb.sedsh.gov.uk/spatialDataDownload/dload.asp
- license = [open government](http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)
- disclaimer = Contains National Statistics data © Crown copyright and database right. Contains OS data © Crown copyright and database right.

usgov:

- repository = https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html
- license = [public domain](https://ask.census.gov/prweb/PRServletCustom/YACFBFye-rFIz_FoGtyvDRUGg1Uzu5Mn*/!STANDARD)

naturalearth:

- repository = http://www.naturalearthdata.com/
- license = [public domain](http://www.naturalearthdata.com/about/terms-of-use/)


## derived topojson metadata


|topojson|country|year|source|resolution|transform|simplify|id-column|id-example|
|---|---|---|---|---|---|---|---|---|
|[ukgov/gbr_ctry_2013.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/gbr_ctry_2013.topojson)|ENG,SCO,WAL|2013|[Country Boundaries](http://geoportal.statistics.gov.uk/datasets?q=CTRY_Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e5 -s 1e-9|CTRY13CD|E92000001|
|[ukgov/eng_cty_2013.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/eng_cty_2013.topojson)|ENG|2013|[County Boundaries](http://geoportal.statistics.gov.uk/datasets?q=CTY+Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e5 -s 1e-9|CTY13CD|E10000019|
|[ukgov/eng_ccg_2013.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/eng_ccg_2013.topojson)|ENG|2013|[NHS Clinical Commissioning Group Boundaries](http://geoportal.statistics.gov.uk/datasets?q=CCG+Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e5 -s 1e-9|CCG13CD|E38000126|
|[ukgov/gbr_lad_2013.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/gbr_lad_2013.topojson)|ENG,SCO,WAL|2013|[Local Area District Boundaries](http://geoportal.statistics.gov.uk/datasets?q=LAD+Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e5 -s 1e-9|LAD13CD|E07000201|
|[ukgov/gbr_lsoa_2011.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/gbr_lsoa_2011.topojson)|ENG,WAL|2011|[Lower Layer Super Output Areas](http://geoportal.statistics.gov.uk/datasets?q=LSOA_Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e5 -s 1e-9|LSOA11CD|E01032764|
|[ukgov/gbr_pcon_2013.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/gbr_pcon_2013.topojson)|ENG,SCO,WAL|2013|[Westminster Parliamentary Constituencies](http://geoportal.statistics.gov.uk/datasets?q=PCON+Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e5 -s 1e-9|PCON16CD|E14000886|
|[ukgov/gbr_wd_2013.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/gbr_wd_2013.topojson)|ENG,SCO,WAL|2013|[Political Wards](http://geoportal.statistics.gov.uk/datasets?q=WD+Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e5 -s 1e-9|WD16CD|E05000950|
|[ukgov/sco_dz_2011.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/sco_dz_2011.topojson)|SCO|2011|Datazone Boundaries|Generalised Clipped (20m)|WGS84|-q 1e5 -s 1e-9|DZ_CODE|S01000001|
|[ukgov/sco_hb_2013.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/sco_hb_2013.topojson)|SCO|2013|NHS Healthboard Boundaries|Generalised Clipped (20m)|WGS84|-q 1e5 -s 1e-9|S0_CODE|S08000001|
|[ukgov/sco_iz_2011.topojson)](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/sco_iz_2011.topojson)|SCO|2011|Intermediate Zone Boundaries|Generalised Clipped (20m)|WGS84|-q 1e5 -s 1e-9|IZ_CODE|S02000001|


