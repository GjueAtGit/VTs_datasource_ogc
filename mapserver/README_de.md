[<img src="https://upload.wikimedia.org/wikipedia/commons/a/ae/Flag_of_the_United_Kingdom.svg" data-canonical-src="https://upload.wikimedia.org/wikipedia/commons/a/ae/Flag_of_the_United_Kingdom.svg" title="von Original flag by Acts of Union 1800SVG recreation by User:Zscout370 [Public domain oder Public domain], vom Wikimedia Commons" width="30" />  -> English version](README.md)

## MapServer: Zugriff auf MBTiles via GDAL-MBTiles Treiber
Ein [Beispiel-*MapFile*](./MBTiles_GDAL2_3.map) für den Zugriff auf Vector Tiles aus MapServer (Version 7.2) unter Nutzung des [GDAL-MBTiles-Treibers](https://www.gdal.org/frmt_mbtiles.html) (Version 2.3).

Als Datengrundlage wurden Daten von [OpenMapTiles verwendet](https://openmaptiles.com/downloads/europe/switzerland/zurich/).
Das MapFile bietet bei MapServer 7.2 keine Möglichkeit, auf die Optionen CLIP und ZOOM_LEVEL_AUTO des MBTiles-Treibers zuzugreifen. Damit werden die Standardeinstellungen (CLIP=YES; ZOOM_LEVEL_AUTO=NO) übernommen.

Der MBTiles-Treiber hat in Version 2.3 keine Möglichkeit zum Zusammenfügen von kachelübergreifenden Features (MERGE) implementiert.

### Ergebnis

![Ergebnis](MapServer_MapFile_GDAL_MBTiles.png?raw=true "Vector Tiles in MapServer via GDAL-MBTiles-Treiber")

Abbildung: erstellt mit [*MapManager*](https://github.com/DMS-Aus/MapManager) unter Verwendung des [Beispiel-*MapFiles*](./MBTiles_GDAL2_3.map); Datenquelle: Vector Tiles aus [Zurich.mbtiles](https://openmaptiles.com/downloads/europe/switzerland/zurich/)
