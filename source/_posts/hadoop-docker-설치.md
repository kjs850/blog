---
title: hadoop docker 설치
date: 2019-04-11 18:45:27
---

```bash

✘ jake.ko  ~  docker run -it sequenceiq/hadoop-docker:2.7.0 /etc/bootstrap.sh -bash
/
Starting sshd:                                             [  OK  ]
Starting namenodes on [0439286d2442]
0439286d2442: starting namenode, logging to /usr/local/hadoop/logs/hadoop-root-namenode-0439286d2442.out
localhost: starting datanode, logging to /usr/local/hadoop/logs/hadoop-root-datanode-0439286d2442.out
Starting secondary namenodes [0.0.0.0]
0.0.0.0: starting secondarynamenode, logging to /usr/local/hadoop/logs/hadoop-root-secondarynamenode-0439286d2442.out
starting yarn daemons
starting resourcemanager, logging to /usr/local/hadoop/logs/yarn--resourcemanager-0439286d2442.out
localhost: starting nodemanager, logging to /usr/local/hadoop/logs/yarn-root-nodemanager-0439286d2442.out
bash-4.1#
bash-4.1# cd $HADOOP_PREFIX
bash-4.1# pwd
bash: ㅔpwd: command not found
bash-4.1# pwd
/usr/local/hadoop
bash-4.1# bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.0.jar grep input output 'dfs[a-z.]+'
19/04/11 07:12:01 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
19/04/11 07:12:03 INFO input.FileInputFormat: Total input paths to process : 31
19/04/11 07:12:03 INFO mapreduce.JobSubmitter: number of splits:31
19/04/11 07:12:04 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1554980872030_0001
19/04/11 07:12:04 INFO impl.YarnClientImpl: Submitted application application_1554980872030_0001
19/04/11 07:12:04 INFO mapreduce.Job: The url to track the job: http://0439286d2442:8088/proxy/application_1554980872030_0001/
19/04/11 07:12:04 INFO mapreduce.Job: Running job: job_1554980872030_0001
19/04/11 07:12:14 INFO mapreduce.Job: Job job_1554980872030_0001 running in uber mode : false
19/04/11 07:12:14 INFO mapreduce.Job:  map 0% reduce 0%
19/04/11 07:12:30 INFO mapreduce.Job:  map 19% reduce 0%
19/04/11 07:12:46 INFO mapreduce.Job:  map 35% reduce 0%
19/04/11 07:12:51 INFO mapreduce.Job:  map 35% reduce 12%
19/04/11 07:12:57 INFO mapreduce.Job:  map 52% reduce 12%
19/04/11 07:13:00 INFO mapreduce.Job:  map 52% reduce 17%
19/04/11 07:13:05 INFO mapreduce.Job:  map 61% reduce 17%
19/04/11 07:13:06 INFO mapreduce.Job:  map 68% reduce 17%
19/04/11 07:13:09 INFO mapreduce.Job:  map 68% reduce 23%
19/04/11 07:13:14 INFO mapreduce.Job:  map 81% reduce 23%
19/04/11 07:13:15 INFO mapreduce.Job:  map 84% reduce 24%
19/04/11 07:13:18 INFO mapreduce.Job:  map 84% reduce 28%
19/04/11 07:13:21 INFO mapreduce.Job:  map 87% reduce 28%
19/04/11 07:13:24 INFO mapreduce.Job:  map 97% reduce 28%
19/04/11 07:13:25 INFO mapreduce.Job:  map 100% reduce 30%
19/04/11 07:13:27 INFO mapreduce.Job:  map 100% reduce 100%
19/04/11 07:13:27 INFO mapreduce.Job: Job job_1554980872030_0001 completed successfully
19/04/11 07:13:27 INFO mapreduce.Job: Counters: 49
	File System Counters
		FILE: Number of bytes read=345
		FILE: Number of bytes written=3697508
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=80529
		HDFS: Number of bytes written=437
		HDFS: Number of read operations=96
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=2
	Job Counters
		Launched map tasks=31
		Launched reduce tasks=1
		Data-local map tasks=31
		Total time spent by all maps in occupied slots (ms)=304349
		Total time spent by all reduces in occupied slots (ms)=51216
		Total time spent by all map tasks (ms)=304349
		Total time spent by all reduce tasks (ms)=51216
		Total vcore-seconds taken by all map tasks=304349
		Total vcore-seconds taken by all reduce tasks=51216
		Total megabyte-seconds taken by all map tasks=311653376
		Total megabyte-seconds taken by all reduce tasks=52445184
	Map-Reduce Framework
		Map input records=2060
		Map output records=24
		Map output bytes=590
		Map output materialized bytes=525
		Input split bytes=3812
		Combine input records=24
		Combine output records=13
		Reduce input groups=11
		Reduce shuffle bytes=525
		Reduce input records=13
		Reduce output records=11
		Spilled Records=26
		Shuffled Maps =31
		Failed Shuffles=0
		Merged Map outputs=31
		GC time elapsed (ms)=1257
		CPU time spent (ms)=20870
		Physical memory (bytes) snapshot=7554891776
		Virtual memory (bytes) snapshot=23357546496
		Total committed heap usage (bytes)=5315231744
	Shuffle Errors
		BAD_ID=0
		CONNECTION=0
		IO_ERROR=0
		WRONG_LENGTH=0
		WRONG_MAP=0
		WRONG_REDUCE=0
	File Input Format Counters
		Bytes Read=76717
	File Output Format Counters
		Bytes Written=437
19/04/11 07:13:28 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
19/04/11 07:13:28 INFO input.FileInputFormat: Total input paths to process : 1
19/04/11 07:13:29 INFO mapreduce.JobSubmitter: number of splits:1
19/04/11 07:13:29 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1554980872030_0002
19/04/11 07:13:29 INFO impl.YarnClientImpl: Submitted application application_1554980872030_0002
19/04/11 07:13:29 INFO mapreduce.Job: The url to track the job: http://0439286d2442:8088/proxy/application_1554980872030_0002/
19/04/11 07:13:29 INFO mapreduce.Job: Running job: job_1554980872030_0002
19/04/11 07:13:40 INFO mapreduce.Job: Job job_1554980872030_0002 running in uber mode : false
19/04/11 07:13:40 INFO mapreduce.Job:  map 0% reduce 0%
19/04/11 07:13:46 INFO mapreduce.Job:  map 100% reduce 0%
19/04/11 07:13:53 INFO mapreduce.Job:  map 100% reduce 100%
19/04/11 07:13:53 INFO mapreduce.Job: Job job_1554980872030_0002 completed successfully
19/04/11 07:13:53 INFO mapreduce.Job: Counters: 49
	File System Counters
		FILE: Number of bytes read=291
		FILE: Number of bytes written=230543
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=570
		HDFS: Number of bytes written=197
		HDFS: Number of read operations=7
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=2
	Job Counters
		Launched map tasks=1
		Launched reduce tasks=1
		Data-local map tasks=1
		Total time spent by all maps in occupied slots (ms)=4172
		Total time spent by all reduces in occupied slots (ms)=4358
		Total time spent by all map tasks (ms)=4172
		Total time spent by all reduce tasks (ms)=4358
		Total vcore-seconds taken by all map tasks=4172
		Total vcore-seconds taken by all reduce tasks=4358
		Total megabyte-seconds taken by all map tasks=4272128
		Total megabyte-seconds taken by all reduce tasks=4462592
	Map-Reduce Framework
		Map input records=11
		Map output records=11
		Map output bytes=263
		Map output materialized bytes=291
		Input split bytes=133
		Combine input records=0
		Combine output records=0
		Reduce input groups=5
		Reduce shuffle bytes=291
		Reduce input records=11
		Reduce output records=11
		Spilled Records=22
		Shuffled Maps =1
		Failed Shuffles=0
		Merged Map outputs=1
		GC time elapsed (ms)=45
		CPU time spent (ms)=1480
		Physical memory (bytes) snapshot=408469504
		Virtual memory (bytes) snapshot=1452711936
		Total committed heap usage (bytes)=274726912
	Shuffle Errors
		BAD_ID=0
		CONNECTION=0
		IO_ERROR=0
		WRONG_LENGTH=0
		WRONG_MAP=0
		WRONG_REDUCE=0
	File Input Format Counters
		Bytes Read=437
	File Output Format Counters
		Bytes Written=197
bash-4.1# bin/hdfs dfs -cat output/*
6	dfs.audit.logger
4	dfs.class
3	dfs.server.namenode.
2	dfs.period
2	dfs.audit.log.maxfilesize
2	dfs.audit.log.maxbackupindex
1	dfsmetrics.log
1	dfsadmin
1	dfs.servers
1	dfs.replication
1	dfs.file
bash-4.1# bin/hdfs dfs -ls
Found 2 items
drwxr-xr-x   - root supergroup          0 2015-05-16 05:43 input
drwxr-xr-x   - root supergroup          0 2019-04-11 07:13 output
bash-4.1# bin/hdfs dfs -ls output/
Found 2 items
-rw-r--r--   1 root supergroup          0 2019-04-11 07:13 output/_SUCCESS
-rw-r--r--   1 root supergroup        197 2019-04-11 07:13 output/part-r-00000
bash-4.1# bin/hdfs dfs -cat output/part-r-00000
6	dfs.audit.logger
4	dfs.class
3	dfs.server.namenode.
2	dfs.period
2	dfs.audit.log.maxfilesize
2	dfs.audit.log.maxbackupindex
1	dfsmetrics.log
1	dfsadmin
1	dfs.servers
1	dfs.replication
1	dfs.file
bash-4.1#



```
출처 : 
- https://ahea.wordpress.com/2017/07/18/docker-%EC%97%90%EC%84%9C-hadoop-%EC%9B%8C%EB%93%9C-%EC%B9%B4%EC%9A%B4%ED%8A%B8-%EC%98%88%EC%A0%9C%EB%A5%BC-%EB%8F%8C%EB%A0%A4%EB%B3%B4%EC%9E%90/
- https://hub.docker.com/r/sequenceiq/hadoop-docker


