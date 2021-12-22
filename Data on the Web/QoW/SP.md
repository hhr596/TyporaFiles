# SP

> These measurements were taken in a MacBook Air, 2.2 GHz Dual-Core Intel Core i7 with 8 GB 1600 MHz DDR3 with 500GB Flash Storage running macOS Big Sur V11.3 and SQLite version 3.36.0 2021-06-18 18:36:39.
>
> k72800ll_Lujin_Li

Consider DBpedia and the relational version of the Mondial database.

# Table of Contents

[TOC]

# 1 Records

This section shows records for the exploratory learning process.

The experiments's goal was trying to retrieve everything relates to a country in Mondial database, including: Capitals, Cities, Provinces, areas, populations, Codes, etc.

## 1.1 TimeSheet

Table 1.1 keeps records of six main activities during the entire process, with corresponding timestamps, how much time I spent and some comments (what did I do in this task) on each task.

| TASK                                 | TIMESTAMP                       | TIME SPENT | COMMENTS                                                     |
| :----------------------------------- | :------------------------------ | :--------- | ------------------------------------------------------------ |
| 1.Play around                        | 6/12/2021 Monday 7:00-10:00     | 3 hours    | (a) Play with DBpedia enpoint, try to find some queries that returns whatever the results.         <br/>(b) Read query examples from DBpedia.          <br/>(c) Learn about the structure of DBpedia. |
| 2.Confirming the target              | 6/12/2021 Monday 10:00-11:00    | 1 hour     | (a) read through the task manual and the schema of Mondial database.                            <br/>(b) confirm the properties needed to filter for countries. |
| 3.Starting from rough search queries | 6/12/2021 Monday 13:00-15:00    | 2 hours    | (a) Try to find at least one country.                                                           <br/>(b) Verify the results to see if they are the literally correct answers. |
| 4.Optimizing queries: preliminary    | 7/12/2021 Tuesday 14:15-17:30   | 3.25 hours | (a) To make sure that the results from DBpedia are basically the same with those from Mondial database. |
| 5.Optimizing queries: advanced       | 8/12/2021 Wednesday 13:00-15:00 | 2 hours    | (a) Find the detailed difference between results from DBpedia and results from Mondial database.                                                                             <br/>(b) Figure out what caused the differences. |
| 6. Further attempts                  | 10/12/2021 Friday 8:00-10:00    | 2 hours    | (a) Seek for further possibilities                           |

<center>Table 1.1 - Timesheet</center>

## 1.2 Questions encountered in each phase

The following table keeps records of the questions I've encountered during each task phase.

| TASK                                 | Frequently encountered questions                             |
| :----------------------------------- | ------------------------------------------------------------ |
| 1.Play around                        | (a) What's the difference between Wikidata and DBpedia, in the way to write a query?                                                                                                                                                                                       <br/>(b) How does it work? What does it mean by `a` and `b`? (They are frequently seen in example queries.)                                                                    <br/>(c) Why some queries go timeout?                                                                                      <br/>(d) Is there a manual that I can use? For example, a manual includes all the valid predicates and subjects.                                                                         <br/>(e) If I made a mistake in the grammar, will the endpoint report the errorness?                                                                                                                          <br/>(f) why the results are links, how can I make it into the names? |
| 2.Confirming the target              | (a) What is available both in the DBpedia and the Mondial database?                   <br/>(b) Is it possible to find all relations of Mondial database in DBpedia? |
| 3.Starting from rough search queries | (a) What predicates can be used to find countries?                                                      <br/>(b) What predicates can be used to find cities?                                                          <br/>(c) What predicates can be used to find capitals?                                                      <br/>(d) What predicates can be used to find provinces?                                                   <br/>(e) What predicates can be used to find areas?                                                          <br/>(f) What predicates can be used to find populations?                                                     <br/>(g) How do we make sure the results are countries? |
| 4.Optimizing queries: preliminary    | (a) Are the results all real countries? Is it possible that some of them are storical countries?                                                                                                              <br/>(b) Are there any duplicates? e.g. Several records with the same country name?                                                                                                                             <br/>(c) How can I search for only English descriptions?                                                     <br/>(d) Why there are still duplicates since we seemed to make sure that there won't be any? |
| 5.Optimizing queries: advanced       | (a) Are the results the same as what we get from the Mondial database?                   <br/>(b) What's the difference between the results from the DBpedia and the Mondial database?                                                                                                       <br/>(c) The number of results from DBpedia is obviously more than that of the Mondial database, why? What caused this situation? |
| 6. Further attempts                  | (a) What other properties we can find w.r.t countries in DBpedia?                            <br/>(b) Does all the properties easy to find in DBpedia?                                                    <br/>(c) What can be really difficult when using DBpedia?                                                 <br/>(d) How do you feel about using DBpedia? Are you familiar with it now? What are the pros and cons? |

<center>Table 1.2 - Question list</center>

# 3 Abbreviated Exploratory Process

This section illustrates the main contents during the whole process of the exploratory work, by describing in a sequence of tasks mentioned in the forementioned timesheet.

## 3.1 Play around

In this phase, we explored basic mechanisms of DBpedia endpoint.

For starters, I ran a few example queries to see what we get from them. Query3.1.1 is one of the examples given by DBpedia default.

```SPARQL
select distinct ?Concept 
where {
  []  a  ?Concept} 
LIMIT 100
```

<center>Query3.1.1 - A simple attempt</center>

Graph 3.1.1 shows part of the results of Query 3.1.1. As we can see from the query, it returned 100 concepts of DBpedia. We can see there are things like: Thing, Class, Company, Organization and Company, etc. One thing we can observe from here is that DBpedia may have something similar to a "schema" but not excactly like an ordinary "schema", it might be like a dictionary.

<img src="https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112151837034.png" alt="image-20211215183725931" style="zoom:67%;" />

<center>Graph3.1.1 - Part of results of Query3.1.1</center>

So I went to look up on the website and took a look at the coursework manual at the same time, I found the link for ["Ontology"](http://mappings.dbpedia.org/server/ontology/classes/). This helped a little bit on understanding how DBpedia works.

## 3.2 Confirming the target & Starting from rough search queries

I decided to start with `Country` table in Mondial database. Graph 3.2.1 shows the table of `Country` in Mondial database.

![image-20211215183908000](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112151839106.png)

<center>Graph3.2.1 - Part of country table in Mondial database</center>

To get started, I wrote a rough query to search for all the entities that might have a relation with country. (As seen in Query3.2.1)


```SPARQL
select distinct ?Country
where {?Country a dbo:Country} LIMIT 100
```

<center>Query3.2.1 - Rough query searching for countries</center>

Then I found something like in the Graph 3.2.2. And they are all links, and it's not easy to be read.

![image-20211215184236414](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112151842504.png)

<center>Graph3.2.2 - Part of results of Query3.2.1</center>

So I added a `?Label` to retrieve the lable of each entity, so to make it readable. (As with Query 3.2.2)

```SPARQL
#ask for labels
#in this way you can access the name label
select distinct ?Country, ?Label
where {?Country a dbo:Country.
      ?Country rdfs:label ?Label} LIMIT 100
```

<center>Query3.2.2 - Added ?Label property </center>

And we have the much readable results with labels. (As seen in Graph 3.2.3)

![image-20211215184522975](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112151845103.png)

<center>Graph3.2.3 - Part of results of Query3.2.2</center>

There are tips that came into my mind:

> 1. Think about filter out  the countries we don't need, such as: storic countries (only exists in stories).
>
> 2. Pay attention to use `rdf:type` to filter the countries.

## 3.3 Optimizing queries: preliminary

We have successfully returned all the entities that may have something to do with "country" in the last phase. So in this phase, our goal is to try to optimize the query, so it can access a more accurate result set.

I started by looking at some pages on DBpedia that actually referring to the real countries. The link down below I found really useful. The search engine that DBpedia offers is not quite useful. It is much easier to search for what we want by replacing the contents after `QueryClass=` and `QueryString=` in the link below and then open the link.

> http://lookup.dbpedia.org/api/search/KeywordSearch?QueryClass=university&QueryString=nankai 

I used this link to do a search for the page of "China". Graph3.3.1 shows the result of this link.

> http://lookup.dbpedia.org/api/search/KeywordSearch?QueryClass=country&QueryString=china

![image-20211214145542913](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141455092.png)

<center>Graph3.3.1 - Part of results of link research</center>

Since it returned some semi-structed data, I also tried to look up countries directly by their name via DBpedia queries. (As with Query3.3.1)

```sparql
select distinct ?Country, ?Label
where {?Country rdf:type dbo:Country.
      ?Country rdfs:label ?Label.
?Country rdfs:label "China".
      
} LIMIT 100
```

<center>Query3.3.1 - Search for "China"</center>



But the query has no returns. (As seen in Graph 3.3.2)

![image-20211214150951979](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141509087.png)

<center>Graph3.3.2 - Results of Query3.3.1</center>

So I dropped the condition for the name of the country, and then added a triple to return countries with Capitals. (In this way, it could probably eliminate some storical countries because they normally have no capitals, as with Query3.3.2)

``` SPARQL
select distinct ?Country, ?Label, ?CapLabel
where {
#it's a country
?Country rdf:type dbo:Country.
?Country rdfs:label ?Label.

#what is the capital
?Country dbo:capital ?Capital.
?Capital rdfs:label ?CapLabel

} LIMIT 100
```

<center>Query3.3.2 - Countries with capitals</center>

It worked, and the number of countries is decreased. (As seen in Graph3.3.3)

![image-20211215190607775](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112151906887.png)

<center>Graph3.3.3 - Part of results of Query3.3.2 </center>

At this timepoint, I started to  think about what decides a thing to be a COUNTRY ?

Here are some possible things I can think of:

> what can we learn from the mondial shcema?
>
> There are some properties: Capital, Province(where the capital belongs to), Area, Population.

So if we keep adding common properties of countries to the query, this might filter out storic countries. e.g. population, area and capitals. (As with Query 3.3.3)

```SPARQL
select distinct ?Country, ?Label, ?CapLabel,?Area, ?Population
where {
#it's a country
?Country rdf:type dbo:Country.
?Country rdfs:label ?Label.
#what kind of country
?Country dbo:area ?Area.
?Country dbo:populationTotal ?Population.
#what is the capital
?Country dbo:capital ?Capital.
?Capital rdfs:label ?CapLabel

} LIMIT 100
```

<center>Query3.3.3 - Added more properties to the query</center>

It works fine with "Area" or "Population", but it gets super slow when it comes together with them both. So I limited the results down to 10. it worked just fine. (As seen in Graph3.3.4)

![image-20211214155049166](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141550266.png)

<center>Graph3.3.4 - Part of results of Code3.3.3 with results limit to 10</center>

A problem has occurred: it seems the results are not distinct, it has redundancy.

After observing the results, I found that there are different versions of the descriptions, including english, chinese, french, etc.

So I decided to use `FILTER (langMatches(lang(?Label),"en"))` to keep only english descriptions. (As with Query3.3.4. Results shown in Graph3.3.5)

```SPARQL
select distinct ?Country, ?Label, ?CapLabel,?Area, ?Population
where {
#it's a country
?Country rdf:type dbo:Country.
?Country rdfs:label ?Label.

#what kind of country
?Country dbo:area ?Area.
?Country dbo:populationTotal ?Population.

#what is the capital
?Country dbo:capital ?Capital.
?Capital rdfs:label ?CapLabel.

FILTER (langMatches(lang(?Label),"en"))
FILTER (langMatches(lang(?CapLabel),"en"))
} LIMIT 10
```

<center>Query3.3.4 - Keep only English descriptions</center>

![image-20211214155459025](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141554114.png)

<center>Graph3.3.5 - Part of results of Query3.3.4</center>

There are still redundancies, we can see some records with the same label name. And judging from the country link, they refer to the same object.

In geneal, it seems that we can't tell any difference between the records. So we keep only `?Country`property to return, to see if it's because some of the properties. (As with Query3.3.5. Results shown in Graph3.3.6)

```sparql
select distinct ?Country
where {
#it's a country
?Country rdf:type dbo:Country.
?Country rdfs:label ?Label.

#what kind of country
?Country dbo:area ?Area.
?Country dbo:populationTotal ?Population.

#what is the capital
?Country dbo:capital ?Capital.
?Capital rdfs:label ?CapLabel.

FILTER (langMatches(lang(?Label),"en"))
FILTER (langMatches(lang(?CapLabel),"en"))
} LIMIT 10
```

<center>Query3.3.5 - Keep only country links</center>

<img src="https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141558600.png" alt="image-20211214155838508" style="zoom:67%;" />

<center>Graph 3.3.6 - Part of results of Query 3.3.5</center>

This time the results seem to be distinct anyway. So the problem must appear on other properties.

After several attempts, I found that it was the `Area` property that caused the redundancy in results.

As we entering `Algeria`'s page, we can see there are acutally two values for `Area`, so that must be the problem. (As shown in graph 3.3.7)

![image-20211214160159875](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141601970.png)

<center>Graph3.3.7 - Page of Algeria on DBpedia</center>

> Why there are two values for the `Area`, and what's the difference?

Then I went searching `Algeria` on wikidata, I found that there's only one record for `Algeria`'s area, which is 2381741 square kilometre. (As shown in Graph 3.3.8) That's the second area record in DBpedia database. So what happend with the first record?

![image-20211214160603917](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141606037.png)

<center>Graph3.3.8 - Area value on wikidata for Algeria</center>

Then I went to search on the world bank data, we can see that the area of `Algeria` had an increase after 2014. It was about 2381740 square kilometre at and before the year of 2014, and it became 2381741 square kilometre at the year of 2015. (As shown in Graph3.3.9 and Graph3.3.10)

![image-20211214160923621](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141609716.png)

<center> Graph3.3.9 - Area value of Algeria in 2014</center>

![image-20211214160945274](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141609464.png)

<center> Graph3.3.10 - Area value of Algeria in 2015</center>

![image-20211214161130343](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141611445.png)

<center> Graph3.3.11 - Latest Area value of Algeria</center>

And it says in the most rencent year (2020), the most recent value of `Algeria`'s area is 2381741 sqare kilometre(As seen in Graph3.3.11). So it is obvious that the data was modified somehow, and the old record is still kept in DBpedia database. Since we cannot filter out the old value because there's no way to find connections between the area values and any other properties, so I decided to leave it alone. And the query is changed into Query 3.3.6. (Results of Query is shown in Graph3.3.12)

```SPARQL
select distinct ?Country, ?Name, ?Capital,?Area, ?Population
where {
#it's a country
?Country rdf:type dbo:Country.
?Country rdfs:label ?Name.

#what kind of country
?Country dbo:area ?Area.
?Country dbo:populationTotal ?Population.

#what is the capital
?Country dbo:capital ?Cap.
?Cap rdfs:label ?Capital.

FILTER (langMatches(lang(?Name),"en"))
FILTER (langMatches(lang(?Capital),"en"))
} 
order by ?Name
LIMIT 100
```

<center>Query3.3.6 - Change back to the former query</center>

![image-20211214162117166](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141621255.png)

<center>Graph3.3.12 - Part of results of Query3.3.6</center>

>  After looking at the statistics, I found that we cannot find "China" in the results, but it is a country. We need to find out what happened.

First, we find the page of `China`:https://dbpedia.org/page/China (As shown in Graph3.3.13 )

![image-20211214164808994](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112151929898.png)

<center>Graph3.3.13 - Part of the page of China</center>

Second, we search all the properties we used in the query, to see if it's because `China` actually lacks some of the properties so it was filtered out during the query process.

After some attempts, I found that when it comes to `dbo:populationTotal`, there are no results in `China`, so this must be where the problem is. 


And I decided to drop this property so we can have a full list of Countries. (As with Query3.3.7)

```sparql
select distinct ?Country, ?Name, ?Capital,?Area
where {
#it's a country
?Country rdf:type dbo:Country.
?Country rdfs:label ?Name.

#what kind of country
?Country dbo:area ?Area.

#what is the capital
?Country dbo:capital ?Cap.
?Cap rdfs:label ?Capital.

#what province is the capital in
FILTER (langMatches(lang(?Name),"en"))
FILTER (langMatches(lang(?Capital),"en"))

} 
order by ?Name
```

<center>Query3.3.7 - Query with population dropped</center>

Use `count(*)` to see how many records we got. (As shown in Graph3.3.14)

![image-20211214165452849](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141654943.png)

<center>Graph3.3.14 - Count records of DBpedia results</center>

And how many records we have in a mondial database. (As shown in Graph3.3.15)

<img src="https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141655680.png" alt="image-20211214165511565" style="zoom:67%;" />

<center>Graph3.3.15 - Count records of Mondial results</center>

Obviously 575 is greater than 244, so there is still redundancy. We need to download the results from DBpedia and compare it to the mondial database, so we can know what we have and what we don't have in the results.

## 3.4 Optimizing queries: advanced

Find patterns of the file with Python, so we can extract what we want from the data. (As shown in Graph 3.4.1)

![image-20211214170409110](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141704237.png)

<center>Graph3.4.1 - File of DBpedia query results</center>

By intercepting the first 14 characters of each line, we can make a list of "line features". (As with Code 3.4.1. Shown in Graph3.4.2. Results shown in Text3.4.1)

```python
countryList = []
wordList = []
with open("HTML5 table.html",'r') as inputFile:
    for line in inputFile:
        ten = line[0:13]
        if ten not in wordList:
            wordList.append(ten)
    print(wordList)
```

<center>Code3.4.1 - Make a list of line features</center>

![image-20211214170659108](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141706210.png)

<center>Graph3.4.2 - Running Python code</center>

```
returned results:

/usr/local/bin/python3.9 "/Users/tablee/Downloads/UoM/0 Data on the Web/QoW/SP/main.py"
['<table class=', '  <tr>\n', '    <td><a hr', '    <td><pre>', '  </tr>\n', '</tbody></tab', '\n', '</body></html']

Process finished with exit code 0
```

<center>Text3.4.1 - Results of intercepted feature list</center>

Regarding the results, we can know that `<tr>\n`indicates the start of a new record, and the `<td><a hr` refers to the link to that record. The first `<td><pre>` that follows `<td><a hr` is the Name of the country, and the second represents for the Capital of the country.

What we need to do is to extract the value that follows the second `<td><pre>` after each `<tr>\n`, and make it into a list. We can use this list to compare with the results from a mondial database. (As with Code 3.4.2)

```python
#find the difference between the results from DBpedia and Mondial database
countryList = []
countryList2 = []
wordList = []
with open("HTML5 table.html",'r') as inputFile:
    for line in inputFile:
        ten = line[0:13]
        if ten not in wordList:
            wordList.append(ten)
with open("intermediate.txt",'w') as outputFile:
    with open("HTML5 table.html",'r') as inputFile:
        for line in inputFile:
            ten = line[0:13]
            if ten == wordList[3]:
                outputFile.write(line.strip(" "))
with open("intermediate.txt",'r') as inputFile:
    flag = 1
    for line in inputFile:
        lineSplit = line.split("\"")
        if flag == 1:
            if lineSplit[1] not in countryList:
                countryList.append(lineSplit[1])
            flag += 1
        elif flag == 3:
            flag = 1
        else:
            flag += 1
with open("countryList.txt",'w') as outputFile:
    for item in countryList:
        # print(f'\033[1;30;43m {item} \033[0m')
        outputFile.write(item)
        outputFile.write('\n')

with open("TestOutput.log",'r') as inputFile:
    for i in range(0,3):
        next(inputFile)
    for line in inputFile:
        country = line.split('|')[0]
        countryList2.append(country)

list1 = []
print("List of countries in DBpedia but not in Mondial (first 10):")
for item in countryList:
    if item not in countryList2:
        list1.append(item)
for i in range(0,10):
    print(list1[i])
print(f'Total:{len(list1)}')
print('\n\n')
list2 = []
print("List of countries in Mondial but not in DBpedia (first 10):")
for item in countryList2:
    if item not in countryList:
        list2.append(item)
list2.sort()
for i in range(0,10):
    print(list2[i])
print(f'Total:{len(list2)}')
```

<center>Code3.4.2 - Find differences between results from DBpedia and Mondial </center>

Text3.4.2 shows the results:

```
/usr/local/bin/python3.9 "/Users/tablee/Downloads/UoM/0 Data on the Web/QoW/SP/main.py"

List of countries in DBpedia but not in Mondial (first 10):
Abkhazia
Adjara
Adélie Land
Aerican Empire
Albania
Ambazonia
Austenasia
Autonomous Administration of North and East Syria
Autonomous Region of Bougainville
Autonomous Republic of Crimea
Total:124



List of countries in Mondial but not in DBpedia (first 10):
American Samoa
Anguilla
Aruba
Bahamas
Bermuda
British Virgin Islands
Cayman Islands
Ceuta
Christmas Island
Cocos Islands
Total:57

Process finished with exit code 0
```

<center>Text3.4.2 - Results of Code3.4.2</center>

The results indicate that there are 124 records that are in DBpedia but not in Mondial and 57 records that are in Mondial but not in DBpedia. Since both the databases have countries that are not in the other database, we need to seek for the reason.

We can literally think of two reasons that may lead to this situation:

>1. Some countries might only exist in history, but not in these days. So the DBpedia has some countries that Mondial has not.
>2. We made a mistake when using some of the properties in the query, thus we omitted some countries. So the Mondial has some countries that DBpedia has not.

We started by looking at the list of countries in DBpedia but not in Mondial.

Taking `Abkhazia` as an example. First we find the page of Abkhazia, and try to find some clues on the page.

We can see that the latest nominal GDP value of `Abkhazia` is in 2010. We don't see any new reports after that. (As shown in Graph3.4.3)

![image-20211214195037309](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141950439.png)

<center>Graph3.4.3 - Latest nominal GDP value record of Abkhazia on DBpedia</center>

> A suspicion raised here is that: Does this country still exists nowadays?

We searched `Abkhazia` on google, and we didn't find anything that suggest `Abkhazia` does not exist anymore.

So we keep finding informations on the page. And then we can see a population was estimated in the year of 2018. (As shown in Graph 3.4.4)

![image-20211214195321689](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112141953842.png)

<center>Graph3.4.4 - Latest Estimated population of Abkhazia on DBpedia</center>

This suggests that `Abkhazia` probably still exists at present.

And the web search results say that present number of countries is 195 (That "countries" usually refers to United Nations Member States).[[1]](https://www.worldometers.info/geography/how-many-countries-are-there-in-the-world/) It is smaller than both the number of DBpedia result and the number of Mondial result. (As shown in Graph3.4.5)

![image-20211214200050208](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112142000368.png)

<center>Graph3.4.5 - Web search results for prsent number of countries in 2021</center>

So we can probably conclude that neither of the databases is 100% correct in the way we might think, and since they are all countries in the real-world ( not in stories ), this should not be a problem.

## 3.5 Further attempts

I also tried to find provinces for the capitals, state/regions within a country, etc. However, not all the information is retrievable.

Take `Zhejiang`province in China for instance, we cannot find anything about either the cities in this province or what country this province belongs to by using triples. Information is rather incomplete for provinces on DBpedia.

![image-20211215012230808](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202112150122954.png)

<center> Graph3.5.1 - Province information of Zhejiang province in China on DBpedia</center>

The only thing that seems to relate to provinces is the connection between the province and its inside universities. (As shown in Graph3.5.1 )

# 4 Conclusion

This section does a brief conclusion of how I feel when I was doing experiments on DBpedia queries.

## 4.1 How effective?

> To what extent did I succeed in writing a set of SPARQL queries that gathers from DBpedia the same information that is available through relational Mondial?

The DBpedia kept relations for coutries with only part of the properties mentioned in a Mondial database. It is hard to retrieve exactly the same relevant properties for a country in DBpedia. Regarding my experiment, I could retrieve 60% of the properties. (e.g. In the Country table of Mondial database, `Code` and `Province` is hard to retrieve, and there are six properties in total, so in this case the extent of retrievability is 4/6 = 66.66%)

## 4.2 How efficient?

> How much time did it take me to explore of the information content of the DBpedia using SPARQL queries that try and gauge what is available in that resource?

It took nearly half of my time to figure out what was retrievable and what was not. The reason why it took so much time is because it needs you to go through the DBpedia page of your results thoroughly, and check every detail in case it might be useful to the queries.

> How much time did it take me to discover how to write the set of SPARQL queries you have succeeded in writing?

The literally time for success in the writing of a set of SPARQL queries is actully not so long, it probably only took 10% of my time. However, trying to get a clue on what's needed to write a "correct" query consumed the majority of the time. Each query returns a bunch of results, and you're expected to read through 80% of results so you could possibly find patterns.

# 5 References

[1] How many countries are there in the world? (2021) - Total & List | Worldometer. 2021. How many countries are there in the world? (2021) - Total & List | Worldometer. [ONLINE] Available at: https://www.worldometers.info/geography/how-many-countries-are-there-in-the-world/. [Accessed 8 December 2021].
