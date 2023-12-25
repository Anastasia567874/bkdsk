Сначала я установил VirtualBox. После я создал виртуальную машину VM A с помощью виртуального образа, который скачал с интернета. С версией Ubunta 22.04.1

# Начинаем настройку машины A.

Для начала заходим в настройки машины А, переходим во вкладку сеть. Сначала нам нужно предоставить доступ в интеренет. ВЫбираем 1 адаптер, тип подключения - NAT. Именно данный вид подключения даст доступ к сети Интернет. NAT изолирует виртуальную машину от внешних соединений. Все запросы проходят через хост-систему, так мы и получим доступ в Интернет. 

![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a1.jpg)

Теперь проверим, если ли доступ в сеть. Для этого используется команда ping, которая позволяет отправлять запросы по ip-адресу. Попробуем подключиться к ip-адресу google. 172.217.22.14

![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a2.jpg)

Подключение работает. Все пакеты дошли.

# Теперь настроим машину B. 

Создаем машину B. 
Заходим в настройки - сеть. Выбираем 1 адаптер, тип подключения - Внутренняя сеть (Internal Network). Выбираем имя - LAN1. У машины A делаем то же самое на 2 адаптере (1 уже занят). 

![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a3.jpg)

# Теперь проверим поключение машин A и B.

В терминале A пишем 
```
ip a
```
![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a4.jpg)

На экране несколько сетей. Первый интерфейс это loopback. Он есть на каждом устройстве, и на каждом устройстве у него ip 127.0.0.1. Это способ хоста обратиться к самому себе же. enp0s3 - это есть сеть для выхода в интернет, enp0s8 - наша локальная сеть между машинами А и B. Дальше с помощью данной команды мы добавим ip-адрес для нашего подключения.

```

sudo ip addr add 192.168.1.1/255.255.255.0 dev enp0s8

```
![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a5.jpg)

Теперь делаем то же самое на машине B, но меняем номер машины в сети на второй - 192.168.1.2, а enp0s8 на enp0s3.

![image](https://github.com/cs-itmo-2023/lab-3-Andrzakourcev/assets/144477949/28706e70-f87e-4652-9571-a5d72e470987)


# Проверка работы машины A и B

Используем команду ping

На машине A

```
ping 192.168.1.2
```

![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a6.jpg)


На машине B

```
ping 192.168.1.1
```
![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a7.jpg)

Как можно заметить, все работает в обе стороны.

#Теперь сделаем все то же самое для машин A и C. 

Создадим машину C. В настройках сети машины A выберем 3 адаптер, тип подключения - Внутренняя сеть. Название - LAN2. 

![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a8.jpg)

У машины C то же самое, в 1 адаптере 

![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a9.jpg)

Теперь проделывааем те же действия, что и для подключения машин A и B. Меняем лишь ip на 192.168.2.1, тк это наша 2 подсеть.

Добавляем порт с нужным ip в машине A для enp0s9.

![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a10.jpg)


Для машины C ip - 192.168.2.2

![image]([https://github.com/Anastasia567874/bkdsk/blob/main/image/a14.jpg](https://github.com/Anastasia567874/bkdsk/blob/main/image/a11.jpg))


# Теперь проверим работу машин A и C

Машина A:

![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a12.jpg)


Машина С:

![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a13.jpg)

# Проверка отсутствия соединения между машинами B и C
Попробуем с помощью ping проверить соединение между B и С.

От B к C:

![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a14.jpg)

От C к B:

![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a15.jpg)

Как мы видим, подключение отсутствует.

# Все три терминала вместе:

![image](https://github.com/Anastasia567874/bkdsk/blob/main/image/a16.jpg)

