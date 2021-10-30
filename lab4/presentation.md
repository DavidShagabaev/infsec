---
## Front matter
lang: ru-RU
title: Лабораторная работа №4
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

Получение практических навыков работы в консоли с расширенными атрибутами файлов.



# Ход выполнения работы

## Этапы 

1. Подключаем расширенный атрибут а файлу.
2. Смотрим что они нам позволяют делать с файлом.
3. Повторяем эти действия с атрибутом i.


## Подключаем расширенный атрибут а файлу.

 определите расширенные атрибуты файла.

(lsattr /home/guest/dir1/file1)

Попробуйте установить на файл /home/guest/dir1/file1 расширенный атрибут a от имени пользователя guest.

(chattr +a /home/guest/dir1/file1)

От имени суперпользователя повторяем попытку установки атрибута.

Проверяем подключение атрибута a.

(lsattr /home/guest/dir1/file1)


## Смотрим что они нам позволяют делать с файлом.

Выполните дозапись в файл file1 слова «test»: 

(echo "test" /home/guest/dir1/file1)

После этого выполните чтение файла file1. 

(cat /home/guest/dir1/file1)

Попробуйте удалить файл file1 либо стереть имеющуюся в нём информацию.

(echo "abcd" > /home/guest/dirl/file1)

Снимите расширенный атрибут a с файла.

(chattr -a /home/guest/dir1/file1)

Повторите операции, которые вам ранее не удавалось выполнить.

## Повторяем эти действия с атрибутом i.

Попробуйте установить на файл /home/guest/dir1/file1 расширенный атрибут i от имени пользователя guest.

(chattr +i /home/guest/dir1/file1)

Повторяем действия из второго этапа рабрты.

# Вывод

Получен практический навык работы в консоли с расширенными атрибутами файлов.


## {.standout}

Спасибо за внимание!
