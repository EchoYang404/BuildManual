# Spark构建指南

## 准备工作

- 安装SBT以及配置相关环境

可参考[使用Repox搭建快速SBT服务器](https://github.com/Blueve/BuildManual/blob/master/Prepare/%E4%BD%BF%E7%94%A8Repox%E6%90%AD%E5%BB%BA%E5%BF%AB%E9%80%9FSBT%E6%9C%8D%E5%8A%A1%E5%99%A8.md)

## Windows

### 命令行

- 编译并打包
```bash
sbt -Pyarn -Phadoop-2.6 -DskipTests assembly
```

- 编译后的Jar为
```
\assembly\target\scala-2.*\spark-assembly-*-SNAPSHOT-hadoop*.jar
```

### IntelliJ IDEA

#### SBT

- 在Spark根目录下执行`sbt assembly`
- 打开IDEA，使用Import
- 选择Spark源码目录
- 选择SBT方式构建(勾选Auto Import)
- 等待
- Build Make Project

#### Maven

- 打开IDEA，使用Import
- 选择Spark源码目录
- 选择Maven方式构建
- 等待
- Build Make Project

#### 编译问题汇总

##### 无法下载到mqttv3

手动下载jar
https://repo.eclipse.org/content/repositories/paho-releases/org/eclipse/paho/org.eclipse.paho.client.mqttv3/1.0.1/
放置到`~/.m2/.../mqttv3/`

##### QueryExecutionListener.sacla during phase: jvm

1. Build
2. Rebuild Project

##### Flume Sink相关

由于IDEA没有将flume-sink相关的文件下载下来所以导致编译错误

1. View -> Tool Windows -> Maven Project
2. 右键单击Spark Project External Flume Sink
3. 点击Generate Sources and Update Folders
4. Build -> Rebuild Project

如果上面的方法不管用，尝试以下方法

1. File -> Project Structure -> Modules
2. spark-streaming-flume-sink_*.**
3. 将target/scala-2.10/src_managed/.../flume/sink Mark as Sources
4. 将target/generated-sources, target/java, target/resolution-cache, target/scala-2.10/cache, target/streams Mark as Excluded
5. Ok, Build -> Rebuild Project

##### Maven Project运行Example项目时出现异常

1. 找到examples/spark-examples_*.**.iml
2. 将所有的`scope="PROVIDED"`删除
3. Run

##### SBT Project运行Example项目时出现异常

Case 1: SBT模块载入不完全

1. View -> Tool Windows -> SBT
2. Refrash All SBT Projects

Case 2: jetty模块冲突

1. File -> Project Structure -> Libraries
2. Delete所有`org.morbay.jetty`开头的jar包

## Ubuntu 14.04 LTS

- 待补充
