# Домашнее задание к занятию «`Защита сети`» - `Игонин В.А.`

### Задание 1

Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

**sudo nmap -sA < ip-адрес >**

**sudo nmap -sT < ip-адрес >**

**sudo nmap -sS < ip-адрес >**

**sudo nmap -sV < ip-адрес >**

*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*

### Решение 1


![alt text](https://github.com/Sayward-k8/sdb-hw-13-03/blob/main/img/1.png)
![alt text](https://github.com/Sayward-k8/sdb-hw-13-03/blob/main/img/1.1.png)
![alt text](https://github.com/Sayward-k8/sdb-hw-13-03/blob/main/img/1.2.png)

### Задание 2

Проведите атаку на подбор пароля для службы SSH:

**hydra -L users.txt -P pass.txt < ip-адрес > ssh**

1. Настройка **hydra**: 
 
 - создайте два файла: **users.txt** и **pass.txt**;
 - в каждой строчке первого файла должны быть имена пользователей, второго — пароли. В нашем случае это могут быть случайные строки, но ради эксперимента можете добавить имя и пароль существующего пользователя.

2. Включение защиты SSH для Fail2Ban:

-  открыть файл /etc/fail2ban/jail.conf,
-  найти секцию **ssh**,
-  установить **enabled**  в **true**.

*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*

### Решение 2

![alt text](https://github.com/Sayward-k8/sdb-hw-13-03/blob/main/img/2.1.png)
![alt text](https://github.com/Sayward-k8/sdb-hw-13-03/blob/main/img/2.1.2.png)
![alt text](https://github.com/Sayward-k8/sdb-hw-13-03/blob/main/img/2.2.png)



