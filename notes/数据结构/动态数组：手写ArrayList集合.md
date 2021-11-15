## 动态数组：手写ArrayList集合



### 数组

**数组**是一种**顺序存储**的线性表，所有元素的内存地址都是连续的。

`int[] array = new int[]{11,22,33};`

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210719213016.png" alt="image-20210719213016678" style="zoom:50%;" />

**缺点：**容量固定，无法动态修改数组容量

解决方法：实现一个可以动态扩容的动态数组。

### 手写ArrayList集合

#### 功能设计

```java
int size();  //元素的数量
boolean  isEmpty();  //判断是否为空
boolean  contains(E element);  // 是否含某个元素
void  add(E element);  //添加元素到末尾
E get(int index);  //返回index位置对应的元素
E set(int index,E element);  //设置index位置的元素
void add(int index,E element);  //往index位置添加元素
E remove(int index);  //删除index位置对应的元素
int indexOf(E element);  //查看元素的位置(索引)
void clear();  // 清除所有元素
```

#### 主要功能分析

```java
/**
 * @author panqiyi
 * @date 2021/7/19 - 22:02
 */
public class ArrayList<E> {
    //元素数量
    private int size;
    //初始化数组
    private E[] elements;

    //默认数组初始容量
    private static final int DEFAULT_CAPACITY = 10;
    //遍历找不到元素，返回-1
    private static final int ELEMENT_NOt_FOUND = -1;

    public ArrayList(int capaticy){
        //自定义初始容量 < 默认时用默认容量，大于默认时用自定义初始容量
        capaticy = (capaticy<DEFAULT_CAPACITY)?DEFAULT_CAPACITY:capaticy;
        elements = (E[]) new Object[capaticy];
    }
    public ArrayList(){
        //调用有参构造方法
        this(DEFAULT_CAPACITY);
    }
}
```



##### 添加add(int index,E element)

往对应index位置添加元素

![image-20210720144417030](https://gitee.com/panqiyi/pqimg/raw/master/20210720144417.png)

```java
//核心代码
 //移动： 移动区域：index到size-1 元素整体向后移动一位，注意必须是从后面开始移动，否则会覆盖
        for (int i = size-1; i > index; i--) {
            elements[i+1]=elements[i];
        }
        //给空出来的index位置赋值
        elements[index] = element;
        size++;
```

##### 删除remove(int index)

删除对应位置的元素，并返回元素

![image-20210720145612176](https://gitee.com/panqiyi/pqimg/raw/master/20210720145612.png)

```java
//核心代码
 //元素的移动： 删除的元素索引index，需要将 index+1 到 size-1 的元素全部向前移动一个位置
        for (int i = index+1; i < size-1 ; i++) {
            elements[i-1] = elements[i];
        }
        size--;
        //返回原来index位置的元素
        return elements[index];
```

内存管理（remove优化）：

<font color="red">注意：动态数组中存储的其实都是对象，如存储int类型也是他的包装类，数组中存储的为对象地址。</font>

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210721085633.png" alt="image-20210721085633690" style="zoom: 67%;" />

移动后：<font color="orange">所谓移动其实就是将后一个元素赋值给前面元素覆盖</font>

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210721090415.png" alt="image-20210721090415408" style="zoom:67%;" />

<font color="red">此时请下拉先看**清除clear()**方法的实现。</font>

当我们使用clear清除时：即将 index=0 ~  index=size-1 的所有元素 等于 NULL；

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210721092243.png" alt="image-20210721092243443" style="zoom:67%;" />

**所以这样的remove后清空并未完全清除**

解决：在原来的基础上将最后一个，index = size 赋值为NULL即可

```Java
/**
     * 删除对应元素并返回
     * @param index
     * @return
     */
    public E remove(int index){
        rangeCheck(index);
        //元素的移动： 删除的元素索引index，需要将 index+1 到 size-1 的元素全部向前移动一个位置
        for (int i = index+1; i < size-1 ; i++) {
            elements[i-1] = elements[i];
        }
       /* size--;
        elements[size] = null;*/
       elements[--size] = null;
        //返回原来index位置的元素
        return elements[index];
    }
```



##### 添加add(E element)

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210720150948.png" alt="image-20210720150948702" style="zoom:80%;" />

```java
/**
 * 添加某元素到末尾
 * @param element
 */
public void add(E element){
    //法一：如：当数组没有元素，在索引0添加，当有3个元素，再添加时就是在索引index=size处添加。0 1 2 3
   /* elements[size] = element;
    size++;*/

   //法二：调用 对应位置添加元素方法add(int index,E element)，当index=size即可
    add(size,element);
}
```

##### 清除clear()

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210720195914.png" alt="image-20210720195914519" style="zoom:80%;" />

<font color="orange">当数组中存储的对象地址变为NULL时，就没有引用指向对象，对象就会被垃圾回收。</font>

<font color="orange">同时数组所有存储的地址变为NULL，就不存在元素了，size = 0; 此时该数组可重复利用。</font>

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210721082907.png" alt="image-20210721082907695" style="zoom:80%;" />

```java
 /**
     * 清除所有元素
     */
    public void clear(){
        for (int i = 0; i < size; i++) {
            elements[i] = null;
        }
        size = 0;
    }
```



##### 动态扩容：

需要扩容的方法：

```java
void  add(E element);  //添加元素到末尾
void add(int index,E element);  //往index位置添加元素
分析：
    因为 add(E element) 方法调用了 add(int index,E element)方法，所以只有 add(int index,E element)方法需要动态扩容
```

动态数组：

![image-20210720130816365](https://gitee.com/panqiyi/pqimg/raw/master/20210720130816.png)

分析：

```
add(int index,E element)方法一次添加一个元素，比如现在 size=4,保证能够添加元素则 数组容量至少为 size+1;
判断是否扩容：如果数组长度>= 数组添加元素至少需要的容量 size+1; 则不需要扩容。否则需要扩容。
扩容：
创建新数组，容量=原数组*1.5; (为了效率，用位运算: 原数组长度+原数组长度>>1)
遍历，将原数组元素赋值到新数组中。
将原数组引用指向新数组。
```

位运算：`arr >> 1 = arr/2^1; arr << 1 = arr*2^1`

```java
/**
 * 往对应位置(索引)添加元素
 * @param index
 * @param element
 */
public void add(int index,E element){
    //判断输入的索引
    //区别：可以=size, 即在末尾可以添加元素
    rangeCheckForAdd(index);

    //数组添加元素需要的最小长度 size+1
    ensureCapacity(size+1);

    //移动： 移动区域：index到size-1 元素整体向后移动一位，注意必须是从后面开始移动，否则会覆盖
    for (int i = size-1; i > index; i--) {
        elements[i+1]=elements[i];
    }
    //给空出来的index位置赋值
    elements[index] = element;
    size++;
}
```

```java
/**
 * 扩容方法
 * @param capacity 添加元素需要的最小容量
 */
public void ensureCapacity(int capacity){
    //判断是否需要扩容
    //原数组长度
    int oldCapacity = elements.length;
    //如果原数组长度 >= 添加元素需要的最小容量 capacity,则不需要扩容
    if (oldCapacity >= capacity) return;

    //扩容
    //新数组容量为旧数组容量的1.5倍
    int newCapacity = oldCapacity+oldCapacity >> 1;
    //新建数组
    E[] newElements = (E[]) new Object[newCapacity];
    //元素赋值到新数组
    for (int i = 0; i < size; i++) {
        newElements[i] = elements[i];
    }
    //引用指向新数组
    elements=newElements;
}
```

测试：

![image-20210720141302851](https://gitee.com/panqiyi/pqimg/raw/master/20210720141302.png)

#### 代码实现

```java
package com.pqy.linear;


/**
 * @author panqiyi
 * @date 2021/7/19 - 22:02
 */
public class ArrayList<E> {

    //元素数量(默认为0)
    private int size;
    //初始化数组
    private E[] elements;

    //默认数组初始容量
    private static final int DEFAULT_CAPACITY = 10;
    //遍历找不到元素，返回-1
    private static final int ELEMENT_NOt_FOUND = -1;

    public ArrayList(int capaticy){
        //自定义初始容量<默认时用默认容量，大于默认时用自定义初始容量
        capaticy = (capaticy<DEFAULT_CAPACITY)?DEFAULT_CAPACITY:capaticy;
        elements = (E[]) new Object[capaticy];
    }
    public ArrayList(){
        //调用有参构造方法
        this(DEFAULT_CAPACITY);
    }

    /**
     * 元素数量
     * @return
     */
    public int size(){
        return size;
    }

    /**
     * 判断是否为空
     * @return
     */
    public boolean isEmpty(){
        //如果size=0则没有元素，为空
        return size==0;
        //相当于
       /* if (size==0){
            return true;
        }else {
            return false;
        }*/
    }

    /**
     * 判断是否包含某元素
     * @param element
     * @return
     */
    public boolean contains(E element){
        return indexOf(element) != DEFAULT_CAPACITY;
    }

    /**
     * 添加某元素到末尾
     * @param element
     */
    public void add(E element){
        //如：当数组没有元素，在索引0添加，当有3个元素，再添加时就是在索引index=size处添加。0 1 2 3
       /* elements[size] = element;
        size++;*/

       //调用 对应位置添加元素方法，当index=size即可
        add(size,element);
    }

    /**
     * 返回对应位置的元素
     * @param index
     * @return
     */
    public E get(int index){
       rangeCheck(index);
        return elements[index];
    }

    /**
     * 设置对应位置的元素，并返回
     * @param index
     * @param element
     * @return
     */
    public E set(int index,E element){
        rangeCheck(index);
        //获取原来位置元素
        E old = elements[index];
        //设置新元素
        elements[index] = element;
        return old;
    }

    /**
     * 往对应位置(索引)添加元素
     * @param index
     * @param element
     */
    public void add(int index,E element){
        //判断输入的索引
        //区别：可以=size, 即在末尾可以添加元素
        rangeCheckForAdd(index);

        //数组添加元素需要的最小长度 size+1
        ensureCapacity(size+1);

        //移动： 移动区域：index到size-1 元素整体向后移动一位，注意必须是从后面开始移动，否则会覆盖
        for (int i = size-1; i > index; i--) {
            elements[i+1]=elements[i];
        }
        //给空出来的index位置赋值
        elements[index] = element;
        size++;
    }

    /**
     * 删除对应元素并返回
     * @param index
     * @return
     */
    public E remove(int index){
        rangeCheck(index);
        //元素的移动： 删除的元素索引index，需要将 index+1 到 size-1 的元素全部向前移动一个位置
        for (int i = index+1; i < size-1 ; i++) {
            elements[i-1] = elements[i];
        }
       /* size--;
        elements[size] = null;*/
       elements[--size] = null;
        //返回原来index位置的元素
        return elements[index];
    }

    /**
     * 查看元素的索引
     * @param element
     * @return
     */
    public int indexOf(E element){
        if (element == null){
            //如果等于null,遍历返回第一个null位置
            for (int i = 0; i < size; i++) {
                if (elements[i] == null) return i;
            }
        }else {
            //遍历找到直接返回索引
            for (int i = 0; i < size; i++) {
                if (element.equals(elements[i]) ) return i;
            }
        }

        //找不到返回-1
        return ELEMENT_NOt_FOUND;
    }

    /**
     * 清除所有元素
     */
    public void clear(){
        for (int i = 0; i < size; i++) {
            elements[i] = null;
        }
        size = 0;
    }

    //封装报异常信息方法
    private void outOfBounds(int index){
        throw new IndexOutOfBoundsException("Index:"+index+",Size:"+size);
    }
    //封装索引检查方法
    private void rangeCheck(int index){
        //判断输入的索引
        if (index<0||index>=size){
            outOfBounds(index);
        }
    }
    //封装对应位置添加元素 索引检查方法
    private void rangeCheckForAdd(int index){
        //判断输入的索引
        if (index<0||index>size){
            outOfBounds(index);
        }
    }

    /**
     * 扩容方法
     * @param capacity 添加元素需要的最小容量
     */
    public void ensureCapacity(int capacity){
        //判断是否需要扩容
        //原数组长度
        int oldCapacity = elements.length;
        //如果原数组长度 >= 添加元素需要的最小容量 capacity,则不需要扩容
        if (oldCapacity >= capacity) return;

        //扩容
        //新数组容量为旧数组容量的1.5倍
        int newCapacity = oldCapacity+ (oldCapacity >> 1);
        //新建数组
        E[] newElements = (E[]) new Object[newCapacity];
        //元素赋值到新数组
        for (int i = 0; i < size; i++) {
            newElements[i] = elements[i];
        }

        System.out.println(oldCapacity+"扩容为："+newCapacity);

        //引用指向新数组
        elements=newElements;
    }

    @Override
    public String toString() {
        //期望打印格式： size=3, [23, 45, 67]
        //大量字符串拼接使用StringBuilder
        StringBuilder builder = new StringBuilder();
        builder.append("size=").append(size).append(", [");

        //不是第一个元素，前面都添加 ", "
        for (int i = 0; i < size; i++) {
            if (i!=0){
                builder.append(", ");
            }
            builder.append(elements[i]);
        }

        //后面
        builder.append("]");

        return builder.toString();
    }

}

```



<font color="orange">注意：Java中的ArrayList集合在同一数组中批量元素的移动或者数组之间的批量拷贝，用的是`System.arraycopy()`</font>

```java
public static native void arraycopy(Object src,  int  srcPos,Object dest, int destPos,int length);
//arraycopy(原数组,  原数组起始位置, 目标数组, 目标数组起始位置, 要copy的长度);
```

![image-20210721164922660](https://gitee.com/panqiyi/pqimg/raw/master/20210721164922.png)

