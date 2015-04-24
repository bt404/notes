1. 每个cotroller定义了一个作用域变量，在该作用域内可以使用该变量，起到数据绑定的作用。

2. 每个scope使得数据和视图分离开来，但是二者的绑定是同步的，即model中的数据修改会即时体现到view中。

3. controller的作用在于将不同的逻辑（对应为view的处理函数）对应于不同的模板。在Django中即URLConf，它讲不同的URL对应到不同的view中的函数。在ng中，ng-controller即一个function可以将不同的view对应到不同的模板上。

4. 每个controller函数可以有一个作用域变量参数$scope，可以用来绑定数据。这些参数的名字非常重要，ng的注入器会使用这些名字来寻找响应的依赖使用它们提供的服务。

5. ng-repaet可以实现for循环的作用。在ng-repeat后可以使用filter实现python中列表解析中的条件判断。

6. 可以使用orderBy过滤器进一步对数据进行处理。

7. 可以给controller传入一个$http来使用XHR，它拥有get方法来向服务器异步请求数据。

8. $常作为ng内部命名的前缀，所以自己创建的名称应该尽量避免使用$作为前缀。由于controller通过名字来绑定服务，在JS压缩时会造成服务不可使用，可通过在controller中设置$inject属性数组来绑定服务，或者直接使用js数组方式构造controller。

9. 因为ng是在整个页面加载完成后开始才开始解析，页面在加载时同时会加载图片，所以不应在img的src中使用数据绑定，否则会被当做字符串被使用。应该在ng-src中进行数据绑定指定图片地址。

10. 可以使用$routeProvider来实现路由，它可以指定url和template以及controller的对应关系。URL中的:后面的可以作为参数保存在$routeParams对象中通过controller传递使用。

11. 可以使用ng-view来实现多模板，类似jinja2中的block功能。

12. 可以使用ng-click来为一个元素注册点击事件，然后在controller中编写事件处理函数。

13. 可以使用ng-cloak防止页面初始加载时未渲染内容输出。

14. directive用来创建可重复使用的组件，它返回一个factory function。
  * templateUrl用来指定组件所依附的html模板，可以是一个表示文件名的字符串，也可以是一个function，接收两个参数，分别表示该directive所在的ele和该ele的attr集合。
  * restrict用来指定表示指令名的元素，A表示指令名作为标签的一个属性出现，C表示作为标签的一个class出现，E表示作为标签名出现（即新建了一种标签）。可以自由组合，比如设置为'ACE'。
  * scope用来指定指令的scope。如果没有该option，则默认指令继承所在部分的scope。若指定，则将directive的scope与外部scope完全隔离，便于将数据逻辑和展示隔离。
  * 如果使用指令操作DOM，需要设置link属性，该属性为一个函数，接收scope、ele、attrs三个属性。link的scope参数和指令的scope option关联。即如果设置了scope的option，则link的scope同该scope，否则为指令所在ctrl的scope。
  * 如果在指令中设置了$iterval，则应在该指令中监听该node的$destroy事件。调用方法为ele.on('$destory',...)或scope.$on('$destory', ...)。
  * 
