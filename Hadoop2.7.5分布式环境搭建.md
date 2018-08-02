### Hadoop2.7.5分布式环境搭建

> 1. 免密码登录

```shell
$ ssh-keygen -t dsa -P ''
$ cd ~/.ssh/
$ cat id_dsa.pub >> authorized_keys
$ chmod 600 authorized_keys 
```



> 2. 配置环境变量

```shell
vi etc/hadoop/hadoop-env.sh

export JAVA_HOME=/usr/local/jdk1.8.0_131
export export HADOOP_CONF_DIR=/home/huwei/hadoop-2.7.5/etc/hadoop
```



> 3. 配置 `core-site.xml` 

```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://node1:9000</value>
    </property>
    <property>
        <name>io.file.buffer.size</name>
        <value>4096</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/home/huwei/hadoop-2.7.5/tmp</value>
    </property>
</configuration>
```



> 4. 配置`hdfs-site.xml`

```xml
<configuration>

    <property>
        <name>dfs.replication</name>
        <value>3</value>
    </property>

    <property>
        <name>dfs.http.address</name>
        <value>node1:50070</value>
    </property>

    <property>
        <name>dfs.secondary.http.address</name>
        <value>node1:50090</value>
    </property>

    <property>
        <name>dfs.webhdfs.enabled</name>
        <value>true</value>
    </property>

    <property>
        <name>dfs.permissions</name>
        <value>false</value>
    </property>

</configuration>
```





> 5. 配置`mapred-site.xml`

```xml

<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
        <final>true</final>
    </property>
    <property>
        <name>mapreduce.jobhistory.address</name>
        <value>node1:10020</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.webapp.address</name>
        <value>node1:19888</value>
    </property>
</configuration>
```



> 6. 配置`yarn-site.xml`

```xml
<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
    <property>
        <name>yarn.resourcemanager.address</name>
        <value>node1:8032</value>
    </property>
    <property>
        <name>yarn.resourcemanager.scheduler.address</name>
        <value>node1:8030</value>
    </property>
    <property>
        <name>yarn.resourcemanager.resource-tracker.address</name>
        <value>node1:8031</value>
    </property>
    <property>
        <name>yarn.resourcemanager.admin.address</name>
        <value>node1:8033</value>
    </property>
    <property>
        <name>yarn.resourcemanager.webapp.address</name>
        <value>node1:8088</value>
    </property>
</configuration>
```



> 7. 配置`slaves`

```shell
node1
node2
node3
```



> 8. 启动服务

```shell

$ bin/hdfs namenode -format

$ sbin/start-dfs.sh 

$ sbin/start-yarn.sh

$ sbin/mr-jobhistory-daemon.sh start historyserver

```



> 9. 页面访问

HDFS	http://node1:50070/dfshealth.html#tab-overview

YARN	http://node1:8088/cluster