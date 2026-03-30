---
lang: ru-RU
title: Настройка DHCP и DNS
subtitle: Лабораторная работа №8
author:
  - Гафоров Нурмухаммад
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 30.03.2026

toc: false
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---

# Цель работы

## Цель

Изучение настройки сетевых сервисов  
DHCP и DNS в Cisco Packet Tracer  
и исследование процесса автоматической  
настройки узлов сети.

# Ход выполнения

## Исходная топология

- Использована готовая сеть  
- Несколько подсетей  
- Маршрутизатор выполняет маршрутизацию  
- Подключены серверы и ПК  

![Топология сети](Screenshot_1.png){ width=75% }

## Настройка DNS-сервера

- Добавлен сервер dns-ngaforov  
- Подключён к коммутатору  
- Настроен статический IP:
  - 10.128.0.5  
- Указан шлюз:
  - 10.128.0.1  

![IP DNS-сервера](Screenshot_2.png){ width=70% }

## Настройка DNS

- Включена служба DNS  
- Добавлены записи типа A:
  - www → 10.128.0.2  
  - mail → 10.128.0.4  
  - file → 10.128.0.3  
  - dns → 10.128.0.5  

![DNS записи](Screenshot_3.png){ width=70% }

## Настройка DHCP

- DHCP настроен на маршрутизаторе  
- Указан DNS-сервер:
  - 10.128.0.5  
- Созданы пулы адресов  

![Настройка DHCP](Screenshot_4.png){ width=80% }

## Проверка DHCP

- Команда show ip dhcp pool  

![DHCP пулы](Screenshot_8.png){ width=80% }

## Проверка DHCP

- Команда show ip dhcp binding  
- Отображаются выданные адреса  

![DHCP binding](Screenshot_9.png){ width=80% }

## Настройка клиентов

- Включён режим DHCP  
- Устройства получают автоматически:
  - IP  
  - шлюз  
  - DNS  

![DHCP клиент](Screenshot_5.png){ width=70% }

## Проверка сети

- Использована команда ping  
- Проверка между подсетями  
- Связь установлена  

![Ping](Screenshot_7.png){ width=75% }

# DHCP в Simulation

## Процесс DHCP (DORA)

- Discover  
- Offer  
- Request  
- Acknowledgment  

![Simulation](Screenshot_10.png){ width=75% }

## DHCP Discover

- Клиент отправляет broadcast  
- IP: 0.0.0.0 → 255.255.255.255  
- Указывается MAC клиента  

![Discover](Screenshot_11.png){ width=80% }

## DHCP Offer

- Сервер предлагает IP  
- Передаёт параметры сети  
- Указывает DNS  

![Offer](Screenshot_12.png){ width=80% }

## DHCP Request

- Клиент подтверждает выбор  
- Сообщение широковещательное  

![Request](Screenshot_13.png){ width=80% }

## DHCP ACK

- Сервер подтверждает выдачу  
- Назначается IP и параметры  

![ACK](Screenshot_14.png){ width=80% }

# Итог

## Вывод

- Настроены DHCP и DNS  
- Реализована автоматическая выдача IP  
- Изучен процесс DORA  
- Проверена связность сети  
- Подтверждена корректная работа сервисов  
