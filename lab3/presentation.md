---
## Front matter
lang: ru-RU
title: Лабораторная работа №3
author: |
	Шагабаев Д.А\inst{1}
institute: |
	\inst{1}RUDN University, Moscow, Russian Federation
date: 2021 Moscow, Russia

## Formatting
toc: false
slide_level: 2
theme: metropolis
header-includes: 
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'
aspectratio: 43
section-titles: true
---

# Цели 

## Цель работы

Получение практических навыков работы в консоли с атрибутами файлов для групп пользователей.



# Ход выполнения работы

## Этапы 

1. Создаём два пользователя.
2. Добавляем второго пользователя в группу первого и проверяем.
3. Заполняем таблицы.


## Создаём два пользователя.

 создайте учётную запись пользователя guest и guest2.

(useradd guest)

Задайте пароль для пользователя guest и guest2.

(passwd guest)


## Добавляем второго пользователя в группу первого и проверяем.

Добавьте пользователя guest2 в группу guest: 

(gpasswd -a guest2 guest)

Уточните имя вашего пользователя, его группу, кто входит в неё и к каким группам принадлежит он сам. 

(pwd)

(groups guest)

(groups)

(id -Gn)

(и id -G)

Сравните полученную информацию с содержимым файла /etc/group.

(cat /etc/group)

## Заполняем таблицы.

От имени пользователя guest2 выполните регистрацию пользователя guest2 в группе guest командой

(newgrp guest)

От имени пользователя guest измените права директории /home/guest, разрешив все действия для пользователей группы:

(chmod g+rwx /home/guest)

От имени пользователя guest снимите с директории /home/guest/dir1 все атрибуты командой:

(chmod 000 dirl)

# Вывод

Получены практические навыки работы в консоли с атрибутами файлов для групп пользователей.


## {.standout}

Спасибо за внимание!
