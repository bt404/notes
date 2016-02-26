1. css 的框模型是由外边距、边框、内边距和元素构成，height 和 width 设置的是 element 的高度和宽度。内边距用来显示背景，即背景应用于由内容和内边距、边框组成的区域。外边距默认透明，不会遮挡住后面的元素。

2. 只有指定了 !DOCTYPE 时，IE7/8 才支持属性选择器（[]）。

3. 用百分比显示数值时，默认是根据其占父元素的该属性值比值计算得出，父元素改变时，其也改变。因为width是element的宽度，所以设置width为百分数时，表示该元素所占父级element宽度的百分比，二者都不包括border和margin的宽度。

4. 元素有4种定位，默认为static，元素根据自己在html文档中的位置定位，此时top、bottom、left和right等4个属性设置无效。

5. 通过设置为absolute或fixed，元素脱离自己在html文档中的位置，并生成一个新的块级元素（无论他之前是什么级别框），即从文档流中删除不再占位。此时使用top等4个属性规定该块级元素的外边距边框相对他的最近已定位祖先元素（已定位是指position为除static以外的元素。若不存在则为最初包含块，即body，对于fixed来说始终是浏览器窗口）外边距边框的位置偏移，可以存在父级元素不是absolute而子元素是。

6. 由于absolute可能存在覆盖，可以设置z-index来规定元素间的叠放次序。

7. relative同样是相对于父级元素位置设定，但不同于absolute和fixed，元素本身并不从文档流中删除。

8. 设置relative可能导致该元素覆盖下面的元素，下一个元素永远是相对于上一个元素本该出现的位置定位（无论该元素是否是relative），所以上一个元素如果设置了relative并确定top等值，那么元素可能覆盖后面的元素。

9. 设置行内元素的垂直内边距、边框和外边距不影响行内框的高度。

10. float属性的框同样不占用html文档中的位置，他向左/右移动，直到遇到包含框或者另一个浮动框为止。所以浮动框同样可能覆盖html文档中的其他框。

11. 有时一个元素被迫折行时，原因大多情况下是父级元素指定了宽度，内框宽度又无法盛下框内元素。不同浏览器（往往是IE）对宽度的渲染会有偏差（比如见过一次IE少了1px），所以可以调整框内元素宽度来实现改变，必要时可以使用IE的hack来真对IE单独设置宽度。

12. ff下，两个float元素（一left一right），可能会造成其中一个元素覆盖住另一个元素。这时可以通过将两个元素设置relative，再分别设置对应的z-index来改变二者的叠放次序。

13. ff下，设置relative的元素，除了设置top，有时还需设置right来限制它的位置，而chrome可以自动规范。

14. IE下遇到设置sans字体导致父元素被挤破从而折行的情况，有时在IE下遇到问题，首先应该确认在其他机器的IE下是否有同样问题；然后应该确认原生IE和IE仿真模式下是否显示也有不同。

15. box-shadow构成的阴影并不会实际占据位置。

16. 当内容超过框大小时，通过设置overflow来设置超出内容的样式。默认为visible，即显示在框外面。可以设置auto和scroll等值来增加滚动条。

17. text-overflow设置文字超过宽度时，超出部分的显示方式。

18. 选择器
  * 两个类（或tag）中间用空格连接，表示后代选择器，即匹配第二个类名是第一个类名子孙的元素（中间可以跨越等级）；
  * 中间用`>`连接，表示子元素选择器，要求第二个类元素必须是第一个元素的子元素（即中间不可有其他等级）；
  * 中间用`,`连接，表示或关系，即两种标签都应用设置的样式；
  * 中间用`.`连接，表示同时匹配两个类名的元素，应用设置的样式。

19. 默认box的宽度是和width、padding、border和margin有关的，通过设置box-sizing: border-box使得后三者不再占据width之外的宽度，即width决定了最终实际宽度。对应不同浏览器分别为-webkit-box-sizing、-moz-box-sizing和box-sizing属性，IE8之后开始支持该属性。

20. em是一种相对计算单位，表示相对与父元素字体大小的值。用来设置弹性布局。一般浏览器默认font-size为16px（通过设置html的font-size为100%，body的font-size为1em），所以1em通常为16px，然后用倍数计算em值，并且最多到小数点后3位。

21. 设置为inline-block的元素可以设置vertical-align来设置垂直对齐方式。

22. 可以设置column-*等属性来将一个内容区域分列显示，不支持IE9一下版本。

23. 设置`@media`可以指定针对不同设备（主要是不同属性，如屏幕宽度和分辨率等）来针对性设置部分css。IE9之后可以使用。

24. 使用find指定`option:checked`可以得到被选中的select选项。

25. scrollTop获得当前屏幕中左上角距离容器顶部的距离，position获得元素相对最近已定位元素的位置偏移量，offset获得元素相对与整个文档的位置偏移量。

26. 判断屏幕是否滚动到底部，可以通过判断 当前滚动位置+$(window).height()-其他容器外fixed元素高度==容器高度 是否成立。

27. 在ff下，在button中添加span元素，他的mouseover等事件不会被执行。

28. js下直接在字符串前添加“+”可以将内容转换为数字。

29. 当查找祖先元素时可以使用`parents()`函数。

30. `delegate`函数直接绑定match元素的指定事件，这里的match元素包括之后动态添加的元素，所以编码时应注意避免重复绑定问题。

31. 设置child的z-index比parent的z-index高是没有效果的，因为他们两个在一个块内。

32. 移动设备设备上有3种viewport：
  * layout viewport：一个较宽值，一般是固定的，为了能显示下为桌面设计的网站。
  * visual viewport：表示浏览器可视区域宽度。
  * ideal viewport：一般为屏幕宽度（不同设备不同），为了避免出现横向滚动条。
  meta标签设置viewport设置的是layout viewport，一般同时设置`width=device-width`和`initial-scale=1.0`来使得layout viewport宽度和ideal viewport一致。因为前者对iPhone/iPad无效，后者对IE无效，无效表现为无论横竖屏，都会把layout viewport设置为竖屏时的ideal viewport。scale（缩放值）计算公式：scale = ideal viewport / visual viewport。设置layout viewport为固定值的意义在于使用和桌面相同的css计算规格来渲染页面，使页面不至于被压缩而模糊不清。而设置viewport这个meta属性修改layout viewport的意义在于，有些网站专门针对移动设备屏幕进行了适配，使用默认layout viewport宽度不再合适，所以修改它。

33. 承上条，虽然默认layout viewport一般都是一个很大的固定值，但在当前大多设备浏览器中都会使页面自动适应屏幕的宽度，这是因为浏览器一般会有一个initial-scale的默认值，来对页面进行缩放。

34. CSS居中的一种方法，设置父元素为relative，子元素为relative（或者根据需要设置为absolute，如果相对窗口，则设置为fixed），然后设置子元素left为50%，margin-left为子元素宽度一半的相反数。

35. 
