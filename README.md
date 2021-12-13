# devops-netology
**Sarkisyan Aleksey**

**Выполнение задания 3.9 Security**


**Задание 1**

![Задание 1](/dz3.9/1.PNG)


**Задание 2.**

![Задание 2](/dz3.9/2.PNG)


**Задание 3.**

![Задание 3](/dz3.9/3.PNG)

на время теста в файле hosts Windows добавил строку, чтобы попадать по ссылке netology.ru на страницу Апач по умолчанию.

**192.168.1.56		netology.ru**

в файле **default-ssl.conf** указал свой сертификат

**SSLCertificateFile      /home/vagrant/netology.ru/netology.ru.crt**

**SSLCertificateKeyFile /home/vagrant/netology.ru/netology.ru.key**

после добавил сертификат в Windows в корневые доверенные.


**Задание 4.**

Команда

**./testssl.sh -U --sneaky https://netology.ru**

![Задание 4](/dz3.9/4.PNG)


**Задание 5.**

![Задание 5](/dz3.9/5.PNG)

![Задание 5](/dz3.9/5_1.PNG)


**Задание 6**

![Задание 6](/dz3.9/6.PNG)

**config файл**

**Host netology**

   **HostName 192.168.1.57**
   
   **IdentityFile ~/.ssh/renamekey**
   
   **User vagrant**
   
**7**

**sudo tcpdump -w data.pcap -i eth0**

![Задание 7](/dz3.9/7.PNG)
   

