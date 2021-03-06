#概述
- 提供分布式存储机制，提供可线性增长的海量存储能力

- 自动数据冗余，无需备份，无需raid

- 为进一步计算提供数据基础

#设计基础
 - 硬件错误是常态，因此需要冗余
 
 - 流式数据访问，批量读取而非随机读写
 
 - 简单一致性模型，为了降低系统复杂度，对文件采用一次性写多次读的逻辑，即文件一经写入，关闭，就不能再修改
 
 - 采用**数据就近**原则分配给节点
 
#体系结构
![](http://i.imgur.com/Y4c3bXP.png)

		namenode/datanode/secondary namenode/事务日志、映像文件
		
##namenode
	
	1.管理文件系统的命名空间
	2.记录每个文件数据块在各个datanode上的位置和副本信息
	3.协调客户端对文件的访问
	4.记录命名空间的改动或空间本身属性的改动
	5.namenode采用事务日志记录hdfs元数据的变化。使用映像文件存储文件系统命名空间，包括文件映射，文件属性等
	
##datanode
	
	1.负责所在物理节点的存储管理
	2.一次写入，多次读取（不可修改）
	3.文件由数据块组成，典型的数据块是64M
	4.数据块尽量散布到各个节点
	
#读写过程

##读过程
	
	![](http://i.imgur.com/bj9mOyy.png)
	
	1.客户端要访问hdfs中的一个文件
	2.首先从namenode获取组成这个文件的数据块的位置列表
	3.根据列表知道存储数据块的datanode
	4.访问datanode获取数据
	5.namenode并不参与数据实际传输
	
##写过程
	
	![](http://i.imgur.com/uf4up2b.png)
	
	1.客户端请求namnode创建新文件
	2.客户端将数据写入DFSOutputStream
	3.建立pipeline依次将目标数据块写入各个datanode,建立多个副本
	
	
	
	
