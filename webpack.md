1. webpack 的本质是将多个文件分别作为一个模块，并且赋予一个 module_id 来标识；通过`__webpack_require__`来引入不同的模块。

2. `!`的意义是从后向前使用 loader 依次处理文件，比如`style!css!less`是指先用 less-loader 处理 regex 匹配到的文件，然后将处理结果交由 css-loader 处理，最后由 style-loader 处理并输出到打包的文件中。

3. `?`的意义是通过 query string 的方式指定对应 loader 的参数，如果是通过`webpack.config.js`配置 webpack 的话，也可以通过`query`字段来设置 option。

4. babel6 之后不再默认帮助转换 js 语法，而是需要设置`presets`字段来设置语法转换工具，比如`es2015/react/stage-0`等。

5. 
