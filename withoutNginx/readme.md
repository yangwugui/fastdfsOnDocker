### 目录设置

fastdfs在容器中的安装路径：/home/fastdfs

在主机的数据硬盘挂载卷data中创建fastdfs文件夹，用于fastdfs的配置和数据存储。
    mkdir -p /data/fastdfs
容器运行时挂载文件卷：
    /data/fastdfs/fdfs_conf, 覆盖容器中的 /home/fastdfs/fastdfs-5.08/conf
    /data/fastdfs/etc_conf,  覆盖容器中的 /etc/fdfs/
    /data/fastdfs/fastdfs_file, 

### 建立配置文件夹

可以通过下述方法创建主机中的配件文件夹：

    docker run -d --name storageconfig fastdfs:5.08

    docker cp storageconfig:/home/fastdfs/fastdfs-5.08/conf /data/fastdfs
    mv /data/fastdfs/conf /data/fastdfs/fdfs_conf

    docker cp storageconfig:etc/fdfs /data/fastdfs
    mv /data/fastdfs/fdfs /data/fastdfs/etc_conf

    从容器中拷贝fastdfs的存储文件目录到宿主机
    docker cp storageconfig:/home/fastdfs_file /data/fastdfs

### 修改配置文件

修改 /data/fastdfs/fdfs_conf/storage.conf:
    tracker_server=ipaddress:22122

修改 /data/fastdfs/fdfs_conf/client.conf:
    tracker_server=ipaddress:22122

说明：ipaddress为具体的ip地址，为你所部署的该节点的ip地址，如192.168.0.1，该ip地址不能为localhost或者127.0.0.1，如果将tracker和storage节点部署在一台服务器上，那么就用其对外公开的ip地址来代替
