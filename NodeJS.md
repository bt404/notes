1. yarn vs npm
  * yarn 在 ~/.yarn-cache 目录下按版本缓存之前安装过的包，之后安装相同版本的包不会再走网络请求，而是直接从本地库拉取。
  * yarn 会创建一个 yarn.lock 来记录当时安装过的包的确定版本号，只要将 lock 文件提交到代码库，即可在其他机器上安装相同版本的包。如果要更新包版本，只要删除 lock 文件重新安装即可。
  * yarn global add 全局安装的包放在 ~/.yarn-config/global 下，不需要 sudo 执行。
  * yarn 的 lock 文件会记录当时下载包的仓库地址。
