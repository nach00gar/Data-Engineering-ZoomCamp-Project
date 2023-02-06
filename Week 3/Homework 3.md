1) Manual creation, I had issues with server location compatibility, I couldn´t connect bucket to bigquery having the dataset in a different continental locations.
```
SELECT count(*) FROM `hw3zoomcamp.hw3`;
```
```
CREATE OR REPLACE TABLE `hw3zoomcamp.no_partitions` AS
SELECT * FROM `hw3zoomcamp.hw3`;
```
2) 
```
SELECT COUNT(DISTINCT affiliated_base_number) FROM `hw3zoomcamp.hw3`;
SELECT COUNT(DISTINCT affiliated_base_number) FROM `hw3zoomcamp.no_partitions`;
```

3)
```
SELECT COUNT(*) FROM `hw3zoomcamp.no_partitions` WHERE PUlocationID IS NULL AND DOlocationID IS NULL;
```
4)
```
CREATE OR REPLACE TABLE `hw3zoomcamp.pc`
PARTITION BY DATE(pickup_datetime)
CLUSTER BY affiliated_base_number AS
SELECT * FROM `hw3zoomcamp.hw3`;
```
5)
```
SELECT DISTINCT affiliated_base_number FROM `hw3zoomcamp.no_partitions`
WHERE DATE(pickup_datetime) BETWEEN '2019-03-01' AND '2019-03-31';
```
```
SELECT DISTINCT affiliated_base_number FROM `hw3zoomcamp.pc`
WHERE DATE(pickup_datetime) BETWEEN '2019-03-01' AND '2019-03-31';
```
6) They`re not in BQ, actually data comes from a Bucket in the same location, that relates to the issue in ex1.
