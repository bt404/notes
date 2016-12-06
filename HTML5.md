1. 当前一共有4种 sectioning element：`<section>, <article>, <nav>, <aside>`，都为块级元素：
  * section 主要用来从逻辑上将内容分块。
  * article 可以作为一个逻辑上独立的块来使用，比如作为一篇博客文章。
  * aside（感觉可以译为“旁白”），用来包裹一些辅助信息，比如 tweets 或者 feeds。
  * nav 用来包裹导航内容。
  以上标签，section 和 article 可以根据需要互相嵌套，nav 一般作为一个文档的主导航只设置一个。

2. Document outline 是 HTML 规范定义的一些规则用来抽离出一个文档的大纲（目录）结构。
  * HTML4 中只使用 h1~h6 来设置文档的 outline，数值越小权重越高（即目录项级别更高。
  * HTML5 中增加了 sectioning element 的 outline 规则，利用 sectioning element 的嵌套关系来确定不同 sectioning element 中 heading 标签的权重。通过嵌套关系形成的 outline 不受 heading 数值大小干扰，父级元素高于子元素。
  * 同一个 sectioning element 中第一个出现的 heading 标签作为该 section 的 heading，后续出现的 rank 大于等于该 heading 的标题会创建一个新的隐式 section，rank 小于它的标题会创建一个隐式的 subsection。对于上述两种情况，该 sectioning element 中第一个 heading 都会作为后续创建的隐式 section 的 heading。（但在 h5o 插件中这两种隐式 section 都会显示）
  * 如果一个 section 没有设置 heading，ua 会自动为它创建一个，value 为`Untitled ${markup_name}`。所以从更好 outline 的角度来讲，最好为每个 section 创建一个 heading，然后通过 CSS 来设置它是否被显示。
  * `<body>`是一个 sectioning root，其它 sectioning root 包括`<blockquote>, <figure>, <details>, <fieldset>, <td>`这些元素。每个上述元素的 heading 不会显示在上层 outline 中。所有后面5个元素中的 heading 不会出现在 body 的 outline 中。
  * 除了最新的 FireFox/Chrome 支持 HTML5 outline，大多数 ua 还只支持 HTML4 outline。所以如果使用前者 outline 可能会同时出现多个 h1 标签，依据 HTML4 规范生成的 outline 会使文档结构显得混乱。所以也要考虑 ua 的兼容性合理设置 heading。
  * 可以使用 h5o 插件来显示一个文档的 outline，并且可以方便定位到对应 section。

3. 
