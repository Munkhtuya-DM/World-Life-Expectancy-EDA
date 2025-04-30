.sql  --   Us Household Income Data Cleaning Steps
SELECT *
FROM US_Household_Income ;

SELECT * 
FROM Us_household_Income_statistics;

SELECT COUNT(id)
FROM US_Household_Income ;
SELECT COUNT(id)
FROM Us_household_Income_statistics;

  --  Found duplicate  
SELECT id, COUNT(id)
FROM US_Household_Income
GROUP BY id
HAVING COUNT (id)> 1; 

SELECT *
FROM (
    SELECT row_id, id, ROW_NUMBER() OVER(PARTITION BY id ORDER BY id ) AS row_num
    FROM US_Household_Income 
    ) duplicates
WHERE row_num > 1 ;

  --  Remove Duplicates
DELETE FROM US_Household_Income
WHERE row_id IN (
   SELECT row_id
   FROM (
    SELECT row_id, id, ROW_NUMBER() OVER(PARTITION BY id ORDER BY id ) AS row_num
    FROM US_Household_Income 
       ) duplicates
WHERE row_num > 1 );

SELECT id , COUNT(id)
FROM Us_household_Income_statistics
GROUP BY id
HAVING COUNT(id) > 1 ;

SELECT DISTINCT State_Name
FROM US_Household_Income
ORDER BY 1;

-- Fixing some data qualify issues by fixing typos and general Standardizion 
 UPDATE US_Household_Income
 SET State_Name = 'Georgia' 
 WHERE State_Name = 'georia'

UPDATE US_Household_Income
SET State_Name = 'Alabama'
WHERE State_name = 'alabama';

SELECT * 
FROM US_Household_Income
WHERE County = 'Autauga County'
ORDER BY 1 ;

UPDATE US_Household_Income
SET Place = 'Autaugaville'
WHERE County = 'Autauga County'
AND City = 'Vinemont';

SELECT Type, COUNT(Type)
FROM US_Household_Income 
GROUP BY type
ORDER BY 1;
UPDATE US_Household_Incom
SET Type = 'Borough'
WHERE Type = 'Broughs' ;

SELECT Aland , Awater
FROM US_Household_Income
WHERE (Awater = 0 OR Awater IS NULL)
AND (Aland = 0 OR Aland = '' OR Aland IS NULL);

 -- US Household Income Exploraty Data Analysis
SELECT State_Name , County, Aland , City, Awater
FROM US_Household_Income ;
--# Identifying top 10 
SELECT State_Name , SUM(Aland) , SUM(Awater)
FROM US_Household_Income
GROUP BY State_Name
ORDER BY 2 DESC 
LIMIT 10 ;

SELECT u.State_Name  ,ROUND(AVG(Mean),1) , ROUND(AVG(Median),1) 
FROM US_Household_Income u
INNER JOIN Us_household_Income_statistics us
      ON u.id = us.id
WHERE Mean <> 0 
GROUP BY u.State_Name
ORDER BY 2 DESC
LIMIT 10 ;

SELECT Type ,ROUND(AVG(Mean),1) , ROUND(AVG(Median),1) 
FROM US_Household_Income u
INNER JOIN Us_household_Income_statistics us
      ON u.id = us.id
WHERE Mean <> 0 
GROUP BY Type
ORDER BY 2 DESC
LIMIT 10 ;

SELECT Type , COUNT(Type) ,ROUND(AVG(Mean),1) , ROUND(AVG(Median),1) 
FROM US_Household_Income u
INNER JOIN Us_household_Income_statistics us
      ON u.id = us.id
WHERE Mean <> 0 
GROUP BY 1
ORDER BY 3 DESC
LIMIT 20 ;

SELECT * 
FROM  US_Household_Income
WHERE Type = 'Community';

SELECT u.State_Name , City , ROUND(AVG(Mean),1), ROUND(AVG(Median),1)
FROM US_Household_Income u
JOIN Us_household_Income_statistics us
      ON u.id = us.id
GROUP BY u.State_Name ,City
ORDER BY ROUND(AVG(Mean),1) DESC  

DELIMITER $$ 
CREATE PROCEDURE Copy_clean_data()
BEGIN
    CREATING OUR TABLE
 CREATE TABLE IF NOT EXISTS  `us_household_income_Cleaned` (
    `row_id` int NOT NULL,
    `id` int NOT NULL,
    `State_Code` int NOT NULL,
    `State_Name` varchar(20) NOT NULL,
    `State_ab` varchar(2) NOT NULL,
    `County` varchar(33) NOT NULL,
    `City` varchar(22) NOT NULL,
    `Place` varchar(36) DEFAULT NULL,
    `Type` varchar(12) NOT NULL,
    `Primary` varchar(5) NOT NULL,
    `Zip_Code` int NOT NULL,
    `Area_Code` varchar(3) NOT NULL,
    `ALand` bigint NOT NULL,
    `AWater` bigint NOT NULL,
    `Lat` decimal(10, 7) NOT NULL,
    `Lon` decimal(12, 7) NOT NULL,
    `TimeStamp` TIMESTAMP DEFAULT NULL,
    PRIMARY KEY (`row_id`)
) ENGINE = InnoDB DEFAULT CHARSET = utf8mb4 COLLATE = utf8mb4_0900_ai_ci;

-- COPY DATA  NEW TABLE for backup
  INSERT INTO  us_household_income_Cleaned
  SELECT * , CURRENT_TIMESTAMP
  FROM US_Household_Income ;
END $$
DELIMITER ;


CALL Copy_clean_data();
SELECT * FROM us_household_income_Cleaned

 -- DEBUGGING OR CHECKING SP WORKS


   SELECT row_id , id, row_num
   FROM (
    SELECT row_id, id, ROW_NUMBER() OVER(PARTITION BY id ORDER BY id ) AS row_num
    FROM US_Household_Income 
       ) duplicates
WHERE row_num > 1 ;

SELECT COUNT(row_id)
FROM US_Household_Income ;

SELECT State_Name , COUNT(State_Name)
FROM US_Household_Income
GROUP BY State_Name;


-- CREATE EVENT 

CREATE EVENT run_data_cleaning
      ON SCHEDULE EVERY 2 MINUTE
      DO CALL Copy_clean_data();
 SELECT *  FROM us_household_income_Cleaned;



-- CREATE TRIGGER
DELIMITER $$ 
CREATE TRIGGER Transfer_clean_data
  AFTER INSERT ON us_household_income
  FOR EACH ROW 
BEGIN 
    CALL Copy_clean_data
END $$
DELIMITER ;


 SELECT DISTINCT TimeStamp
 FROM us_household_income_Cleaned;
