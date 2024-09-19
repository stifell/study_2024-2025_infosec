---
## Front matter
title: "Информационная безопасность"
subtitle: "Индидивуальный проект №2"
author: "Матюшкин Денис Владимирович (НПИбд-02-21)"

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
papersize: a4
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

# Цель работы

Целью данной работы является установка DVWA в гостевую систему к Kali Linux.

# Теоретическое введение

VirtualBox (Oracle VM VirtualBox) — программный продукт виртуализации для операционных систем Windows, Linux, FreeBSD, macOS, Solaris/OpenSolaris, ReactOS, DOS и других [@virtualbox-doc:documentation].

Kali Linux — возникший как результат слияния WHAX и Auditor Security Collection. Предназначен прежде всего для проведения тестов на безопасность. Наследник развивавшегося до 2013 года на базе Knoppix дистрибутива BackTrack [@kali-doc:documentation].

Damn Vulnerable Web Application (DVWN) — это программный проект, который намеренно включает уязвимости безопасности и предназначен для образовательных целей [@dvwa:repository].

# Ход работы

1. Перейдите в каталог html и клонируйте репозиторий git (рис. [-@fig:001]).

![Клонирование репозитория dvwa](image/1.png){#fig:001 width=100%}

2. Измените права доступа к папке установки. Перейдите к файлу конфигурации в каталоге установки, скопируйте файл конфигурации и переименуйте его (рис. [-@fig:002]).

![Копирование файла конфигурации](image/2.png){#fig:002 width=100%}

3. Откройте файл настроек и измените пароль на что-то более простое для ввода (рис. [-@fig:003]).

![Новый пароль](image/3.png){#fig:003 width=100%}

4. Установите mariadb (рис. [-@fig:004]).

![Установка утилит](image/4.png){#fig:004 width=100%}

5. Создайте пользователя базы данных. Нужно использовать те же имя пользователя и пароль, которые использовались в файле конфигурации. Предоставьте пользователю все привилегии (рис. [-@fig:005]).

![Новый пользователь БД](image/5.png){#fig:005 width=100%}

6. Откройте для редактирования файл php.ini в каталоге /etc/php/8.2/apache2, чтобы включить следующие параметры: allow_url_fopen и allow_url_include (рис. [-@fig:006]).

![Редактирование файла php.ini](image/6.png){#fig:006 width=100%}

7. Запустите сервер Apache (рис. [-@fig:007]).

![Запуск apache2](image/7.png){#fig:007 width=100%}

8. Откройте DVWA в браузере, введя в адресной строке следующее: 127.0.0.1/DVWA/. Прокрутите вниз и нажмите Create / Reset Database (Создать / сбросить базу данных). Это создаст базу данных, и через несколько секунд вы будете перенаправлены на страницу входа в DVWA (рис. [-@fig:008]).

![Запуск dvwa](image/8.png){#fig:008 width=100%}

9. Войдите в учетную запись (рис. [-@fig:009]).

![Вход в dvwa](image/9.png){#fig:009 width=100%}

# Выводы

В ходе данной лабораторной работы мы установили DVWA в гостевую систему к Kali Linux.

# Список литературы{.unnumbered}

::: {#refs}
:::
