# CentOS7 更换镜像源(如果在虚拟机里面建议更换阿里源，不然可能无法使用脚本哦)

## 首先安装 wget

```
yum -y install wget
```

## 一、备份

```
cp /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

## 二、下载新的CentOS-Base.repo 到/etc/yum.repos.d/

```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo

或

curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

## 三、添加EPEL

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

# 国内云服务器访问GitHub

**使用一下脚本可能会出现443的错误 是因为github服务器的原因 国内访问会出现以下情况 那么就使用github镜像站**

1. 使用 GitHub 镜像站

镜像站是 GitHub 的内容副本，可以通过以下镜像站加速访问：

**GitHub 镜像站：**

```
https://github.com.cnpmjs.org/
https://hub.fastgit.org/
https://github.wuyou.workers.dev/
```

2. 修改 Hosts 文件

通过手动修改 hosts 文件，直接解析 GitHub 域名到更快的 IP 地址。可以通过以下步骤操作：

    打开 https://www.ipaddress.com/，输入 github.com，获取 GitHub 的最新 IP
    编辑云服务器的 hosts 文件：
```
sudo vim /etc/hosts
```

添加 GitHub 相关的 IP 地址：

```
    140.82.114.4 github.com
    185.199.108.153 assets-cdn.github.com
    151.101.185.194 github.global.ssl.fastly.net
```
    保存并退出，刷新 DNS 缓存。 





# 适用于centos 7 Hadoop的傻瓜式安装脚本（在root用户根目录下运行脚本）

## Hadoop一键安装脚本 安装完以后就可以不用这个脚本了

```
wget -o /usr/local/bin/hadoop_install https://raw.githubusercontent.com/kukuqi666/hadoop/main/hadoop/target/hadoop_install && chmod +x /usr/local/bin/hadoop_install && hadoop_install
```

## Hadoop启动和停止脚本 等安装完Hadoop以后就可以使用这个脚本进行启动和关闭了

```
wget -o /usr/local/bin/hadoop_server https://raw.githubusercontent.com/kukuqi666/hadoop/main/hadoop/target/hadoop_server && chmod +x /usr/local/bin/hadoop_server
```

### 如果不能用尝试从releases下载

```
wget https://github.com/kukuqi666/hadoop/releases/download/v1.0.0/hadoop_install && chmod +x hadoop_install && ./hadoop_install
```

```
wget https://github.com/kukuqi666/hadoop/releases/download/v1.0.0/hadoop_server && chmod +x hadoop_server
```

```
./hadoop_server
```

## 安装脚本的相关说明

### 这是刚进入hadoop_install的安装页面 回车或空格进行运行脚本

![image](https://gitee.com/kukuqi666/images/raw/master/1001.png)

### 这里看个人情况选择 我是用的3.3.6版本

![image](https://gitee.com/kukuqi666/images/raw/master/1002.png)

### ssh配置免密登录选择 y 即可

![image](https://gitee.com/kukuqi666/images/raw/master/1003.png)

### 安装完成界面 可以通过上面的IP访问web页面

![image](https://gitee.com/kukuqi666/images/raw/master/1004.png)

### 输入**jps**查看hadoop运行状态 也可以通过**netstat -tunlp**来查看端口和进程

![image](https://gitee.com/kukuqi666/images/raw/master/1005.png)

### 后面的开启和关闭hadoop使用hadoop_server即可 hadoop_install用不到了

![image](https://gitee.com/kukuqi666/images/raw/master/1006.png)

### 上面图片已经关闭hadoop服务了 现在输入**jps**和**netstat -tunlp**就不显示进程了

![image](https://gitee.com/kukuqi666/images/raw/master/1007.png)

### 参考视频

[![Hadoop安装脚本适用于centos 7](https://gitee.com/kukuqi666/images/raw/master/1009.png)](https://www.bilibili.com/video/BV1nkxjezEsy/)



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





# Hadoop 常用命令


Hadoop是一个开源框架，允许使用简单的编程模型来分布式地处理大规模数据集。以下是一些常用的Hadoop命令：

1. **启动和停止Hadoop集群**
   - 启动所有Hadoop守护进程：
     ```
     $HADOOP_HOME/sbin/start-all.sh
     ```
   - 停止所有Hadoop守护进程：
     ```
     $HADOOP_HOME/sbin/stop-all.sh
     ```
   - 启动NameNode守护进程：
     ```
     $HADOOP_HOME/sbin/hadoop-daemon.sh start namenode
     ```
   - 启动DataNode守护进程：
     ```
     $HADOOP_HOME/sbin/hadoop-daemon.sh start datanode
     ```
   - 启动ResourceManager守护进程：
     ```
     $HADOOP_HOME/sbin/yarn-daemon.sh start resourcemanager
     ```
   - 启动NodeManager守护进程：
     ```
     $HADOOP_HOME/sbin/yarn-daemon.sh start nodemanager
     ```

2. **文件系统操作**
   - 查看HDFS文件系统：
     ```
     hdfs dfs -ls [path]
     ```
   - 创建目录：
     ```
     hdfs dfs -mkdir -p [path]
     ```
   - 删除文件或目录：
     ```
     hdfs dfs -rm -r [path]
     ```
   - 上传文件到HDFS：
     ```
     hdfs dfs -put localpath hdfspath
     ```
   - 从HDFS下载文件：
     ```
     hdfs dfs -get hdfspath localpath
     ```
   - 复制HDFS中的文件：
     ```
     hdfs dfs -cp src_path dest_path
     ```
   - 移动/重命名HDFS中的文件：
     ```
     hdfs dfs -mv src_path dest_path
     ```

3. **查看Hadoop集群状态**
   - 查看NameNode状态：
     ```
     jps # 查看Java进程，NameNode通常在里面
     hdfs dfsadmin -report # 查看HDFS状态
     ```
   - 查看ResourceManager状态：
     ```
     yarn resourcemanager admin -status
     ```

4. **运行MapReduce作业**
   - 提交作业：
     ```
     hadoop jar your-job.jar MainClassName [args...]
     ```
   - 查看作业状态：
     ```
     yarn application -status Application_ID
     ```
   - 杀死作业：
     ```
     yarn application -kill Application_ID
     ```

5. **查看日志文件**
   - 查看NameNode日志：
     ```
     cat $HADOOP_HOME/logs/*namenode*.log
     ```
   - 查看DataNode日志：
     ```
     cat $HADOOP_HOME/logs/*datanode*.log
     ```
   - 查看ResourceManager日志：
     ```
     cat $HADOOP_HOME/logs/*resourcemanager*.log
     ```
   - 查看NodeManager日志：
     ```
     cat $HADOOP_HOME/logs/*nodemanager*.log
     ```

6. **HDFS管理**
   - 安全模式：
     ```
     hdfs dfsadmin -safemode enter # 进入安全模式
     hdfs dfsadmin -safemode leave # 退出安全模式
     ```
   - 元数据信息：
     ```
     hdfs dfsadmin -metasave filename # 保存元数据到文件
     ```
   - 启用/禁用平衡器：
     ```
     yarn balancer # 查看是否启用
     yarn balancer -t 100 # 设置100秒的间隔启用平衡器
     ```

7. **YARN管理**
   - 资源管理器状态：
     ```
     yarn rmadmin -status
     ```
   - 节点管理器状态：
     ```
     yarn node -status [node_id]
     ```
   - 杀掉NodeManager：
     ```
     yarn rmadmin -refreshNodes
     ```

8. **其他**
   - 查看Hadoop版本：
     ```
     hadoop version
     ```
   - 查看Hadoop配置：
     ```
     hdfs getconf -confKey [key]
     ```

请确保在执行这些命令之前，你已经正确设置了Hadoop的环境变量，并且Hadoop服务已经启动。此外，这些命令可能需要根据你的Hadoop版本和配置进行适当的调整。



# Hadoop安装目录 可根据自己的需求修改

在使用Hadoop的过程中，有几个关键的目录需要了解，因为它们存储了Hadoop运行时的重要数据和配置文件。以下是一些Hadoop常用的目录：

1. **Hadoop安装目录**：
   - 这是Hadoop的安装位置，通常在`/usr/local/hadoop`或者你解压Hadoop压缩包的目录。

2. **配置目录**：
   - `$HADOOP_HOME/etc/hadoop/`：存放Hadoop的配置文件，如`core-site.xml`、`hdfs-site.xml`、`mapred-site.xml`和`yarn-site.xml`。

3. **临时工作目录**：
   - `$HADOOP_HOME/tmp`：Hadoop的临时工作目录，用于存放临时文件。

4. **日志目录**：
   - `$HADOOP_HOME/logs/`：存放Hadoop的日志文件，包括NameNode、DataNode、ResourceManager、NodeManager等守护进程的日志。

5. **NameNode的元数据存储目录**：
   - `$HDFS_NAMENODE_NAME_DIR`：NameNode的元数据存储位置，默认在`$HADOOP_HOME/tmp/hadoop-hdfs/namenode`。

6. **DataNode的数据存储目录**：
   - `$HDFS_DATANODE_DATA_DIR`：DataNode的数据存储位置，默认在`$HADOOP_HOME/tmp/hadoop-hdfs/datanode`。

7. **MapReduce框架的临时存储目录**：
   - `$HADOOP_MAPRED_LOCAL_DIR`：MapReduce作业的临时数据存储位置，默认在`$HADOOP_HOME/tmp/hadoop-mapred/mapred/local`。

8. **YARN的临时目录**：
   - `$YARN_LOCAL_DIRS`：YARN框架的临时目录，用于存放NodeManager的临时数据，默认在`$HADOOP_HOME/tmp/hadoop-yarn/nm-local-dir`。

9. **HDFS存储目录**：
   - 用户上传到HDFS的文件和目录默认存储在`/user`目录下。

10. **Hadoop二进制目录**：
    - `$HADOOP_HOME/bin`：存放Hadoop的可执行文件，如`hadoop`、`hdfs`、`yarn`等。

11. **Hadoop库目录**：
    - `$HADOOP_HOME/lib`：存放Hadoop的库文件。

12. **Hadoop的sbin目录**：
    - `$HADOOP_HOME/sbin`：存放用于启动和停止Hadoop守护进程的脚本。

13. **Hadoop的web界面访问地址**：
    - NameNode的默认访问地址是`http://<namenode-host>:9870/`。
    - ResourceManager的默认访问地址是`http://<resourcemanager-host>:8088/`。

请根据你的实际安装路径和配置来确定这些目录的确切位置。在生产环境中，这些目录通常位于高性能的存储系统上，以确保Hadoop集群的高效运行。








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
rm -rf hadoop
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
