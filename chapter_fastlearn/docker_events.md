
## events

* 用法


    Usage: docker events [OPTIONS]

	Get real time events from the server

    -f, --filter=[]    Filter output based on conditions provided
    --help=false       Print usage
    --since=           Show all events created since timestamp
    --until=           Stream events until this timestamp



* 例子

第一个窗口用来监听事件

    $ docker events

第二个窗口 起停容器

    $ docker start 4386fb97867d
    $ docker stop 4386fb97867d
    $ docker stop 7805c1d35632

执行完后，shell窗口会同步打印如下信息：

    2014-05-10T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) start
    2014-05-10T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) die
    2014-05-10T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) stop
    2014-05-10T17:42:14.999999999Z07:00 7805c1d35632: (from redis:2.8) die
    2014-05-10T17:42:14.999999999Z07:00 7805c1d35632: (from redis:2.8) stop

使用since参数按时间筛选

    $ sudo docker events --since 1378216169
    2014-03-10T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) die
    2014-05-10T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) stop
    2014-05-10T17:42:14.999999999Z07:00 7805c1d35632: (from redis:2.8) die
    2014-03-10T17:42:14.999999999Z07:00 7805c1d35632: (from redis:2.8) stop
    $ sudo docker events --since '2013-09-03'
    2014-09-03T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) start
    2014-09-03T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) die
    2014-05-10T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) stop
    2014-05-10T17:42:14.999999999Z07:00 7805c1d35632: (from redis:2.8) die
    2014-09-03T17:42:14.999999999Z07:00 7805c1d35632: (from redis:2.8) stop
    $ sudo docker events --since '2013-09-03T15:49:29'
    2014-09-03T15:49:29.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) die
    2014-05-10T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) stop
    2014-05-10T17:42:14.999999999Z07:00 7805c1d35632: (from redis:2.8) die
    2014-09-03T15:49:29.999999999Z07:00 7805c1d35632: (from redis:2.8) stop

只保留三分钟内的事件

    $ sudo docker events --since '3m'
    2015-05-12T11:51:30.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) die
    2015-05-12T15:52:12.999999999Z07:00 4 4386fb97867d: (from ubuntu-1:14.04) stop
    2015-05-12T15:53:45.999999999Z07:00  7805c1d35632: (from redis:2.8) die
    2015-05-12T15:54:03.999999999Z07:00  7805c1d35632: (from redis:2.8) stop

也可以使用过滤器筛选

    $ docker events --filter 'event=stop'
    2014-05-10T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) stop
    2014-09-03T17:42:14.999999999Z07:00 7805c1d35632: (from redis:2.8) stop
    $ docker events --filter 'image=ubuntu-1:14.04'
    2014-05-10T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) start
    2014-05-10T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) die
    2014-05-10T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) stop
    $ docker events --filter 'container=7805c1d35632'
    2014-05-10T17:42:14.999999999Z07:00 7805c1d35632: (from redis:2.8) die
    2014-09-03T15:49:29.999999999Z07:00 7805c1d35632: (from redis:2.8) stop
    $ docker events --filter 'container=7805c1d35632' --filter 'container=4386fb97867d'
    2014-09-03T15:49:29.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) die
    2014-05-10T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) stop
    2014-05-10T17:42:14.999999999Z07:00 7805c1d35632: (from redis:2.8) die
    2014-09-03T15:49:29.999999999Z07:00 7805c1d35632: (from redis:2.8) stop
    $ docker events --filter 'container=7805c1d35632' --filter 'event=stop'
    2014-09-03T15:49:29.999999999Z07:00 7805c1d35632: (from redis:2.8) stop
    $ docker events --filter 'container=container_1' --filter 'container=container_2'
    2014-09-03T15:49:29.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) die
    2014-05-10T17:42:14.999999999Z07:00 4386fb97867d: (from ubuntu-1:14.04) stop
    2014-05-10T17:42:14.999999999Z07:00 7805c1d35632: (from redis:2.8) die
    2014-09-03T15:49:29.999999999Z07:00 7805c1d35632: (from redis:2.8) stop


* 总结

	打印容器实时的系统事件。
