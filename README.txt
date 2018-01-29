# 复用Hive ODBC实现Tableau到MaxCompute的连通
阿里云文章[利用HiveServer2 Proxy实现MaxCompute与Hive生态工具的互通](https://yq.aliyun.com/articles/61262)，增加了认证配置，默认无认证，详情参考 <https://cwiki.apache.org/confluence/display/Hive/Setting+Up+HiveServer2>

将下载到的压缩包解压，得到名为apache-hive-2.1.0-odps-proxy的文件夹。设置好HIVE_HOME环境变量：

```shell
cd ./apache-hive-2.1.0-odps-proxy
export HIVE_HOME=$(pwd)
echo $HIVE_HOME
#/tmp/apache-hive-2.1.0-odps-proxy
```

如果你安装了hadoop请配置环境变量HADOOP_HOME，如果跳过没有安装的，可以使用proxy自带的hadoop依赖，即根目录下的hadoop目录。可以在根目录下执行如下命令：

```shell
cd ./apache-hive-2.1.0-odps-proxy
export HADOOP_HOME=$(pwd)/hadoop
```
完成环境变量的配置之后进入根目录下的conf文件夹，修改hive-site.xml中的相关配置项，样例如下所示，其中每一项的说明已在description标签中有所描述：

只需要修改odps.accessid、odps.accesskey、odps.project及odps.projects四项即可，其余项可以保留默认配置。如果20000端口已被占用，可以通过hive.server2.thrift.port更换端口配置。

完成相关配置之后，请回到根目录，执行`bin/hiveserver2`启动proxy。
