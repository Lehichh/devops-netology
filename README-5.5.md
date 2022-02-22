# devops-netology
**Sarkisyan Aleksey**

**Домашнее задание - Оркестрация группой Docker контейнеров на примере Docker Compose**


**Задание 1**

**а)** В глобальном режиме будет развертываться одна реплика на каждом узле нашего кластера, а для реплициеруемой службы мы указываем количество идентичных задачь для запуска.

**б)** Raft

**с)** Overlay-сеть создает Docker по технологии vxlan с использованием порта 4789. Overlay создает подсеть, которую могут использовать контейнеры в разных физических хостах swarm-кластера и с использованием шифрования обмениваться данными.


**Задание 2**

![Задание 1](/dz5.5/2.PNG)


**Задание 3**

![Задание 1](/dz5.5/3.PNG)


**Задание 4**

При вводе данной команды мы получим сгенерированный ключ шифрования для разблокировки роя. Эта функция защищает ключ TLS для обмена между узлами swarm'a и ключ шифрования/расшифрования журнала Raft(эти ключи при перезапуске Docker'a загружаются в память узлов). Мы становимся владельцем этих ключей и чтобы разблокировать рой необходим сгенерированный ключ.