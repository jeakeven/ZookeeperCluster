
# ZookeeperCluster
Zookeeper伪分布式集群，在同一台pc上启动多个zookeeper实例

1、更改zookeeper0/conf/zoo.cfg文件为:

Bash代码
tickTime=2000
initLimit=5
syncLimit=2
dataDir=/Users/apple/zookeeper0/data
dataLogDir=/Users/apple/zookeeper0/logs
clientPort=4180
server.0=127.0.0.1:8880:7770
server.1=127.0.0.1:8881:7771
server.2=127.0.0.1:8882:7772


2、在之前设置的dataDir中新建myid文件, 写入一个数字, 该数字表示这是第几号server. 
该数字必须和zoo.cfg文件中的server.X中的X一一对应.
/Users/apple/zookeeper0/data/myid文件中写入0
/Users/apple/zookeeper1/data/myid文件中写入1
/Users/apple/zookeeper2/data/myid文件中写入2.


3、分别进入/Users/apple/zookeeper0/bin, /Users/apple/zookeeper1/bin, /Users/apple/zookeeper2/bin三个目录, 
分别启动server，命令：./zkServer.sh start

启用成功后，输入 jps 看下进程
20351 ZooKeeperMain
20791 QuorumPeerMain
20822 QuorumPeerMain
20865 QuorumPeerMain


4、任意选择一个server目录, 启动客户端:
Bash代码
./zkCli.sh -server localhost:4180
