[<img src="https://upload.wikimedia.org/wikipedia/commons/b/ba/Flag_of_Germany.svg" data-canonical-src="https://upload.wikimedia.org/wikipedia/commons/b/ba/Flag_of_Germany.svg" title="von User:SKopp, User:Madden, and other users [Public domain oder Public domain], via Wikimedia Commons" width="30" /> -> German version](README_de.md)

## MapServer: Access to MBTiles via GDAL-MBTiles driver
A [*MapFile* example](./MBTiles_GDAL2_3.map) for accessing Vector Tiles from MapServer (version 7.2) using the [GDAL-MBTiles driver](https://www.gdal.org/frmt_mbtiles.html) (version 2.3).

Data from [OpenMapTiles verwendet](https://openmaptiles.com/downloads/europe/switzerland/zurich/) was used as the data basis. With MapServer 7.2, MapFile does not offer the possibility to access the options CLIP and ZOOM_LEVEL_AUTO of the MBTiles driver. Thus the default settings (CLIP=YES; ZOOM_LEVEL_AUTO=NO) are adopted.

The MBTiles driver in version 2.3 has no possibility to merge features across tiles (MERGE).

### Result

![result](./MapServer_MapFile_GDAL_MBTiles.png?raw=true "Vector Tiles in MapServer via GDAL-MBTiles-driver")

Figure: created with [*MapManager*](https://github.com/DMS-Aus/MapManager) using the [*MapFile* example](./MBTiles_GDAL2_3.map); data source: Vector Tiles from [Zurich.mbtiles](https://openmaptiles.com/downloads/europe/switzerland/zurich/)
