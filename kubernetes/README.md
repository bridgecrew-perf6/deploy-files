# yamls

这里存放了用于将 `pulsar` 部署在 `k8s` 上的yaml文件,目前是存放的yaml文件主要是用于部署去 `zookeeper` 后的 `pulsar` 集群文件,虽然是按照集群方式部署的,但是默认的配置都是副本为1的,如果apply了这些yaml文件后将会产生以下相关Pod:  

- pulsar broker
- bookkeeper
- etcd
- pulsar-client producer  用于测试发送pulsar消息
- pulsar-client consumer  用于测试接收pulsar消息
- pulsar-admin  用于初始化pulsar集群信息,以job形式启动,初始化后就退出.
- pulsarctl  用于调用pulsar admin API,默认是关闭的(副本数是1)
- busybox  用于调试,例如nslookup等命令,默认是关闭的(副本数是1)  

# 注意
由于 `bookkeeper` 和 `etcd` 都需要持久化数据,因此在应用yaml之前需要提前准备好可用的 `PVC` 或 `StorageClass`,默认填写的是 `openebs-hostpath`.