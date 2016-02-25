###jQuery笔记整理
1. append执行插入操作，直接操作DOM。add主要用来组成一个元素的集合，并不能直接向DOM中插入元素。add更想一个选择工具，用来将一组元素合成一个集合，然后对他们进行统一操作，比如修改CSS等。而append则是一个动作，用来修改DOM结构。

2. 常用的DOM操作函数：append/appendTo, after/before

3. each函数中使用return;相当于原生循环中的continue，return false;相当于break。因此需要注意既不能在each中用return作为函数的返回，也不能直接使用break作为终止循环的语句。

4. ready方法根据浏览器支持程度分别绑定`document`的`DOMContentLoaded`和`onreadystatechange`两个事件，为了防止这两个事件没有被触发，又同时绑定了`window`对象的`load`事件，但在回调中移除了事件监听，保证`ready()`方法只被执行一次。

5. 
