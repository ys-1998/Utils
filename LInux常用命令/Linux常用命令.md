## 远程跳板机情况

### 1.远程连接其他服务器

```
ssh 192.168.0.1(远程服务器地址)
```

### 2.跳板机传输文件给目标服务器

```
例子：
将/usr/local/javaproject目录下的xs1.sql文件,传输到192.168.0.1(目标服务器)的/usr/local/software/mysql/logs目录下

scp /usr/local/javaproject/xs1.sql root@192.168.0.1:/usr/local/software/mysql/logs
```

### 3.接受文件后解压文件

```
unzip [包名].zip
zip [包名].zip -d 目录  #解压到指定目录
```

### 4.文件夹改名

```
mv 旧文件名 新文件名
```

### 5.删除文件夹

```
rm -rf 文件夹名
```

### 6.服务器请求接口

```
curl 接口
可参考博文：https://blog.csdn.net/wuhuagu_wuhuaguo/article/details/90764856#t5
```

### 7.服务器下载文件

```
sz 文件名 下载后默认地址在windows电脑的下载里面
```



## docker方面

### =========================================镜像======================================

### 1.拉取镜像

```
docker pull [镜像名]:[版本号]
```



### 2.查看拥有的镜像

```
docker images
```



### 3.删除镜像

```
docker rmi [镜像名]
```



### 4.运行镜像

#### 4.1运行中间件容器

```
docker run -itd --name [容器名] -p 3344:80 [镜像名]

-it使用交互方式运行
-d后台运行
--name给容器取名
-p 宿主机端口:容器内部端口

！！！数据挂载
以mysql为例
docker run -itd -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql5.7

-v 卷挂载
-e 环境变量配置 安装启动mysql需要配置密码
```

#### 4.2运行jar包

```
docker run -itd --name=xxx -v /usr/local/javaproject/workapi:/app -p 8080:8080 -e TZ=Asia/Shanghai -w /app openjdk:8u342 java -jar xxx.jar

-w 指定容器工作路径 与前挂载路径相同
-e TZ=Asia/Shanghai 设置环境变量，设置时区
```

### =========================================容器======================================

### 5.查看正在运行的容器

```
docker ps 
docker ps -a 查看所有容器
```



### 6.停止/重启容器

```
docker stop [容器id]
docker restart [容器id]
```



### 6.删除容器

```
docker rm [容器ID]
```



### 7.查看容器运行日志

```
docker logs 容器名
```



### 8.进入容器

```
两种
docker exec -it [容器id] /bin/bash  
docker attach [容器id]
```



### 9.容器和宿主机之间传输文件

```
复制容器文件到宿主机器
docker cp [容器id]/test/a.txt /usr/local/

复制宿主机器文件到容器
docker cp /usr/local/a.txt [容器id]:/test/
```

