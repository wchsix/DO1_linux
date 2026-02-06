# Операционные системы UNIX/Linux (Базовый).

Установка и обновления системы Linux. Основы администрирования.

## Part 1. Установка ОС

###  Установить **Ubuntu 20.04 Server LTS** без графического интерфейса. (Используем программу для виртуализации - VirtualBox)

<img width="936" height="56" alt="image" src="https://github.com/user-attachments/assets/9e732971-2c22-47a4-81f0-c76caa3dc915" />


## Part 2. Создание пользователя


### Создать пользователя, отличного от пользователя, который создавался при установке. Пользователь должен быть добавлен в группу `adm`.

Для создания нового пользователя нужно воспользоваться командой **sudo adduser caylaleg**

<img width="500" height="40" alt="image" src="https://github.com/user-attachments/assets/8a2e3845-bafa-49b4-9d0f-56bcd6b24848" />


Команда для добавления пользователя в группу **adm sudo usermod -aG adm caylaleg**

<img width="600" height="40" alt="image" src="https://github.com/user-attachments/assets/6bad2b9e-1152-4f1d-9faa-33bac9b9dece" />

Команда **groups** проверяет, показывает в какой группе находится пользователь

Вывод команды **cat /etc/passwd**

<img width="800" height="615" alt="image" src="https://github.com/user-attachments/assets/a9054bb3-355e-439d-b588-7a2c8c07b7ec" />



## Part 3. Настройка сети ОС


### Задать название машины вида user-1  

Задать название машины можно через команду **sudo set-hostnamectl set-hostname user-1**

<img width="860" height="40" alt="image" src="https://github.com/user-attachments/assets/8b2eb84a-5bd0-4425-97a8-d20939790bca" />


### Установить временную зону, соответствующую вашему текущему местоположению.  

Установить временную зону можно с помощью команды **sudo timedate set-timezone Europe/Moscow** (в соответствии с текущем местоположением) 

<img width="860" height="306" alt="image" src="https://github.com/user-attachments/assets/248712e6-9fae-478b-963b-a260c042db84" />


### Вывести названия сетевых интерфейсов с помощью консольной команды.

Для вывода названия сетевых интерфейсов используется команда – **ip link**

**Интерфейс lo(loopback)** – это виртуальный сетевой интерфейс. Он не виден самому пользователю и с помощью него компьютер может сам себе отправлять запросы. Его еще используют для верстки сайтов или тестировании программ. 

<img width="974" height="284" alt="image" src="https://github.com/user-attachments/assets/38770ac8-e1a9-4435-a38e-e4c9125191c9" />


###  Используя консольную команду получить ip адрес устройства, на котором вы работаете, от DHCP сервера. 

Для вывода IP адреса используется команда – **ip link show (или ip link a)**

<img width="774" height="270" alt="image" src="https://github.com/user-attachments/assets/845a1ae6-4b6d-47d6-b091-58604a655527" />

**DHCP Dynamic Host Configuration Protocol (Протокол Динамической Конфигурации Узла)** - это протокол, который дает автоматически компьютеру IP адрес. 

В данном случае DHCP выдал компьютеру следующий IP адрес: **10.0.2.15/24**

### Определить и вывести на экран внешний ip-адрес шлюза (ip) и внутренний IP-адрес шлюза, он же ip-адрес по умолчанию (gw). 

Для определения внутреннего IP шлюза используется команда **ip route**. В строке default via показан внутренний IP адрес – это IP адрес, через который компьютер выходит в сеть. 
Внешний IP адрес можно найти использовав команду **curl ifconfig.me.**

<img width="936" height="142" alt="image" src="https://github.com/user-attachments/assets/2c648ada-49c8-4c1d-b0c7-ba7c26d40a7c" />

**Внутренний IP-адрес шлюза: 10.0.2.2**

**Внешний IP-адрес шлюза: 77.238.228.195**

### Задать статичные (заданные вручную, а не полученные от DHCP сервера) настройки ip, gw, dns (использовать публичный DNS серверы, например 1.1.1.1 или 8.8.8.8).  

Для того, чтобы задать статичный IP адрес используется программа *Netplan*. Это инструмент в Linux, который может настраивать сеть. 
Чтобы ее открыть для начала надо перейти в соответствующую папку *cd /etc/netplan*, а далее, открыть файл с помощью команды *sudo nano 00-installer-config.yaml.* 
Нужно вписать статичные IP адреса, где: 
- dhcp – это IP адрес, который выдает автоматические DHCP, меняем его на no. 
- Addresses – это IP-адрес компьютера
- Gateway – внутренний IP адрес-шлюза.
-  Nameservers – вписываются DNS сервера. В нашем случае – это 8.8.8.8 и 1.1.1.1

<img width="936" height="702" alt="image" src="https://github.com/user-attachments/assets/e99edf33-4516-4703-a0df-78de3bb6889e" />

Необходимо применить данные изменения с помощью команды **sudo netplan apply**

Проверить изменения через команду **ip a**.

<img width="936" height="346" alt="image" src="https://github.com/user-attachments/assets/7351d721-d3e1-4a67-8f43-47aafb044155" />

<img width="936" height="104" alt="image" src="https://github.com/user-attachments/assets/cd785a80-87e7-4d31-a843-4a52ac7b5ef2" />

### Перезагрузить виртуальную машину. Убедиться, что статичные сетевые настройки (ip, gw, dns) соответствуют заданным в предыдущем пункте.  

Перезагрузка виртуальной машины происходит через команду **sudo reboot**.

<img width="936" height="332" alt="image" src="https://github.com/user-attachments/assets/81473c28-7efc-45bb-96d8-c7837d7e6f97" />

Пропинговать хосты можно через команду **ping**.

Она проверяет связь между собственным компьютером и другим устройством в сети. Фраза «0% packet loss» означает то, что все пакеты дошли успешно. 

<img width="936" height="270" alt="image" src="https://github.com/user-attachments/assets/a97e7086-58be-4445-a306-39cff65e731e" />

<img width="936" height="270" alt="image" src="https://github.com/user-attachments/assets/10ec5ad5-c718-46cc-a234-38a8542b3f6e" />

## Part 4. Обновление ОС


### Обновить системные пакеты до последней на момент выполнения задания версии.  

Для обновления системы используется команда **sudo apt update**. Она нужна для проверки наличия системных пакетов, которые можно установить.
Для обновления используется команда **sudo apt upgrade**. 

<img width="936" height="262" alt="image" src="https://github.com/user-attachments/assets/d4e7e0da-dd4a-49b2-9ff9-2e0d93db1de6" />

После обновления системных пакетов, если ввести команду обновления повторно, то появляется сообщение, что новые системные пакеты отсутствуют. 

<img width="910" height="192" alt="image" src="https://github.com/user-attachments/assets/67af265c-4a91-40c2-bf97-5bac9fa7b07a" />


## Part 5. Использование команды **sudo**


### Разрешить пользователю, созданному в [Part 2](#part-2-создание-пользователя), выполнять команду sudo.

С помощью команды **sudo usermod -aG sudo caylaleg** добавляем пользователя в группу sudo.

**-a** – это добавление пользователя в новую группу, а не замена ее. **-G sudo** означает то, что пользователя добавляют именно в эту группу. 
Для проверки в какую группу добавлен пользователь используется команда – **groups caylaleg**

<img width="936" height="106" alt="image" src="https://github.com/user-attachments/assets/361ccca6-259d-40c9-b0c1-2418d81cf856" />

**Команда sudo** – это команда, которая позволяет обычному пользователю выполнять действия с правами суперпользователя (root). С помощью этой команды можно выполнять операции, присущие администратору, без необходимости постоянно работать от его имени.

Перейдя в профиль, которому дали разрешения выполнять программу sudo, от его лица поменяли hostname ОС с помощью команды **sudo hostnamectl set-hostname user-1**

<img width="936" height="48" alt="image" src="https://github.com/user-attachments/assets/b2b82ba7-cbfc-477e-8b9a-d0f957d81b99" />

## Part 6. Установка и настройка службы времени

### Настроить службу автоматической синхронизации времени.  

<img width="936" height="164" alt="image" src="https://github.com/user-attachments/assets/65058a18-8c42-4969-b41f-6e7bc0809171" />

<img width="936" height="196" alt="image" src="https://github.com/user-attachments/assets/b430c7dd-bc2a-448b-af79-b0bec515c747" />

Автоматическая синхронизация времени работает. В выводе команды **timedatectl show** видно NTPSynchronized=yes, что означает, что системные часы синхронизированы с сервером времени NTP.

## Part 7. Установка и использование текстовых редакторов 

### Установить текстовые редакторы **VIM** (+ любые два по желанию **NANO**, **MCEDIT**, **JOE** и т.д.)  
### Используя каждый из трех выбранных редакторов, создайте файл *test_X.txt*, где X -- название редактора, в котором создан файл. Напишите в нём свой никнейм, закройте файл с сохранением изменений.  

Для установки текстового редактора воспользуемся следующей командой: **sudo apt install X**, где X – это название редактора 

**Текстовый редактор VIM.**

Для его сохранения нужна команда **:w название файла**, далее команда **:q** для выхода. 

<img width="652" height="490" alt="image" src="https://github.com/user-attachments/assets/e830bac7-c54a-4b39-9018-b97adde956c8" />

**Текстовый редактор NANO**

Для его сохранения нужно нажать **control o**, чтобы выйти **control x.**

<img width="652" height="490" alt="image" src="https://github.com/user-attachments/assets/df5f7c5a-c2d4-4a18-a300-6c18ef8f8c53" />

**Текстовый редактор JOE**

Для его сохранения нужно нажать **control K + D**, для выхода из редактора **control C**

<img width="652" height="490" alt="image" src="https://github.com/user-attachments/assets/382d8086-301e-4eee-8eb2-f803d4eefdf2" />


### Используя каждый из трех выбранных редакторов, откройте файл на редактирование, отредактируйте файл, заменив никнейм на строку "21 School 21", закройте файл без сохранения изменений.


**Текстовый редактор VIM**

Для того чтобы выйти без сохранений нужно использовать команду **:q!**

<img width="652" height="409" alt="image" src="https://github.com/user-attachments/assets/3b62c5b9-9aca-4baf-88c1-e06a483fc8d8" />

**Текстовый редактор NANO**

Для того, чтобы выйти без сохранений нужно нажать **control X** и выбрать, что файл не нужно сохранять 

<img width="652" height="409" alt="image" src="https://github.com/user-attachments/assets/f40b77e9-7e89-4336-be37-99fb11a1a162" />

**Текстовый редактор JOE**

Для того, чтобы выйти без сохранений, нужно нажать **control C** и подтвердить, что файл сохранять не нужно 

<img width="652" height="409" alt="image" src="https://github.com/user-attachments/assets/bc13e0cc-a3a4-468b-b0db-cc9291f04374" />


### Используя каждый из трех выбранных редакторов, отредактируйте файл ещё раз (по аналогии с предыдущим пунктом), а затем освойте функции поиска по содержимому файла (слово) и замены слова на любое другое.

**Текстовый редактор VIM**

<img width="652" height="409" alt="image" src="https://github.com/user-attachments/assets/c216635b-76c5-489e-9d49-443f338a0f81" />

Для поиска и замены слова используется команда: **:%s/old/new/g**, где **old** – это старое слово, которое надо найти и заменить, **new** – это слово, на которое надо заменить и **g** – global, который означает, что надо заменить все слова в данном файле 
После замены видно следующее: 


<img width="652" height="409" alt="image" src="https://github.com/user-attachments/assets/759b3700-19fb-4c1b-873f-7e4164ba64fd" />

**Текстовый редактор NANO**

<img width="652" height="409" alt="image" src="https://github.com/user-attachments/assets/86ea6004-37ef-4433-8dc3-fabdb4f7b476" />

Для поиска и замены слов используется команда **control J**, где нужно выбрать какое слово найти и заменить 

<img width="652" height="409" alt="image" src="https://github.com/user-attachments/assets/34f69b39-eafc-4541-b8de-b475c5b4b46c" />

Далее, указать на какое слово заменять 
После замены видно следующее: 

<img width="652" height="409" alt="image" src="https://github.com/user-attachments/assets/fec5910d-0557-4b3f-af2a-6b766c758de4" />

**Текстовый редактор JOE**

<img width="652" height="409" alt="image" src="https://github.com/user-attachments/assets/e525830f-c1d6-4128-8283-4f67089e6f34" />

Для поиска слов нужно использовать команду **control K + F**

Ввести нужное слово для поиска и замены, далее, нужно нажать **r** (replace) и вписать на что изменить 

<img width="652" height="409" alt="image" src="https://github.com/user-attachments/assets/fb314cd8-e9c0-4fcd-8866-9806c9aa35fc" />

Программа спросит, нужно ли заменять это слово

<img width="652" height="409" alt="image" src="https://github.com/user-attachments/assets/96b47195-a9a8-41b0-96b4-a1badb01dc2d" />

После замены видно следующее: 

<img width="652" height="409" alt="image" src="https://github.com/user-attachments/assets/70fcc851-148f-49f4-a163-06cc6106b219" />

## Part 8. Установка и базовая настройка сервиса **SSHD**

### Установить службу SSHd.  

Для установки sshd нужно воспользоваться командой **sudo apt install ssh**

### Добавить автостарт службы при загрузке системы. 

Для автостарта нужно использовать команда **sudo systemctl enable ssh**

<img width="936" height="88" alt="image" src="https://github.com/user-attachments/assets/744ce407-f009-4a8b-94af-65cc16d09bbd" />

### Перенастроить службу SSHd на порт 2022.  

Для того, чтобы перенастроить службу sshd на необходимый порт, нужно выполнить команду **sudo nano /etc/ssh/sshd_config**

<img width="936" height="702" alt="image" src="https://github.com/user-attachments/assets/49bd141b-bf16-4a5c-8c60-020aa97ce6c1" />

### Используя команду ps, показать наличие процесса sshd. Для этого к команде нужно подобрать ключи.

Для этого нужно использовать команду ps -C sshd -f 

<img width="932" height="86" alt="image" src="https://github.com/user-attachments/assets/bd99c39c-dd68-4e91-80fb-dff59acb61d8" />

**ps** – это команда для просмотра процесса, **-C sshd** – означает, что мы смотрим процссы для sshd. **-f** – это полный формат вывода. 
**Строка UID – root** означает то, что программа работает от имени администратора (root) 
**PID (process id)** – номер процесса 
**PPID – 1.** Означает, что sshd запущен и работает системой.

### Перезагрузить систему.

Перезагрузка системы выполняется при помощи команды **sudo systemctl restart ssh**

Использованиe команды **netstat -tan** содержит **tcp 0 0 0.0.0.0:2022 0.0.0.0:* LISTEN**

<img width="936" height="138" alt="image" src="https://github.com/user-attachments/assets/5e6dc678-d7fa-48cb-a3cc-9f509f4480c8" />

**-t** (TCP – соединения) он показывает только tcp соединения. 

**-a**. Этот ключ означает, что он покажет все соединения. 

Показывает и слушающие порты и установленные соединения. В данном случае он в состоянии LISTEN и ssh слушает порт 2022 и готов принять клиента. 

**-n** показывает читаемые имена в цифрах. 

**Recv-Q/Send-Q** – нет ожидающих данных. 

**Local address** это локальный IP адрес и порт. 

**Значения 0.0.0.0** означает, что клиент с любого IP может присоединиться к серверу и подключиться к порту 2022. 

**Foreign Address = 0.0.0.0:*** означает то, что пока нет активных подключений к серверу. 

**State LISTEN** – сервер готов принимать подключения. 

## Part 9. Установка и использование утилит **top**, **htop**

### Установить и запустить утилиты top и htop.  

Утилита top предназначена для вывода списка процессов в реальном времени 
Для установки утилиты top нужна команда **sudo apt install procps**. Для открытия команды нужно воспользоваться командой **top**

<img width="936" height="702" alt="image" src="https://github.com/user-attachments/assets/d79f58d7-0a53-4f9e-950e-6549973a9ec9" />


<img width="936" height="110" alt="image" src="https://github.com/user-attachments/assets/a3234370-ad32-4524-b322-bfb5af188031" />

**Uptime** показывает сколько времени работает система – 12:31:16 

Из скрина видно время работы системы, далее 3 минуты – это время работы сервера. 

**Load average** – это средняя нагрузка системы за 1 минуту, за 5 минут и за 15 минут. В данном случае – это **0,17 0,17 0,08**

**1 user** – количество авторизированных пользователей. 

Всего **90 процессов**, один из которых прямо сейчас используется. 

**:Cpu(s)** – это сколько процессор тратит процентное время либо на пользовательские программы **(us)**, в данном случае  - это **0,3**, системное время **(sy)** - **0,3**, процессы с пониженным приоритетом **(ni)** – **0,0**, процессы, которые не выполняют операций **(id)** – **99,3**, остальные процессы по нулям. 

**MiB mem** – это количество занятой оперативной памяти. В данном случае – это **1956,9**, а свободно – **1466,0**

**MiB Swap** – это количество файлов на диске, он хранит неактивные данные из оперативной памяти. В данном случае – **2048,0**. 

С помощью команды **top -o RES** можно отсортировать процессы по тому, какая занимает память больше всего. 

В данном случае **PID (номер процесса) – 716**.  Или это можно сделать, если зайти в **TOP и нажать на M**. 

<img width="824" height="618" alt="image" src="https://github.com/user-attachments/assets/c1e46eeb-5d9e-4d09-a94e-6854d275033f" />

 С помощью команды **top -o TIME** можно сортировать процессы по тому, кто занимает больше всего процессорного времени. 
 
 В данном случае **PID (номер процесса) – 595**.  Или это можно сделать, если зайти в **TOP и нажать на T**. 

 <img width="838" height="628" alt="image" src="https://github.com/user-attachments/assets/7a552821-72ac-4acc-887d-ece46e41720c" />

Для того чтобы скачать утилиту **htop** нужно воспользоваться командой **sudo apt install htop** и открыть с помощью команды **htop**. 

<img width="854" height="640" alt="image" src="https://github.com/user-attachments/assets/04b989a3-3a79-4d81-8739-3009392c7f03" />

Для сортировки нужно нажать на клавиши **F6**. 

<img width="854" height="640" alt="image" src="https://github.com/user-attachments/assets/ad5171af-149a-4a7c-be7b-c5f124957321" />

Сортировка по **PID**

<img width="854" height="640" alt="image" src="https://github.com/user-attachments/assets/6edc2ccc-d9f0-4385-a6ed-704aaae62437" />

Сортировка по **PERCENT_CPU**

<img width="854" height="640" alt="image" src="https://github.com/user-attachments/assets/e1578912-7c55-4c2a-9b30-e4a177729776" />

Сортировка по **PERCENT_MEM**

<img width="854" height="640" alt="image" src="https://github.com/user-attachments/assets/1b08f375-a1c5-47d9-85a6-fceb4b44663f" />

Сортировка по **TIME**

<img width="854" height="640" alt="image" src="https://github.com/user-attachments/assets/f6b43dd3-dd7d-463a-91f0-a42a75370385" />

Для фильтрации нужно нажать **F4**. И отфильтровать процесс sshd

<img width="854" height="640" alt="image" src="https://github.com/user-attachments/assets/f0581f09-c3ba-4ce5-92b1-de331eb6228b" />

Для поиска нужно воспользоваться клавишей F10. 

<img width="854" height="640" alt="image" src="https://github.com/user-attachments/assets/b74c1077-4e78-4787-9009-650eb5e2b3ba" />

Для добавления hostname, clock и uptime нужно нажать **F2** и выбрать, то, что нужно добавить. 

<img width="854" height="640" alt="image" src="https://github.com/user-attachments/assets/dd3719bd-4d51-4a2b-9aaa-c04e6ce32086" />


<img width="854" height="640" alt="image" src="https://github.com/user-attachments/assets/b47a78ec-33fb-4208-b5d0-ad5985aac819" />

## Part 10. Использование утилиты **fdisk**

### Запустить команду fdisk -l.

Команда запускается с помощью **sudo fdisk -l**

<img width="936" height="162" alt="image" src="https://github.com/user-attachments/assets/2fe8c6a3-18f3-4d94-9827-4952cd4ba02e" />


Название диска - **/dev/sda**, размер **25 GiB** и количество секторов **52428800**

Размер **swap** можно посмотреть с помощью команды **swapon –show**

<img width="936" height="82" alt="image" src="https://github.com/user-attachments/assets/3b895c0e-0126-423c-9544-5e88afe5e6e8" />

Его размер составляет **2G**

## Part 11. Использование утилиты **df** 

### Запустить команду df.  

<img width="936" height="336" alt="image" src="https://github.com/user-attachments/assets/f0898c34-ef1f-4159-9e80-3c4aafaeb7b4" />

С помощью команды **df** можно узнать размер файлов в **1K-blocks**, что является 1 килобайтом. 

Для перевода в мегабайты нужно это число разделить на 1024. А для гигабайт еще на 1024.

**Размер корневого раздела составляет**: 11218472/1024 = 10955 мегабайт, 10955/1024 = 10,67 гигабайт ≈ 11 гигабайт 

**Размер занятого пространства составляет**: 4942/1024 = 4826 мегабайт, 4826/1024 ≈ 4,7 гигабайт


**Размер свободного пространства составляет**: 5684756/1024 = 5552 мегабайт, 5552/1024 ≈ 5,4 гигабайта


Для того, чтобы посмотреть размеры файла нужно использовать команду **df -th**. Ключ h используется для читаемости размера файлов. 

<img width="936" height="326" alt="image" src="https://github.com/user-attachments/assets/9c637784-4fa0-447e-9346-654e666d8675" />

**Размер корневого раздела** составляет 11G

**Размер занятого пространства** составляет 4,8G 

**Размер свободного пространства** составляет 5,5G 

**Процент используемого пространства** составляет 47% 

**G** – это гигабайты. 

Тип файловой системы: **ext4**

## Part 12. Использование утилиты **du**

### Запустить команду du.

Команда **du** показывает размер файлов и папок на диске. Изначально при ее использовании она показывает размер папок в блоках по 1024 байта. 

<img width="936" height="326" alt="image" src="https://github.com/user-attachments/assets/427e7c94-538a-4d3e-82be-6fc0889c71ea" />

### Вывести размер папок /home, /var, /var/log (в байтах, в человекочитаемом виде)

С помощью команды **sudo du -b** можно посмотреть размер папки в **байтах**. 

Для папки **/home**

<img width="936" height="384" alt="image" src="https://github.com/user-attachments/assets/159b29a8-6655-403e-b329-ba7947557be2" />

Для папки **/var**

<img width="936" height="702" alt="image" src="https://github.com/user-attachments/assets/b460db51-1f9b-42f8-a146-2a4b51d47679" />


Для папки **/var/log**

<img width="968" height="56" alt="image" src="https://github.com/user-attachments/assets/ffaf0b7d-ea7f-4d7b-b82f-80cd0dd5dc02" />

С помощью команды **sudo du -h** можно посмотреть размер папки в человекопечатаемом виде 

Для папки **/home**

<img width="936" height="402" alt="image" src="https://github.com/user-attachments/assets/f9234963-9ed7-478e-a274-d58195d74fed" />

Для папки **/var**

<img width="936" height="702" alt="image" src="https://github.com/user-attachments/assets/c50d9b92-c3ab-49a1-866a-274d29707fc4" />

Для папки **/var/log**

<img width="936" height="234" alt="image" src="https://github.com/user-attachments/assets/6f16bb0b-114c-46eb-b0e1-129dde85c11d" />

Чтобы вывести размер в байтах можно еще использовать команду **sudo du -sb**. Где ключ **s** отвечает за то, что размер всех файлов и папок суммируются. Ключ b отвечает за то, что вывод размера был в байтах. 


<img width="936" height="146" alt="image" src="https://github.com/user-attachments/assets/b70ee671-855c-4a3a-be2b-1bec4b4d5de0" />

Чтобы вывести размер в байтах можно еще использовать команду sudo du -sh. Где ключ s отвечает за то, что размер всех файлов и папок суммируются. Ключ h отвечает за то, что вывод размера был человекопечаемом виде. 

<img width="936" height="144" alt="image" src="https://github.com/user-attachments/assets/0f5240df-af03-4518-a8cc-f1e0826094bc" />

### Вывести размер всего содержимого в /var/log (не общее, а каждого вложенного элемента, используя *)

Для всего содержимого нужно использовать команду **sudo -ha /var/log/***

<img width="936" height="702" alt="image" src="https://github.com/user-attachments/assets/9b10d4b1-12f8-43d8-b0b1-e7f4ed7f2f16" />


## Part 13. Установка и использование утилиты **ncdu**

### Установить утилиту ncdu.

Для установки утилиты нужно использовать команду **sudo apt install ncdu**

### Вывести размер папок /home, /var, /var/log.

Для использовании утилиты нужно воспользоваться командой **ncdu** 

Для папки **/home**

<img width="936" height="702" alt="image" src="https://github.com/user-attachments/assets/d1c672b2-29df-4dbf-8530-4d2080963b57" />

Для папки **/var** 

<img width="936" height="702" alt="image" src="https://github.com/user-attachments/assets/e6fa0f3f-1ae7-4203-9db7-d459fc016861" />

Для папки **/var/log**

<img width="936" height="702" alt="image" src="https://github.com/user-attachments/assets/08731a67-5969-4cf2-8807-196a06a42ce4" />



## Part 14. Работа с системными журналами

### Открыть для просмотра:
### 1. /var/log/dmesg
### 2. /var/log/syslog
### 3. /var/log/auth.log  

Для просмотра системных журналов есть несколько способов. Один из который – это использование команды **less**. 

**1. Просмотр /var/log/dmesg**

<img width="784" height="588" alt="image" src="https://github.com/user-attachments/assets/6f4101f4-dbc3-4095-ad1e-3bd9033a8cb8" />

**2.Просмотр /var/log/syslog**

<img width="830" height="622" alt="image" src="https://github.com/user-attachments/assets/602dc735-3653-4401-a66f-0453db705daf" />

**3.Просмотр /var/log/auth.log**

<img width="842" height="632" alt="image" src="https://github.com/user-attachments/assets/5b932ae2-290d-44ed-a86b-5a4bd9ac4101" />

Также, для просмотра системных журналов можно использовать утилиту **lnav**. Для ее установки нужно использовать команду **sudo apt install lnav**. Эта утилита удобнее для использования, поскольку сразу показывает последняя изменения.

**1.Просмотр /var/log/dmesg**

<img width="936" height="702" alt="image" src="https://github.com/user-attachments/assets/f5dccc1a-fa03-4e78-b5b8-0774cf0a5a4e" />

**2.Просмотр /var/log/syslog**

<img width="858" height="644" alt="image" src="https://github.com/user-attachments/assets/92f732fd-4a03-40db-95d1-b3b3057c96c1" />

**3.Просмотр /var/log/auth.log**

<img width="936" height="702" alt="image" src="https://github.com/user-attachments/assets/2ec7e649-f0b3-4ea3-987a-87724258d7d2" />

Информацию о том, когда осуществлялся вход можно посмотреть в **/var/log/auth.log**

<img width="936" height="286" alt="image" src="https://github.com/user-attachments/assets/1623d529-8e79-4489-96a0-b0eb6674ae33" />

Вход в систему осуществлялся 6 февраля 12:53:05. Пользователь nastya. C помощью локального входа (ввод логина) 

Перезапустить службу sshd можно с помощью команды **sudo systemctl restart sshd**

После перезапуска в **/var/log/auth.log** появится эта информация 

<img width="936" height="134" alt="image" src="https://github.com/user-attachments/assets/676a1b68-c743-48ab-b7fb-106400fbb8e8" />

В **/var/log/syslog** увидим следующее: 

<img width="936" height="114" alt="image" src="https://github.com/user-attachments/assets/09652ef5-2e62-42ea-9a03-250d963053fc" />


## Part 15. Использование планировщика заданий **CRON**

### Используя планировщик заданий, запустите команду uptime через каждые 2 минуты.

Для использования планировщика задач нужно использовать команду **crontab -e** и далее выбрать текстовый редактор, в котором предпочтительнее работать. 

<img width="936" height="702" alt="image" src="https://github.com/user-attachments/assets/e330b1aa-282c-4529-906b-9f7d4f06d46e" />

Для того чтобы добавить задачу, чтобы запускалась программа uptime через каждые 2 минуты нужно вписать следующее: 

*/2 * * * * /usr/bin/uptime 

Где, */2 – это часть отвечает за то, что команда выполняется каждые две минуты 
Далее, второй символ * - это часы, третий – день месяца, четвертый – месяц, и пятый – день недели. Дальше используется путь. 

Чтобы узнать о том, выполнилась ли команда, можно зайти в системный журнал, а именно в **/var/log/syslog** 

<img width="936" height="84" alt="image" src="https://github.com/user-attachments/assets/50ab4ab6-ec46-4013-881d-12419c4bf589" />

<img width="936" height="82" alt="image" src="https://github.com/user-attachments/assets/0e635d0a-f682-4d27-a864-5fea8a8fe55f" />

Как видно, команда выполняется каждые 2 минуты 

Для вывода на экран список текущих задач нужно воспользоваться командой **crontab -l** 

<img width="936" height="498" alt="image" src="https://github.com/user-attachments/assets/fc3801b8-cd64-4b7b-999e-2112a07d1eef" />

### Удалите все задания из планировщика заданий.

Удалить все задания можно использовав команду **crontab -r**

Можно узнать об удалении программы зайдя в **/var/log/syslog**

<img width="936" height="70" alt="image" src="https://github.com/user-attachments/assets/0d85d5f9-5a25-46b3-9533-306b6e659b28" />
