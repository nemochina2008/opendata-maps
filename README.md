# opendata-maps

## notes & code used to convert shapefiles

inspect shape file properties:
```
ogrinfo -so -al Westminster_Parliamentary_Constituencies_December_2016_Generalised_Clipped_Boundaries_in_Great_Britain.shp
```
use gdal to convert coordinate system:
```
ogr2ogr -t_srs EPSG:4326 Westminster_Parliamentary_Constituencies_December_2016_Generalised_Clipped_Boundaries_in_Great_Britain_WGS84.shp Westminster_Parliamentary_Constituencies_December_2016_Generalised_Clipped_Boundaries_in_Great_Britain.shp
```
use topojson (v1.6.27) to simply & convert format shapefile to topojson
```
topojson -o Westminster_Parliamentary_Constituencies_December_2016_Generalised_Clipped_Boundaries_in_Great_Britain_WGS84.topojson --id-property 'pcon16cd' -q 1e+6 -s 1e-9 --filter small Westminster_Parliamentary_Constituencies_December_2016_Generalised_Clipped_Boundaries_in_Great_Britain_WGS84.shp
```

see notes in gist for more details & sample R code for rendering shapefile / topojson:

- https://gist.github.com/andyjudson/1a1ba0bd85e8b41ba19f

## source shapefile repositories

ukgov:

- repository = http://geoportal.statistics.gov.uk/
- license = [open government](http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)
- disclaimer = Contains National Statistics data © Crown copyright and database right. Contains OS data © Crown copyright and database right.

ukgov.scotland:

- repository = [http://www.nrscotland.gov.uk/statistics-and-data/geography](http://www.nrscotland.gov.uk/statistics-and-data/geography)
- license = [open government](http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)
- disclaimer = Contains National Statistics data © Crown copyright and database right. Contains OS data © Crown copyright and database right.

usgov:

- repository = [http://www.census.gov/](https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html)
- license = [public domain](https://ask.census.gov/prweb/PRServletCustom/YACFBFye-rFIz_FoGtyvDRUGg1Uzu5Mn*/!STANDARD)

naturalearth:

- repository = http://www.naturalearthdata.com/
- license = [public domain](http://www.naturalearthdata.com/about/terms-of-use/)


## derived topojson metadata


|topojson|country|year|boundary|resolution|transform|simplify|id-column|id-example|
|---|---|---|---|---|---|---|---|---|
|[ukgov/eng_ccg16.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/eng_ccg16.topojson)|ENG|2016|[NHS Clinical Commissioning Group Boundaries](http://geoportal.statistics.gov.uk/datasets?q=CCG+Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e6 -s 1e-9|CCG16CD|E38000126|
|[ukgov/eng_rgn16.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/eng_rgn16.topojson)|ENG|2016|[Region Boundaries](http://geoportal.statistics.gov.uk/datasets?q=RGN+Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e6 -s 1e-9|RGN16CD|E12000002|
|[ukgov/eng_wal_ctyua16.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/eng_wal_ctyua16.topojson)|ENG,WAL|2016|[County & Unitary Boundaries](http://geoportal.statistics.gov.uk/datasets?q=CTYUA+Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e6 -s 1e-9|CTYUA16CD|E06000005|
|[ukgov/eng_wal_lsoa11.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/eng_wal_lsoa11.topojson)|ENG,WAL|2011|[Lower Layer Super Output Areas](http://geoportal.statistics.gov.uk/datasets?q=LSOA_Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e6 -s 1e-9|LSOA11CD|E01032764|
|[ukgov/gbr_ctry16.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/gbr_ctry16.topojson)|ENG,SCO,WAL|2016|[Country Boundaries](http://geoportal.statistics.gov.uk/datasets?q=CTRY_Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e6 -s 1e-9|CTRY16CD|E92000001|
|[ukgov/gbr_eer16.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/gbr_eer16.topojson)|ENG,SCO,WAL|2016|[European Electoral Region Boundaries](http://geoportal.statistics.gov.uk/datasets?q=EER+Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e6 -s 1e-9|EER16CD|E15000001|
|[ukgov/gbr_lad16.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/gbr_lad16.topojson)|ENG,SCO,WAL|2016|[Local Area District Boundaries](http://geoportal.statistics.gov.uk/datasets?q=LAD+Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e6 -s 1e-9|LAD16CD|E07000201|
|[ukgov/gbr_pcon16.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/gbr_pcon16.topojson)|ENG,SCO,WAL|2016|[Westminster Parliamentary Constituencies](http://geoportal.statistics.gov.uk/datasets?q=PCON+Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e6 -s 1e-9|PCON16CD|E14000886|
|[ukgov/gbr_wd16.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/gbr_wd16.topojson)|ENG,SCO,WAL|2016|[Electoral Wards](http://geoportal.statistics.gov.uk/datasets?q=WD+Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e6 -s 1e-9|WD16CD|E05000950|
|[ukgov/sco_dz11.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/sco_dz11.topojson)|SCO|2011|[Datazone Boundaries](http://sedsh127.sedsh.gov.uk/Atom_data/ScotGov/ZippedShapefiles/SG_DataZoneBdry_2011.zip)|Generalised Clipped (20m)|WGS84|-q 1e6 -s 1e-9|DATAZONE|S01000001|
|[ukgov/sco_iz11.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/sco_iz11.topojson)|SCO|2011|[Intermediate Zone Boundaries](http://sedsh127.sedsh.gov.uk/Atom_data/ScotGov/ZippedShapefiles/SG_IntermediateZoneBdry_2011.zip)|Generalised Clipped (20m)|WGS84|-q 1e6 -s 1e-9|INTERZONE|S02000001|
|[ukgov/sco_hb14.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/sco_hb14.topojson)|SCO|2014|[NHS Healthboard Boundaries](http://sedsh127.sedsh.gov.uk/Atom_data/ScotGov/ZippedShapefiles/SG_NHS_HealthBoards_2014.zip)|Generalised Clipped (20m)|WGS84|-q 1e6 -s 1e-9|HBCODE|S08000001|
|[ukgov/sco_pcon16.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/sco_pcon16.topojson)|SCO|2016|[Scottish Parliamentary Constituencies](http://geoportal.statistics.gov.uk/datasets?q=SPC_Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e6 -s 1e-9|SPC16CD|S16000078|
|[ukgov/wal_nawc16.topojson](https://github.com/andyjudson/opendata-maps/blob/master/ukgov/wal_nawc16.topojson)|WAL|2016|[National Assembly Wales Constituencies](http://geoportal.statistics.gov.uk/datasets?q=NAWC+Boundaries)|Generalised Clipped (20m)|WGS84|-q 1e6 -s 1e-9|NAWC16CD|W09000015|
|[usgov/cb_2013_us_nation_500k.topojson](https://github.com/andyjudson/opendata-maps/blob/master/usgov/cb_2013_us_nation_500k.topojson)|USA|2013|[National Boundaries](https://www.census.gov/geo/maps-data/data/cbf/cbf_nation.html)|1:5m Resolution|WGS84|-q 1e5 -s 1e-9|GEOID|US|
|[usgov/cb_2013_us_state_500k.topojson](https://github.com/andyjudson/opendata-maps/blob/master/usgov/cb_2013_us_state_500k.topojson)|USA|2013|[State Boundaries](https://www.census.gov/geo/maps-data/data/cbf/cbf_state.html)|1:500k Resolution|WGS84|-q 1e5 -s 1e-9|STUSPS|NY|
|[usgov/cb_2013_us_state_mainland_500k.topojson](https://github.com/andyjudson/opendata-maps/blob/master/usgov/cb_2013_us_state_mainland_500k.topojson)|USA|2013|[State Boundaries](https://www.census.gov/geo/maps-data/data/cbf/cbf_state.html)|1:500k Resolution|WGS84 + filtered to 48 states|-q 1e5 -s 1e-9|STUSPS|NY|
|[naturalearth/ne_10m_admin_0_countries.topojson](https://github.com/andyjudson/opendata-maps/blob/master/naturalearth/ne_10m_admin_0_countries.topojson)|WORLD|2015|[Countries Admin-0](http://www.naturalearthdata.com/downloads/10m-cultural-vectors/10m-admin-0-countries/)|1:10m Cultural Vectors|WGS84|-q 1e5 -s 1e-9|ADM0_A3|GBR|


