# Домашнее задание к занятию «`Защита сети`» - `Игонин В.А.`

### Задание 1

Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

**sudo nmap -sA < ip-адрес >**

**sudo nmap -sT < ip-адрес >**

**sudo nmap -sS < ip-адрес >**

**sudo nmap -sV < ip-адрес >**

*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*

### Решение 1

При сканирование nmap, в Fail2Ban никаких событий не было, поскольку это не попытки авторизации, а просто сетевое сканирование.
А вот Suricata реагирует на все события, включая 2ое задание при переборе пароля.

Как видно на скриншоте после сканирование определен "плохой трафик" [Classification: Potentially Bad Traffic] 

 - ET SCAN Suspicious inbound to mySQL port 3306
 - ET SCAN Suspicious inbound to PostgreSQL port 5432
 - ET SCAN Suspicious inbound to Oracle SQL port 1521
 - ET SCAN Suspicious inbound to MSSQL port 1433

определен [Classification: Web Application Attack]

 - ET SCAN Nmap Scripting Engine User-Agent Detected (Nmap Scripting Engine)
 - ET SCAN Possible Nmap User-Agent Observed

![alt text](https://github.com/Sayward-k8/sdb-hw-13-03/blob/main/img/1.0.png)

Часть логов относящаяся ко 2ому заданию:

Замечена аномальная активность на 22 порту. [Classification: Attempted Information Leak]

 - ET SCAN Potential SSH Scan
 - ET SCAN Potential SSH Scan OUTBOUND

И подтверждение, что пароль пытались перебрать [Classification: Generic Protocol Command Decode]

 - SURICATA Applayer Detect protocol only one direction
 - SURICATA STREAM excessive retransmissions

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

Логи Suricata я описал выше, а в логах Fail2Ban мы видим, что происходят неудачные попытки авторизации

![alt text](https://github.com/Sayward-k8/sdb-hw-13-03/blob/main/img/2.1.2.png)

Fail2Ban сработал и заблокировал атакующий IP

![alt text](https://github.com/Sayward-k8/sdb-hw-13-03/blob/main/img/2.2.png)

Через 10 минут был unban

2026-03-11 17:29:10,066 fail2ban.actions        [1133190]: NOTICE  [sshd] Unban 172.18.15.132

