# Домашнее задание к занятию "Уязвимости и атаки на информационные системы" - Фумелли Петр

### Задание 1

```
Starting Nmap 7.95 ( <https://nmap.org> ) at 2025-05-17 16:26 MSK
Nmap scan report for 192.168.125.161
Host is up (0.99s latency).
Not shown: 977 closed tcp ports (conn-refused)
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec
513/tcp  open  login
514/tcp  open  shell
1099/tcp open  rmiregistry
1524/tcp open  ingreslock
2049/tcp open  nfs
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
5432/tcp open  postgresql
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13
8180/tcp open  unknown

```

1. vsftpd 2.3.4 – Бэкдор
Описание: В этой версии FTP-сервера присутствует бэкдор, активируемый при вводе имени пользователя, заканчивающегося на :).

Эксплуатация: После ввода такого имени пользователя открывается шелл на порту 6200.

2. UnrealIRCd 3.2.8.1 – Бэкдор
Описание: IRC-сервер содержит бэкдор, позволяющий удалённое выполнение команд.

Эксплуатация: Отправка определённой команды на порт 6667 приводит к выполнению произвольных команд на сервере.

3. distccd – Удалённое выполнение команд
Описание: Сервис distccd позволяет удалённое выполнение команд без аутентификации.

Эксплуатация: Использование Metasploit-модуля exploit/unix/misc/distcc_exec позволяет получить доступ к системе.

### Задание 2

При SYN-сканировании Metasploitable отвечает на открытые порты SYN+ACK, а на закрытые — RST. При FIN и Xmas сканах сервер (на Linux) игнорирует пакеты к открытым портам, но отвечает RST'ом на закрытые. UDP-пакеты не вызывают ответа от открытых портов, но для закрытых получаем ICMP Destination Port Unreachable.
