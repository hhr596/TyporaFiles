三对query怎么写

> 第一对：用index和不用index



```sqlite
sqlite3 -init sqliterc mondial.db
--terminal里面设置初始数据库
.eqp on
可以看到具体执行plan
```



# 番茄0

### 你需要干的事情：了解Qow Lab大概内容

1. 要干什么，有什么是给的

> 有两个 Tastk， 1和2
>
> Task1：写三对SQL语句（mondial DB)
>
> 要求：每对SQL语句中有两句，两句的写法不同，结果相同。其中一句是要体现优化了的SQL查询. **或者**，两个query写法相同，但是运行环境不同（例如，控制是否access an index）
>
> Task2：总结Task1做的实验，用一个图表。转述结果以及添加评论村 
>
> 

2. 要看什么资料，需要具备什么知识才能做

> 1. on running experiments & on plotting, interpreting and commenting 
>
> 2. 学习SQLite DBMS 运用的optimization：https://www.sqlite.org/docs.html
>
> 3. 特别学习这个部分：https://www.sqlite.org/optoverview.html
>
> 4. 这个部分详细学习：https://www.sqlite.org/queryplanner-ng.html
>
>    （以上学习的内容超过了本实验需要的深度）
>
>    

3. 有哪些要注意的地方

> 1. 每对pair着重点要不一样
> 2. 每对pair是一个能被优化执行，一个不能被优化执行
> 3. query结果的时间要输出到log

4. 实验考察的内容是什么，得分点是什么

> 1. 着重考察的是对sqlite optimizer和evaluator的控制
> 2. 优化达到10%以上是优秀的优化，5-10%勉强可用，不要使用5%以下的优化
> 3. 有你的阐述显示你学过了SQLite optimizer
> 4. 表述了pair之间的差异
> 5. 表述自己明白的query optimizer的重要性

**when it performs better, when it performs less well**

# 番茄1

完善番茄0的内容 + 老师给的指示

1. 老师给的指示

> 第一对pair
>
> 1. 知道optimizer什么时候能用index什么时候不能用（使用/不使用index对数据量的吞吐有没有影响）
> 2. 需要自己创建index，然后drop index再运行一次
> 3. （这是一种情况，语句相同，使用不同index）
>
> 例如：
>
> WHERE语句被用特殊的方式书写的时候，他就不能使用index（document里面有写，需要去study）

> 第二对pair
>
> 1. 改变谓词p的顺序
> 2. 谓词p的顺序会影响optimizer是否可以进行优化

> 第三对pair
>
> 1. 对join ordering  strategy的控制
> 2. 在query能通过reorder优化的时候，使用cross join，迫使他不进行优化。
> 3. 但是这种做法不是对所有的query都有效（建议触发方式：让join之间的尺寸的差异尽可能的大）

老师给的帮助

> 使用 .eqp on 展示执行过程中的query plan

```sqlite
./loadandrunsqlitescript.sh mondial20.db TestScript.sql TimeScript.output TimeScript.log
```

快速运行query多次的方法：

用`AFewRuns.sh`把语句都放在里面

```sqlite
./AFewRuns.sh
```

运行就可以 了

**上传的文件**

可以把sql文件和对应的log还有output一起打包成zip，另外就是答案写进一个pdf.



# 番茄2

看SQLite Query Optimizer Overview

1. 每个部分都讲了什么？

2. 有没有提到index的东西？

### 1. introduction

整篇文章讲的是query planner 和query optimizer 的工作原理

**query planner 的作用是**： 选择算法实现query，使得`disk I/O and CPU`成本最小

#### query planning 的背景文档

> https://www.sqlite.org/queryplanner.html

SQL是declarative language, 不是procedural language.

`query planner` 选择最优算法实现SQL语句

**query planner 需要和indices协作**

> These indices must normally be added by programmers.

#### 所以query planning到底是怎么工作的？

1. searching
2. sorting
3. searchign and sorting at the same time
4. without ROWID tables

#### 1. Searching

> **什么是 'rowid'?**
>
> Except for [WITHOUT ROWID](https://www.sqlite.org/withoutrowid.html) tables, all rows within SQLite tables have a 64-bit signed integer key that uniquely identifies the row within its table. This integer is usually called the "rowid". The rowid value can be accessed using one of the special case-independent names "rowid", "oid", or "_rowid_" in place of a column name. If a table contains a user defined column named "rowid", "oid" or "_rowid_", then that name always refers the explicitly declared column and cannot be used to retrieve the integer rowid value.
>
> quick-read：SQLite有内置的64位的整型key来定位每条记录，这个整型integer就是rowid。可用`rowid`访问。如果用户设置了一列名字也叫rowid，那就会抢占名字。

![figure 1](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111280840944.gif)

> **什么是 *full table scan*？**
>
> 例如语句
>
> ```sqlite
> SELECT price FROM fruitsforsale WHERE fruit='Peach';
> ```
>
> 在没有index的table里面， 搜索会逐行进行。遍历整个table。
>
> O(N)

> **如何避免full table scan？**
>
> 采用`lookups by rowid`
>
> O(logN)
>
> ```sqlite
> SELECT price FROM fruitsforsale WHERE rowid=4;
> ```
>
> 通过id直接选中那一行？还是那一行作为开始？（有integer型的primary key的话也可以用primary key）

> **Lookup by index**
>
> 1. 对某一行添加index
>
> ```sqlite
> CREATE INDEX Idx1 ON fruitsforsale(fruit);
> ```
>
> ![figure 4](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111280847300.gif)
>
> 2. 然后再search
>
> ```sqlite
> SELECT price FROM fruitsforsale WHERE fruit='Peach';
> ```
>
> 原理：
>
> 通过先生成一个index和这列的表，这个表会把fruit列进行排序，这样就可以进行一个`binary search`，找到Peach对应的rowid，再去原表，因为rowid列也是按序排好的，所以又可以`binary search`找到对应的行，提取price。
>
> ![figure 5](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111280849188.gif)

> **如何处理返回结果是多行的情况？**
>
> 先从第一个开始，通过rowid去提取原表中的信息；再在index表中到下一个，再获得对应rowid去原表提取信息。
>
> 所以对于一个有两行结果的search来讲，cost是3次binary search。
>
> ![figure 6](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111280926139.gif)
>
> O((K+1)*LogN)

> **如何处理多个条件的AND语句？**
>
> 1. 不怎么efficient的方法：
>
> ![](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111280928652.gif)
>
> 先通过第一个条件找到对应的row，再逐行判断第二个条件
>
> ```sqlite
> SELECT price FROM fruitsforsale WHERE fruit='Orange' AND state='CA'
> ```
>
> 2. 给第二个条件设置一个index
>
> ```sqlite
> CREATE INDEX Idx2 ON fruitsforsale(state);
> ```
>
> 让sqlite使用这个index，其实效果和上面差不多。
>
> 如果在执行前运行了`ANALYZE`，那么sqlite就会自动选择最优的index表（这里是index1，因为表小，没必要再开个index2，这样反而会增加分析一列）。但如果没有运行`ANALYZE`的话，就是随机选的
>
> 3. 同时设置多行的index，如下。（more efficient）

> **多列一起建立index表**
>
> ![figure 1](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111280938099.gif)
>
> ```sqlite
> CREATE INDEX Idx3 ON FruitsForSale(fruit, state);
> ```
>
> 注意点：
>
> 1. 最左边的列作为排序的第一标准
> 2. 后面的列依次作为，前面列出现相同元素后，怎么排的依据

### 总结使用index：

1. where后面几个条件就用几个元素一起创建一个index表
2. 只需要一张index表是最好的
3. 原理就是用binary search代替full table search

> **更厉害的：Covering indices**
>
> ![figure 13](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111280944602.gif)
>
> ```sqlite
> CREATE INDEX Idx4 ON FruitsForSale(fruit, state, price);
> ```
>
> 把所有需要的列都一起建立一张index表。
>
> 所以叫"covering indices"，把所有的都cover了
>
> > Because all of the information needed is in the covering index, SQLite never needs to consult the original table in order to find the price.
>
> 这样可以直接避免访问原表。（相当于是精简了原表）

> **原始应对OR的办法：OR-by-UNION**
>
> ```sqlite
> SELECT price FROM FruitsForSale WHERE fruit='Orange' OR state='CA';
> ```
>
> SQLite 通常的处理方式：
>
> 1. 分别处理每个OR条件，建立他们的index表，找到对应的rowid
> 2. 让后把这些rowid UNION一下，再去源表调出行
>
> ![figure 15](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111280950492.gif)
>
> **注意：先UNION rowid，再去表里lookup**
>
> 结论：建议多用用AND，可以将 OR 改成 AND-by-INTERSECT

#### 2. Searching

`order by`指令也可以通过index来加速

> **一般sort需要多久？**
>
> ```sqlite
> SELECT * FROM fruitsforsale ORDER BY fruit;
> ```
>
> ![figure 16](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111280956735.gif)
>
> 假设有K行结果，那么**O(KlogK）**
>
> 同时还会占用大量的内存

> **使用ROWID来加速？**
>
> ```sqlite
> SELECT * FROM fruitsforsale ORDER BY rowid;
> ```
>
> ![figure 17](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111280958252.gif)
>
> 结果的顺序可能会有点奇怪。
>
> 有没有用？感觉没有什么效果，因为rowid一般就是按顺序排好的，根本不需要重新sort。不过用在把整个表倒过来输出的时候很好。

> **使用Index来加速？**
>
> ![figure 18](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111281001472.gif)
>
> 解决的第一个问题：sort的话直接从头读到尾，
>
> 解决的第二个问题：在原表可以用bianry search加速了。一条一条找到每条对应的行。
>
> 但是新的问题：这里的时间复杂度还是O(NlogN)，**完全没有变化！**
>
> 但是通常情况下，query planner会选择用index，因为index不需要将整张表load进memory，速度差不多，但是节省空间。

> **最好的办法：Covering index！**
>
> ![figure 19](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202111281005242.gif)
>
> O(N)
>
> 只需要根据index表从头到尾读就可以了，还不需要将整表load进内存！省时省空间！

#### 3. Searching And Sorting At The Same Time

如何让searching + sorting整体的时间最短

1. 用 multi-column index
2. 用 covering index



# 番茄3

看The SQLite Query Optimizer Overview

每个部分主要讲了什么？哪些是有用的

1. introduction

