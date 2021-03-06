## kafka
1.查询全部的topic
```
./bin/kafka-topics.sh --zookeeper localhost:2181 --list
```

2.创建执行分区数的topic
```
./bin/kafka-topics.sh --create --topic test_t3_java_log_a_10000_00125  --zookeeper 10.25.151.169:2181 --partitions 10 --replication-factor 1
```

3.查询指定topic的当前offset情况
```
./bin/kafka-run-class.sh kafka.tools.GetOffsetShell --broker-list 127.0.0.1:9092 --topic test-log --time -1
```

4.新增指定topic的分区数
```
./bin/kafka-topics.sh --zookeeper  10.25.246.47:2181  --alter --partitions 13 --topic  t3_java_log_a_10000_test1
```

## Linux
1.查看当前路径下指定所有包含00099的文件的总大小，单位kb 
```
du -sk 00099 | awk '{c+=$1}END{print c}'
```

2.查看指定路径下包含00099的文件的总大小

```
find /data/test/day -name "00099" |xargs du -ck
```

3.查看指定路径下指定类型文件的包含指定内容的总行数
```
find 00099.dat.l | xargs grep "2019-04-07 20" | wc -l
```

4.查看当前进程号的所有tcp链接
```
lsof -p 11771 -nP | grep TCP
```

5.挂载本地ios镜像

5.1 上传ISO镜像至系统目录/root，使用mount命令挂载镜像至/mnt
```
[root@yc ~]# mount /root/CentOS-7-x86_64-DVD-1708.iso /mnt -o loop
```
5.2 创建本地的repo文件,编辑文件/etc/yum.repos.d/local.repo
```
[root@yc ~]# vi /etc/yum.repos.d/local.repo
```
5.3 写入以下内容，file后面的/mnt目录与上一节中ISO挂载目录保持一致
```
[local]
name=local
baseurl=file:///mnt
enabled=1
gpgcheck=0
```
5.4 移动默认的配置文件到上一层
```
mv /etc/yum.repos.d/Centos-* ../
```
5.5 清理yum
```
yum clean all
```
5.6 查看yum挂载情况
```
yum list
```

6.CPU
```
# 总核数 = 物理CPU个数 X 每颗物理CPU的核数 
# 总逻辑CPU数 = 物理CPU个数 X 每颗物理CPU的核数 X 超线程数

# 查看物理CPU个数
cat /proc/cpuinfo| grep &quot;physical id&quot;| sort| uniq| wc -l

# 查看每个物理CPU中core的个数(即核数)
cat /proc/cpuinfo| grep &quot;cpu cores&quot;| uniq

# 查看逻辑CPU的个数
cat /proc/cpuinfo| grep &quot;processor&quot;| wc -l

#查看CPU信息（型号）
cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c
```

7.查看当前系统版本
```
# 查看版本
cat /etc/issue

# 查看CentOS版本
cat /etc/redhat-release

# 查看主机和版本信息
uname -a

# 查看系统是32位或者64位的方法
getconf LONG_BIT 
getconf WORD_BIT
```

## Vim
1.vim打开文件后删除指定长度的内容（修改里面的10）
```
:%s/^.{10}//
```

2.批量删除指定列
```
:1 切换到行首
ctrl+v  这样会启动可视模式，按 j/k 可以发现它能够在一列上面选中字符
按下 G 这样可以从文本的第一行选中到最后一行
按下 x 就会把这一列删掉
 :sort 排序
```

## Curl
1.上传文件 
```
[root]# curl http://127.0.0.1:18081/file/batchUpload -X POST -F "filePath=@/data/shell/1554947856915.log"  -F "filePath=@/data/shell/1554947856915.log" --header "Content-Type:multipart/form-data"  -v
```
```
[root]# curl http://127.0.0.1:18081/file/batchUpload -X POST -F "filePath=@/data/shell/1554947856915.log"  -F "filePath=@/data/shell/1554947856915.log" --header "Content-Type:multipart/form-data"  -v
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 18081 (#0)
> POST /file/batchUpload HTTP/1.1
> Host: 127.0.0.1:18081
> User-Agent: curl/7.57.0
> Accept: */*
> Content-Length: 963
> Content-Type: multipart/form-data; boundary=------------------------d426837656228ad7
> 
< HTTP/1.1 200 OK
< Server: gunicorn/19.9.0
< Date: Tue, 23 Apr 2019 07:24:28 GMT
< Connection: close
< Content-Type: text/html; charset=utf-8
< Content-Length: 178
< 
* Closing connection 0
{"code": "000000", "desc": "success", "data": {"1554947856915.log": "000000", "1554947856915.log": "000000"}}
```
