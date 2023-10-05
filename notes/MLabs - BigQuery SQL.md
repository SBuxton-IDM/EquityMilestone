
Basic Info to access the measurement-lab project in BigQuery is available at:

https://www.measurementlab.net/data/docs/bq/quickstart/ 

Citing information at:

https://www.measurementlab.net/data/

Queries used to extract test data from the measurement-lab project from the general area of the Eastern Upper Peninsula MI study area.

DOWNLOAD Tests
---------
SELECT id, a.TestTime, client.Geo.Latitude, client.Geo.Longitude, ST_GEOGPOINT(client.Geo.Longitude, client.Geo.Latitude) AS geometry, a.MeanThroughputMbps AS DownMeanMbps, a.minRTT AS DownminRTT
FROM measurement-lab.ndt.unified_downloads
WHERE ST_Within(ST_GEOGPOINT(client.Geo.Longitude, client.Geo.Latitude), ST_GEOGFROMTEXT("POLYGON((-86 48, -83 48, -83 45, -86 45, -86 48))"))
AND
DATE BETWEEN "2023-01-01" AND "2023-10-01";

UPLOAD Tests
---------
SELECT a.UUID, a.MeanThroughputMbps AS UpMeanMbps, a.minRTT AS UpminRTT, ST_GEOGPOINT(client.Geo.Longitude, client.Geo.Latitude) AS geometry, client.Geo.Subdivision1Name
FROM measurement-lab.ndt.unified_uploads
WHERE ST_Within(ST_GEOGPOINT(client.Geo.Longitude, client.Geo.Latitude), ST_GEOGFROMTEXT("POLYGON((-86 48, -83 48, -83 45, -86 45, -86 48))"))
AND
DATE BETWEEN "2023-01-01" AND "2023-10-01";
