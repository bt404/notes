## 基本语法

1. `this.props`是只读的，在组件中这些属性不可直接改变；

2. 可以使用state来完成props无法完成的一些任务，即值的修改；`getInitialState`函数返回一个对象用来设置状态初始值，`setState`函数可以直接修改state；

3. 应该尽可能使用props而非state，保证可变化的值最少；常用的模式是创建多个无状态组件，然后在上层创建一个有状态组件，并把它的状态通过props传递给子级；

4. 可以使用{...other}来向下传递props；

5. 表单组件通过是否设置value来区分为受限组件和非受限组件，对于非受限组件如果要设置默认值，应该设置defaultValue/defalutOption等属性；受限组件的值一旦设置是无法修改的；

6. 对于需要操作组件中的DOM节点，可以设置组件中DOM节点的ref属性，然后在方法中通过`this.refs.refName.getDOMNode`方法来获得该DOM节点，然后在该节点上直接调用底层API；使用该方法必须保证该组件事例已经被挂载在了DOM中，否则将抛出异常；

7. 组件生命周期处理方法：
  1. 挂载
    * getInitialState
    * componentWillMount
    * componentDidMount
  2. 更新
    * componentWillReceiveProps
    * shouldComponentUpdate
    * componentWillUpdate
    * componentDidUpdate
  3. 移除
    * componentWillUnmount

8. flux单向绑定中的4个主要角色：Action/Dispatcher/Store/Vies；流程为用户通过与View交互产生Action，所有Action到达Dispatcher并由它向相关的Store分发，Store执行注册过的和该Action相关的回调，最后将数据更新返回到view；

9. 可以使用ReactLink实现双向绑定，本质还是单向绑定，内部实现是通过valueLink/checkedLink将一个state和handleChange函数和一个组件绑定在一起实现的，使用中通过linkState方法绑定；

10. 


## Reflux流程

### 第一种代码结构

1. 创建Action；

2. 创建Store，并且listenTo一个Action；并且给出handler，部分handler中有一个trigger方法用来更新view；

3. 创建view，是的Store开始listen；

4. 交互调用Action方法。

## 第二种代码结构

1. 创建Action里面有各种方法名（此时Action类似一个接口）；

2. 创建Store，在listenables中指定实现的Action；

3. 在Store的适当方法中执行trigger方法，是的数据更新后刷新view；

4. 在view中connect到适当的Store，每个connect绑定到自己的一个state，当Store中trigger时会自动更新对应state。


## ReactRouter用法

### 用到的几个重要组件

`Route RouteHandler run(method) Link State(mixins)`

### Route

主要组件，用来实现路由

1. 层级关系默认代表了url和view的双重嵌套关系；

2. view的层级仅和Route的嵌套关系有关，和url无关；若Route层级相同，url同样可以有层级关系；同样，view有层级时，url也可以不用层级关系（通过绝对路径来实现）；

3. 在需要Route的地方替换为RouteHandler；

4. Route中设置name，可以由Link中的to来导向；

5. State是一个mixin，提供了一些函数用来获取当前页面的hash和path等信息；

6. 可以在url中通过`xxx/:param`的形式来指定参数，然后就可以通过`this.props.params.param`来获取该参数。
