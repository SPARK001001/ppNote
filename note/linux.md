### 1.查看java安装路径   

1. which java   查看路径/usr/bin/java
2. ls -l /usr/bin/java   看看这是否是个软连接，找出这个软连接指向的路径/etc/alternatices/java
3. ls -l /etc/alternatices/java  指向/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java
4. ls -l /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java指向本身，即位java安装路径



2. ubuntu:
   1. sudo apt-get install vim安装软件
   2. sudo apt-get remove vim-common  卸载
