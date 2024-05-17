# Домашнее задание к занятию «Уязвимости и атаки на информационные системы» - Михайлов Дмитрий


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

- Какие сетевые службы в ней разрешены?

Я использовал команду:
sudo nmap -sV 192.168.0.250

Информация о том, какие службы разрешены:

![1-1](https://github.com/blackgult/hw13-01/blob/main/1-1.PNG)


- Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)

Полный вывод команды sudo nmap -sV --script vulners 192.168.0.250 вот здесь --> https://github.com/blackgult/hw13-01/blob/main/nmap_vulners.txt

Были найдены уязвимости сразу с прямыми сслыками, например следующие:

|     	SSV:78173	7.8	https://vulners.com/seebug/SSV:78173	*EXPLOIT*

|     	SSV:69983	7.8	https://vulners.com/seebug/SSV:69983	*EXPLOIT*

|     	EDB-ID:24450	7.8	https://vulners.com/exploitdb/EDB-ID:24450	*EXPLOIT*

|     	EDB-ID:15215	7.8	https://vulners.com/exploitdb/EDB-ID:15215	*EXPLOIT*


![1-2](https://github.com/blackgult/hw13-01/blob/main/1-2.PNG)


### Задание 2

Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

Запишите сеансы сканирования в Wireshark.

Ответьте на следующие вопросы:

- Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
- Как отвечает сервер?

*Приведите ответ в свободной форме.*


### Решение 2

_Сканирование Metasploitable в режиме SYN:_

Когда Nmap работает в этом режиме, он отправляет SYN пакет, что заставляет хост думать, что пытаются установить соединение. Если приходит SYN/ACK, то порт открыт; если RST - порт закрыт; если нет ответа или получено ICMP сообщение - порт фильтруется.

![2-1](https://github.com/blackgult/hw13-01/blob/main/2-1.PNG)

Запись сеанса сканирования в Wireshark:

![2-2](https://github.com/blackgult/hw13-01/blob/main/2-2.PNG)

_Сканирование Metasploitable в режиме FIN:_

Когда Nmap использует FIN-исследование вместо SYN-пакетов, он отправляет FIN-пакеты для проверки портов на удаленном хосте. Поскольку Nmap не устанавливает соединение с хостом заранее, удаленный хост отвечает RST-пакетом для сброса соединения, демонстрируя свое существование.

![2-3](https://github.com/blackgult/hw13-01/blob/main/2-3.PNG)

Запись сеанса сканирования в Wireshark:

![2-4](https://github.com/blackgult/hw13-01/blob/main/2-4.PNG)

_Сканирование Metasploitable в режиме Xmas:_

В случае использования этого метода, TCP-пакеты отправляются с установленными флагами PSH, URG и FIN. Этот тип сканирования также ожидает получить пакеты RST для портов, которые закрыты. В случае отправки пакета без флагов SYN, RST или ACK, если порт закрыт, узел отправит RST, а если порт открыт, не придет никакой ответ. При Xmas-сканировании устанавливаются флаги FIN, PSH и URG. Если получен RST в ответ, значит порт закрыт, если нет ответа, то порт либо открыт, либо находится за фильтром.

![2-5](https://github.com/blackgult/hw13-01/blob/main/2-5.PNG)

Запись сеанса сканирования в Wireshark:

![2-6](https://github.com/blackgult/hw13-01/blob/main/2-6.PNG)

_Сканирование Metasploitable в режиме UDP:_

Этот метод сканирования позволяет проверять порты, используемые службами UDP, отправляя пустой UDP заголовок. Если приходит сообщение об ошибке "порт недостижим", Nmap определяет, открыт ли порт, закрыт ли он или фильтруется. Если в ответ приходит UDP-пакет, порт считается открытым, если нет ответа, статус будет open|filtered. UDP сканирование работает медленно, поэтому для ускорения процесса лучше указать список интересующих портов.

![2-7](https://github.com/blackgult/hw13-01/blob/main/2-7.PNG)

Запись сеанса сканирования в Wireshark:

![2-8](https://github.com/blackgult/hw13-01/blob/main/2-8.PNG)

