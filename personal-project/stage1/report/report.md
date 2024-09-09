---
## Front matter
title: "Информационная безопасность"
subtitle: "Индидивуальный проект №1"
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

Целью данной работы является приобретение практических навыков установки операционной системы Kali Linux на виртуальную машину, настройки минимально необходимых для дальнейшей работы сервисов.

# Теоретическое введение

VirtualBox (Oracle VM VirtualBox) — программный продукт виртуализации для операционных систем Windows, Linux, FreeBSD, macOS, Solaris/OpenSolaris, ReactOS, DOS и других [@virtualbox-doc:documentation].

Kali Linux — возникший как результат слияния WHAX и Auditor Security Collection. Предназначен прежде всего для проведения тестов на безопасность. Наследник развивавшегося до 2013 года на базе Knoppix дистрибутива BackTrack. [@kali-doc:documentation].

# Ход работы

1. Создайте новую виртуальную машину. Укажите имя виртуальной машины, тип операционной системы — Linux, Kali (рис. [-@fig:001]).

![Окно «Имя машины и тип ОС»](image/1.png){#fig:001 width=100%}

2. Укажите размер основной памяти виртуальной машины — 2048 МБ (или большее число, кратное 1024 МБ, если позволяют технические характеристики вашего компьютера) и количество виртуальных процессоро (рис. [-@fig:002]).

![Окно «Размер основной памяти»](image/2.png){#fig:002 width=100%}

3. Задайте размер диска — 40 ГБ (или больше) (рис. [-@fig:003]).

![Окно определения размера виртуального динамического жёсткого диска](image/3.png){#fig:003 width=100%}

4. Создайте виртуальную машину (рис. [-@fig:004]).

![Окно создания виртуальной машины](image/4.png){#fig:004 width=100%}

5. Запустите виртуальную машину, выберите English в качестве языка интерфейса и перейдите к настройкам установки операционной системы (рис. [-@fig:005]).

![Установка английского языка интерфейса ОС](image/5.png){#fig:005 width=100%}

6. Выберите местоположение (рис. [-@fig:006]).

![Выбор местоположения](image/6.png){#fig:006 width=100%}

7. Включите сетевое соединение и в качестве имени узла укажите user.localdomain, где вместо user укажите имя своего пользователя в соответствии с соглашением об именовании (рис. [-@fig:007]).

![Окно настройки установки: сеть и имя узла](image/7.png){#fig:007 width=100%}

8. Задайте имя пользователя и пароль (рис. [-@fig:008] и [-@fig:009]).

![Настройка пользователя](image/8.png){#fig:008 width=100%}

![Установка пароля для пользователя](image/9.png){#fig:009 width=100%}

9. Выберите часовой пояс (рис. [-@fig:010]).

![Выбор часового пояса](image/10.png){#fig:010 width=100%}

10. Выберите способ разбиения жесткого диска (рис. [-@fig:011]).

![Способ разбиения ЖД](image/11.png){#fig:011 width=100%}

11. Выберите схему разбиения. По умолчанию выбран вариант Все файлы в одном разделе (рис. [-@fig:012]).

![Схема разбиения](image/12.png){#fig:012 width=100%}

12. Начните загрузку компонентов (рис. [-@fig:013]).

![Загрузка компонентов](image/13.png){#fig:013 width=100%}

13. Войдите в ОС под заданной вами при установке учётной записью. В меню Устройства виртуальной машины подключите образ диска дополнений гостевой ОС (рис. [-@fig:014] и [-@fig:015]).

![Вход в ОС](image/14.png){#fig:014 width=100%}

![Подключение образа диска дополнений гостевой ОС](image/15.png){#fig:015 width=100%}

# Выводы

В ходе данной лабораторной работы мы приобрели практические навыки установки операционной системы Kali Linux на виртуальную машину, настроили минимально необходимые для дальнейшей работы сервисы.

# Список литературы{.unnumbered}

::: {#refs}
:::
