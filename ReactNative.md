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

4. 
