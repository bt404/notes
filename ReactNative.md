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

8. RNChart由于配合的rn版本问题，不能直接`npm install`，需要`npm install https://github.com/onefold/react-native-chart --save`；而且文档中传递的`color`参数有错，具体参见dc代码，不应传递一个字符串；

9. RNChart的data元素数量必须大于等于xLables的元素数量，而且不能全为0；并且RNChart的data元素全小于1时，y轴会出现全显示0的bug；

10. 可以将组件作为props传入另一个组件，然后在另一个组件中直接通过标签的形式来引入该组件；

11. TouchableHighlight只能有一个直接子组件（类似的还有其它一些组件）；

12. NavigatorIOS中设置translucent为false可以取消半透明效果，颜色即为设置值，否则会自动添加半透明效果，而且设置为true（default）后wrapper需要设置marginTop（有时为65），否则内容部分会整体向上偏移；

13. 可以将父组件的state绑定到子组件的state上，这样想要刷新子组件，可以通过修改父组件的state，然后在子组件中的componentWillReceiveProps方法中修改子组件的state为新的props，该过程应该可以优化；

14. 必须显示设置Image的宽高，才能让图片显示；

15. rn-0.13+版本有坑：使用ListView有多次随机触发onEndReached事件的bug，即每一次列表触底会触发3次触底事件，造成列表渲染错误。。降回rn-0.12+后，该坑填平，开始进入16号坑，详见下条；

16. 当在ScrollView中嵌套ListView子组件时，因为两个组件都具有滚动事件，滑动时会造成“什么狗屁玩意儿我也不知道怎么就出现数据不加载而且系统也不给你错误提示总之就是很cao蛋搞s你不偿命”这种bug，所以要把ScrollView改为View，解决该问题；

17. 修复RNChart bug，使用NSNumber代替NSUInterger表示y轴标签，并保留1位小数，使得最大数据小于1时y轴坐标为1位小数；

18. 修复RNChart bug，当传入图表的数据数组首尾相同时，会使得scale为+INF，导致程序crash，现加上置0兼容；

19. to be fuckinued...
