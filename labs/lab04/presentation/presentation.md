---
lang: ru-RU
title: Первоначальное конфигурирование сети
subtitle: Лабораторная работа №4
author:
  - Гафоров Нурмухаммад
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 02.03.2026

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

Провести первоначальную настройку коммутаторов  
и подготовить сеть к дальнейшему администрированию.

# Ход выполнения

## Построение топологии L1

- Размещены 5 коммутаторов Cisco 2950T-24  
- Подключены ПК и серверы  
- Сегменты: msk-pavlovskaya и msk-donskaya  
- Использованы кабели Copper Straight-Through  

![Топология сети L1](Screenshot_1.png){ width=80% }

## Структура сети

Коммутаторы:

- msk-pavlovskaya-ngaforov-sw-1  
- msk-donskaya-ngaforov-sw-1  
- msk-donskaya-ngaforov-sw-2  
- msk-donskaya-ngaforov-sw-3  
- msk-donskaya-ngaforov-sw-4  

Серверы:

- web-ngaforov  
- file-ngaforov  
- mail-ngaforov  

# Первоначальная настройка

## Общая последовательность конфигурации

На каждом коммутаторе выполнено:

- Назначение hostname  
- Настройка interface vlan 2  
- Назначение IP-адреса  
- Установка ip default-gateway 10.128.1.1  
- Настройка console и vty  
- Установка enable secret  
- Включение service password-encryption  
- Создание пользователя admin  
- Назначение доменного имени  
- Генерация RSA-ключей  
- Включение SSH  
- Сохранение конфигурации  

## IP-адреса VLAN 2

- sw-1 — 10.128.1.2/24  
- sw-2 — 10.128.1.3/24  
- sw-3 — 10.128.1.4/24  
- sw-4 — 10.128.1.5/24  
- pavlovskaya-sw-1 — 10.128.1.6/24  

Шлюз по умолчанию: 10.128.1.1  

# Настройка коммутаторов

## msk-donskaya-ngaforov-sw-1

- IP: 10.128.1.2/24  
- VLAN 2 активирован  
- Настроен SSH-доступ  
- Конфигурация сохранена  

![Настройка sw-1](Screenshot_2.png){ width=80% }

## msk-donskaya-ngaforov-sw-2

- IP: 10.128.1.3/24  
- Настроены console и vty  
- Создан пользователь admin  
- Включено шифрование паролей  

![Настройка sw-2](Screenshot_3.png){ width=80% }

## msk-donskaya-ngaforov-sw-3

- IP: 10.128.1.4/24  
- Активирован SSH  
- Сохранена конфигурация  

![Настройка sw-3](Screenshot_4.png){ width=80% }

## msk-donskaya-ngaforov-sw-4

- IP: 10.128.1.5/24  
- Выполнена базовая настройка безопасности  

![Настройка sw-4](Screenshot_5.png){ width=80% }

## msk-pavlovskaya-ngaforov-sw-1

- IP: 10.128.1.6/24  
- Исправлена синтаксическая ошибка в CLI  
- Настроен SSH-доступ  
- Конфигурация сохранена  

![Настройка pavlovskaya-sw-1](Screenshot_6.png){ width=80% }

# Итог

## Вывод

В ходе работы:

- Построена топология L1  
- Настроены интерфейсы управления VLAN 2  
- Назначены IP-адреса в сети 10.128.1.0/24  
- Настроен удалённый доступ по SSH  
- Обеспечена базовая защита доступа  
- Конфигурация сохранена во всех коммутаторах  