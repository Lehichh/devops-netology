# devops-netology
**Sarkisyan Aleksey**

**Выполнение задания 3.8 Network**


**1.**

https://yapx.ru/v/PdTLR


**2.**

**root@vagrant:~# ip route add 8.0.0.0/8 via 10.0.2.2**

**root@vagrant:~# ip route add 8.8.0.0/16 via 10.0.2.2**

**root@vagrant:~# ip route**

**default via 10.0.2.2 dev eth0 proto dhcp src 10.0.2.15 metric 100**

**8.0.0.0/8 via 10.0.2.2 dev eth0**

**8.8.0.0/16 via 10.0.2.2 dev eth0**

**10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.15**

**10.0.2.2 dev eth0 proto dhcp scope link src 10.0.2.15 metric 100**


**3.**

https://yapx.ru/v/Pd2j2

например служба **sshd** принимающая запросы на соединения работает по протоколу **tcp** на **22** порту


**4.**

https://yapx.ru/v/Pd2nR

служба **rpcbind** порт **111**, отображает службы RPC на порты


**5.**

https://yapx.ru/v/Pd7wS