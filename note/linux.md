### 1.查看java安装路径   

1. which java   查看路径/usr/bin/java
2. ls -l /usr/bin/java   看看这是否是个软连接，找出这个软连接指向的路径/etc/alternatices/java
3. ls -l /etc/alternatices/java  指向/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java
4. ls -l /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java指向本身，即位java安装路径

### ubuntu:

1. sudo apt-get install vim安装软件
2. sudo apt-get remove vim-common  卸载
### 命令
- less
    - less运行时可以输入的命令有：
    - 空白键  ：向下翻动一页；
    - [pagedown]：向下翻动一页；
    - [pageup] ：向上翻动一页；
    - /字串   ：向下搜寻『字串』的功能；
    - ?字串   ：向上搜寻『字串』的功能；
    - n     ：重复前一个搜寻 (与 / 或 ? 有关！)
    - N     ：反向的重复前一个搜寻 (与 / 或 ? 有关！)
    - q     ：离开 less 这个程序；

- tail
  - 取文件最后几行： tail -10 info.log
  - 持续监测文档： tail -f info.log

- head
  - 查看文件前几行：head -10 info.log 

- df
  - 显示磁盘总体使用情况 ：df -h
  - 显示文件磁盘使用情况 ：df -h /etc

- du
  - du: 查看当前文件夹文件占用空间情况