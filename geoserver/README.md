# Anwendungsbeispiele für GeoServer
## Vector Tiles aus GeoServer in QGIS einlesen
(*GeoServer 2.14.* + *VectorTilesPlugin*, *QGIS 2.18.24* + [*Vector Tiles Reader QGIS-Plugin*](https://github.com/geometalab/Vector-Tiles-Reader-QGIS-Plugin))
  
**Datengrundlage:** [DLM1000 Deutschland](http://www.geodatenzentrum.de/geodaten/gdz_rahmen.gdz_div?gdz_spr=deu&gdz_akt_zeile=5&gdz_anz_zeile=1&gdz_unt_zeile=2&gdz_user_id=0)

Für Testzwecke im Rahmen der vorliegenden Arbeit sollten mit GeoServer Vector Tiles im [*MVT*-Format](https://github.com/mapbox/vector-tile-spec) erzeugt und in *QGIS* dargestellt werden. *QGIS* kann in der aktuellen Version *MVT*-Vector Tiles mit dem [*Vector Tiles Reader QGIS-Plugin*](https://github.com/geometalab/Vector-Tiles-Reader-QGIS-Plugin) darstellen. Im [GitHub Repository des Plugins](https://github.com/geometalab/Vector-Tiles-Reader-QGIS-Plugin/issues/112) wird die [Frage](https://github.com/geometalab/Vector-Tiles-Reader-QGIS-Plugin/issues/112) nach der Einbindung von Daten aus *GeoServer* über eine [TileJSON](https://github.com/mapbox/tilejson-spec)-Datei ausführlich diskutiert. Demnach scheint die Umsetzung aktuell nicht möglich. Via *TMS* scheint die Einbindung in *QGIS* aktuell tatsächlich nicht zu funktionieren.

### Verknüpfung über WMTS
Jedoch besteht die Möglichkeit im *tiles*-tag der [TileJSON](https://github.com/mapbox/tilejson-spec)-Datei statt der Verknüpfung zum *TMS* von *GeoServer* den *WMTS*-Endpunkt zu nutzen. Die hierzu erforderlichen Angaben sind über *GetCapabilities* des Dienstes abrufbar. In der Oberfläche von *GeoServer* unter *Caching Standards -> Gehe zur GeoWebCache Startseite -> WMTS 1.0.0 GetCapabilities document* erreichbar.
Daraus ergibt sich beispielhaft für den Layer *sie01_f*, Datenspeicher *DLM* im Arbeitsbereich *DLM* (Datenquelle = *sie01_f.shp* des DLM1000) folgende TileJSON-Datei:
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
Diese Datei unter `C:\...YourGeoServerDirectory...\data_dir\www\YOUR_FILE.json` abspeichern und im *Vector Tiles Reader QGIS-Plugin* im Register *Server* -> *New* im Feld *TileJSON URL* mit `http://localhost:8080/geoserver/www/YOUR_FILE.json` verknüpfen.
```diff
! Bei kleinstem Maßstab/kleinster Zoomstufe stürzt QGIS regelmäßig ab,           !
! deswegen erst einen Teilbereich von Deutschland auswählen und dann verknüpfen. !
```

### Verknüpfung über TMS

Wird dieselbe TileJSON-Datei verwendet, um die Vector Tiles über *TMS* einzubinden, d.h. der Pfad in *tiles* entsprechend angepasst, geschieht bei erstmaliger Einbinsung in *QGIS* nichts.

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
Die Verknüpfung zu *GeoServer* scheint nicht zu funktionieren. Sind dagegen aus vorherigen Versuchen mit der *WMTS*-Verknüpfung (s.o.) Vector Tiles im Cache von *QGIS* (!) vorhanden, werden diese angezeigt. Im Cache von *GeoServer* bzw. *GeoWebCache* liegende Vector Tiles haben jedoch keinen Auswirkung. Erstaunlicherweise ebenfalls ohne Auswirkung ist die Einstellung von `{-y}` oder `{y}` in der URL des *TMS*.
