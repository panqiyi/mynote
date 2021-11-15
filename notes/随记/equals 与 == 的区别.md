## equals 与 == 的区别

**原生的equals与 == 没有区别**

原生的equals即类没有重写equals方法；

此时的equals与 == 比较的效果一样；

如比较基本数据类型都是比较值，比较引用数据类型都是比较地址；

**重写了equals方法的类**

如String类 与Date类等都重写了equals方法；此时调用equals方法就是比较对象的内容；很多情况下我们也会在自定义类中重写equals方法；

