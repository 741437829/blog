#hadoop架构
![](http://i.imgur.com/4Lmdc2S.png)
![](http://i.imgur.com/IoJQFjm.png)

> 由namenode、jobtracker、namenode和tasktracker组成

#namenode

- hdfs的守护程序
- 记录文件是如何分割成数据块的，以及这些数据块存储到哪些节点上
- 对内存和io进行集中管理
- 是单点，发生故障将使整个集群瘫痪

#Secondary namenode

- 监控hdfs状态的后台辅助程序
- 每个集群都有一个
- 与namenode通讯，定期保存namenode快照
- 当namenode故障可以当备用namenode使用

#datanode

- 每台从服务器都运行一个
- 负责把hdfs数据块读写到本地文件系统

#jobtracker
 
 1.用于处理作业（用户提交代码）的后台程序
 
 2.决定有哪些文件参与处理，然后切割task并分配给节点
 
 3.监控task，并在其他节点启动失败的task
 
 4.整个集群只有唯一一个jobtracker，位于master
 
#tasktracker

 1.位于slave节点，与datanode结合（代码与数据一起的原则）
 
 2.管理各自节点上的task（由jobtracker分配）
 
 3.每个节点只有一个tasktracker,但一个tasktracker可以启动多个jvm，用于并行执行map或reduce任务
 
 4.与jobtracker交互
 
#master与slave
 - master：namenode、jobtracker、secondary namenode,master不是唯一的
 - slave: datanode、tasktracker