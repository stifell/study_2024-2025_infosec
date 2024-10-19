---
## Front matter
title: "Информационная безопасность"
subtitle: "Лабораторная работа №7"
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

Освоить на практике применение режима однократного гаммирования.

# Теоретическое введение

VirtualBox (Oracle VM VirtualBox) — программный продукт виртуализации для операционных систем Windows, Linux, FreeBSD, macOS, Solaris/OpenSolaris, ReactOS, DOS и других [@virtualbox-doc:documentation].

Rocky Linux — дистрибутив Linux, разработанный Rocky Enterprise Software Foundation. Предполагается, что это будет полный бинарно-совместимый выпуск, использующий исходный код операционной системы Red Hat Enterprise Linux (RHEL) [@rocky-doc:documentation].

# Задача

Нужно подобрать ключ, чтобы получить сообщение «С Новым Годом,
друзья!». Требуется разработать приложение, позволяющее шифровать и
дешифровать данные в режиме однократного гаммирования. Приложение
должно:

1. Определить вид шифротекста при известном ключе и известном открытом тексте.

2. Определить ключ, с помощью которого шифротекст может быть преобразован в некоторый фрагмент текста, представляющий собой один из
возможных вариантов прочтения открытого текста.

# Программа

Написанная программа на Java:

```java
import java.util.Random;

/**
 * @author Денис on 19.10.2024
 */

public class Main {

    public static String xorText(String text, String key) {
        if (text.length() != key.length()) {
            return "Ошибка: Ключ и текст разной длины";
        }

        StringBuilder xorText = new StringBuilder();
        for (int i = 0; i < text.length(); i++) {
            char xorChar = (char) (text.charAt(i) ^ key.charAt(i));
            xorText.append(xorChar);
        }

        return xorText.toString();
    }

    public static String generateKey(int length) {
        String chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
        StringBuilder key = new StringBuilder();
        Random random = new Random();
        for (int i = 0; i < length; i++) {
            key.append(chars.charAt(random.nextInt(chars.length())));
        }

        return key.toString();
    }

    public static void main(String[] args) {
        String text = "С Новым Годом, друзья!";
        System.out.println("Текст: " + text);

        String key = generateKey(text.length());
        System.out.println("Ключ: " + key);

        String encryptedText = xorText(text, key);
        System.out.println("Зашифрованный текст: " + encryptedText);

        String decryptedText = xorText(encryptedText, key);
        System.out.println("Расшифрованный текст: " + decryptedText);
    }
}
```

Вывод программы (рис. [-@fig:001]).

![Вывод программы](image/1.png){#fig:001 width=100%}

# Выводы

В ходе данной лабораторной работы мы освоили на практике применение режима однократного гаммирования.

# Список литературы{.unnumbered}

::: {#refs}
:::
