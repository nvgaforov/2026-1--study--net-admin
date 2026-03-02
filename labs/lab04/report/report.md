---
## Front matter
title: "Отчёт по лабораторной работе 4"
subtitle: "Первоначальное конфигурирование сети"
author: "Гафоров Нурмухаммад"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Введение

## Цель работы  

Провести подготовительную работу по первоначальной настройке коммутаторов сети.

## Ход выполнения

В логической рабочей области Packet Tracer был создан новый проект. В соответствии со схемой сети L1 размещены пять коммутаторов Cisco 2950T-24, рабочие станции PC-PT и серверы Server-PT. Топология включает два сегмента (msk-pavlovskaya и msk-donskaya), соединённых магистральными линиями.

Коммутаторы соединены между собой через интерфейсы FastEthernet/GigabitEthernet. Оконечные устройства подключены к портам FastEthernet с использованием медного прямого кабеля (Copper Straight-Through).

![Топология сети L1](Screenshot_1.png){ width=85% }

В структуру сети используются следующие коммутаторы:
- msk-pavlovskaya-ngaforov-sw-1
- msk-donskaya-ngaforov-sw-1
- msk-donskaya-ngaforov-sw-2
- msk-donskaya-ngaforov-sw-3
- msk-donskaya-ngaforov-sw-4

Также подключены серверы:
- web-ngaforov
- file-ngaforov
- mail-ngaforov

### Первоначальная настройка коммутаторов

Настройка каждого коммутатора выполнялась через CLI в привилегированном режиме. Для каждого устройства были выполнены следующие действия:

1. Переход в режим конфигурации и назначение имени устройства (hostname).
2. Создание интерфейса управления VLAN 2.
3. Активация интерфейса командой no shutdown.
4. Назначение IP-адреса согласно плану адресации.
5. Настройка шлюза по умолчанию 10.128.1.1.
6. Настройка удалённого доступа (line vty 0 4) с паролем cisco.
7. Настройка консольного доступа (line console 0).
8. Установка enable secret cisco.
9. Включение service password-encryption.
10. Создание локального пользователя admin privilege 1 secret cisco.
11. Назначение доменного имени donskaya.rudn.edu.
12. Генерация RSA-ключей и включение SSH-доступа.
13. Сохранение конфигурации командой write memory.

При генерации RSA-ключей был выбран размер 512 бит. Система выдала предупреждение о необходимости ключа не менее 768 бит для SSH версии 2, однако SSH был активирован.

### IP-адреса интерфейсов управления (VLAN 2)

В соответствии с планом IP-адресации назначены следующие адреса:

- msk-donskaya-ngaforov-sw-1 — 10.128.1.2/24
- msk-donskaya-ngaforov-sw-2 — 10.128.1.3/24
- msk-donskaya-ngaforov-sw-3 — 10.128.1.4/24
- msk-donskaya-ngaforov-sw-4 — 10.128.1.5/24
- msk-pavlovskaya-ngaforov-sw-1 — 10.128.1.6/24

Для всех коммутаторов установлен шлюз по умолчанию 10.128.1.1.

### Настройка msk-donskaya-ngaforov-sw-1

На интерфейсе VLAN 2 назначен IP-адрес 10.128.1.2 255.255.255.0. Интерфейс переведён в состояние up. Настроены параметры удалённого доступа, включено шифрование паролей, создан пользователь admin и активирован SSH.

![Конфигурация msk-donskaya-ngaforov-sw-1](Screenshot_2.png){ width=85% }

### Настройка msk-donskaya-ngaforov-sw-2

Интерфейс VLAN 2 получил IP-адрес 10.128.1.3 255.255.255.0. Выполнена базовая настройка безопасности и удалённого доступа. Конфигурация сохранена.

![Конфигурация msk-donskaya-ngaforov-sw-2](Screenshot_3.png){ width=85% }

### Настройка msk-donskaya-ngaforov-sw-3

Назначен IP-адрес 10.128.1.4 255.255.255.0. Настроены линии vty и console, установлен enable secret, создан пользователь admin, включён SSH-доступ.

![Конфигурация msk-donskaya-ngaforov-sw-3](Screenshot_4.png){ width=85% }

### Настройка msk-donskaya-ngaforov-sw-4

На интерфейсе VLAN 2 назначен IP-адрес 10.128.1.5 255.255.255.0. Выполнена стандартная последовательность команд первоначальной настройки. Конфигурация сохранена в энергонезависимую память.

![Конфигурация msk-donskaya-ngaforov-sw-4](Screenshot_5.png){ width=85% }

### Настройка msk-pavlovskaya-ngaforov-sw-1

Интерфейсу VLAN 2 назначен IP-адрес 10.128.1.6 255.255.255.0. При вводе команды line console 0 первоначально была допущена синтаксическая ошибка, после чего команда была введена корректно. Настроен удалённый доступ по SSH и сохранена конфигурация.

![Конфигурация msk-pavlovskaya-ngaforov-sw-1](Screenshot_6.png){ width=85% }

# Вывод

В ходе работы создана топология сети L1, выполнено физическое подключение устройств, настроены интерфейсы управления VLAN 2, назначены IP-адреса в подсети 10.128.1.0/24, установлен шлюз по умолчанию, настроены механизмы аутентификации и удалённого доступа по SSH, включено шифрование паролей и сохранена конфигурация всех коммутаторов.

## Контрольные вопросы

### 1. При помощи каких команд можно посмотреть конфигурацию сетевого оборудования?

Для просмотра текущей конфигурации (running configuration), которая хранится в оперативной памяти (RAM), используется команда:

show running-config

или сокращённый вариант:

show run

Данная команда отображает все активные параметры устройства: имя хоста, интерфейсы, IP-адреса, настройки VLAN, параметры доступа (console, vty), маршрутизацию, службы и другие элементы конфигурации.

Для просмотра отдельных разделов конфигурации могут использоваться уточняющие команды, например:

show ip interface brief — краткая информация об интерфейсах  
show vlan — список VLAN  
show interfaces — подробная информация об интерфейсах  

### 2. При помощи каких команд можно посмотреть стартовый конфигурационный файл оборудования?

Стартовая конфигурация (startup configuration) хранится в энергонезависимой памяти (NVRAM) и загружается при включении устройства.

Для её просмотра используется команда:

show startup-config

или сокращённая форма:

show start

Эта команда позволяет проверить, какая конфигурация будет применена после перезагрузки устройства.

### 3. При помощи каких команд можно экспортировать конфигурационный файл оборудования?

Экспорт конфигурации возможен путём копирования её на внешний сервер (TFTP, FTP, SCP).

Для сохранения текущей конфигурации на TFTP-сервер используется команда:

copy running-config tftp

Для сохранения стартовой конфигурации:

copy startup-config tftp

Также возможны варианты:

copy running-config ftp  
copy running-config scp  

После ввода команды указывается IP-адрес сервера и имя файла.

### 4. При помощи каких команд можно импортировать конфигурационный файл оборудования?

Импорт конфигурации выполняется копированием файла с внешнего сервера в память устройства.

Для загрузки конфигурации в оперативную память:

copy tftp running-config

Для загрузки конфигурации в энергонезависимую память:

copy tftp startup-config

После выполнения команды указывается IP-адрес сервера и имя файла конфигурации.
