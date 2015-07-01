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

8. flux单向绑定中的4个主要角色：Action/Dispatcher/Store/Vies；流程为用户通过与View交互产生Action，所有Action到达Dispatcher并由它向相关的Store分发，Store执行注册过的和该Action相关的回调，最后将数据更新返回到view。

9. 
