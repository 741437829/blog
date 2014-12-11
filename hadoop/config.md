#要配置的文件

- hadoop-env.sh

	配置hadoop运行时候的一些环境变量

- core-site.xml

	hadoop核心设置，比如io设置等

- hdfs-site.xml

	配置hdfs后台程序，namenode/secondary namenode/datanode

- mapred-site.xml

	配置mapreduce后台程序，jobtracker/tasktracker

- masters

	配置哪些机器上要运行secondary namenode

- slaves

	配置哪些机器上要运行datanode和tasktracker

- hadoop-metrics.properties

	控制阵列在hadoop上面部署的方式

- log4j.properties

	你懂得
	
#重要配置项

1. fs.default.name
	在core-site.xml中配置，namenode的远程地址和端口，默认是8020，习惯上配置成9000
	
2. dfs.name.dir
	- the list of directories where the namenode stores its persistent metadata,the namenode stores a copy of metadata in each directory in the list
	- the default value is ${hadoo.temp.dir}/dfs/name

3. dfs.data.dir
	- the list of directories where the datanode stores blocks,each block is stored only one of these directories
	- the default value of this is ${hadoop.temp.dir}/dfs/data

4. fs.checkpoint.dir
	- the list of directories where the secondary namenode stores checkpionts,it stores a copy of checkpoint in each directory in the list
	
#mapred-site.xml

- mapred.job.tracker
	
	jobtracker的地址和端口

- mapred.local.dir
	
	配置任务产生临时文件的目录（可配置多个），当任务结束，里面的文件也被清空
	
- mapred.system.dir

	任务执行的时候，共享文件存储的目录
	
#
	

	