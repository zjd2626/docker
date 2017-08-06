Docker CI Demo
==============
1、登录Jenkins，新建一个自由风格的软件项目。
2、源码管理选择git，并添加Repository URL、Credentials
3、构建选择 Execute Shell，命令如下：
docker stop front_dev || true;
docker rm front_dev || true;
docker build -t front_dev .;
docker run --name front_dev -p 10080:80 -d front_dev;

这里有几个注意点：

docker stop／rm 命令后加上 || true
当shell中有命令执行失败时，jenkins会判定构建失败，从而结束构建工作。而加上||true，无论当前front_dev是否在运行，命令都返回执行成功，使shell可以继续执行下去。
docker run -d 
-d 表示容器以daemon状态运行，有些镜像run之后会处于挂起状态，使得构建的shell脚本一直无法结束。

shell中的front_dev为镜像、容器名字，可以自行重命名。
