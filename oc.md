####扩充类
1. 普通变量未初始化会赋予它一个不确定的值，而指针未初始化会自动赋予它nil。


2. 可以使用.来获取一个对象的属性，也可以使用getter和setter。


3. 属性对应有instance variable，名字相同但是前面加一个_，不过一般情况下在method中也使用self配合属性来访问，而不是直接使用对应的variable。


4. extension可以实现私有访问，在同一个头文件中，在extension中创建读写属性，在原定义中创建只读属性，那么该属性对类外部来说是只读，而对内部是读写的。


5. NS的大多数集合类中只能存储一些对象类型，而不是原生类型。如果要保存一些原生类型，需要先将他们转换为相应类型的对象。


6. procotol也可以有继承。


####数据类型


7. collection一般只能保存NS的对象类型，原生类型（如int，char等可以使用原生数组保存）。


8. NSString初始化方法：
  initWithCString:encoding:   （NSUTF8StringEncoding）
  stringWithCString:encoding:    （不需要alloc）
  stringWithString:   （需要使用NSString类型字符串，即@“”。该方法会提示你冗余，可以直接使用下面的方法来初始化该字符串）
  @“ns string”


9. NSString对象是不可变（immutable）的，一旦创建不能修改，有需要可新建一个该类型对象。NSMutableString对象可以创建可修改的字符串对象，比如它拥有appendString方法。


10. format string主要用来使用各种不同类型对象来组装一个字符串。它对应的初始化方法为stringWithFormat:，后跟一个NS类型的format字符串。


11. OC中使用NSNumber对象来表示任何C原生数字类型，对应的初始化方法为（需要alloc）initWithInt/UnsignedInt/Long/BOOL，以及（不需要alloc）numberWithFloat/Double/Char。也可以直接使用对象初始化，不过之前都需要加上@，比如@42,@42l,@3.14f,@YES等。
对应的也可以将一个NSNumber对象转换为原生类型的值，相应的方法为intValue/longValue/boolValue等。


12. NSNumber对象和NSInteger/NSUInteger之间也可以互相转换，后者拥有更好的跨平台性，但是对于一些local使用场景如迭代器，可以考虑使用原生类型。


13. 使用NSRange可以获得有NSString通过使用rangeOfString返回的一个位序和子串长度信息。


14. NSNumber类是NSValue类的子类，可以使用NSValue类创建NSNumber无法表示的原生类型的对象，比如struct等。


15. NSArray/NSSet/NSDictionary都是immutable，相应的存在对应的mutable类型。使用它们来存储原生类型必须先将原生类型保存为NSNumber类型等。


16. 同一个NSArray对象可以存储不同类型的对象，并且它们使用强链接。


17. 对于类方法（+）可以直接通过类名调用，而对于实例对象，往往先使用alloc返回一个对象，然后再进行调用。


18. 常用的NSArray初始化方法：
  + (id) arrayWithObject: (id) anObject;
  + (id) arrayWithObjects: (id) firstObject, …;
  -  (id) initWithObjects: (id) firstObject, …;


19. 对于NSArray，nil表示了一个该对象的结尾，使用上一条的最后两个方法初始化的对象必须以nil结尾。如果用来初始化的对象中中间有nil，那么将在此被截断，后面的对象不在保存在NSArray对象中。


20. 也可以直接使用对象列表来初始化一个NSArray，格式为@[obj1, obj2, …]。这种方法中不能使用nil来结尾，否则会有runtime错误，如果需要保存nil，可以使用NSNull类。一个NSArray结尾的nil不会记入长度。


21. 对于一个NSArray对象，使用count获得他的长度，使用containsObject:可以判断是否包含一个对象，objectAtIndex:来获得指定位置的对象（也可以直接像C中一样直接使用索引）。


22. 排序使用：sortedArrayUsingSelector:@selector(compare:)


23. NSMutableArray的一些方法：addObject:/replaceObjectAtIndex:withObject:等。


24. 排序方法：sortUsingSelector:@selector(caseInsentiveCompare:)


25. NSSet的初始化方法有setWithObjects:和initWithObjects:，使用它们初始化时同样需要nil结尾。


26. 对于NSDictionary，每个key都是一个副本，所以用作key的对象需要支持NSCopying。


27. NSDictionary的初始化方法有dictionaryWithObjectAndKeys:和initWithObjectAndKeys，value在前，key在后，而且所有对象之间都以“,”分隔。最后需要nil结尾。
直接使用@{}同样可以初始化，但是key在前，value在后。


28. dictionary可以使用objectForKey:和dict[key]两种方法索引。


29. 所有NSNull实例的null方法会返回同一个对象，所以可以使用obj==[NSNull null]来判断一个对象是否等于nil。


30. 遵从NSFastEnumeration protocol的对象可以使用fast enumeration，可以使用for..in…，但是在迭代过程中，不能修改容器，即使他是mutable对象。否则会报runtime exception。


31. 同样可以使用上述对象的nextObject方法来获得下一个对象，也可以获得他的reverseObjectEnumerator来for in反向遍历。


32. dictionary的for in迭代的是他的keys。


####数据封装


33. 对于每个property，都存在一个实例变量与他对应，默认变量名为property名字之前加上一个下划线。


34. 可以设置getter=来手动设置getter的名字。


35. 可以使用“.”来获取或设置property。


36. 方法的签名和参数的名称无关，interface和implementation中的同一个方法可以使用不同的参数变量名，只要方法签名保持一致。


37. 类名必须唯一，否则会有编译错误。


38. self关键字类似其它语言中的this关键字，作为当前对象的指针。


39. 子类可以重写父类的方法（不需要特殊关键字，直接编写相同签名的方法即可），可以使用super关键字调用父类方法（沿着继承链向上寻找）。


40. 一些库中的类出了使用alloc+init方法初始化一个对象外，还可以直接使用工厂方法（通常为类方法）来初始化一个对象。


41. 如果类的初始化不需要参数，可以直接使用[class new]来生成并初始化对象。


42. oc中同样可以用父类引用调用子类对象。


43. 对于对象，比较是否想等应该使用isEqual方法，比较大小应该使用compare方法，并且判断结果是否==NSOrderedAscending（或者有其它常量）。


44. 可以只申请实例变量而不设置响应属性，这时只要在interface或者implementation中的最顶层添加一个大括号，在其中声明实例变量。


45. 可以自己编写定制的属性访问和设置方法。


46. 默认属性是线程安全的，即对getter和setter的操作是原子的。


47. 承46，系统不允许只自己设置一个非原子的accessor（不用nonatomic修饰）而另一个仍由系统实现。但是可以自己编写一个属性实现用nonatomic修饰，另一个留给系统自动实现（atomic）。


48. 为了避免强链接循环造成的内存泄露，可以使用weak修饰属性来避免这种情况。
强链接循环的意思是两个对象相互保持一个强引用指针指向对方，造成两个对象无法被内存释放。


49. 对于实例变量，也可以使用__weak来修饰使它成为弱引用，不计入引用计数，当它指向的对象被释放后，该变量自动设置为nil。在多线程程序中，对一个弱引用判空需要先用一个强引用的过渡性变量缓存该变量，再用它进行判空操作。


50. 对于Cocoa和Cocoa Touch中的一些类不支持weak和__weak，只能使用unsafe_unretained和__unsafe_unretained关键字来声明，和前者不同的是当引用对象被删除后，系统不会对该指针赋nil，成为悬挂指针，对该指针传递消息会造成崩溃。


51. 当将一个强引用设置为mutable对象时，它的值是可能发生改变的。使用copy修饰属性可以将赋予的值创建一个副本由当前引用指向，则该引用不受赋值对象的影响。一些实例对象都有copy方法用来创建自己的副本，支持该机制的对象都需要实现NSCopying protocol。


####修改已有类（category和extension）
1. 使用category来扩展一个已有类，category中定义的方法和原类中的方法没有区别，也可以被原类的子类调用。语法如下：
```
@interface ClassName (CategoryName)
@end
```


2. 不应该在category中设置实例变量或者属性（原类中有的除外），系统将不为该类自动保存这些变量和属性。如果要这样做，需要使用extension。


3. 使用分类扩展类有时候会造成方法明冲突，如果是自定义的类，此时对该方法的结果是未定义的；如果是扩展framework中的类，这时会造成命名冲突从而使程序崩溃。


4. 解决这种问题的方法是在扩展framework中的类时，在方法名的前面添加一个前缀，像对自定义类添加的前缀一样，不过使用小写，并且跟着一个下划线。


5. extension的语法和category类似，只是括号里面没有任何参数。它适用于知道原类的源代码的时候，对已有类进行内部修改，可以添加属性和实例变量。通过extension可以实现私有变量，因为extension和原类中可以定义重名的属性和实例变量。


6. 可以将extension放在一个单独的头文件中，在放出该类的API时，只放出原类的头文件，在原类的头文件中引入extension的头文件。两个头文件可以分别为：`ClassName.h`和`ClassNamePrivate.h`。


7. 综上，category通常用来为类添加一些新的行为，而extension更多的是一种机制实现的辅助设施。


8. 对于分类的一个好处是可以将对一个类的实现分散在多个文件中。每个实现包含一个interface和implementation，在调用该类时只需要引入该类的头文件就行`ClassName.h`。


9. 文档中讲述了Objective-C Runtime Programming Guide，标记后看。同时讲述引用时，讲述到了delegate的概念，同样标记后看。


####协议


1. 协议可以用`@required`和`@optional`来分别表示必须实现和可选实现的方法。


2. 运行时调用optional方法时，应该先判断对象是否实现了该方法，方法为：
```
[obj respondsToSelector: @selector(methodSignature)]
```
其中methodSignature为方法签名，应该包括它的冒号。


####块的使用
1. block也是作为一个对象处理，可以存储在NSArray等对象中。格式为：`^(arg1, arg2, ...){ code }` 。


2. OC中的函数指针只要将C中的*改为^，定义指针后可以将一个block赋值给它。指针定义格式为：`void (^blockPotinter)(void);`。


3. block可以返回结果，也可以捕获scope内的其它变量值。当它捕获block外的变量值时，变量值是作为const类型被捕获的，他对该变量的修改不会影响原变量。


4. 承接上一点，如果想要是block内也可以修改块外的变量，块外的变量需要用__block修饰（放在最前）。


5. block可以作为参数传递给方法或者函数，如果该方法或函数接收多个参数，那么block应该作为最后一个参数。这种用法通常可以用在传递一个回调函数（block实现）。


6. 可以使用typedef来顶一个函数指针类型，用法同C。


7. 为一个对象定义一个block属性，应该指定copy属性。


8. 对于作为回调函数的情况，如果在block中使用self可能会造成强链接循环，进而内存泄露。通常解决方法是在方法内声明一个弱链接赋值为self，然后在block中使用该弱链接。


####错误处理

1. OC中，用户编程错误是Exception，其它所有错误都是NSError类的实例。


2. 