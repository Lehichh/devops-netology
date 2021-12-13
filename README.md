# devops-netology
**Sarkisyan Aleksey**

**Выполнение задания 3.9 Security**


**1.**

https://yapx.ru/v/PgNKM


**2.**

https://yapx.ru/v/PgNLU


**3.**

https://yapx.ru/v/PgNNX

на время теста в файле hosts Windows добавил строку, чтобы попадать по ссылке netology.ru на страницу Апач по умолчанию.

**192.168.1.56		netology.ru**

в файле **default-ssl.conf** указал свой сертификат

**SSLCertificateFile      /home/vagrant/netology.ru/netology.ru.crt**

**SSLCertificateKeyFile /home/vagrant/netology.ru/netology.ru.key**

после добавил сертификат в Windows в корневые доверенные.


**4.**

Команда

**./testssl.sh -U --sneaky https://netology.ru**

https://yapx.ru/v/Pge8g


**5.**

https://yapx.ru/v/PgvgN

https://yapx.ru/v/Pg18V


**6**

https://yapx.ru/v/PiaBB

**config файл**

**Host netology**

   **HostName 192.168.1.57**
   
   **IdentityFile ~/.ssh/renamekey**
   
   **User vagrant**
   
**7**

**sudo tcpdump -w data.pcap -i eth0**

https://yapx.ru/v/PiqDT
   

