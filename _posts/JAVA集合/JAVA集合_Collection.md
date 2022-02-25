# Collection

整体框架

![img1](../photos/Collection框架图.png)

## Set

### TreeSet

### HashSet

**注意事项**

1. HashSet的底层是HashMap。
   ![](image/JAVA集合_Collection/1637134723507.png)
2. HashSet可以存放null值，但是只能有一个null值。
3. HashSet存储的元素不是有序的。

## List

### LinkedList

1. 底层实现的是双向链表和双端队列的特点
2. 线程不安全
3. LinkedList元素允许为null，允许重复元素

### Vector

### ArrayList

**注意事项**

1. ArrayList可以加入null元素。
2. ArrayList底层是数组实现的。
3. ArrayList是线程不安全的，可以看到源码中的方法是没有Sycnchronized关键字的。![img](image/JAVA集合_Collection/1637129139511.png)

**源码分析**

1. ArrayList中维护了一个Object类型的数组，elementData。transient关键字表示瞬间的、短暂的，表示该属性不会被序列化。
   ![img](./image/JAVA集合_Collection/1637130163122.png)
2. 创建ArrayList的两种方式
   ![img](./image/JAVA集合_Collection/1637130734203.png)![img](image/JAVA集合_Collection/1637130892334.png)
   一种是无参的构建方式，直接创建一个为空的数组，带一个int的构建方式会创建一个相应大小的数组。
3. 扩容方式
   如果采用的是无参构造方式，初始大小为0，第一次添加数据扩容为10，下一次再扩容为原来大小的1.5倍
   如果采用的有参构造方式，初始化大小为传入参数大小，下一次扩容为原来的1.5倍

### LinkedList和ArrayList的区别

1. ArrayList基于动态数组实现的非线程安全的集合；LinkedList基于链表实现的非线程安全的集合。
2. 对于随机index访问的get和set方法，一般ArrayList的速度要优于LinkedList。因为ArrayList直接通过数组下标直接找到元素；LinkedList要移动指针遍历每个元素直到找到为止。
3. 新增和删除元素，一般LinkedList的速度要优于ArrayList。因为ArrayList在新增和删除元素时，可能影响数组内的其他数据的下标，扩容和复制数组；LinkedList实例化对象需要时间外，只需要修改指针即可。
4. LinkedList集合不支持 高效的随机随机访问（RandomAccess）
5. 内存空间占用：LinkedList 比 ArrayList 更占内存，因为 LinkedList的节点除了存储数据，还存储了两个引用，一个指向前一个元素，一个指向后一个元素

综合来说，在需要频繁读取集合中的元素时，更推荐使用 ArrayList，而在插入和删除操作较多时，更推荐使用 LinkedList
