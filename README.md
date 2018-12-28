[<img src="https://upload.wikimedia.org/wikipedia/commons/b/ba/Flag_of_Germany.svg" data-canonical-src="https://upload.wikimedia.org/wikipedia/commons/b/ba/Flag_of_Germany.svg" title="von User:SKopp, User:Madden, and other users [Public domain oder Public domain], via Wikimedia Commons" width="30" /> -> German version](README_de.md)

```diff
-- The Master thesis is currently being evaluated --
```
# Vector Tiles as data source for OGC view services
### A master thesis at University of Salzburg - UNIGIS

With the increase in the need to make geodata accessible via internet with a high client-side flexibility, interest in efficient and versatile data exchange formats is growing. Raster data, which are widely used for the representation of geodata, requires a high storage capacity and a higher data throughput and are limited in their flexibility. Original vector data, e.g. provided via WFS, offering a high client-side flexibility. The services are, however, often very slow. At this point, Vector Tiles can be used to distribute geodata because they can combine the advantages of raster and vector data.

Since Vector Tiles are not or only insufficiently implemented in popular desktop clients, the idea was born to investigate whether it is possible and reasonable to offer geodata in Vector Tiles for direct use and to achieve an acceleration of OGC display services in parallel by using these Vector Tiles as data source. As part of the detailed research for the realization of this idea, a comprehensive, structured basic presentation of Vector Tiles was developed and current software for their use was determined. Based on the lessons learnt two scenarios of a WMS based on Vector Tiles were implemented. One scenario takes the detour via raster tiles rendered with *TileServer GL* and is provided via *Mapproxy*. The second solution uses direct integration of Vector Tiles into *MapServer* via *GDAL* library. However, this is currently only implemented to a very limited extent. The performance of the two scenarios was compared in load tests with two conventional WMS based on *shape* files.

As a result, it was determined that the performance of WMS could not be clearly increased with the examined software. When using *TileServer GL* and *Mapproxy* the focus of the interpretation of the results decides on the answer to the question. In the scenario with *MapServer* the currently insufficient integration of *GDAL* library and its limited functionality prevented an effective access to the data. In addition, the first scenario has decisive disadvantages, such as the omission of attribute information. With regard to the problems that have occurred and the limitations that have been established, combined with the current strong progress in the development of Vector Tiles, a productive use of the investigated solution approaches is not recommendable. It can be assumed that after the development of an open standard for Vector Tiles, more practicable and better performing solutions will be published. This will serve as a data basis for a presentation service in the medium term. The direct integration of Vector Tiles into *MapServer* can be seen as first step in this direction.

### Files
- The text version of the Master Thesis in German language is available [here](https://unigis.at/club-unigis/abschlussarbeiten/) after its evaluation, probably in January 2019.
- [Work table Software Vector Tiles (*PDF*)](Software_Vector_Tiles_Arbeitstabelle.pdf)
- [Work table Software Vector Tiles (LibreOffice Calc *ODS*)](Software_Vector_Tiles_Arbeitstabelle.ods)
