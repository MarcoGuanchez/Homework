# 7.1 HW Questions 
## 1. Using EVregistry, Write a query to select the `ModelYear`, `Make`, and `Model` off all of the vehicles in the registry.  
SELECT ModelYear, Make, Model
from evRegistry  
## 2. Using the EVRegistry table, Write a query that lists all of the unique types of EV's. your reult set should have one column, `ElectricVehicleType`.
SELECT DISTINCT ElectricVehicleType
from evRegistry  
## 3. Using the EVRegistry, Write a query that shows all of the information on Battery Electric Vehicles (BEV) that are in the registry.
 select * from  evRegistry where ElectricVehicleType = 'Battery Electric Vehicle (BEV)'
## 4. Using the EVRegistry, wirte a query that returns the `Make` and `Model` of all of the EV's that have a BaseMSRP between 20000 and 35000?
 select Make, Model 
 from  evRegistry 
 where BaseMSRP BETWEEN 20000 and 350007

 # 7.2 HW Questions  

 ## 1. Using EVRegistry, write a query to find a record  where the `City` attribute is NULL. Return all of the available columns.
 select *
 from  evRegistry 
 where City is NULL;
 ## 2. Write a query to find the `make`, `model`, and `ElectricVehicleType` where the VIN number has  that ends in '3E1EA1J'.
 select Make, model, ElectricVehicleType
 from  evRegistry 
 where VIN like "%3E1EA1J"
 ## 3. Select the `ModelYear`, `make`, `model`, `ElectricVehicleType`, and `range` of the Tesla vehicles or cheverolet vehicles in the registry. Order the result set by Make and Model year in from newest to oldest.
 select ModelYear, Make, Model, ElectricVehicleType,ElectricRange
 from  evRegistry 
 where Make = "Tesla" or Make = "Chevrolet"
 ORDER by Make, ModelYear desc
 ## 4. Using EVCharging, Write a query to find out how many many times those stations were used. Order them by the most used to the least used and limit the output to 5 records. 
 select stationId, count(sessionid)
 from    evcharging
 GROUP	by stationId
 order by count(*)DESC
 LIMIT 5;
 ## 5.  Using EVCharging, For the folks who charged longer than 0.5 hours, show the min and max of the charging time for each user. Your output columns should be `userid`, `minTime`, and `maxTime`. Order this result set by the last two columns respectively. 
 select userid, min(chargetimehrs) as minTime, max(chargetimehrs) as maxTime
 from    EVCharging
 WHERE chargeTimeHrs > .5
 GROUP by userId
 ORDER by 2,3;

 # 7.3 HW Questions

## 1. Using EVCharging, Which day of the week has the highest average charging time? Round the answer to 2 decimal points.  
 select  weekday, round(avg(chargetimehrs),2)  
 from    EVCharging
 GROUP by weekday
 ORDER by 2 DESC; 
 ## 2. Using, EV charging, Find the total power consumed from charging EV's by each User. Return the `userId` and name the calculated column, `totalPower`. Round the answer to 2 deciaml points and list the out put in highest to lowest order. Limit the order to the top 15 users.
SELECT userID, ROUND(SUM(kwhTotal), 2) as totalPower
FROM EVCharging
Group By userId
ORDER by 2 DESC
LIMIT 15;
 ## 3. Using dimfacility and factCharge, write a query to find out which type of facility (GROUP BY) has the most amount of charging stations. Return `type Facility` and name the calculated column `numStation`. Order the result set from highest to lowest number of charging stations. 
select dF.typeFacility as typeFacility,count(fC.stationID) as numStation
from dimFacility dF, factCharge fC
where df.FacilityKey = fC.facilityID
group by typeFacility
order by numStation DESC
 ## 4. In your own words, Briefly explain Primary Keys and Foreign Keys. 
 Primary Key: identifies the records in a table.  
 Foreign Key: assists connecting another table with similar record indetifiers. 
 ## 5. Using EV Charging, For the folks who charged longer than one hour, show the min and max of the charging time for each user. Your output columns should be `userid`, `minTime`, and `maxTime`. Order this result set by the last two columns respectively. HINT: USE `HAVING`
 SELECT userId,
 min(chargetimehrs) as minTime, 
 MAX(chargetimehrs) as maxTime
 from EVCharging
 Group by 1
 having chargeTimeHrs > 1
 order by 2, 3