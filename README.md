# devops-netology
**Sarkisyan Aleksey**

**Выполнение задания 3.3 ОС**

**1.**

Системный вызов - **chdir("/tmp")** 

**2.**

база данных находится тут - **/usr/share/mime/magic**

**3.

мы может по пиду процесса командой **lsof -p** увидеть номер дескриптора файла в поле fd, и по пути каталога для дескрипторов **/proc/PID/fd/*Номер дескриптора*** используя перенаправление > присвоить пустую строку ему.

**4.**

Зомби не занимают памяти (как процессы-сироты), но блокируют записи в таблице процессов, размер которой ограничен для каждого пользователя и системы в целом.

**5.**

https://yapx.ru/v/PNTXJ

**6.**

*uname()* системный вызов

Part of the utsname information  is  also  accessible  via  **/proc/sys/kernel/{ostype**,
hostname, osrelease, version, domainname}.

**7.**

В первом случае у нас идет разделение команд и **echo** выполняется.

Во втором случае оператор **&&**(AND) не выполнит вторую команду, если первая завершилась некорректно.

в использовании **set -e** смылса нет - она не работает с конвеерными командами.

**set -e** - указывает оболочке выйти, если команда дает ненулевой статус выхода.

**8.**

**-e** - указывает оболочке выйти, если команда дает ненулевой статус выхода.

**-u** - находит неопределенные переменные.

**-x** - печатает аргументы команды во время выполнения.

**-o pipefail** - возвращает значение цепочки действий: статус последней команды с не-нулевым статумом или 0 если ни одна команда не завершилась с ошибкой.

хорошо использовать, так как это более наполненная информация(логи) и это поможет быстрее найти ошибку, так как лучше понятно на каком этапе ошибка.

**9.**

Больше всего спящих процессов **(S)**

**<** - высокий приоритет

**N** - низкий приоритет 

**L** - имеет страницы, заблокированные в памяти

**s** - лидер сеанса

**l** - многопоточный

**+** - находится в группе процессов переднего плана
