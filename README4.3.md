# Домашнее задание к занятию "4.3. Языки разметки JSON и YAML"


## Обязательная задача 1
Мы выгрузили JSON, который получили через API запрос к нашему сервису:
```
 { "info": "Sample JSON output from our service\\t",
        "elements":[
            { "name": "first",
            "type": "server",
            "ip": 7175 
            },
            { "name": "second",
            "type": "proxy",
            "ip": "71.78.22.43"
            }
        ]
    }
```
  Нужно найти и исправить все ошибки, которые допускает наш сервис

## Обязательная задача 2
В прошлый рабочий день мы создавали скрипт, позволяющий опрашивать веб-сервисы и получать их IP. К уже реализованному функционалу нам нужно добавить возможность записи JSON и YAML файлов, описывающих наши сервисы. Формат записи JSON по одному сервису: `{ "имя сервиса" : "его IP"}`. Формат записи YAML по одному сервису: `- имя сервиса: его IP`. Если в момент исполнения скрипта меняется IP у сервиса - он должен так же поменяться в yml и json файле.

### Ваш скрипт:
```python
#!/usr/bin/env python3

import time
import socket
import json
import yaml

host_list = ["mail.google.com", "drive.google.com", "google.com"]
old_ip = {host_list[0]: socket.gethostbyname(host_list[0]), host_list[1]: socket.gethostbyname(host_list[1]), host_list[2]: socket.gethostbyname(host_list[2])}

#with open('fileyaml.yml', 'w') as p1:
a = 0
while (a == 0):
    for host in host_list:
        ip_address = socket.gethostbyname(host)
        if ip_address == old_ip[host]:
            print(host + ' ' + ip_address)
            with open('fileyml.yml', 'w') as p1:
                p1.write(yaml.dump(old_ip))
            with open('filejson.json', 'w') as p2:
                p2.write(json.dumps(old_ip))
            time.sleep(30)
        else:
            print('[ERROR] ' + host + ' IP mismatch:' + old_ip[host] + ' ' + ip_address)
            old_ip[host] = ip_address
            with open('fileyml.yml', 'w') as p1:
                p1.write(yaml.dump(old_ip))
            with open('filejson.json', 'w') as p2:
                p2.write(json.dumps(old_ip))
            time.sleep(30)
```

### Вывод скрипта при запуске при тестировании:
```
mail.google.com 216.58.210.165
drive.google.com 173.194.222.194
google.com 216.58.210.174
mail.google.com 216.58.210.165
drive.google.com 173.194.222.194
google.com 216.58.210.174
mail.google.com 216.58.210.165
drive.google.com 173.194.222.194
google.com 216.58.210.174
mail.google.com 216.58.210.165
drive.google.com 173.194.222.194
google.com 216.58.210.174
mail.google.com 216.58.210.165
drive.google.com 173.194.222.194
[ERROR] google.com IP mismatch:216.58.210.174 216.58.209.174
mail.google.com 216.58.210.165
drive.google.com 173.194.222.194
```

### json-файл(ы), который(е) записал ваш скрипт:
```json
{"mail.google.com": "216.58.210.165", "drive.google.com": "173.194.222.194", "google.com": "216.58.209.174"}
```

### yml-файл(ы), который(е) записал ваш скрипт:
```yaml
drive.google.com: 173.194.222.194
google.com: 216.58.209.174
mail.google.com: 216.58.210.165
```

## Дополнительное задание (со звездочкой*) - необязательно к выполнению

Так как команды в нашей компании никак не могут прийти к единому мнению о том, какой формат разметки данных использовать: JSON или YAML, нам нужно реализовать парсер из одного формата в другой. Он должен уметь:
   * Принимать на вход имя файла
   * Проверять формат исходного файла. Если файл не json или yml - скрипт должен остановить свою работу
   * Распознавать какой формат данных в файле. Считается, что файлы *.json и *.yml могут быть перепутаны
   * Перекодировать данные из исходного формата во второй доступный (из JSON в YAML, из YAML в JSON)
   * При обнаружении ошибки в исходном файле - указать в стандартном выводе строку с ошибкой синтаксиса и её номер
   * Полученный файл должен иметь имя исходного файла, разница в наименовании обеспечивается разницей расширения файлов

### Ваш скрипт:
```python
???
```

### Пример работы скрипта:
???