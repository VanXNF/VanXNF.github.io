---
title: Spark分布式大数据分析平台安装与配置
date: 2019-03-15 15:02:46
updated: 2019-03-15 15:02:46
tags: [大数据, Spark]
categories: Programming
---
> 大数据分析方法与应用 课程实验一

## 1.实验目的
&nbsp;&nbsp;通过本实验，搭建基于 spark 的大数据分析与设计平台，为（可能的）后续的大数据实验做准备。能够在 Linux 操作系统下 pyspark 交互式方式下运行 python spark 语句。能够使用 spark-submit 提交数据处理任务。

## 2.实验步骤
### 0.1 准备 Linux 操作系统，Ubuntu 16.04
&nbsp;&nbsp;本次采用阿里云平台**轻量应用服务器**作为搭建平台，安装的操作系统为 **Ubuntu 16.04**，以下操作均通过 Xshell 连接服务器完成，由于以 **root 账户**登录，下述命令不再以 `sudo` 命令开始。
### 0.2 安装 JDK1.8
- 首先添加源
```bash
apt-get install python-software-properties
add-apt-repository ppa:webupd8team/java
```
- 更新 source
```bash
apt-get update
```
- 安装 JDK
```bash
apt-get install oracle-java8-installer
```
- 配置环境变量
  虽然安装完成后已经可以执行 java 命令，但最好还是配置一下环境变量：
```bash
echo '#set oracle jdk environment' >> /root/.bashrc
echo 'export JAVA_HOME="/usr/lib/jvm/java-8-oracle"' >> /root/.bashrc
echo 'export JRE_HOME="${JAVA_HOME}/jre"' >> /root/.bashrc
echo 'export CLASSPATH=".:${JAVA_HOME}/lib:${JRE_HOME}/lib"' >> /root/.bashrc
echo 'export PATH="${JAVA_HOME}/bin:$PATH"' >> /root/.bashrc
source /root/.bashrc
```

![Java8 安装完成](https://upload-images.jianshu.io/upload_images/3153051-965b5b6eb67addbd.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 0.3 安装 Anaconda
&nbsp;&nbsp;本次安装的版本为 [Anaconda3-2018.12-Linux-x86_64.sh](https://repo.continuum.io/archive/Anaconda3-2018.12-Linux-x86_64.sh)。
- 首先下载 anaconda
```bash
wget https://repo.continuum.io/archive/Anaconda3-2018.12-Linux-x86_64.sh
```
- 安装 anaconda 
```bash
bash Anaconda3-2018.12-Linux-x86_64.sh
```
&nbsp;&nbsp;期间按 `Enter` 键阅读协议，同意协议后才能正常安装。可执行以下命令配置 conda 环境变量(**请自行替换 anaconda 路径**)：
```bash
echo 'export PATH="/root/anaconda3/bin:$PATH"' >> /root/.bashrc
source ~/.bashrc
```
&nbsp;&nbsp;输入`conda -V` 可查看 conda 版本，输入`conda upgrade --all` 可更新 conda版本。

![Anaconda 安装完成](https://upload-images.jianshu.io/upload_images/3153051-9f38a1061b5db265.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 0.4 安装 PySpark
&nbsp;&nbsp;安装 PySpark 可采取多种方式，
1. 使用 pip 进行安装，执行以下命令，即可完成安装：`pip install pyspark`。
    ![PySpark 安装完成](https://upload-images.jianshu.io/upload_images/3153051-5e7d84a7188059df.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. 官网下载官方包手动解压安装的方式:
- 本次安装版本为
   [**http://apache.stu.edu.tw/spark/spark-2.4.0/spark-2.4.0-bin-hadoop2.7.tgz**](http://apache.stu.edu.tw/spark/spark-2.4.0/spark-2.4.0-bin-hadoop2.7.tgz)
- 首先从官网下载 
```bash
wget http://apache.stu.edu.tw/spark/spark-2.4.0/spark-2.4.0-bin-hadoop2.7.tgz
```
- 然后解压、安装
  1. 首先解压缩
  ```bash
  tar -zxvf spark-2.4.0-bin-hadoop2.7.tgz
  ```
  2. 移动到账户文件夹下（可选）
  ```
  mv spark-2.4.0-bin-hadoop2.7 /opt/spark
  ```
  3. 配置环境变量
  ```bash
  echo '#spark' >> /root/.bashrc
  echo 'export SPARK_HOME="/opt/spark"' >> /root/.bashrc
  echo 'export PATH="$PATH:${SPARK_HOME}/bin:${SPARK_HOME}/sbin"' >> /root/.bashrc
  source /root/.bashrc
  ```
  &nbsp;&nbsp;创建 `spark-env.sh` 文件
  ```bash
  cp /opt/spark/conf/spark-env.sh.template /opt/spark/conf/spark-env.sh
  ```
  &nbsp;&nbsp;在里面写入：
  ```bash
  JAVA_HOME=/usr/lib/jvm/jdk1.8.0_181
  SPARK_WORKER_MEMORY=1g
  ```
  &nbsp;&nbsp;使用内存大小根据机器配置自行选择。
  4. 问题解决
      &nbsp;&nbsp;在服务器端无论使用 pip 还是手动安装，在启动时收获一个异常：
      ![Exception: Java gateway process exited before sending its port number](https://upload-images.jianshu.io/upload_images/3153051-ec783289605be077.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
      ~~对于**该异常目前搜遍了谷歌百度尚无较好的解决方案**~~，已解决，请参看 {% post_link Exception-Java-gateway-process-exited-before-sending-its-port-number-解决方案 %}

### 0.5 配置 PySpark
- 第1步 配置 Spark standalone 模式
  - 1.1 运行 `pyspark`
  - 1.2 执行以下代码
  ```
  textFile = spark.read.text("/opt/spark/README.md")
  textFile.count()
  ```
  输出结果为 `105`。

- 第2步 配置 singlenode cluster 模式
  - 2.1 配置 `conf/slaves` 文件，增加 localhost
  ```
  cp /opt/spark/conf/slaves.template /opt/spark/conf/slaves
  ```
  在文件内增加一行 `localhost`
  ![slaves](https://upload-images.jianshu.io/upload_images/3153051-0e7d3fb03df31147.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  - 2.2 执行`sbin/start-master.sh` 查看 `http://服务器 ip:8080`


![start-master](https://upload-images.jianshu.io/upload_images/3153051-44123c7d5ab9d478.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  - 2.3 `sbin/start-slaves.sh spark://127.0.0.1:7077` 查看 `http://服务器 ip:8080`
    ![workers](https://upload-images.jianshu.io/upload_images/3153051-7852cf287b263124.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  - 2.4 运行 `/bin/pyspark --master spark://127.0.0.1:7077` 
    ![pyspark master](https://upload-images.jianshu.io/upload_images/3153051-0b4d15b1e6b9d190.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  - 2.5（退出上一步的交互式环境）运行Spark例子：
  ```bash
  ./bin/spark-submit  --master spark://127.0.0.1:7077 ./examples/src/main/python/pi.py 1000
  ```
&nbsp;&nbsp;查看 `http://服务器 ip:8080` 中的信息
![spark-submit](https://upload-images.jianshu.io/upload_images/3153051-53872597b2d5de72.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


- 第3步 愉快的开始spark Python编程

### 0.6 实验总结与收获

&nbsp;&nbsp;在实验中，日志很重要，遇到问题时首先查看错误错误日志，根据日志解决问题将事半功倍。