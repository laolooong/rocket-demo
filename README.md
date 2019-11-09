# rocket-demo
spring boot + gradle + docker
添加了bmuschko支持，可以远程部署到远程linux服务中

1、远程部署前提需要开启docker远程访问功能

CentOS 7 修改/usr/lib/systemd/system/docker.service文件，在ExecStart后面添加一行
ExecStart=/usr/bin/dockerd  -H tcp://0.0.0.0:2375  -H unix:///var/run/docker.sock

2、重启docker服务：
systemctl daemon-reload    
systemctl restart docker.service 

3、在centOS中开放2375端口
firewall-cmd --zone=public --add-port=2375/tcp --permanent

4、更新防火墙规则
firewall-cmd --reload

5、查看端口开放情况
netstat  -anp |grep 2375

6、我们在gradle.build中已经定义好了buildDockerImage方法，用来构建docker镜像

7、在终端中用gradle命令将项目打包并且部署到远程linux服务器中

gradlew buildDockerImage --info

8、在centOS中查看当前的镜像

docker ps -a

9、运行我们远程部署的docker镜像，并且添加端口映射

docker run -itd -p 8081:8081 --name myDockerApp rocket-demo:0.0.1-SNAPSHOT

10、如果访问不到地址，需要在linux中开放我们刚才定义的项目的端口地址

