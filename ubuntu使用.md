#### 查找文件

1. locate + 文件名
2. find / -name + 文件名



#### boot空间不足

1. 查看boot的剩余空间

   ![image-20200911234202550](/home/qinh1/.config/Typora/typora-user-images/image-20200911234202550.png)

2. 删除boot中多余的内核

   * 查看当前使用的内核

     `uname -r`

     ![image-20200911234309520](/home/qinh1/.config/Typora/typora-user-images/image-20200911234309520.png)

   * 查看当前所有存在的内核

     `dpkg --get-selections |grep linux-image`

     ![image-20200911234451452](/home/qinh1/.config/Typora/typora-user-images/image-20200911234451452.png)

   * 删除多余的内核



#### dpkg用法

**说明：dpkg是一个Debian的一个命令行工具，它可以用来安装、删除、构建和管理Debian的软件包**

* `dpkg -l` 查询系统中所有安装的软件包
* `dpkg -L + filename` 查询该软件包的名称



#### grep用法

grep 的全称：Global search Regular Expression and Print out the line

*  grep "dpkg"  ubuntu 使用.md 

* `grep "words" filenames`

* `grep -w` 只显示要查找的内容，完全相同

* `grep -win` 显示所在的行数

* `grep -win - B 2` 显示要查找的所在的行和之前两行
* `grep -win - A 2` 显示要查找的所在的行和后两行

* `grep -win - C 2` 显示要查找的所在的行和后两行和前两行
* `grep -win "ubuntu" ubuntu使用.md ./*` 可以同时显示文件和行数
* `grep -winr "ubuntu" ./` **在不同文件中查找**
* `grep -wirl "ubuntu" .` 不显示行数，只显示文件
* ` history | grep "git commit"` 将上次的输出作为本次的输入
* `history | grep "git commit" | grep "docker"` 将一直输出作为输入



#### linux基础

* `|` 上个命令的输出作为下个命令的输入























