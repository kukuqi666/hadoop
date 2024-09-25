# 为了在国内环境中加速下载 Hadoop，你可以使用以下国内镜像站点（脚本里面用的清华源）：

    1.
    清华大学开源软件镜像站：
        链接：https://mirrors.tuna.tsinghua.edu.cn/apache/hadoop/common/
        使用说明：访问上述链接，选择你需要的 Hadoop 版本进行下载。
    2.
    阿里云开源镜像站：
        链接：https://mirrors.aliyun.com/apache/hadoop/common/
        使用说明：阿里云提供的开源镜像站点同样提供 Hadoop 的免费下载服务，你可以通过该链接访问并下载所需的 Hadoop 版本。
    3.
	Apache镜像站：
	    链接：https://downloads.apache.org/hadoop/common/
	    使用说明：访问上述链接，选择你需要的（下载会特别慢 建议选择上面的两个）		




# CentOS7 更换镜像源(如果在虚拟机里面建议更换阿里源，不然可能无法使用脚本哦)


首先安装 wget

yum -y install wget

## 一、备份

```
cp /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

## 二、下载新的CentOS-Base.repo 到/etc/yum.repos.d/

**CentOS 5**
```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-5.repo

或者

curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-5.repo
```

**CentOS 6**
```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo

或者

curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
```

**CentOS 7**
```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo

或

curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

## 三、添加EPEL

**CentOS 6**
```
wget -O /etc/yum.repos.d/epel-6.repo http://mirrors.aliyun.com/repo/epel-6.repo
```

**CentOS 7**
```
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
```

## 四、清理缓存并生成新的缓存

```
yum clean all

yum makecache
```
## 五、更新源

```
yum update
```



# 适用于centos 7 Hadoop的傻瓜式安装脚本


```
wget -o /usr/local/bin https://raw.githubusercontent.com/kukuqi666/hadoop/main/hadoop/target/hadoop_install

wget -o /usr/local/bin https://raw.githubusercontent.com/kukuqi666/hadoop/main/hadoop/target/hadoop_server

```




























# Hadoop 常用命令


## 启动和停止Hadoop集群

启动所有Hadoop守护进程：

```
$HADOOP_HOME/sbin/start-all.sh
```

停止所有Hadoop守护进程：

```
$HADOOP_HOME/sbin/stop-all.sh
```

启动NameNode守护进程：

```
$HADOOP_HOME/sbin/hadoop-daemon.sh start namenode
```

启动DataNode守护进程：

```
$HADOOP_HOME/sbin/hadoop-daemon.sh start datanode
```

启动ResourceManager守护进程：

```
$HADOOP_HOME/sbin/yarn-daemon.sh start resourcemanager
```

启动NodeManager守护进程：

``` 
$HADOOP_HOME/sbin/yarn-daemon.sh start nodemanager
```

文件系统操作

查看HDFS文件系统：

```
hdfs dfs -ls [path]
```

创建目录：

```
hdfs dfs -mkdir -p [path]
```

删除文件或目录：

```
hdfs dfs -rm -r [path]
```

上传文件到HDFS：

```
hdfs dfs -put localpath hdfspath
```

从HDFS下载文件：

```
hdfs dfs -get hdfspath localpath
```

复制HDFS中的文件：

```
hdfs dfs -cp src_path dest_path
```

移动/重命名HDFS中的文件：

```
hdfs dfs -mv src_path dest_path
```

查看Hadoop集群状态

    查看NameNode状态：

jps # 查看Java进程，NameNode通常在里面
hdfs dfsadmin -report # 查看HDFS状态

查看ResourceManager状态：

    yarn resourcemanager admin -status

运行MapReduce作业

    提交作业：

hadoop jar your-job.jar MainClassName [args...]

查看作业状态：

yarn application -status Application_ID

杀死作业：

    yarn application -kill Application_ID

查看日志文件

    查看NameNode日志：

cat $HADOOP_HOME/logs/*namenode*.log

查看DataNode日志：

cat $HADOOP_HOME/logs/*datanode*.log

查看ResourceManager日志：

cat $HADOOP_HOME/logs/*resourcemanager*.log

查看NodeManager日志：

    cat $HADOOP_HOME/logs/*nodemanager*.log

HDFS管理

    安全模式：

hdfs dfsadmin -safemode enter # 进入安全模式
hdfs dfsadmin -safemode leave # 退出安全模式

元数据信息：

hdfs dfsadmin -metasave filename # 保存元数据到文件

启用/禁用平衡器：
```
    yarn balancer # 查看是否启用
    yarn balancer -t 100 # 设置100秒的间隔启用平衡器
```
YARN管理

    资源管理器状态：
```
yarn rmadmin -status
```
节点管理器状态：
```
yarn node -status [node_id]
```
杀掉NodeManager：
```
    yarn rmadmin -refreshNodes
```
其他

    查看Hadoop版本：
	
```
hadoop version
```

查看Hadoop配置：

```
hdfs getconf -confKey [key]
```










# CentOS 7 下的 Hadoop 一键脚本（老版本已弃用）

## 使用方法

脚本完成的是Hadoop的分布式集群配置
包含wordcount例子 (在wordcount文件夹下面)

单机版配置方法请看下面的注意事项

前提条件：

- 登录用户具有sudo权限（root也可）
- 具有网络连接
- 安装了git
  - 如果服务器上没有git，可以把文件复制到服务器上。
  - 使用 `sudo yum install git` 安装git


## 运行方式

运行脚本安装
```bash
git clone https://github.com/kukuqi666/hadoop.git
cd hadoop
chmod +x hadoop.sh
./hadoop.sh
```

运行wordcount测试
```bash
cd wordcount
chmod +x wordcount.sh
./wordcount.sh
```

wordcount 统计性别的输入文件路径: `input/data/*.txt`
注意使用Local编译。

## 说明

- hosts.txt文件里的hosts记录会被追加到 `/etc/hosts` 里；未修改hostname。
- jdk和hadoop文件在这个账户目录下，系统变量使用用户配置文件的设置，不会和系统配置冲突。
- 自定义hadoop配置文件在项目的 `etc` 目录下
- 脚本使用了 `hostname -I` 获取本机IP地址
- 会为当前账户生成一个 *~/.ssh/id_rsa* 的RSA非对称密钥，注意冲突。
- 使用 `LANG=zh_CN.UTF-8` 设置为中文显示，有些Terminal可能不支持显示
- 脚本会在 `~/hadoop_files` 下放置HDFS文件，可通过修改xml文件自定义
- jdk和hadoop文件是直接从ftp上下载的，Local选项仅用作Debug


- wordcount测试文件在 `wordcount/input` 下面，可自行替换
### 注意
- `etc/hadoop/core-site.xml` 里面的路径 *hadoop.tmp.dir* 可能需要修改为自己的用户目录
- 如果想体验单机版

  1. 把 `hosts.txt` 中的ip映射修改为只留下master，注意设置本机ip。
  2. 把 `etc/masters` 里的其他清空，只留下本机（填写 `localhost` 或者 `master`）
  3. 把 `etc/slaves` 里清空（因为不需要其他机器）
  4. 把 `etc/hdfs-site.xml` 里的 *dfs.namenode.secondary.http-address* 记录删除掉，因为没有第二台机器放置namenode。
