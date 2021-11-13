---
## Front matter
lang: ru-RU
title: Лабораторная работа №5
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

Изучение механизмов изменения идентификаторов, применения SetUID- и Sticky-битов. Получение практических навыков работы в консоли с дополнительными атрибутами. Рассмотрение работы механизма смены идентификатора процессов пользователей, а также влияние бита Sticky на запись и удаление файлов.

# Ход выполнения работы

## Этапы 

2. Создание программы.
3. Исследование Sticky-бита.


## Создание программы.

 Создайте программу simpleid.c

Скомплилируйте программу и убедитесь, что файл программы создан

gcc simpleid.c -o simpleid

Выполните программу simpleid: 

./simpleid

Выполните системную программу id: 

id

## Создание программы.

Скомпилируйте и запустите simpleid2.c:

 gcc simpleid2.c -o simpleid2 

./simpleid2

От имени суперпользователя выполните команды:

chown root:guest /home/guest/simpleid2 

chmod u+s /home/guest/simpleid2

Выполните проверку правильности установки новых атрибутов и смены владельца файла simpleid2: 

ls -l simpleid2

Запустите simpleid2 и id:

Проделайте тоже самое относительно SetGID-бита

Создайте программу readfile.c:

## Исследование Sticky-бита

Выясните, установлен ли атрибут Sticky на директории /tmp, для чего выполните команду 

ls -l / | grep tmp

От имени пользователя guest создайте файл file01.txt в директории /tmp со словом test: echo "test" > /tmp/file01.txt

От пользователя guest2 (не являющегося владельцем) попробуйте прочитать файл /tmp/file01.txt: 

cat /tmp/file01.txt

От пользователя guest2 попробуйте дозаписать в файл /tmp/file01.txt слово test2 командой

От пользователя guest2 попробуйте записать в файл /tmp/file01.txt слово test3, стерев при этом всю имеющуюся в файле информацию командой

От пользователя guest2 попробуйте удалить файл /tmp/file01.txt командой 

rm /tmp/fileOl.txt

и выполните после этого команду, снимающую атрибут t (Sticky-бит) с директории /tmp: chmod -t /tmp

Повторите предыдущие шаги. Какие наблюдаются изменения?

# Вывод

Изучили механизмы изменения идентификаторов, применения SetUID- и Sticky-битов. Получили практические навыки работы в консоли с дополнительными атрибутами. Рассмотрели работы механизма смены идентификатора процессов пользователей, а также влияние бита Sticky на запись и удаление файлов.


## {.standout}

Спасибо за внимание!
