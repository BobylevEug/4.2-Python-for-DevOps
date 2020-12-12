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

## 3,4. При запуске скрипта указываем полный путь до репозитория (python <name_script.py> <path_repositories>)

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
