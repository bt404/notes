1. homebrew将程序安装在/usr/local/Cellar/下，然后将该文件夹链接到/usr/local/opt/下。

2. 设置一个程序开机启动，需要编写好相应的plist文件，链接到~/Library/LaunchAgents/下。

3. brew安装好的程序通常将他的plist文件全部拷贝到上述文件夹下，可以设置开机启动。

4. 使用brew info package_name可以查看如何重启一个用brew安装的程序。

5. 当由于网络问题没有无法通过 brew 下载需要的包时，可以手动下载，然后放在 ~/Library/Caches/Homebrew 文件夹下，然后 brew install pkg_name 即可。
