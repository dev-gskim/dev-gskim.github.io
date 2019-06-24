---
title: "CDH oozie 에서 Sqoop 실행"
date: 2019-03-29 08:26:28 -0400
categories: jekyll update
---

## CDH oozie 에서 sqoop 실행
> hue 에서 workflow 실행시 shell 로 sqoop 실행시 다음과 같은 오류가 발생했다.
~~~sh
SLF4J: Found binding in [jar:file:/opt/cloudera/parcels/CDH-6.1.1-1.cdh6.1.1.p0.875250/jars/slf4j-log4j12-1.7.25.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/opt/cloudera/parcels/CDH-6.1.1-1.cdh6.1.1.p0.875250/jars/log4j-slf4j-impl-2.8.2.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.slf4j.impl.Log4jLoggerFactory]
19/03/29 16:32:56 INFO sqoop.Sqoop: Running Sqoop version: 1.4.7-cdh6.1.1
19/03/29 16:32:56 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/03/29 16:32:56 INFO tool.BaseSqoopTool: Using Hive-specific delimiters for output. You can override
19/03/29 16:32:56 INFO tool.BaseSqoopTool: delimiters with --fields-terminated-by, etc.
19/03/29 16:32:56 INFO manager.SqlManager: Using default fetchSize of 1000
19/03/29 16:32:56 INFO tool.CodeGenTool: Beginning code generation
19/03/29 16:32:56 INFO tool.CodeGenTool: Will generate java class as codegen_table1
19/03/29 16:32:56 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM "table1" AS t LIMIT 1
19/03/29 16:32:56 INFO orm.CompilationManager: HADOOP_MAPRED_HOME is /opt/cloudera/parcels/CDH-6.1.1-1.cdh6.1.1.p0.875250/lib/hadoop-mapreduce
19/03/29 16:32:58 INFO orm.CompilationManager: Writing jar file: /tmp/sqoop-yarn/compile/3620bab4f73431832875cd2a87403c4e/codegen_table1.jar
19/03/29 16:32:58 WARN manager.PostgresqlManager: It looks like you are importing from postgresql.
19/03/29 16:32:58 WARN manager.PostgresqlManager: This transfer can be faster! Use the --direct
19/03/29 16:32:58 WARN manager.PostgresqlManager: option to exercise a postgresql-specific fast path.
19/03/29 16:32:58 WARN manager.CatalogQueryManager: The table table1 contains a multi-column primary key. Sqoop will default to the column site_seq only for this job.
19/03/29 16:32:58 WARN manager.CatalogQueryManager: The table table1 contains a multi-column primary key. Sqoop will default to the column site_seq only for this job.
19/03/29 16:32:58 INFO mapreduce.ImportJobBase: Beginning import of table1
19/03/29 16:32:58 INFO Configuration.deprecation: mapred.jar is deprecated. Instead, use mapreduce.job.jar
19/03/29 16:32:58 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM "table1" AS t LIMIT 1
19/03/29 16:32:58 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM "table1" AS t LIMIT 1
19/03/29 16:32:58 INFO conf.HiveConf: Found configuration file file:/etc/hive/conf.cloudera.hive/hive-site.xml
19/03/29 16:32:59 INFO hive.metastore: Trying to connect to metastore with URI thrift://hadoop1:9083
19/03/29 16:32:59 INFO hive.metastore: Opened a connection to metastore, current connections: 1
19/03/29 16:32:59 INFO hive.metastore: Connected to metastore.
19/03/29 16:33:00 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
19/03/29 16:33:00 INFO client.RMProxy: Connecting to ResourceManager at hadoop1/192.168.3.21:8032
19/03/29 16:33:00 ERROR tool.ImportTool: Import failed: org.apache.hadoop.security.AccessControlException: Permission denied: user=yarn, access=WRITE, inode="/user/yarn":hdfs:supergroup:drwxr-xr-x
	at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.check(FSPermissionChecker.java:400)
	at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkPermission(FSPermissionChecker.java:256)
	at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkPermission(FSPermissionChecker.java:194)
	at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkPermission(FSDirectory.java:1855)
	at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkPermission(FSDirectory.java:1839)
	at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkAncestorAccess(FSDirectory.java:1798)
	at org.apache.hadoop.hdfs.server.namenode.FSDirMkdirOp.mkdirs(FSDirMkdirOp.java:60)
	at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.mkdirs(FSNamesystem.java:3099)
	at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.mkdirs(NameNodeRpcServer.java:1123)
	at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.mkdirs(ClientNamenodeProtocolServerSideTranslatorPB.java:696)
	at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
	at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:523)
	at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:991)
	at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:869)
	at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:815)
	at java.security.AccessController.doPrivileged(Native Method)
	at javax.security.auth.Subject.doAs(Subject.java:422)
	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1731)
	at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2675)

	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
	at org.apache.hadoop.ipc.RemoteException.instantiateException(RemoteException.java:121)
	at org.apache.hadoop.ipc.RemoteException.unwrapRemoteException(RemoteException.java:88)
	at org.apache.hadoop.hdfs.DFSClient.primitiveMkdir(DFSClient.java:2335)
	at org.apache.hadoop.hdfs.DFSClient.mkdirs(DFSClient.java:2309)
	at org.apache.hadoop.hdfs.DistributedFileSystem$27.doCall(DistributedFileSystem.java:1247)
	at org.apache.hadoop.hdfs.DistributedFileSystem$27.doCall(DistributedFileSystem.java:1244)
	at org.apache.hadoop.fs.FileSystemLinkResolver.resolve(FileSystemLinkResolver.java:81)
	at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirsInternal(DistributedFileSystem.java:1261)
	at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirs(DistributedFileSystem.java:1236)
	at org.apache.hadoop.mapreduce.JobSubmissionFiles.getStagingDir(JobSubmissionFiles.java:162)
	at org.apache.hadoop.mapreduce.JobSubmissionFiles.getStagingDir(JobSubmissionFiles.java:113)
	at org.apache.hadoop.mapreduce.JobSubmitter.submitJobInternal(JobSubmitter.java:148)
	at org.apache.hadoop.mapreduce.Job$11.run(Job.java:1570)
	at org.apache.hadoop.mapreduce.Job$11.run(Job.java:1567)
	at java.security.AccessController.doPrivileged(Native Method)
	at javax.security.auth.Subject.doAs(Subject.java:422)
	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1731)
	at org.apache.hadoop.mapreduce.Job.submit(Job.java:1567)
	at org.apache.hadoop.mapreduce.Job.waitForCompletion(Job.java:1588)
	at org.apache.sqoop.mapreduce.ImportJobBase.doSubmitJob(ImportJobBase.java:202)
	at org.apache.sqoop.mapreduce.ImportJobBase.runJob(ImportJobBase.java:175)
	at org.apache.sqoop.mapreduce.ImportJobBase.runImport(ImportJobBase.java:272)
	at org.apache.sqoop.manager.SqlManager.importTable(SqlManager.java:691)
	at org.apache.sqoop.manager.PostgresqlManager.importTable(PostgresqlManager.java:126)
	at org.apache.sqoop.tool.ImportTool.importTable(ImportTool.java:534)
	at org.apache.sqoop.tool.ImportTool.run(ImportTool.java:633)
	at org.apache.sqoop.Sqoop.run(Sqoop.java:146)
	at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
	at org.apache.sqoop.Sqoop.runSqoop(Sqoop.java:182)
	at org.apache.sqoop.Sqoop.runTool(Sqoop.java:233)
	at org.apache.sqoop.Sqoop.runTool(Sqoop.java:242)
	at org.apache.sqoop.Sqoop.main(Sqoop.java:251)
Caused by: org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.security.AccessControlException): Permission denied: user=yarn, access=WRITE, inode="/user/yarn":hdfs:supergroup:drwxr-xr-x
	at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.check(FSPermissionChecker.java:400)
	at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkPermission(FSPermissionChecker.java:256)
	at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkPermission(FSPermissionChecker.java:194)
	at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkPermission(FSDirectory.java:1855)
	at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkPermission(FSDirectory.java:1839)
	at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkAncestorAccess(FSDirectory.java:1798)
	at org.apache.hadoop.hdfs.server.namenode.FSDirMkdirOp.mkdirs(FSDirMkdirOp.java:60)
	at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.mkdirs(FSNamesystem.java:3099)
	at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.mkdirs(NameNodeRpcServer.java:1123)
	at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.mkdirs(ClientNamenodeProtocolServerSideTranslatorPB.java:696)
	at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
	at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:523)
	at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:991)
	at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:869)
	at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:815)
	at java.security.AccessController.doPrivileged(Native Method)
	at javax.security.auth.Subject.doAs(Subject.java:422)
	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1731)
	at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2675)

	at org.apache.hadoop.ipc.Client.getRpcResponse(Client.java:1499)
	at org.apache.hadoop.ipc.Client.call(Client.java:1445)
	at org.apache.hadoop.ipc.Client.call(Client.java:1355)
	at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:228)
	at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:116)
	at com.sun.proxy.$Proxy11.mkdirs(Unknown Source)
	at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.mkdirs(ClientNamenodeProtocolTranslatorPB.java:640)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:422)
	at org.apache.hadoop.io.retry.RetryInvocationHandler$Call.invokeMethod(RetryInvocationHandler.java:165)
	at org.apache.hadoop.io.retry.RetryInvocationHandler$Call.invoke(RetryInvocationHandler.java:157)
	at org.apache.hadoop.io.retry.RetryInvocationHandler$Call.invokeOnce(RetryInvocationHandler.java:95)
	at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:359)
	at com.sun.proxy.$Proxy12.mkdirs(Unknown Source)
	at org.apache.hadoop.hdfs.DFSClient.primitiveMkdir(DFSClient.java:2333)
	... 29 more
~~~
> yarn이 권한이 없다는 것으로 다음과 같이 supergroup을 전 클러스터 서버에 추가하고 ( 몇대 안되긴 했다. )
> yarn에 supergroup 그룹을 추가했다.
> 이후 정상적으로 동작하는 것을 확인했다.
~~~sh
groupadd supergroup
usermod -a -G supergroup yarn
~~~
  
