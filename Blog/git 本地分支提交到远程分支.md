### git 本地分支提交到远程分支master
date: 2017-03-02 20:57:02

最全步骤列举：

##### 1.本地分支和远程master做对比-----确认修改文件是否正确；
![git](https://github.com/Bantina/Bantina.github.io/blob/master/img/git/git01.png?raw=true)
必要时使用 git diff 查看修改详情；

##### 2.切换到master分支 pull最新项目；
![git](https://github.com/Bantina/Bantina.github.io/blob/master/img/git/git02.png?raw=true)

##### 3.与本地分支再次做对比；(新增了刚pull下来的远程别人修改已push后的文件)
![git](https://github.com/Bantina/Bantina.github.io/blob/master/img/git/git03.png?raw=true)

##### 4.切换到 本地分支 merge到master;
注：--squash 参数去除本地commit提交记录；
![git](https://github.com/Bantina/Bantina.github.io/blob/master/img/git/git04.png?raw=true)

##### 5.查看状态 (出现pull下来的本地未修改的文件和本地已修改的文件) 提交
![git](https://github.com/Bantina/Bantina.github.io/blob/master/img/git/git05.png?raw=true)

![git](https://github.com/Bantina/Bantina.github.io/blob/master/img/git/git06.png?raw=true)

![git](https://github.com/Bantina/Bantina.github.io/blob/master/img/git/git07.png?raw=true)

##### 6.查看状态 并 与master做对比 (只有本地自己修改的文件)；
![git](https://github.com/Bantina/Bantina.github.io/blob/master/img/git/git08.png?raw=true)

##### 7.切换到master 分支 ，merge本地分支；-----带参数--squash
![git](https://github.com/Bantina/Bantina.github.io/blob/master/img/git/git09.png?raw=true)

##### 8.做最后一次提交+说明；
![git](https://github.com/Bantina/Bantina.github.io/blob/master/img/git/git10.png?raw=true)

##### 9.在master分支上直接 push，，但有可能会出现错误，如下：
![git](https://github.com/Bantina/Bantina.github.io/blob/master/img/git/git11.png?raw=true)
原因分析：在你pull了一次远程代码，还未push到远程的期间，有人先你一步，又push了代码；

##### 10.解决：先pull到最新，状态无异常(可能会出现冲突)，再重新push；
![git](https://github.com/Bantina/Bantina.github.io/blob/master/img/git/git12.png?raw=true)

![git](https://github.com/Bantina/Bantina.github.io/blob/master/img/git/git13.png?raw=true)

##### 11.完成----查看log
![git](https://github.com/Bantina/Bantina.github.io/blob/master/img/git/git14.png?raw=true)
