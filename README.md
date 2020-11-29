# 4.2-Python-for-DevOps

##1.

a = 1
b = '2'
c = a + b
print (c)
В "с" будет ошибка

a = '1'
b = '2'
c = a + b
print (c)
В "с" будет 12

a = 1
b = 2
c = a + b
print (c)
В "с" будет 3

##2.

bash_command = ["cd ~/netology/sysadm-homeworks", "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
is_change = False
for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:   ', '')
        print(prepare_result)
        break
