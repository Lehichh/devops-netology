# devops-netology
**Sarkisyan Aleksey**

**Выполнение задания 3.5 FS**

**1.**

Дополнительные опции задаются после пути к демону в ExecStart

[Unit]

Description=Node Exporter
 
[Service]

User=node_exporter

Group=node_exporter

ExecStart=/usr/local/bin/node_exporter $EXTRA_OPTS
 
[Install]

WantedBy=multi-user.target
