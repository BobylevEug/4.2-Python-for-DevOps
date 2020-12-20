# 4.2-Python-for-DevOps

##1.

```python
a = 1
b = '2'
c = a + b
print (c)
```
В "с" будет ошибка

```python
a = '1'
b = '2'
c = a + b
print (c)
```
В "с" будет 12

```python
a = 1
b = 2
c = a + b
print (c)
```
В "с" будет 3

## 2.

```python
#!/usr/bin/env python3

import os

bash_command = ["cd ~/netology/sysadm-homeworks", "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:   ', '')
        print(prepare_result)
#       brake - убираем из цикла выход
```

## 3. При запуске скрипта указываем полный путь до репозитория (python <name_script.py> <path_repositories>)

```python
#!/usr/bin/env python3

import os
import sys

print ('проверяем ваш путь {}'.format(sys.argv[1]))
bash_command = [f"cd {sys.argv[1]}", "git status"] 
result_os = os.popen(' && '.join(bash_command)).read()
for result in result_os.split('\n'):
    if result.find('modified') != -1: 
        prepare_result = result.replace('\tmodified:   ', '')
        print('По указанному пути',sys.argv[1],'изменен файл',prepare_result)
```

## 4. Мы хотим написать скрипт, который опрашивает веб-сервисы, получает их IP, выводит информацию в стандартный вывод в виде: <URL сервиса> - <его IP>. Также, должна быть реализована возможность проверки текущего IP сервиса c его IP из предыдущей проверки. Если проверка будет провалена - оповестить об этом в стандартный вывод сообщением: [ERROR] <URL сервиса> IP mismatch: <старый IP> <Новый IP>. Будем считать, что наша разработка реализовала сервисы: drive.google.com, mail.google.com, google.com.

```python
#!/usr/bin/env python3

import socket
import sys
import shutil
import os

domain_search = 'google.com'
domain_mail = 'mail.google.com'
domain_drive = 'drive.google.com'

def domain_name(x) : # объявление фунцкии
        ip = socket.gethostbyname(x) #определение ip 
        print(x,' - ', ip) #вывод в консоль
        with open('current_ip.txt', 'a') as f: # открытие файла на дозапись
            f.write(ip + '\n') #построчная запись в файл 

shutil.copy2(os.path.abspath('current_ip.txt'), os.path.abspath('past_ip.txt'))
#копируем файл current_ip в past_ip внутри текущей директории

f = open('current_ip.txt', 'w') #создание файла она же отчистка
f.close() #закрытие файла

domain_name (domain_search)
domain_name (domain_mail)
domain_name (domain_drive)

with open("past_ip.txt") as f1, open("current_ip.txt") as f2:
#построчное сравнение файлов
    for x1, x2 in zip(f1,f2):
        if x1 == x2: #если строка одного файла равна строке второго файла
            print(x1, 'не изменился')
        else:
            print('[ERROR] IP ' + x1 + 'сменился на IP ', x2)
```
