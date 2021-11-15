## XSD

The schema of shcema, XML Schema Definition.

## XML Schema' Schema

RelaxNG Schema is a shema language for XML.

![image-20211022204529403](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211022204529403.png)

![image-20211022204929984](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211022204929984.png)

### XSD Schema

1. 一种元素element和类型type只能被声明一次

2. \<xs:annotation\>...\</xs:annotation\>: make comments, 需要放在first child
3. 支持导入重用: xs:import, xs:include, xs:redefine

### XSD datatype definition

![image-20211022205814680](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211022205814680.png)

lexical space: alternatives, e.g. use 1 for true, 0 for false.

surjective:满射的.  injective:单射的.

### XSD types

![image-20211022210648382](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211022210648382.png)

可以不给名字

![image-20211022210834386](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211022210834386.png)

<center>第一个结果只是一个数，第二个内容比较多</center>

![image-20211022211055138](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211022211055138.png)

也可以给名字，但一般不建议，因为要改的时候，全部要改掉

#### 限制string的长度和格式

![image-20211022211152988](/Users/tablee/Library/Application%20Support/typora-user-images/image-20211022211152988.png)

\<xs:restriction\>

simple types is for element that don't have element child and they don't have element attributes. 有属性attribute或者内容content的就是complex type





























