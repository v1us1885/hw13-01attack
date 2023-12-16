# Домашнее задание к занятию «Уязвимости и атаки на информационные системы» - Филатов А. В.

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

------

### Задание 1

Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину, используя **nmap**.

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

- Какие сетевые службы в ней разрешены?
- Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)
  
*Приведите ответ в свободной форме.*  

### Решение 1

Исходя из результатов сканирования Nmap, можно выделить следующие сетевые службы и обнаруженные уязвимости:

Сетевые службы:   

FTP (порт 21): vsftpd 2.3.4 с разрешенным анонимным входом.   
SSH (порт 22): OpenSSH 4.7p1 Debian 8ubuntu1.   
Telnet (порт 23): Linux telnetd.   
SMTP (порт 25): Postfix smtpd.   
DNS (порт 53): ISC BIND 9.4.2.   
HTTP (порт 80): Apache httpd 2.2.8 (Ubuntu).   
RPC (порт 111): rpcbind, NFS.   
NetBIOS (порты 139 и 445): Samba smbd 3.X - 4.X.   
MySQL (порт 3306): MySQL 5.0.51a-3ubuntu5.   
PostgreSQL (порт 5432): PostgreSQL DB 8.3.0 - 8.3.7.   
VNC (порт 5900): VNC (protocol 3.3).   
IRC (порт 6667): UnrealIRCd.   
Apache Jserv (порт 8009): Apache Jserv (Protocol v1.3).   
Apache Tomcat (порт 8180): Apache Tomcat/Coyote JSP engine 1.1.   

Обнаруженные уязвимости:   

 - vsftpd 2.3.4 (FTP): vsftpd 2.3.4 - Backdoor Command Execution (Metasploit)   
 - OpenSSH 4.7p1 (SSH): OpenSSH 2.3 < 7.7 - Username Enumeration (PoC)   
 - Postfix smtpd (SMTP): Postfix SMTP 4.2.x < 4.2.48 - 'Shellshock' Remote Command Injection   

---

### Задание 2

Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

Запишите сеансы сканирования в Wireshark.

Ответьте на следующие вопросы:

- Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
- Как отвечает сервер?

*Приведите ответ в свободной форме.*

### Решение 2

Эти режимы сканирования отличаются в том, как они формируют и отправляют пакеты, а также в том, как серверы реагируют на эти пакеты.   

 - Сканирование SYN:   

Основной режим сканирования, при котором клиент отправляет пакеты с установкой флага SYN.
Если порт открыт, сервер отвечает пакетом с установкой флага SYN и ACK.
Если порт закрыт, сервер отвечает только пакетом с установкой флага RST.

 - Сканирование FIN:

Клиент отправляет пакет с установкой флага FIN.   
Ответ от сервера может быть различным:   
Если порт открыт, сервер может проигнорировать пакет или отправить RST.   
Если порт закрыт, сервер может отправить RST.   

 - Сканирование Xmas:   

Клиент отправляет пакет с установкой флагов FIN, PSH и URG.   
Ответ сервера:   
Если порт закрыт, сервер может отправить RST.   
Если порт открыт, сервер может проигнорировать пакет или отправить RST.   

 - Сканирование UDP:   

Для сканирования UDP, клиент отправляет пакеты на UDP-порты.   
Ответ сервера:   
Если порт закрыт, сервер может отправить ICMP сообщение о недостижимости.   
Если порт открыт, сервер может не отправить никакого ответа.   

 - Общие замечания:

Сканирование SYN чаще всего используется, так как оно более надежно и эффективно.   
Сканирование FIN и Xmas менее надежны, так как некоторые системы могут не реагировать так, как ожидается.   
Сканирование UDP может быть менее точным из-за того, что протокол UDP не требует установки соединения.   