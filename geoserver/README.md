[<img src="https://upload.wikimedia.org/wikipedia/commons/b/ba/Flag_of_Germany.svg" data-canonical-src="https://upload.wikimedia.org/wikipedia/commons/b/ba/Flag_of_Germany.svg" title="von User:SKopp, User:Madden, and other users [Public domain oder Public domain], via Wikimedia Commons" width="30" /> -> German version](README_de.md)

# Application examples for GeoServer
## Importing Vector Tiles from GeoServer into QGIS
(*GeoServer 2.14.* + *VectorTilesPlugin*, *QGIS 2.18.24* + [*Vector Tiles Reader QGIS-Plugin*](https://github.com/geometalab/Vector-Tiles-Reader-QGIS-Plugin))

**datasource:** [DLM1000 Germany](http://www.geodatenzentrum.de/geodaten/gdz_rahmen.gdz_div?gdz_spr=deu&gdz_akt_zeile=5&gdz_anz_zeile=1&gdz_unt_zeile=2&gdz_user_id=0)

For test purposes in the context of this paper, *GeoServer* should be used to generate Vector Tiles in [*MVT*-format](https://github.com/mapbox/vector-tile-spec) and display them in *QGIS*. In the current version, *QGIS* can display *MVT*-Vector Tiles with the [*Vector Tiles Reader QGIS plugin*](https://github.com/geometalab/Vector-Tiles-Reader-QGIS-Plugin). In the [GitHub repository of the plugin](https://github.com/geometalab/Vector-Tiles-Reader-QGIS-Plugin/issues/112) the question of the integration of data from *GeoServer* via a [TileJSON](https://github.com/mapbox/tilejson-spec) file is discussed in detail. Therefore the implementation seems to be not possible at the moment. The integration into *QGIS* [via *TMS*](https://github.com/GjueAtGit/VTs_datasource_ogc/blob/master/geoserver/README.md#verkn%C3%BCpfungsversuch-%C3%BCber-tms) does not seem to work at the moment.

However, it is possible to use the *WMTS* endpoint in the *tiles* tag of the[TileJSON](https://github.com/mapbox/tilejson-spec) file instead of the link to *GeoServer's* *TMS*. The information required for this can be retrieved via *GetCapabilities* of the service. In the interface of *GeoServer* under *Caching Standards* -> *Go to GeoWebCache Home* -> *WMTS 1.0.0 GetCapabilities document* accessible. This results in the [following TileJSON file](https://github.com/GjueAtGit/VTs_datasource_ogc/blob/master/geoserver/example_tilejson_vts_wmts.json) as an example for the layer *sie01_f*, data storage *DLM* in the workspace *DLM* (data source = sie01_f.shp of *DLM1000*):

```json
{
"tilejson":"2.0.0",
"tiles":["http://localhost:8080/geoserver/gwc/service/wmts?REQUEST=GetTile&SERVICE=WMTS&VERSION=1.0.0&LAYER=DLM:sie01_f&STYLE=&TILEMATRIX=EPSG:900913:{z}&TILEMATRIXSET=EPSG:900913&FORMAT=application/x-protobuf;type=mapbox-vector&TILECOL={x}&TILEROW={y}"],
"name":"GeoServer-TestTiles",
"format":"pbf",
"basename":"DLM1000",
"id":"dlm1000",
"minzoom":0,
"maxzoom":14,
"center":[10.5668,51.14895,3],
"bounds":[5.5888,47.2718,15.5448,55.0261],
"version":"3.3",
"crs":"3857",
"vector_layers":[
	{"id":"sie01_f",
	 "geometry_type":"polygon",
	 "minzoom":0,
	 "maxzoom":14,
	 "fields":{"BEGINN":"String","BEMERKUNG":"String","ENDE":"String","LAND":"String","MODELLART":"String","NAM":"String","OBJART":"String","OBJART_TXT":"String","OBJID":"String","RGS":"String"},
	 "description":"Test layer description"}
]
}
```
Save this file under `C:\...YourGeoServerDirectory...\data_dir\www\YOUR_FILE.json` and connect it to `http://localhost:8080/geoserver/www/YOUR_FILE.json` in the *Vector Tiles Reader QGIS-Plugin* in register *Server* -> *New* field *TileJSON URL*.

```diff
! QGIS crashes regularly at smallest scale / zoom level                      !
! therefore first select a part of Germany and then connect to vector tiles. !
```
### Test to connect via TMS
If the same *TileJSON* file ([see above](https://github.com/GjueAtGit/VTs_datasource_ogc/tree/master/geoserver#vector-tiles-aus-geoserver-in-qgis-einlesen)) is used to include the Vector tiles via *TMS*, i.e. the path in *tiles* is adapted accordingly, nothing happens the first time it is included in *QGIS*.

```json
{
"tilejson":"2.0.0",
"tiles":["http://localhost:8080/geoserver/gwc/service/tms/1.0.0/DLM:sie01_f@EPSG:900913@pbf/{z}/{x}/{-y}.pbf"],
"name":"GeoServer-TestTiles",
"format":"pbf",
"basename":"DLM1000",
"id":"dlm1000",
"minzoom":0,
"maxzoom":14,
"center":[10.5668,51.14895,3],
"bounds":[5.5888,47.2718,15.5448,55.0261],
"version":"3.3",
"crs":"3857",
"vector_layers":[
	{"id":"sie01_f",
	 "geometry_type":"polygon",
	 "minzoom":0,
	 "maxzoom":14,
	 "fields":{"BEGINN":"String","BEMERKUNG":"String","ENDE":"String","LAND":"String","MODELLART":"String","NAM":"String","OBJART":"String","OBJART_TXT":"String","OBJID":"String","RGS":"String"},
	 "description":"Test layer description"}
]
}
```
The link to *GeoServer* does not seem to work. However, if there are Vector tiles in the cache of *QGIS* (!) from previous tests with the *WMTS* connection ([see above](https://github.com/GjueAtGit/VTs_datasource_ogc/tree/master/geoserver#vector-tiles-aus-geoserver-in-qgis-read)), they are displayed. However, Vector Tiles in the cache of *GeoServer* or *GeoWebCache* have no effect, i.e. they are not retrieved. Surprisingly, the setting of `{-y}` or `{y}` in the URL of the *TMS* has no effect either.
