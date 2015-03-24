# PHP 学习笔记

## Class 和 Object

1. property 的值必须在编译时已知（不可是一个计算表达式，不可是另一个变量，但可以是一个 constant。

2. PHP5 中如果用 var 代替其他权限访问符修饰 property，变量默认为 public。var 用作兼容。

3. 类中使用静态属性用 `self::$property` 来表示。

4. class/interface constant 使用 const 声明定义，不需要 $ 来起始。可以对一个变量复制类名相同的字符串，然后像使用该类一样使用该变量。

5. 使用 `__construct` 和 `__destruct` 分别表示构造函数和析构函数。如果没有 `__construct` 可以使用同类名相同的方法作为构造函数（仅为兼容）。5.3.3中，当类有所属 namespace 时，该方法无效。无所属 namespace 时有效。

6. 使用 extend 表示继承，单继承。使用 parent 表示父类。使用 `parent::__construct` 和 `parent::destruct` 调用父类构造/析构函数。

7. 脚本被终止后仍然会调用析构函数，在析构函数中执行 `exit()` 可以终止当前脚本执行。

8. 一个类的 instance 可以调用相同类的另一个 instance 中的 private 属性。

9. PHP_EOL 表示一个换行。

10. static 的三个使用场景：类的静态方法/属性，静态变量以及延迟静态绑定。

11. 静态属性必须初始化为常量或字符串。

12. 直接对类声明 abstract 或则其为抽象类，抽象类中可以不声明抽象方法。抽象类不可实例化，父类中声明的抽象方法不可在该类中被实现。

13. 子类可以部分实现父类中的抽象方法，若如此，则该子类也需要声明为抽象类。

14. 子类中实现的抽象方法应和父类中访问权限相同（或者更低）。函数签名匹配中，子类重写的方法可以有可选参数（optional arguments）。

15. 5.3.9之前，一个类不可同时实现两个包含相同方法名的 interface；之后版本可以，当且仅当同命方法具有完全相同的函数签名。

16. interface 也有继承关系。

17. 一个非抽象类需要实现所实现 interface 的所有方法。或者将该类声明为抽象类，然后部分实现 interface，并将未实现方法声明为抽象方法。

18. interface 中定义的 constant 不能在类中修改他的值。

19. PHP 中的 overloading 不同与其他语言，他不支持通常意义的重载，定义不同签名的两个同名方法会报错。

20. `__get($name), __set($name, $value), __isset($name), __unset($name)` 4个 magic function 在访问类中未设置的属性时被触发。`__call($name, $arguments), __callStatic($name, $arguments)` 在调用类中未设置的方法时被触发。上述方法必须被定义为 public。

21. 当调用方法使用参数数量超过签名中参数数量时，多出的参数会被自动忽略，方法照常执行。

22. `foreach` 可以遍历一个 object 中所有可见的 property。也可通过实现 Iterator 接口来指定 `foreach` 的执行行为，相关的还有 IteratorAggregate 接口。

23. 使用 `clone` 关键字来复制一个 object，本质是调用类的 `__clone()` 方法。

24. 
