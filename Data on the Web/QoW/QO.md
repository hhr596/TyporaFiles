# QO

> These measurements were taken in a MacBook Air, 2.2 GHz Dual-Core Intel Core i7 with 8 GB 1600 MHz DDR3 with 500GB Flash Storage running macOS Big Sur V11.3 and SQLite version 3.36.0 2021-06-18 18:36:39.
>
> k72800ll_Lujin_Li

Consider the relational version of the Mondial database.

# Table of Contents

[TOC]

# Task1: Query Analysis

## 1. Pair one: on indices

Optimization taken: considering manually established indices to accelerate query executions.

### 1.1 sql queries

In this pair of queries, only the 'City' table is involved. A query is written to search for the countries that have its code as "NL", its province as "Overijssel" and its population equaled to "123440".

The second query had a pre-founded index `Idx1`.

```sqlite
--sql1.1
select Country from City where Country = "NL" and Province = "Overijssel" and Population = "123440";

--sql1.2
CREATE INDEX Idx1 ON City(Country, Province, Population);
select Country from City where Country = "NL" and Province = "Overijssel" and Population = "123440";
```

### 1.2 Execution times

Each query has been run separately for 100 times. To eliminate possible extreme running conditions, the maximun and the minumun query time of 100 executions are excluded in the calculation of the average time cost. 

The index `Idx1` is manually added when it's needed for the second query.

The suffix `Avg` indicates that it's an average time cost over 100 executions.

```
sql1.1:
realAvg: 0.02783
userAvg: 0.00696
sysAvg: 0.01648

sql1.2:
realAvg: 0.02139
userAvg: 0.00224
sysAvg: 0.01445

realTime improvement percentage: +23.140495867768642
('+' means an improvement is made in sql1.2, '-' means the opposite)
```

### 1.3 Explanation

In this pair of queries. The second query's execution is approximately **23.14% faster**.

This the first query's query plan:

>QUERY PLAN SQL1.1
>
>`--SCAN City

![image-20211129094250071](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111290942175.png)

<center>Graph 1.1.1 - sql1.1 query plan</center>

This the second query's query plan:

>QUERY PLAN SQL1.2
>
>`--SEARCH City USING COVERING INDEX Idx1 (Country=? AND Province=? AND Population=?)

![image-20211129094230903](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111290942103.png)

<center>Graph 1.1.2 - sql1.2 query plan</center>

The SQLite planner would normally set an automatic covering index to accelerate the query. But in this case, since there's only one table used, the optimizer will not generate an automatic query plan. So in the first query, it did a whole table scan for the query, which takes a lot of time, the time cost, in this case, would be O(N). 

However, in the second query, due to the index we added, SQLite took advantage of the index, it can then use a binary search in the index, in this case, the time cost would go down to O(logN). As we are using the 20 times enlarged Mondial database, this brought a great difference to the time cost between these two queries.

## 2. Pair two: on the order of tables

Optimization taken: considering different orders of tables to accelerate query executions.

### 2.1 sql queries

In this pair of queries, we use two tables: Country and Citypops. We simply join the tables together and return every record from the result.

The order of the tables is switched in the second query.

```sqlite
--sql2.1
select * from Country, Citypops  where  Country.Code = Citypops.Country LIMIT 100;

--sql2.2
select * from Citypops, Country  where  Citypops.Country = Country.Code LIMIT 100;
```

### 2.2 Execution times

Each query has been run separately for 100 times. To eliminate possible extreme running conditions, the maximun and the minumun query time of 100 executions are excluded in the calculation of the average time cost. 

The index `Idx1` is manually added when it's needed for the second query.

The suffix `Avg` indicates that it's an average time cost over 100 executions.

```
sql2.1:
realAvg: 0.38948
userAvg: 0.27907
sysAvg: 0.10368

sql2.2:
realAvg: 0.02547
userAvg: 0.00930
sysAvg: 0.01179

realTime improvement percentage: +93.46051145116567
('+' means an improvement is made in sql2.2, '-' means the opposite)
```

### 2.3 Explanation

In this pair of queries. The second query's execution is approximately **93.46% faster**.

This the first query's query plan:

>QUERY PLAN SQL2.1
>
>|--SCAN Country
>
>`--SEARCH Citypops USING AUTOMATIC COVERING INDEX (Country=?)

![image-20211129132109810](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111301606630.png)

<center>Graph 1.2.1 - sql2.1 query plan</center>

This the second query's query plan:

>QUERY PLAN SQL2.2
>
>|--SCAN Citypops
>
>`--SEARCH Country USING AUTOMATIC COVERING INDEX (Code=?)

![image-20211129132153777](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111301606248.png)

<center>Graph 1.2.2 - sql2.2 query plan</center>

This is an extraordinary optimize over the query. The reason behind this is probably because the table index generation strategy of the SQLite optimizer.

When it comes to 2 tables joining in a query, SQLite will do a full scan on the left table. In this scenario, it also generates an automatic index for the second table. The size of the table `Country` is 4880, and the size of the table `Citypops` is 184520. On a modern computer, a full scan under this many rows won't take too much time, but generating an index will because it also involves reordering. Since we limit the number of returned results to 100, so the actual 'search' job won't take too much time. The size of `Citypops` is almost 46 times larger than `Country`, so SQLite will spend more time on generating the automatic index for the `Citypops` table.

To demonstrate my idea, I pre-founded the indices for both two tables and then ran these two queries 100 times separately again. This time it didn't show much time difference (As seen in the results below).

```
--This extra test is run with pre-founded indices on both tables

sql2.1:
realAvg: 0.01712
userAvg: 0.00294
sysAvg: 0.01024

sql2.2:
realAvg: 0.01684
userAvg: 0.00294
sysAvg: 0.00985

realTime improvement percentage: +1.635514018691563
('+' means an improvement is made in sql2.2, '-' means the opposite)
```



## 3. Pair three: on joins

Optimization taken: considering replacing cross-joins with joins to accelerate query executions.

### 3.1 sql queries

In this pair of queries, we use three tables: City, Country and Citypops. We join the tables and return every record from the results.

The 'cross join' is disposed in the second query.

```sqlite
--sql3.1
select * from City cross join Citypops cross join Country where City.Country = Citypops.Country and Citypops.Country = Country.Code and Country.Code = "AL" LIMIT 10;

--sql3.2
select * from City, Citypops, Country where City.Country = Citypops.Country and Citypops.Country = Country.Code and Country.Code = "AL" LIMIT 10;
```

### 3.2 Execution times

Each query has been run separately for 100 times. To eliminate possible extreme running conditions, the maximun and the minumun query time of 100 executions are excluded in the calculation of the average time cost. 

The suffix `Avg` indicates that it's an average time cost over 100 executions.

```
sql3.1:
realAvg: 0.39705
userAvg: 0.28876
sysAvg: 0.10093

sql3.2:
realAvg: 0.15285
userAvg: 0.10734
sysAvg: 0.03976

realTime improvement percentage: +61.50358896864375
('+' means an improvement is made in sql3.2, '-' means the opposite)
```

### 3.3 Explanation

In this pair of queries. The second query's execution is approximately **61.5% faster**.

This the first query's query plan:

>QUERY PLAN SQL3.1
>
>|--SCAN City
>
>|--SEARCH Citypops USING AUTOMATIC COVERING INDEX (Country=?)
>
>`--SEARCH Country USING AUTOMATIC COVERING INDEX (Code=?)

![image-20211130173026888](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111301730026.png)

<center>Graph 1.3.1 - sql2.1 query plan</center>

This the second query's query plan:

>QUERY PLAN SQL3.2
>
>|--SCAN Citypops
>
>|--SEARCH City USING AUTOMATIC COVERING INDEX (Country=?)
>
>`--SEARCH Country USING AUTOMATIC PARTIAL COVERING INDEX (Code=?)

![image-20211130173104413](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111301731538.png)

<center>Graph 1.3.2 - sql2.2 query plan</center>

The reason that the second query is faster is probably because in the first query, the 'cross join' prevents the optimizer from reordering the tables in nest join loops. So it joins tables with the exact given order of tables. It first scanned the `City` table, and the generated a automatic index for `Citypops` and `Country` table. This consumes a lot of time because the size of `Citypops` table is much bigger than the other two tables, so it is not a good idea to generate the index for it since we only return 10 results. Comparing to this, the second query reordered the tables to put tables with smaller sizes together. The `Citypop` table was processed first, it did a full-scan on `Citypop` table but did not generate the index for it.



# Task2: Reflection

The graph 2.1, graph 2.2 and graph 2.3 show the detailed exuction time results for the three pairs of queries.

![image-20211130181809472](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111301818576.png)

<center>Graph 2.1 - execution results of the first pair of queries</center>

![image-20211130181726492](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111301817608.png)

<center>Graph 2.2 - execution results of the second pair of queries</center>

![image-20211130181847089](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111301818213.png)

<center>Graph 2.3 - execution results of the third pair of queries</center>

The graphs show that, even with the same query, the execution time still fluctuates a bit. In graph 2.1 and graph 2.2, we can see some runs have comparatively much longer execution time than the other runs. The execution time of a query is still affected by the I/O, CPU or memory issues.

During my study of the SQLite optimizer and evaluator, I found that SQLite sometimes does not make the best choice for a query though it can analyze the query physically and logically, and the automatically generated index over a large table sometimes is a big problem. For example in a query with "LIMIT 100" condition (As in query pair 2), which only returns 100 records, the optimizer wouldn't expect this will affect the execution time that much, so it takes the "ideal plan" by generating an automatic covering index for the largest table in the query, but it seems not to be the best plan.

As I've learned from the experiments with the three pairs of queries. There are three things we may keep in mind w.r.t writing a query. The first thing is that we should try our best to take advantage of indices, sometimes we don't need to load the whole table into the memory, we will only need part of it through the index table. The second thing is that we should avoid full scans of the table. The Mondial database used in this report is diminutive, but the database in the real world can be a thousand times bigger, so it might take a large amount of time to do a full scan with a table. The third thing is that we should prevent irrelevant columns or rows from the query, this does not only save time, it also saves space in the memory when processing the query.
