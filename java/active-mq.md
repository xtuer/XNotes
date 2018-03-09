## 定时删除 ActiveMQ 的消息并重启

```bash
30 1 * * * /usr/local/edu/activemq/bin/activemq stop; sleep 120; rm -rf /usr/local/edu/activemq/data/kahadb/db*; sleep 10; /usr/local/edu/activemq/bin/activemq start
```



