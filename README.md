# devops-netology
**Sarkisyan Aleksey**

**Выполнение задания 3.9 Security**


**1.**

![Задание 1](/dz3.9/1.png)


**2.**

![Задание 2](/dz3.9/2.png)


**3.**

![Задание 3](/dz3.9/3.png)

на время теста в файле hosts Windows добавил строку, чтобы попадать по ссылке netology.ru на страницу Апач по умолчанию.

**192.168.1.56		netology.ru**

в файле **default-ssl.conf** указал свой сертификат

**SSLCertificateFile      /home/vagrant/netology.ru/netology.ru.crt**

**SSLCertificateKeyFile /home/vagrant/netology.ru/netology.ru.key**

после добавил сертификат в Windows в корневые доверенные.


**4.**

Команда

**./testssl.sh -U --sneaky https://netology.ru**

![Задание 4](/dz3.9/4.png)


**5.**

![Задание 5](/dz3.9/5.png)

![Задание 5](/dz3.9/5_1.png)


**6**

![Задание 6](/dz3.9/6.png)

**config файл**

**Host netology**

   **HostName 192.168.1.57**
   
   **IdentityFile ~/.ssh/renamekey**
   
   **User vagrant**
   
**7**

**sudo tcpdump -w data.pcap -i eth0**

![Задание 7](/dz3.9/7.png)
   

