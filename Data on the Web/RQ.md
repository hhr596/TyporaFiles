README

This directory contains the files needed for the Relational Querying (RQ) lab.  Specifically, we have:

`sqlite3`: The executable for SQLite. Note for a Mac - you may need to download a
 replacement for your machine.

`sqliterc`: Some parameters for sqlite3

`TestScript.sql`: A script file that runs a query using sqlite3

`TestOutput.log`: A log file produced as a result of running TestScript.sql

`ra.jar`: The Java jar file for the RA Relational Algebra system. Note you will need to have Java installed to run this.

`RA:Documentation.pdf`: The documentation for the RA Relational Algebra system

`TestQuery.ra`: A file containing a relational algebra query

`RaOutput.log`:  A log file produced as a result of running TestQuery.ra

`mondial.db`: The Mondial database for sqlite3

`mondial.properties`: Information on the database to use, for ra

`mondial-schema.sql`: The Mondial database schema

Here is the unix command line to <u>run sqlite3 on TestScript.sql</u>, which will populate TestOutput.log.

```sqlite
--use this command to run sql on mondial db
sqlite3 -init sqliterc mondial.db < TestScript.sql
```

Here is the unix command line to <u>run ra on TestQuery.ra</u>, which populate RaOutput.log; of course this needs java to be installed.

```sqlite
-- use this command to run ra on mondial db, with generating a log file
java -jar ra.jar mondial.properties -i TestQuery.ra -o RaOutput.log
```



# RQ

> These measurements were taken in a MacBook Air, 2.2 GHz Dual-Core Intel Core i7 with 8 GB 1600 MHz DDR3 with 500GB Flash Storage running macOS Big Sur V 11.3 and SQLite version 3.36.0 2021-06-18 18:36:39.

Consider the relational version of the Mondial database.

## **Task 1**

Write tuple-relational calculus (TRC) expressions that, upon evaluation, return the data characterized by each of the following English-language specifications:

**(1)  Return the name of any country that has a lake.**

$\{  A| \exists C\in Counry\ \exists L\in geo\_Lake\\( C.Code=L.Counry\and A.Country\_Name=  C.Name) \} $



**(2)  Return all the available attributes on cities whose population is between 3 and 5 million inhabitants.**

$\{A|A \in City \ \and\ A.Population > 3000000 \and \ A.Population < 5000000 \}$



**(3)  Return the country code and the continent of every country not in Europe or in Australia/Oceania.**

$\{A|\exists C \in Country \ \exists T \in Continent \ \exists E \in encompasses(C.code = E.country  \ \\\and\  T.Name \and \neg \ (T.Name = "Europe" \and \ T.Name = "Australia/Oceania") \\ \and \ A.Country\_Code = C.code \and\  A.Continent = T.Name)\}$



**(4)  Return the names of countries that also give their name to one of its own provinces.**

$\{A|\exists C \in Country \ \exists P \in Province \ (C.Code = P.Country \ \\\and \ C.Name = P.Name \ \and A.Country\_Name = C.Name) \}$



**(5)  Return the names of countries that are not landlocked (i.e., have a sea coast).**

$\{A|\exists C \in Country \ \exists S \in geo\_Sea \ (C.Code = S.country \ \\ \and \ A.Country\_Name = C.Name) \}$

## **Task 2** 

Write relational-algebraic (RA) expressions that, upon evaluation, returns the data characterized by each of the following English-language specifications.

**(6)  Return the names of countries that are not landlocked (i.e., have a sea coast).**

```sqlite
//Q6
\rename_{Country_Name} \project_{Name}(
		Country \join_{Code=Country} geo_Sea
);
```



**(7)  Return the names of all lakes, rivers and seas.**

```sqlite
//Q7
\rename_{Name} \project_{Lake}(
		geo_Lake \union geo_Sea \union geo_River
);
```



**(8)  Return the name of the country and the name of the organization of countries with Buddhist populations.**

```sqlite
//Q8
\rename_{country_Name,org_Name} \project_{C_Name,O_Name}(
	\rename_{C_Name,C_Code,C_Capital,C_Province,C_Area,C_Popultion} Country \join_{C_Code = R_Country and R_Name = "Buddhist"} \rename_{R_Country,R_Name,R_Percentage} Religion \join_{C_Code = M_Country} \rename_{M_Country,M_Organization,M_Type} isMember \join_{O_Abbreviation = M_Organization} \rename_{O_Abbreviation,O_Name,O_City,O_Country,O_Province,O_Established} Organization
);
```



**(9)  Return the names of countries that also give their name to one of its own provinces.**

```sqlite
//Q9
\rename_{Country_Name} \project_{Name}(
	\select_{Name = p_Name}(
		Country \join_{Code = p_Country} \rename_{p_Name,p_Country,p_Population,p_Area,p_Capital,p_CapProv} Province
	)
);
```



**(10)  Return, for every river in Great Britain, the length of that river.**

```sqlite
//Q10
\rename_{river_Name,Length} \project_{Name,Length}(
	\select_{r_Country = "GB"}(
		River \join_{Name = r_River} \rename_{r_River,r_Country,r_Province} geo_River
	)
);
```




**(11)  Return the names of all cities that have a population larger than that of the capital city of the country.**

```sqlite
//Q11
\rename_{city_Name} \project_{CI2_Name}(
  \rename_{CI1_Name,CI1_Country,CI1_Province,CI1_Population,CI1_Latitude,CI1_Longitude,CI1_Elevation} City \join_{CI1_name = CO_Capital and CI1_Country = CO_Code} \rename_{CO_Name,CO_Code,CO_Capital,CO_Province,CO_Area,CO_Population} Country \join_{CO_Code = CI2_Country and CI2_Population > CI1_Population} \rename_{CI2_Name,CI2_Country,CI2_Province,CI2_Population,CI2_Latitude,CI2_Longitude,CI2_Elevation} City
);

```



## **Task 3** 

Write SQL expressions that, upon evaluation, returns the data characterized by each of the following English-language specifications. Use duplicate removal where appropriate (e.g., when a duplicate is not required in the intended answer).

**(12)  Return the names of up to 10 countries and the value corresponding to half the country’s population.**

```sqlite
--Q12
select C.Name as country_Name,C.Population/2 as HalfPopulation
from Country C
LIMIT 10;
```




**(13)  Return all the information available about cities whose name is Manchester.**

```sqlite
--Q13
select *
from City
where Name = "Manchester";
```




**(14)  Return the name of cities whose name starts with the substring 'Man’.**

```sqlite
--Q14
select Name as city_Name
from City C
where C.Name like 'Man%';
```



**(15)  Return the name of the country and the name of the organization of countries with Buddhist populations that are members of organizations established after 1st December 1994.**

```sqlite
--Q15
select BCM.Name as country_Name,O.name as org_Name
from Organization O,(
	select BC.Name,M.Organization
	from isMember M,
		(select C.Code,C.Name
		from Country C, Religion R
		where C.Code = R.Country and R.Name = "Buddhist") BC
	where BC.Code = M.Country) BCM
where O.Abbreviation = BCM.Organization and Established > "1999-12-01"
;
```




**(16)  Return the name of each country with the number of islands in it.**

```sqlite
--Q16
select C.Name as country_Name,L.island_Num
from Country C,(
select I.Country, count(Country) as island_Num
from geo_Island I
group by Country
) L
where C.Code = L.Country
order by C.Name ;
```
