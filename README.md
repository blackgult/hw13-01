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

Сканирование Metasploitable в режиме SYN:

![2-1](https://github.com/blackgult/hw13-01/blob/main/2-1.PNG)

Запись сеанса сканирования в Wireshark:

![2-2](https://github.com/blackgult/hw13-01/blob/main/2-2.PNG)

Сканирование Metasploitable в режиме FIN:

![2-3](https://github.com/blackgult/hw13-01/blob/main/2-3.PNG)

Запись сеанса сканирования в Wireshark:

![2-4](https://github.com/blackgult/hw13-01/blob/main/2-4.PNG)

Сканирование Metasploitable в режиме Xmas:

![2-5](https://github.com/blackgult/hw13-01/blob/main/2-5.PNG)

Запись сеанса сканирования в Wireshark:

![2-6](https://github.com/blackgult/hw13-01/blob/main/2-6.PNG)

Сканирование Metasploitable в режиме UDP:

![2-7](https://github.com/blackgult/hw13-01/blob/main/2-7.PNG)

Запись сеанса сканирования в Wireshark:

![2-8](https://github.com/blackgult/hw13-01/blob/main/2-8.PNG)

- Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?

- Как отвечает сервер?
