> https://developer.aliyun.com/article/779151

扔掉inde

```sqlite
drop index Idx1;
```

> The *optimizer cannot use* an *index* on the converted column



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



修改operator的参数获得最suitable的query

连续运行多次，看看运行时间是不是稳定的。

最终结果取平均值、最小或者。。。。

```
#在shell里写多条命令
#然后运行shell直接全部运行
./dfdf.sh
```



> https://www.tutorialspoint.com/sqlite/sqlite_commands.htm

The above is a link to SQLite commands, including those for timing (.timer).  You can use these as an alternative to the operating system for timing queries.



Run the 20times script to get a bigger database.

> Script from Norman

```sql

Hi,

Following on from the lab yesterday, here is a little more information on scripting to obtain times executing query plans:

To run specific tasks and capture the results, you can use loadandrunsqlitescript.sh.  Here is an example, which runs the task in TestScript.sql over the mondial10.db database, appending the time that it took to Timescript.log:

./loadandrunsqlitescript.sh mondial10.db TestScript.sql TimeScript.output TimeScript.log

After two runs of the above command, TimeScript.log will contain something like:

Thu 18 Nov 2021 09:42:20 GMT
Normans-iMac.local mondial10.db TestScript.sql TimeScript.output

real    0m0.899s
user    0m0.002s
sys     0m0.006s
Thu 18 Nov 2021 09:42:56 GMT
Normans-iMac.local mondial10.db TestScript.sql TimeScript.output

real    0m0.009s
user    0m0.002s
sys     0m0.003s

So, it has captured which task was run, over which database, and how long it took.  As such, the queries for the lab can be written in files like TestScript.sql, and a single script file can be created containing multiple runs of loadandrunsqlitescript.sh to execute all the runs for the lab.  Interestingly, the second run is much faster than the first, potentially as a result of the fact that the first run was 'cold'.

Hope this helps with colelcting the times, so that you can concentrate your efforts on identifying suitable queries and analysing their execution.

Regards, Norman
```

