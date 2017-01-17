1. yarn vs npm
  * yarn在~/.yarn-cache目录下按版本缓存之前安装过的包。
  * yarn会创建一个yarn.lock来记录当时安装过的包的确定版本号，只要将lock文件提交到代码库，即可在其他机器上安装相同版本的包。如果要更新包版本，只要删除lock文件重新安装即可。
  * yarn global add全局安装的包放在~/.yarn-config/global下，不需要sudo执行。
