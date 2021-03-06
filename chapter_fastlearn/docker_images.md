

## images

* 使用方法


	docker images [OPTIONS] [REPOSITORY]

	List images

 	-a, --all=false      Show all images (default hides intermediate images)
  	--digests=false      Show digests
  	-f, --filter=[]      Filter output based on conditions provided
  	--help=false         Print usage
  	--no-trunc=false     Don't truncate output
  	-q, --quiet=false    Only show numeric IDs

* 例子：

查询本里存储的镜像

	$ sudo docker imgaes
    REPOSITORY           TAG       IMAGE ID        CREATED      VIRTUAL SIZE
    docker.io/ubuntu     latest    63e3c10217b8    7 days ago    188.3 MB
    docker.google/etcd   2.1.1     2c319269dd15    8 days ago    23.32 MB
    docker.io/postgres   latest    730d1d72bda2    2 weeks ago   265.3 MB
    centos               latest    770327a1e9e7    2 weeks ago   418.9 MB
    …
将ID完整展现

    $ sudo docker images --no-trunc
    REPOSITORY                  TAG                 IMAGE ID                                                           CREATED             VIRTUAL SIZE
    scratch1                    latest              dc869bfd3085af05a1a070c7409193e8be88de00ff4560e2e9af80ffa9d2041d   58 minutes ago      0 B
    registry.liugang/centos     latest              770327a1e9e746cf8d4449a7134e87917982b33c7f5cea584d941350f5ead7ac   4 weeks ago         418.9 MB
    registry.liugang/busybox    latest              8c2e06607696bd4afb3d03b687e361cc43cf8ec1a4a725bc96e39f05ba97dd55   4 months ago        2.43 MB
    docker.io/scratch           latest              511136ea3c5a64f264b78b5433614aec563103b4d4702f3ba7d4d2698e22c158   2 years ago         0 B

使用该命令将展现没有tag的镜像

    $ sudo docker images --filter "dangling=true"
    REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
    <none>              <none>              b133995b6291        About an hour ago   0 B
    <none>              <none>              6fae83243a01        About an hour ago   0 B
    <none>              <none>              4c6412305cfa        About an hour ago   0 B

* 总结

其中第一字段是image镜像的名称；TAG一般表示为版本号，也可以自己定义 ；IMAGE ID 表示镜像的唯一ID  ，这也是判断两个镜像文件是否为同一个的判断标准。

