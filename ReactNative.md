1. 有时候编译报错
> cannot read property 'root' of null
可能是因为watchman版本不够，`brew update`之后`brew install watchman`，然后关掉console后重新start即可；

2. 流程：
  1. 引入react-native；
  2. 定义常量（只是规范，并不强制要求在该位置进行）；
  3. 声明定义React中用到的组件；
  4. `render`中编写自己的组件；
  5. 通过`StyleSheet`来定义样式；
  6. 最后通过`AppRegistry.registerComponent`来注册自己的组件。

3. 每个组件可以声明使用多个style（通过数组方式，最右边的样式有较高优先级，但是`false/undefined/null`不会覆盖左侧定义的样式；

4. 和state有关的错误，确定下是否在自己的component的getInitialState里返回了对应state；

5. PickerIOS组件无法直接使用Animated来定制动画效果，使用Animated.View来包裹该组件可以实现；

6. 使用map渲染TouchableHightlight组件，并绑定事件时，还是会存在this指针指向错误的问题；处理方法是在render方法开始时缓存this(var mSelf=this;)，然后在绑定事件处理器时.bind(mSelf)；并且对于部分事件处理器可以在render中通过变量保存事件处理器，避免在事件绑定时使用this指针；

7. 使用setState不保证马上同步修改state值，如果需要在setState后立即使用修改后的state值，需要setState提供第2个参数，是一个回调函数，该函数在state值确认修改后执行；

8. 
