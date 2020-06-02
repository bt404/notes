# Python 笔记

1. `collections.Counter`可以将多个字典合并，使得相同键值的value相加。

2. Python中的time和datetime模块可以通过time.time_struct对象互相转换。datetime和date对象的timetuple方法会返回time_struct类型的对象，而time的mktime方法可以将该类型对象转换为POSIX时间（秒为单位）。time的gmtime方法与mktime相反，将秒转换为time_struct。

3. time更贴近底层的C实现，而datetime实现了对时间操作的简易封装。datetime.date和datetime.time分别提供了对日期和时间的访问以及算数操作。datetime.datetime是二者的组合。


## 1. 内置函数

1. `bool`既是一个`type`，又是`int`的一个子类，如果不传参数，则返回`False`。

2. `all`当数组为空时也返回`True`，`any`则返回`False`。

3. `callable`用来判断一个 Object 是否可调用，`class`都可以调用，但类的实例只有拥有`__call__`方法时可以被调用。

4. `classmethod`类方法第一个参数为 class 本身，实例和类都可以调用类方法，但无法通过 cls 访问实例属性（即使是通过实例调用且初始化了对应属性）。

5. `cmp`返回1、-1、0。

6. `delattr`相当于 del 一个属性。

7. `isinstance`支持子类实例判断。

8. 