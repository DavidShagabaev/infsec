---
# Front matter
lang: ru-RU
title: "Лабораторная работа №6"
subtitle: "Мандатное разграничение прав в Linux"
author: "Шагабаев Давид, НПИбд-02-18"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian
polyglossia-otherlangs: english
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: true
pdf-engine: lualatex
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Развить навыки администрирования ОС Linux. Получить первое практическое знакомство с технологией SELinux1 . Проверить работу SELinx на практике совместно с веб-сервером Apache.

# Выполнение лабораторной работы

1. Установка Apache командой

    yum install httpd -y

    ![Установка Apache](image/001.png){ #fig:001 width=70% }

2. В конфигурационном файле /etc/httpd/httpd.conf необходимо задать параметр ServerName: ServerName test.ru

    ![Изменение ServerName](image/002.png){ #fig:002 width=70% }

3. Также необходимо проследить, чтобы пакетный фильтр был отключён или в своей рабочей конфигурации позволял подключаться к 80-у и 81-у портам протокола tcp.

    ![разрешающие правила](image/003.png){ #fig:003 width=70% }

6. Запуск и проверка сервера.

   ![Запуск и проверка сервера.](image/004.png){ #fig:004 width=70% }

7. Найдите веб-сервер Apache в списке процессов, определите его контекст безопасности и занесите эту информацию в отчёт. Например, можно использовать команду

   ps -eZ | grep httpd

   ![контекст безопасности](image/005.png){ #fig:005 width=70% }

6. Посмотрите текущее состояние переключателей SELinux для Apache с помощью команды sestatus -bigrep httpd

![состояние переключателей](image/006.png){ #fig:006 width=70% }

7. Посмотрите статистику по политике с помощью команды seinfo, также определите множество пользователей, ролей, типов.

![Посмотреть статистику по политике](image/007.png){ #fig:007 width=70% }

8. Определите тип файлов и поддиректорий, находящихся в директории /var/www, с помощью команды ls -lZ /var/www

![Определите тип файлов и поддиректорий](image/008.png){ #fig:008 width=70% }

9. Создайте от имени суперпользователя (так как в дистрибутиве после установки только ему разрешена запись в директорию) html-файл /var/www/html/test.html следующего содержания

![содержание файла](image/009.png){ #fig:009 width=70% }

10. Проверьте контекст созданного вами файла. Занесите в отчёт контекст, присваиваемый по умолчанию вновь созданным файлам в директории /var/www/html.

    ![проверка файла](image/010.png){ #fig:010 width=70% }

11. Обратитесь к файлу через веб-сервер, введя в браузере адрес http://127.0.0.1/test.html. Убедитесь, что файл был успешно отображён

    ![обращение к файлу через веб-сервер](image/011.png){ #fig:011 width=70% }

12. Изучите справку man httpd_selinux и выясните, какие контексты файлов определены для httpd. Сопоставьте их с типом файла test.html. Проверить контекст файла можно командой ls -Z. ls -Z /var/www/html/test.html

13. Измените контекст файла /var/www/html/test.html с httpd_sys_content_t на любой другой, к которому процесс httpd не должен иметь доступа, например, на samba_share_t: chcon -t samba_share_t /var/www/html/test.html 

    ls -Z /var/www/html/test.html

    ![Измените контекст файла /var/www/html/test.html](image/012.png){ #fig:012 width=70% }

14. Попробуйте ещё раз получить доступ к файлу через веб-сервер, введя в браузере адрес http://127.0.0.1/test.html. Вы должны получить сообщение об ошибке

![сообщение об ошибке](image/013.png){ #fig:013 width=70% }

15. Проанализируйте ситуацию. Почему файл не был отображён, если права доступа позволяют читать этот файл любому пользователю? ls -l /var/www/html/test.html

![выполнение команд](image/014.png){ #fig:014 width=70% }

Просмотрите log-файлы веб-сервера Apache. Также просмотрите системный лог-файл:

![Просмотрите log-файлы](image/015.png){ #fig:015 width=70% }

16. Попробуйте запустить веб-сервер Apache на прослушивание ТСР-порта 81 (а не 80, как рекомендует IANA и прописано в /etc/services). Для этого в файле /etc/httpd/httpd.conf найдите строчку Listen 80 и замените её на Listen 81.

![Просмотрите log-файлы](image/016.png){ #fig:016 width=70% }

17. Выполните перезапуск веб-сервера Apache.

![перезапуск](image/017.png){ #fig:017 width=70% }

![ошибка](image/018.png){ #fig:018 width=70% }

18. Проанализируйте лог-файлы: tail -nl /var/log/messages Просмотрите файлы /var/log/http/error_log, /var/log/http/access_log и /var/log/audit/audit.log и выясните, в каких файлах появились записи.

    ![/var/log/http/error_log](image/019.png){ #fig:019 width=70% }

    ![/var/log/http/access_log и /var/log/audit/audit.log](image/020.png){ #fig:020 width=70% }

    ![продолжение](image/021.png){ #fig:021 width=70% }

19. Выполните команду semanage port -a -t http_port_t -р tcp 81 После этого проверьте список портов командой semanage port -l | grep http_port_t Убедитесь, что порт 81 появился в списке.

![выполнение команд](image/022.png){ #fig:022 width=70% }

20. Попробуйте запустить веб-сервер Apache ещё раз. Поняли ли вы, почему он сейчас запустился, а в предыдущем случае не смог?

    мы добавили 81 порт, поэтому сейчас всё сработало.

![запустили веб-сервер Apache ещё раз](image/024.png){ #fig:024 width=70% }

21. Верните контекст httpd_sys_cоntent__t к файлу /var/www/html/ test.html: chcon -t httpd_sys_content_t /var/www/html/test.html После этого попробуйте получить доступ к файлу через веб-сервер, введя в браузере адрес http://127.0.0.1:81/test.html. Вы должны увидеть содержимое файла — слово «test».

![получили доступ](image/025.png){ #fig:025 width=70% }

22. Исправьте обратно конфигурационный файл apache, вернув Listen 80.

![исправили обратно](image/026.png){ #fig:026 width=70% }

23. Удалите привязку http_port_t к 81 порту: semanage port -d -t http_port_t -p tcp 81 и проверьте, что порт 81 удалён.
24. Удалите файл /var/www/html/test.html: rm /var/www/html/test.html

![Удалили файл](image/027.png){ #fig:027 width=70% }



# Выводы

Развили навыки администрирования ОС Linux. Получили первое практическое знакомство с технологией SELinux1 . Проверили работу SELinx на практике совместно с веб-сервером Apache.