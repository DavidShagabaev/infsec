---
## Front matter
lang: ru-RU
title: Лабораторная работа №7
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

Освоить на практике применение режима однократного гаммирования.

# Ход выполнения работы

## Этапы 

1. первая часть
2. вторая часть


## первая часть

def make_cypher(text, code):
    if len(text)!=len(code):
        return None
    return''.join(chr(ord(a) ^ ord(b)) for a,b in zip(text, code))

make_cypher('С новым годом, друзья!', 'ХожуНаОчныеПары В ВУЗ!')

make_cypher('\x04О\x0b}/{"ѧ\x0eu\x01!\x0cѬѫДRѣ%oX\x00', 'ХожуНаОчныеПары В ВУЗ!')

## вторая часть

def make_cypher(text, code):
    if len(text)!=len(code):
        return None
    return''.join(chr(ord(a) ^ ord(b)) for a,b in zip(text, code))

make_cypher('С новым годом, друзья!', '\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00')

# Вывод

Освоил на практике применение режима однократного гаммирования.


## {.standout}

Спасибо за внимание!
