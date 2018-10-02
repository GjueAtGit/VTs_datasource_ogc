## MapServer: Zugriff auf MBTiles via GDAL-MBTiles Treiber
Ein Beispiel für den Zugriff auf Vector Tiles aus MapServer (Version 7.2) unter Nutzung des [GDAL-MBTiles-Treibers](https://www.gdal.org/frmt_mbtiles.html) (Version 2.3).

Als Datengrundlage wurden Daten von [OpenMapTiles verwendet](https://openmaptiles.com/downloads/europe/switzerland/zurich/).
Das MapFile bietet bei MapServer 7.2 keine Möglichkeit, auf die Optionen CLIP und ZOOM_LEVEL_AUTO des MBTiles-Treibers zuzugreifen. Damit werden die Standardeinstellungen (CLIP=YES; ZOOM_LEVEL_AUTO=NO) übernommen.

Der MBTiles-Treiber hat in Version 2.3 keine Möglichkeit zum Zusammenfügen von kachelübergreifenden Features (MERGE) implementiert.

### english:
## MapServer: Access to MBTiles via GDAL-MBTiles driver
An example for accessing Vector Tiles from MapServer (version 7.2) using the [GDAL-MBTiles driver](https://www.gdal.org/frmt_mbtiles.html) (version 2.3).

Data from [OpenMapTiles verwendet](https://openmaptiles.com/downloads/europe/switzerland/zurich/) was used as the data basis. With MapServer 7.2, MapFile does not offer the possibility to access the options CLIP and ZOOM_LEVEL_AUTO of the MBTiles driver. Thus the default settings (CLIP=YES; ZOOM_LEVEL_AUTO=NO) are adopted.

The MBTiles driver in version 2.3 has no possibility to merge features across tiles (MERGE).
