### 递归
(递归和迭代的关系)

函数直接或间接调用自己的编程技术

#### 尾递归

递归调用函数的最后返回值是它自己

> 尾递归的优点：没有后续的处理，每次递归覆盖当前栈帧，无需新添加，从而节约内存，效率更高