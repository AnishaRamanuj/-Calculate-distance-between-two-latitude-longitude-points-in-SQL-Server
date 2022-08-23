## -Calculate-distance-between-two-latitude-longitude-points-in-SQL-Server

First, we create a table and insert two records in this table. We need to enter the value of the latitude and longitude for a point.

```ruby
create database db_GPS
use db_GPS

create table googlemap
(
Id int identity(1,1),  
Location GEOGRAPHY,
LocationName nvarchar(128)
)

insert into googlemap values
(GEOGRAPHY::Point(21.1959,72.7933, 4326),'Adajan' ),
(GEOGRAPHY::Point(21.1418,72.7709, 4326),'Vesu' ),
(GEOGRAPHY::Point(21.1452,72.7571, 4326),'VR mall' ),
(GEOGRAPHY::Point(21.26951,72.8584, 4326),'Kamrej' ),
(GEOGRAPHY::Point(21.1824,72.8154, 4326),'RTO' ),
(GEOGRAPHY::Point(19.0760,72.8777, 4326),'Mumbai' )


SELECT*FROM googlemap

select [LocationName], 
  [Location].Lat as Lat,  [Location].Long as Lon , [Location].STDistance(geography::Point(21.154707,72.764202, 4326)) / 1000  AS DistInKM ,
  [Location].STDistance(geography::Point(22.2587,71.1924, 4326)) / 1609.344 AS Miles
  from googlemap 
  where [Location].STDistance(geography::Point(21.154707,72.764202, 4326)) / 1000 <= 10   //This line will give distance near to 10 Km tradius.


--declare @DistInKM GEOGRAPHY
--SELECT  @DistInKM=Location from googlemap 
--select Location,LocationName, [Location].Lat as Lat,  [Location].Long as Lon , 
--@DistInKM.STDistance(Location)/ 1000[Distance] 
--from googlemap where @DistInKM.STDistance(Location)/ 1000<=300
```
In the query given above, we need to insert two points with the latitude and the longitude values. Afterwards, we need to calculate geographical values for each point using "GEOGRAPHY::Point" method and subsequently we need to calculate the distance of a point from another point.
