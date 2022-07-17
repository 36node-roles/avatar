# avatar

安装 kafka、elasticsearch、vector，并配置 basic-auth 的 ingress

阿凡达，寓意信息的链接

Avatar 是 36node 团队采用的消息总线方案，用于日志采集和微服务间的异步通知。

## 依赖

ansible-galaxy collection install community.general

## 访问方式

<https://kibana.{domain>}

## 查看状态

```
helm status elasticsearch -n { namespace }
helm status kafka -n { namespace }
helm status vector -n { namespace }
```

## 用 kafkacat 进行测试

```sh
## 通常已经部署
kubectl run kafka-client --restart='Never' --image confluentinc/cp-kafkacat --command -- sleep infinity

## 进入
kubectl exec --tty -i kafka-client -- bash

## 消费
kafkacat -b kafka.avatar:9092 -C -t xxtopic -o end

## 生产
kafkacat -b kafka.avatar:9092 -t xxtopic  -P
```

## 查看 kibana

```sh
kubectl -n avatar port-forward svc/elasticsearch-kibana 5601:5601
```

## 清理索引的方法

<https://www.ibm.com/docs/en/cloud-private/3.2.0?topic=configuration-manually-removing-log-indices>

## Develop guide

Link to local installed role for convenience.

```sh
rm -rf /Users/zzs/.ansible/roles/36node.avatar
ln -s $PWD /Users/zzs/.ansible/roles/36node.avatar
```
