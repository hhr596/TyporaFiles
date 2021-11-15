# Tuple Relational Calculus





# Relational Algebra

# 重点与难点

> - 关系代数基本操作：并、差、积、选择、投影、（更名）
> - 关系代数扩展操作：交、![\theta](https://ewr1.vultrobjects.com/imgur2/000/005/605/864_81c_f01.gif)-连接、自然连接
> - 关系代数复杂扩展操作：除、外连接
> - 书写关系代数的基本思维训练：“一个集合，施加一个操作得到一个集合，依次施加关系代数操作，进而得到所需结果” “以集合为中心”

## 一、什么是关系代数

> - 关系代数运算的特点
>
>    
>
>   - 基于集合提供了一系列的关系代数操作，是一种集合思维的操作语言
>   - 关系代数操作以一个或多个关系为输入，结果是一个新的关系
>   - 用对关系的运算来表达查询，需要指明所用操作，具有一定的过程性
>   - 是一种抽象的语言，是学习其他数据库语言，如SQL等的基础
>
>  
>
> - 关系代数操作：集合操作和纯关系操作
>
>    
>
>   - 集合操作：并、交、差、笛卡尔积
>   - 纯关系操作：投影、选择、连接、除 

## 二、并相容性的概念

> - 参与运算的两个关系及其相关属性之间有一定的对应性、可比性或意义关联性
>
> - 定义：关系R和关系S存在相容性，当且仅当：
>
>    
>
>   - 关系R和关系S的属性数目必须相同
>   - 对于任意i，关系R的第i个属性的域必须和关系S的第i个属性的域相同

## 三、并（Union）操作

> - 定义：假设关系R和关系S是并相容的，则关系R与关系S的并运算结果也是一个关系，记做：![R \cup S](http://static.noobyard.com/static/loading.gif)，它由或者出现在关系R中，或者出现在S中的元组构成
> - 数学表述：![R \cup S = \{t | t \in R \vee t \in S \}](http://static.noobyard.com/static/loading.gif)，其中t是元组
> - 并运算是将两个关系的元组合并成一个关系，在合并时去掉重复的元组
> - ![img](http://static.noobyard.com/static/loading.gif)

## 四、差（Difference）操作

> - 定义：假设关系R和关系S是并相容的，则关系R与关系S的并运算结果也是一个关系，记做：![R - S](https://ewr1.vultrobjects.com/imgur3/000/009/816/393_70d_990.gif)，它由出现在关系R中但不出现在S中的元组构成
> - 数学表述：![R - S = \{t | t \in R \wedge t \notin S \}](https://ewr1.vultrobjects.com/imgur3/000/009/816/394_8b8_467.gif)，其中t是元组
> - ![img](https://ewr1.vultrobjects.com/imgur3/000/009/816/395_954_b25.png)

## 五、广义笛卡尔积（Cartesian Product）操作

> - 定义：关系R![(<a_{1},a_{2},...,a_{n} >)](https://ewr1.vultrobjects.com/imgur3/000/009/816/396_66f_823.gif)与关系S![(<b_{1},b_{2},...,b_{m} >)](https://ewr1.vultrobjects.com/imgur3/000/009/816/397_878_98f.gif)的广义笛卡尔积（简称广义积或笛卡尔积）运算结果也是一个关系，记做：![R \times S](https://ewr1.vultrobjects.com/imgur3/000/009/816/398_32e_62d.gif)，它由关系R中的元组与关系S的元组进行所有可能的凭借（或串接）构成。
> - 数学描述：![R \times S = \{<a_{1}, a_{2},...,a_{n},b_{1}, b_{2},...,b_{m}> |\\ <a_{1}, a_{2},...,a_{n}> \ \in R \ \wedge <b_{1}, b_{2},...,b_{m}> \ \in S\}](https://ewr1.vultrobjects.com/imgur3/000/009/816/399_d3d_dfd.gif)
> - ![R \times S = S \times R](https://ewr1.vultrobjects.com/imgur3/000/009/816/400_77e_85a.gif)（行位置无关性和列位置无关性）
> - R是n度关系，S是m度关系，![R \times S](https://ewr1.vultrobjects.com/imgur3/000/009/816/398_32e_62d.gif)是![n+m](https://ewr1.vultrobjects.com/imgur3/000/009/816/401_666_624.gif)度关系
> - R基数是x，S基数是y，![R \times S](https://ewr1.vultrobjects.com/imgur3/000/009/816/398_32e_62d.gif)基数是![x \times y](https://ewr1.vultrobjects.com/imgur3/000/009/816/402_91b_762.gif)
> - ![img](https://ewr1.vultrobjects.com/imgur3/000/009/816/403_455_0d8.png)

## 六、选择（Select）操作

> - 定义：给定一个关系R，同时给定一个选择的条件condition（简记con），选择运算结果也是一个关系，记做![\sigma_{con}(R)](https://ewr1.vultrobjects.com/imgur3/000/009/816/404_778_ed1.gif)，它从关系R中选择出满足给定条件condition的元组构成。
>
> - 数学描述：
>
>   
>
>   - 设![R(A_{1},A_{2},...,A_{n})](https://ewr1.vultrobjects.com/imgur3/000/009/816/406_30b_24c.gif)，t是R的元组，t的分量记做![t[A_{i}]](https://ewr1.vultrobjects.com/imgur3/000/009/816/407_548_df4.gif)，或简写为![A_{i}](https://ewr1.vultrobjects.com/imgur2/000/008/002/600_275_5fd.gif)
>   - 条件con由逻辑运算符连接比较表达式组成
>   - 逻辑运算符：![\wedge](https://ewr1.vultrobjects.com/imgur3/000/009/816/408_8f2_c44.gif)，![\vee](https://ewr1.vultrobjects.com/imgur3/000/009/816/409_73c_d7c.gif)，![\lnot](https://ewr1.vultrobjects.com/imgur3/000/009/816/410_005_e63.gif)或谢伟and，or，not
>   - 比较表达式：![X \theta Y](https://ewr1.vultrobjects.com/imgur3/000/009/816/411_aa5_208.gif)，其中X，Y是t的分量、常量或简单函数，![\theta](https://ewr1.vultrobjects.com/imgur2/000/005/605/864_81c_f01.gif)是比较运算符，![\theta \in \{ >, \ge,<,\le,=,\ne\}](https://ewr1.vultrobjects.com/imgur3/000/009/816/412_b6b_06e.gif)
>
> - ![img](https://ewr1.vultrobjects.com/imgur3/000/009/816/413_3e6_68c.png)

## 七、投影（Project）操作

> - 定义：给定一个关系R，投影运算结果也是一个关系，记做![\Pi_{A}(R)](https://ewr1.vultrobjects.com/imgur3/000/009/816/414_5c3_555.gif)，它从关系R中选出属性包含在A中的列构成。
>
> - 数学描述：
>
>   
>
>   - 设![R(A_{1},A_{2},...,A_{n})](https://ewr1.vultrobjects.com/imgur3/000/009/816/406_30b_24c.gif)
>   - ![\{{A_{i1},A_{i2},...,A_{ik} \} \subseteq \{{A_{1},A_{2},...,A_{n} \}](https://ewr1.vultrobjects.com/imgur3/000/009/816/416_b71_2bf.gif)
>   - ![t[A_{i1}]](https://ewr1.vultrobjects.com/imgur3/000/009/816/417_d94_d6e.gif)表示元组t中相应于属性![A_{i}](https://ewr1.vultrobjects.com/imgur2/000/008/002/600_275_5fd.gif)的分量
>   - 投影运算可以对原关系的列在投影后重新排列
>
> - ![img](https://ewr1.vultrobjects.com/imgur3/000/009/816/418_e54_256.png)![img](https://ewr1.vultrobjects.com/imgur3/000/009/816/419_924_9a4.png)

## 八、交（Intersection）操作

> - 定义：假设关系R和关系S是并相容的，则关系R与关系S的交运算结果也是一个关系，记做：![R \cap S](https://ewr1.vultrobjects.com/imgur3/000/009/816/420_434_fe7.gif)，它由同时出现在关系R和关系S中的元组构成。
> - 数学描述：![R \cap S=\{t\ |\ t \in R \wedge t \in S\}](https://ewr1.vultrobjects.com/imgur3/000/009/816/421_7c5_097.gif)，其中t是元组
> - ![R \cap S = R - (R - S) = S - (S - R)](http://static.noobyard.com/static/loading.gif)
> - ![img](http://static.noobyard.com/static/loading.gif)

## 九、theta连接（![\theta](http://static.noobyard.com/static/loading.gif)-Join,theta-Join）操作及更名操作

> - 定义：给定关系R和关系S，R和S的![\theta](http://static.noobyard.com/static/loading.gif)连接运算结果也是一个关系，记做![img](http://static.noobyard.com/static/loading.gif)，它由关系R和关系S的笛卡尔积中，选取R中属性A与S中属性B之间满足![\theta](http://static.noobyard.com/static/loading.gif)条件的元组构成。
> - 数学描述：![img](http://static.noobyard.com/static/loading.gif)
> - ![img](http://static.noobyard.com/static/loading.gif)
> - ![img](http://static.noobyard.com/static/loading.gif)

> - 等值连接（Equi-Join）
> - 当![\theta](http://static.noobyard.com/static/loading.gif)-连接中运算符为“=”时，就是等值连接。
> - 数学描述：![img](http://static.noobyard.com/static/loading.gif)

## 十、自然连接（Natural-Join）操作

> - 定义：给定关系R和关系S，R和S的自然连接运算结果也是一个关系，记做![img](http://static.noobyard.com/static/loading.gif)，它由关系R和关系S的笛卡尔积中选取相同属性组B上值相等的元组构成。
>
> - 数学描述：
>
>   
>
>   - 自然连接是一种特殊的等值连接
>   - 要求关系R和关系S必须有相同的属性组B
>   - R，S属性相同，值必须相等才能连接
>   - 要在结果中去掉重复的属性列
>
> - ![img](http://static.noobyard.com/static/loading.gif)
>
> - ![img](http://static.noobyard.com/static/loading.gif)

## 十一、除（Division）操作

> - 除法运算经常用于求解“查询... 全部的/所有的...”问题
>
> - 前提条件：给定关系![R(A_{1},A_{2},...,A_{n})](http://static.noobyard.com/static/loading.gif)为n度关系，关系![S(B_{1},B_{2},...,B_{m})](http://static.noobyard.com/static/loading.gif)为m度关系。如果可以进行关系R与关系S的除运算，当且仅当：属性集![\{B_{1},B_{2},...,B_{m}\}](http://static.noobyard.com/static/loading.gif)是属性集![\{A_{1},A_{2},...,A_{n}\}](http://static.noobyard.com/static/loading.gif)的真子集，即![m < n](http://static.noobyard.com/static/loading.gif)
>
> - 定义：关系R和关系S的除运算结果也是一个关系，记做
>
>   
>
>   ，分两部分来定义：
>
>    
>
>   - 设属性集![\{C_{1},C_{2},...,C_{k}\} = \{A_{1},A_{2},...,A_{n}\} - \{B_{1},B_{2},...,B_{m}\}](http://static.noobyard.com/static/loading.gif)，则有k=n-m，则![R \div S](http://static.noobyard.com/static/loading.gif)结果关系是k度（n-m度）关系，由![\{C_{1},C_{2},...,C_{k}\}](http://static.noobyard.com/static/loading.gif)属性构成
>   - 再设关系![R(<a_{1},...,a_{n}>)](http://static.noobyard.com/static/loading.gif)和关系![S(<b_{1},...,b_{m}>)](http://static.noobyard.com/static/loading.gif)组合形成的一个新元组都是R中的某一个元组![<a_{1},...,a_{n}>](http://static.noobyard.com/static/loading.gif)
>
> - 数学描述：![R \div S = \{ t \ | \ t \in \Pi_{R-S} \wedge \forall u \in S \ (tu \in R) \} \\ =\Pi_{R-S}(R)-\Pi_{R-S}((\Pi_{R-S}(R) \times S)-R)](http://static.noobyard.com/static/loading.gif)
>
> - ![img](http://static.noobyard.com/static/loading.gif)
>
> - ![img](https://ewr1.vultrobjects.com/imgur3/000/009/816/445_407_ffe.png)
>
> - ![img](https://ewr1.vultrobjects.com/imgur3/000/009/816/446_84f_600.png)

## 十二、外连接（Outer-Join）操作

> - 定义：两个关系R与S进行连接时，如果关系R（或S）中的元组在S（或R）中找不到相匹配的元组，则为了避免该元组信息丢失，从而将该元组与S（或R）中假定存在的全为空值的元组形成连接，放置在结果关系中，这种连接称之为外连接。
>
> - 外连接 = 自然连接（![、theta](https://ewr1.vultrobjects.com/imgur3/000/009/816/447_d1d_3d6.gif)或![\theta](https://ewr1.vultrobjects.com/imgur2/000/005/605/864_81c_f01.gif)连接） + 失配的元组（与全空元组形成的连接）
>
> - 外连接的形式：左外连接、右外连接、全外连接
>
>    
>
>   - 左外连接 = 自然连接（![、theta](https://ewr1.vultrobjects.com/imgur3/000/009/816/447_d1d_3d6.gif)或![\theta](https://ewr1.vultrobjects.com/imgur2/000/005/605/864_81c_f01.gif)连接） + 左侧表中失配的元组
>   - 右外连接 = 自然连接（![、theta](https://ewr1.vultrobjects.com/imgur3/000/009/816/447_d1d_3d6.gif)或![\theta](https://ewr1.vultrobjects.com/imgur2/000/005/605/864_81c_f01.gif)连接） + 右侧表中失配的元组
>   - 全外连接 = 自然连接（![、theta](https://ewr1.vultrobjects.com/imgur3/000/009/816/447_d1d_3d6.gif)或![\theta](https://ewr1.vultrobjects.com/imgur2/000/005/605/864_81c_f01.gif)连接） + 两侧表中失配的元组
>
> - ![img](https://ewr1.vultrobjects.com/imgur3/000/009/816/448_aaa_081.png)
>
> - ![img](https://ewr1.vultrobjects.com/imgur3/000/009/816/449_725_efc.png)
>
> - ![img](https://ewr1.vultrobjects.com/imgur3/000/009/816/450_a75_c05.png)
>
> - ![img](https://ewr1.vultrobjects.com/imgur3/000/009/816/451_a3b_3a0.png)
>
> - ![img](https://ewr1.vultrobjects.com/imgur3/000/009/816/452_159_d75.png)

