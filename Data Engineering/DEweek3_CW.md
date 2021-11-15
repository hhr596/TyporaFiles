# 1. Task5

# 1.1 Task 5.1 (in Excel)

## Step1

Open the CSV file in Excel to see the original dataset and adjust column A's format into `dddd yyyy/m/d hh:mm:ss` by using the format cell setting. (As shown in graph 1.1)

![image-20211019004105220](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019004105220.png)

<center>Graph 1.1 - Original dataset with formatted column A</center>

## Step 2

Add a column to mark weekday info for each record with Excel function `=WEEKDAY(...)`. (As shown in graph 1.2, 3 for Tuesdays, 6 for Fridays)

![image-20211019004443912](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019004443912.png)

<center>Graph 1.2 - Mark with weekdays</center>

## Step 3

Keep records for Tuesdays by using the ![image-20211019004645003](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019004645003.png). (As shown in graph 1.3)

![image-20211019005139314](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019005139314.png)

<center>Graph 1.3 - Filter for Tuesdays</center>

## Step 4

Save Filter results (All for Tuesdays' records) into a separate file named `Tuesdays.xlxs`. (As shown in graph 1.4)

![image-20211019005522343](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019005522343.png)

<center>Graph 1.4 - Save Tuesdays' records</center>

## Step 5

Use `Tuesdays.xlxs`, add three columns: 

1. `Time satisfied`: If the time is between 7:00 to 19:00, mark it as 1 else 0. The code is as follows.

```
=COUNTIFS(A2,">=2018/2/6  7:00:00",A2,"<2018/2/6  19:00:00")+COUNTIFS(A2,">=2018/2/13  7:00:00",A2,"<2018/2/13  19:00:00")+COUNTIFS(A2,">=2018/2/20  7:00:00",A2,"<2018/2/20  19:00:00")+COUNTIFS(A2,">=2018/2/27  7:00:00",A2,"<2018/2/27  19:00:00")
```

2. `isBlank_Gap(s)`: If the corresponding `Gap(s)`column is empty, mark it as True else False. The code is as follows.

``` 
=ISBLANK(H2)
```

2. `isBlank_Headway(s)`: If the corresponding `Headway(s)`column is empty, mark it as True else False. The code is as follows.

``` 
=ISBLANK(G2)
```

Then apply them to each cell in the column. (As shown in graph 1.5)

![image-20211019040051735](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019040051735.png)

<center>Graph 1.5 - Time satisfiled and isBlank columns</center>

## Step 6 (Final & Analysis)

Add four columns to collect the final answer: 

1. `Column`: This column has two records, one stands for results for `Gap(s)`, the other stands for results for `Headway(s)`.
2. `Total records`: The number of records that is between 7:00 to 19:00, the code is as follows.

```
=COUNTIFS(A:A,">=2018/2/6  7:00:00",A:A,"<2018/2/6  19:00:00")+COUNTIFS(A:A,">=2018/2/13  7:00:00",A:A,"<2018/2/13  19:00:00")+COUNTIFS(A:A,">=2018/2/20  7:00:00",A:A,"<2018/2/20  19:00:00")+COUNTIFS(A:A,">=2018/2/27  7:00:00",A:A,"<2018/2/27  19:00:00")
```

3. `Empty Gap(s)`: The number of records that is within 7:00 to 19:00 and the corresponding `Gap(s)` and `Headway(s)`cell is empty. The code is as follows.

```
=COUNTIF(M:M,"=TRUE")
=COUNTIF(N:N,"=TRUE")
```

4. `Column Completeness`: Column_Completeness = (number_of_non-empty_cells x 100) / number_of_cells. The code is as follows:

```
=(N2-O2)*100/N2
=(P3-Q3)*100/P3
```

Then apply these formula, get the final results. (As shown in graph 1.6)

![image-20211019040341709](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019040341709.png)

<center>Graph 1.6 - Final results for Task 5.1</center>

> The `Gap(s)`column Completeness is **<u>96.41615911</u>**.
>
> The `Headway(s)`column Completeness is **<u>97.45929149</u>**.

Analysis: 

For `Gap(s)`, if the data is for academic use, this will not be a data in good quality. Even it's just about 4% of data loss, it turns out to be 7000+ records, especially under those occasions where the police is using the data to analyse car accidents, data incompletion at some key points may cause confusion in analysing.  

For `Headway(s)`, comparing to `Gap(s)` 's completeness, the `Headway(s)`'s is 1% higher, which is an improvement. However, if the data is for academic use, this will still not be a data in good quality. It still has 5000+ records missing. 

However, if the data is just for fun, they can all be acceptable completenesses.



# 1.2 Task 5.2 (in Excel + Python)

## Step 1

Copy `Tuesdays.xlsx` into `Tuesdays-2.xlsx` and use the `Tuesdays-2.xlsx`. (As shown in graph 1.7)

![image-20211019044238707](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019044238707.png)

<center>Graph 1.7 - Tuesdays-2.xlsx</center>

## Step 2

Add a new column next to column A, and copy column A's content into the new column. Change it's header's name to `Time` (As shown in graph 1.8)

![image-20211019044430832](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019044430832.png)

<center>Graph 1.8 - Add column B and copy column A</center>

## Step 3

Change Column B's format into `hh:mm:ss`. (As shown in graph 1.9)

![image-20211019045716668](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019045716668.png)

<center>Graph 1.9 - Change format of column B</center>

## Step 4

Use ![image-20211019045524187](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019045524187.png)to delete all the date info within column B to keep only time info. (Dates concerning 2/6, 2/13, 2/20, 2/27. As shown in graph 1.10 )

![image-20211019045923085](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019045923085.png)

<center>Graph 1.10 - Delete all date info</center>

## Step 5

Use ![image-20211019050322758](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019050322758.png)to sort the date by column B, in this case, we get a dataset that is ordered exactly by time (Date exclusive). (As shown in graph 1.11)

![image-20211019050500603](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019050500603.png)

<center>Graph 1.11 - Sorted by time (Date exclusive)</center>

## Step 6

Use ![image-20211019050859823](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019050859823.png)to keep records only for NB_MID lane (North direction), copy them into a new file `Tuesdays-3.xlsx` . (As shown in graph 1.12)

![image-20211019053936145](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019053936145.png)

<center>Graph 1.12 - Tuesdays-3.xlsx</center>

# Step 7

Export `Tuesdays-2.xlsx` as a csv file, use python to obtain each hour's start row number and end row number. (As shown in graph 1.13)

```python
# python code
with open('Tuesdays-2.csv','r') as csvFile:
    flag = 0
    countA = 2
    countB = 2
    next(csvFile)
    column = 'I'
    for row in csvFile:
        content = row.split(',')
        time = content[1].split(':')
        if int(time[0]) != flag:
            print('=MEDIAN('+column+str(countA)+':'+column+str(countB-1)+')')
            countA = countB
            flag +=1
        countB += 1
    print('=MEDIAN(' + column + str(countA) + ':' + column + str(countB - 1) + ')')
```

![image-20211019063442421](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019063442421.png)

<center> Graph 1.13 - Use python to obtain time points </center>

## Step 8

Add three columns into `Tuesdays-2.xlsx`:

1. `Hour(x to x+1)`: to mark hour period, 0 would be for 0:00:00 to 0:59:59.
2. `Median Gap(s)`: receive results for hourly Gap(s)'s median calculation.
3. `Median Headway(s)`: receive results for hourly Headway(s)'s median calculation.

Use the time points obtained from python. In `Tuesdays-2.xlsx`, apply `median` function to calculate each hour's median `Gap(s)` and `Headway(s)`. (As shown in graph 1.14)

![image-20211019063759859](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019063759859.png)

<center>Graph 1.14 - Calculate hourly median</center>


## Step 9

Export `Tuesdays-3.xlsx` as CSV file, use python to fill in empty cells of `Headway(s)`column and `Gap(s)`Column with corresponding median values of the hour, write the result into a new file name `Tuesdays-4.xlsx`. (As shown in graph 1.15)

```python
# python code
def list2string(row):
    convertedString = ''
    for item in row:
        convertedString += str(item)
        convertedString += ','
    return convertedString[0:len(convertedString) - 1]

#gap column = 8
gapMedian = [32, 44.058, 45.418, 50.9995, 35.623, 13.342, 3.5035, 1.996, 2.101, 2.3085, 3.112, 3.153, 2.964, 2.882, 2.6725, 2.109, 1.8105, 1.877, 2.04, 2.999, 4.7055, 7.0065, 9.8695, 17.6705]
#headway column = 7
headwayMedian = [31.5,44.45,45,50.25,35.75,13.15,3.912,2.752,3,2.917,3.521,3.544,3.356,3.254,3.075,2.604,2.45,2.584,2.636,3.375,5.123,7.1,9.8,17.8]

with open('Tuesdays-3.csv', 'r') as inputFile:
    with open('Tuesdays-4.csv', 'w') as outputFile:
        outputFile.write(next(inputFile))
        for row in inputFile:
            rowinList = row.split(',')
            timeinList = rowinList[1].split(':')
            hour = int(timeinList[0])
            if rowinList[8] == '':
                rowinList[8] = gapMedian[hour]
            if rowinList[7] == '':
                rowinList[7] = headwayMedian[hour]
            outputFile.write(list2string(rowinList))
```

![image-20211019071212259](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019071212259.png)

<center>Graph 1.15 - Python filling in empty cells with median values</center>

# Step 10 (Final & Analysis)

Open `Tuesdays-4.xlsx`to see the updated dataset. (As shown in graph 1.16)

![image-20211019071428050](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019071428050.png)

<center>Graph 1.16 - Updated dataset with median values</center>

Interpretation of results:

In this case, 1263 records have empty `Headway(s)` or `Gap(s)`or both, and each empty cell has been filled with the median value of `Headway(s)` or `Gap(s)`in that hour on all Tuesdays.

This is the median value calculation result (Chart 1.1):

| Hour(x  to x+1) | Median Gap(s) | Median Headway(s) |
| --------------- | ------------- | ----------------- |
| 0               | 32            | 31.5              |
| 1               | 44.058        | 44.45             |
| 2               | 45.418        | 45                |
| 3               | 50.9995       | 50.25             |
| 4               | 35.623        | 35.75             |
| 5               | 13.342        | 13.15             |
| 6               | 3.5035        | 3.912             |
| 7               | 1.996         | 2.752             |
| 8               | 2.101         | 3                 |
| 9               | 2.3085        | 2.917             |
| 10              | 3.112         | 3.521             |
| 11              | 3.153         | 3.544             |
| 12              | 2.964         | 3.356             |
| 13              | 2.882         | 3.254             |
| 14              | 2.6725        | 3.075             |
| 15              | 2.109         | 2.604             |
| 16              | 1.8105        | 2.45              |
| 17              | 1.877         | 2.584             |
| 18              | 2.04          | 2.636             |
| 19              | 2.999         | 3.375             |
| 20              | 4.7055        | 5.123             |
| 21              | 7.0065        | 7.1               |
| 22              | 9.8695        | 9.8               |
| 23              | 17.6705       | 17.8              |

<center>Table 1.1 - Hourly median results on Tuesdays</center>



# 2. Task 6 (in Python)

## Step 1

In python, keep records for <u>Fridays</u> and <u>North lanes</u>, and save the result as a new file `1083-1.csv`. (As shown in graph 2.1 and graph 2.2)

```python
# python code
givenDate = ['2018-02-02','2018-02-09','2018-02-16','2018-02-23']
with open('rawpvr_2018-02-01_28d_1083 TueFri.csv','r') as inputFile:
    with open('1083-1.csv','w') as outputFile:
        outputFile.write(next(inputFile))
        for row in inputFile:
            rowinList = row.split(',')
            dateTimeinList = rowinList[0].split(' ')
            date = dateTimeinList[0]
            direction = rowinList[4]
            if date in givenDate and direction == 'North':
                outputFile.write(row)
```



![image-20211019223445382](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019223445382.png)

<center>Graph 2.1 - Python filtering out Fridays and North lanes</center>

![image-20211019223518944](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019223518944.png)

<center>Graph 2.2 - 1083-1.csv</center>

## Step 2

Repeat step 1&2 for site 1415's records, and save the result into a new file `1415-1.csv`. (Choose direction as NorthEast. As shown in graph 2.3)

```python
# python code
givenDate = ['2018-02-02','2018-02-09','2018-02-16','2018-02-23']
with open('rawpvr_2018-02-01_28d_1415 TueFri.csv','r') as inputFile:
    with open('1415-1.csv','w') as outputFile:
        outputFile.write(next(inputFile))
        for row in inputFile:
            rowinList = row.split(',')
            dateTimeinList = rowinList[0].split(' ')
            date = dateTimeinList[0]
            direction = rowinList[4]
            if date in givenDate and direction == 'NorthEast':
                outputFile.write(row)
```



![image-20211019223642103](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019223642103.png)

<center>Graph 2.3 - 1415-1.csv</center>

## Step 3

Use Python to process both `1083-1.csv`and`1415-1.csv`, keep records between 17:00 to 18:00, and save the result into `1083-1-17to18.csv`and `1415-1-17to18.csv` . (As shown in graph 2.4, 2.5 and 2.6)

```python
# python code
def filter17to18(fileQueue):
    for item in fileQueue:
        with open(item+'.csv','r') as inputFile:
            with open(item+'-17to18.csv','w') as outputFile:
                outputFile.write(next(inputFile))
                for row in inputFile:
                    rowinList = row.split(',')
                    integrateTimeinList = rowinList[0].split(' ')
                    timeinList = integrateTimeinList[2].split(':')
                    hour = int(timeinList[0])
                    if hour == 17:
                        outputFile.write(row)

#main body
fileQueue = ['1083-1','1415-1'] #input csv files
filter17to18(fileQueue)
```

![image-20211019170839595](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019170839595.png)

<center>Graph 2.4 - Python filtering for records between 17:00 and 18:00</center>

![image-20211019171049253](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019171049253.png)

<center>Graph 2.5 - 1083-1-17to18.csv</center>

![image-20211019171209942](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019171209942.png)

<center>Graph 2.6 - 1415-1-17to18.csv</center>

## Step 4 (Final & Analysis)

By far we've successfully kept records between 17:00 to 18:00 on Fridays with only the North direction lanes. Now we need to calculate the hourly average vehicle speed for each lane on two sites. There are 5 lanes in total: NB_NS, NB_MID, NB_OS, NE_NS, NE_OS. Use python to calculate the result, and print it on the screen. (As shown in graph 2.7 and 2.8)

```python
# python code
fileQueue = ['1083-1','1415-1'] #input csv files
def mph2kmh(mph):
    return mph*float(1.609344)
def averageSpeedof(file):
    averageSpeed = [0,0,0,0,0,0]
    with open(file+'-17to18.csv','r') as inputFile:
        next(inputFile)
        for row in inputFile:
            rowinList = row.split(',')
            laneinRow = int(rowinList[1])
            speedinRow = float(rowinList[5])
            speedinRow = mph2kmh(speedinRow)
            averageSpeed[laneinRow-1] += 1
            averageSpeed[laneinRow+2] += speedinRow
    return averageSpeed

distance = float(4.86) #km
average1083 = averageSpeedof(fileQueue[0])
average1415 = averageSpeedof(fileQueue[1])
averageList = [average1083[3]/average1083[0],average1083[4]/average1083[1],average1083[5]/average1083[2],average1415[3]/average1415[0],average1415[4]/average1415[1]]
totalAverageSpeed = 0
print('Separate lane average speed (rounded to 2 decimals, kmh):')
print('{',end='')
for item in averageList:
    totalAverageSpeed += item
    print(format(item,'.2f'), end=', ')
totalAverageSpeed = totalAverageSpeed / len(averageList)
print('}')
print()
print('Total Average Speed (rounded to 2 decimals):')
print(format(totalAverageSpeed,'.2f'),'kmh')
print()
print('Total Average Travel time (rounded to 2 decimals):')
print(format(distance/totalAverageSpeed*60,'.2f'),'min')
```

![image-20211019181505891](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019181505891.png)

<center>Graph 2.7 - Python processing fianl average travel time</center>

![image-20211019181525960](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019181525960.png)

<center>Graph 2.8 - Fianl Receipt</center>

Interpretation of results:

>  **The typical Friday journey time** for the road fragment between site 1083 and site 1415, between 17:00 and 18:00, using only the North direction lanes, **is around 6.71 minutes**.

During the processing of looking into the data, I found the average travel speed is basically around 38-48 kmh, fluctuating up and down 10 kmh, which leads to approximately 1 minute's traveling time gap between the slowest and the fastest.



# 3. Task 7

# 3.1 Task 7.1

## (i) Suggesting a Row completeness formula

Suggesting the **Row Completeness Formula** is:

<center><p style="font-style:italic; font-size:20px">
  Row_Completeness = (Total_rows - Number_of_Rows_with_empty_cells) * 100 /Total_rows
  </p></center>
>Why make suggestion like this: Regarding *Column_Completeness = (number_of_non-empty_cells x 100) / number_of_cells*, it refers to if the column is complete. Because the column here is specific, so it would be the completeness regarding cells in a column. When it comes to Row Completeness, which means we're expected to assess whether rows are complete, rows with empty cells are not complete, so the completeness is refering to the number of rows that have no empty cell in every column.


## (ii) Make the assessment (in Excel + Python)

### Step 1

In Excel, change the column A's format into `dddd yyyy/m/d hh:mm:ss`, add a column named `weekday` using  **WEEKDAY** function to mark each row with it's weekday info.  Then use ![image-20211019210231083](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019210231083.png) to filter out records associated with Tuesdays. Save the result into file `task7-1.csv`. (As shown in graph 3.1)

![image-20211019212320277](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019212320277.png)

<center>Graph 3.1 - Filter out Tuesday's records</center>

### Step 2

In Python, import the`task7-1.csv`, filter out records between 7:00 and 19:00, and save it to `task7-2.csv`. (As shown in graph 3.2 and graph 3.3)

```python
# python code
with open('task7-1.csv','r') as inputFile:
    with open('task7-2.csv','w') as outputFile:
        outputFile.write(next(inputFile))
        for row in inputFile:
            rowinList = row.split(',')
            dateTimeinList = rowinList[0].split(' ')
            timeinList = dateTimeinList[2].split(':')
            hour = int(timeinList[0])
            if hour>=7 and hour<19:
                outputFile.write(row)
```

![image-20211019212900442](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019212900442.png)

<center>Graph 3.2 - Filter out records between 7:00 to 19:00</center>

![image-20211019213020246](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019213020246.png)

<center>Graph 3.3 - task7-2.csv</center>

### step 3 (Fianl)

In Python, calculate number of total rows, number of rows with empty columns, and exert the **Row Completeness Formula**. (As shown in graph 3.4 and graph 3.5)

<center><p style="font-style:italic; font-size:20px">
  Row_Completeness = (Total_rows - Number_of_Rows_with_empty_cells) * 100 /Total_rows
  </p></center>

```python code
rowswithEmptyCells = 0
totalRows = 0
with open('task7-2.csv','r') as inputFile:
    next(inputFile)
    for row in inputFile:
        totalRows += 1
        rowinList = row.split(',')
        rowinList = rowinList[0:9]
        for item in rowinList:
            if item == '':
                rowswithEmptyCells += 1
                break
print(f'Number of rows with empty cells: {rowswithEmptyCells}')
print(f'Total rows: {totalRows}')
print(f'Row Completeness: {(totalRows-rowswithEmptyCells)*100/totalRows}')
```

![image-20211019213830734](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019213830734.png)

<center>Graph 3.6 - Code for Row Completeness</center>

![image-20211019213909913](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019213909913.png)

<center>Graph 3.7 - Row Completeness Receipt</center>

Interpretation:

> **The Row Completeness is approximately 98.03%**.

This is a nearly-satisfying percentage of row completeness, but it's not perfect. It indicates how many records are completely valid regarding every parameter (in here, columns). Rows with incompletion may be of no use under some occasions (e.g. when analysing data requires for all columns to be not empty).

### (iii) Discuss

Completeness in data means whether the data is complete regarding every parameter you require from a record. For example, in a dataset with one record and 5 parameters required, the record only has data for 3 parameters, this will be an incomplete dataset because it's missing 40% of data! 

Comparing row completeness formula with column completeness formula, I think they are not in a relationship that one is better than the other. The reason behind this is that it really depends on the situation. For instance, if I only need `Time` column to analyse the total vehicle volume, in this case, any other column would appear to be not important at all ! The column completeness of `Time`column would have a better assessment of the data in this way. 

On top of that, it's always good to use both formulas at the same time to evaluate the completeness of a dataset.



# Task 7.2 (in Excel)
## Step 1

Open site 1083 csv file, change the format of column A into `dddd yyyy/m/d hh:mm:ss`add a new column named `weekday`, use `WEEKDAY`function to mark each record with a weekday code. (1 for Sunday, 6 for Friday, shown in graph 3.8)

![image-20211019084145511](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019084145511.png)

<center>Graph 3.8 - Mark weekdays for records</center>

## Step 2

Use ![image-20211019084939087](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019084939087.png)to keep records for <u>Fridays</u> and <u>North lanes</u>, and save the result as a new file `1083-1.csv`. (As shown in graph 3.9)

![image-20211019162238237](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019162238237.png)

<center>Graph 3.9 - 1083-1.csv</center>

## Step 3

Repeat step 1&2 for site 1415's records, and save the result into a new file `1415-1.csv`. (Choose direction as northeast. As shown in graph 3.10)

![image-20211019170622317](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019170622317.png)

<center>Graph 3.10 - 1415-1.csv</center>

## Step 3

In Excel, process both `1083-1.csv`and`1415-1.csv`, add a column name 17to18, to mark those records within this time period with "1". Then use the ![image-20211019233753962](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019233753962.png)to keep records between 17:00 to 18:00, and save the result into `1083-1-17to18.csv`and `1415-1-17to18.csv` . (As shown in graph 3.11, 3.12 and 3.13)

```
=COUNTIFS(A2,">=2018/2/2  17:00:00",A2,"<2018/2/2  18:00:00")+COUNTIFS(A2,">=2018/2/9  17:00:00",A2,"<2018/2/9  18:00:00")+COUNTIFS(A2,">=2018/2/16  17:00:00",A2,"<2018/2/16  18:00:00")+COUNTIFS(A2,">=2018/2/23  17:00:00",A2,"<2018/2/23  18:00:00")
```

![image-20211019233857597](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019233857597.png)

<center>Graph 3.11 - Add column 17to18 and mark each record</center>

![image-20211019234348532](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019234348532.png)

<center>Graph 3.12 - 1083-1-17to18.csv</center>

![image-20211019234413438](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019234413438.png)

<center>Graph 3.13 - 1415-1-17to18.csv</center>

## Step 4 (Final & Analysis)

By far we've successfully kept records between 17:00 to 18:00 on Fridays with only the North direction lanes. Now we need to calculate the hourly average vehicle speed for each lane on two sites. There are 5 lanes in total: NB_NS, NB_MID, NB_OS, NE_NS, NE_OS. Use![image-20211019233753962](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019233753962.png) to filter out each lane separately, and count the average speed. With just selecting the whole column, the average value will appear at the bottom of excel GUI. (1mph = 1.609344kmh, As shown in graph 3.14, and table 3.1)

![image-20211019234931377](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211019234931377.png)

<center>Graph 3.14 - Calculating average travel time</center>



| lane                | average speed (kmh, rounded to 2 decimals) |
| ------------------- | ------------------------------------------ |
| 1083-1              | 40.06                                      |
| 1083-2              | 46.32                                      |
| 1083-3              | 48.53                                      |
| 1415-1              | 38.78                                      |
| 1415-2              | 43.71                                      |
| Total_Average_Speed | 43.48                                      |

<center>Table 3.1 - Average receipt</center>

So the traveling time is: 

<center><p style='font-size:20px;font-style:bold'>
  Distance * 60 / Total_Average_Speed = </p>
  <p style='font-size:20px;font-style:bold'>
  4.68km * 60 / 43.48kmh ≈ 6.71 min 
  </p>
  <center>

Interpretation of results:

>  **The typical Friday journey time** for the road fragment between site 1083 and site 1415, between 17:00 and 18:00, using only the North direction lanes, **is around 6.71 minutes**.

### Comparison between using Python and Excel (on task 6)

1. Advantages and disadvantages

With Python, the biggest drawback is that I have to open the output file from time to time to check whether the output stream is correct, and then I need a draft of the programming to make it  work. The strength of Python is that it has a perfect data manipulation because it programs from the data itself, in a way it is super quick especially for calculating sum value under sophisticated conditions.

With Excel, the biggest problem is that it becomes too complicated when you want to filter records with complex requirements. For example, I want to filter out records between 17:00 and 18:00 with lanes in north direction. It may take several steps to achieve this in Excel while it only takes 2 or 3 lines of code in Python. The good thing about Excel is that operations are reallly instinctive, and the result can be seen at once because it has an integrated GUI.

2. Extra work or limitations & time costs

Frankly speaking, to perform tasks like task 6, using Excel will take less time. However, if the dataset is going to be any larger, Excel may fail or perform rather slow due to hardware limitations (especially for RAM memory size). Instead, Python is much more effective dealing with a massive dataset. But using Python is no doubt taking extra work than using Excel in the majority of occassions. For example, in the "count average speed" step, in Excel it's just about cliking the column, and the average value appears right away. Nevertheless, it takes python tens of lines of code to accomplish.

On top of that, I would prefer to use them together to perform a task. To use Excel for basic filtering and counting, and use Python for complex algorithms.
