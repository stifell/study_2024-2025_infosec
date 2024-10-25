---
## Front matter
title: "Информационная безопасность"
subtitle: "Лабораторная работа №8"
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

Освоить на практике применение режима однократного гаммирования
на примере кодирования различных исходных текстов одним ключом.

# Теоретическое введение

VirtualBox (Oracle VM VirtualBox) — программный продукт виртуализации для операционных систем Windows, Linux, FreeBSD, macOS, Solaris/OpenSolaris, ReactOS, DOS и других [@virtualbox-doc:documentation].

Rocky Linux — дистрибутив Linux, разработанный Rocky Enterprise Software Foundation. Предполагается, что это будет полный бинарно-совместимый выпуск, использующий исходный код операционной системы Red Hat Enterprise Linux (RHEL) [@rocky-doc:documentation].

# Задача

Два текста кодируются одним ключом (однократное гаммирование).
Требуется не зная ключа и не стремясь его определить, прочитать оба текста. Необходимо разработать приложение, позволяющее шифровать и дешифровать тексты P1 и P2 в режиме однократного гаммирования. Приложение должно определить вид шифротекстов C1 и C2 обоих текстов P1 и
P2 при известном ключе ; Необходимо определить и выразить аналитически способ, при котором злоумышленник может прочитать оба текста, не
зная ключа и не стремясь его определить.


# Программа

Написанная программа на Python:

```python
import secrets

def generate_random_key(length):
    return secrets.token_bytes(length)

def xor_operation(text, key):
    return bytes([t ^ k for t, k in zip(text, key)])

def encrypt(text, key):
    return xor_operation(text, key)

def decrypt_unknown_key(c1, c2, known_plaintext):
    return xor_operation(xor_operation(c1, c2), known_plaintext)

P1 = b"NaVashishodyashiyot1204"
P2 = b"VSevernyyfilialBanka"

key_length = max(len(P1), len(P2))
K = generate_random_key(key_length)

C1 = encrypt(P1, K)
C2 = encrypt(P2, K)
recovered_P2 = decrypt_unknown_key(C1, C2, P1)

print(f'Ключ K: {K}\n')
print(f'Шифротекст C1: {C1.hex()}')
print(f'Шифротекст C2: {C2.hex()}')
print(f'Восстановленный P2: {recovered_P2}')
```

Вывод программы (рис. [-@fig:001]).

![Вывод программы](image/1.png){#fig:001 width=100%}

# Контрольные вопросы

Ответы на ваши вопросы можно найти в содержании загруженного файла:

1. **Как, зная один из текстов (P1 или P2), определить другой, не зная при этом ключа?**  
   Если известен один из текстов и оба зашифрованы одним и тем же ключом, то злоумышленник может вычислить другой текст, не зная ключа. Поскольку $C1 \oplus C2 = P1 \oplus P2$, зная $P1$, можно получить $P2$ через $C1 \oplus C2 \oplus P1 = P2$.

2. **Что будет при повторном использовании ключа при шифровании текста?**  
   Повторное использование одного и того же ключа приводит к утечке информации. При шифровании разных текстов одним ключом, результат их сложения по модулю 2 будет равен сложению исходных текстов, что делает возможным раскрытие информации о каждом из них.

3. **Как реализуется режим шифрования однократного гаммирования одним ключом двух открытых текстов?**  
   Однократное гаммирование реализуется так: каждый исходный текст (например, $P1$ и $P2$) шифруется с помощью операции XOR с ключом $K$, давая шифротексты $C1 = P1 \oplus K$ и $C2 = P2 \oplus K$.

4. **Перечислите недостатки шифрования одним ключом двух открытых текстов.**  
   - Возможность вычислить второй текст, зная один из шифротекстов и один открытый текст.
   - Увеличивается вероятность раскрытия содержания при многократном использовании ключа.
   - Падает стойкость шифрования, так как с каждой новой парой текстов и их шифровок вероятность восстановления ключа возрастает.

5. **Перечислите преимущества шифрования одним ключом двух открытых текстов.**  
   Основным преимуществом может быть простота и быстрота шифрования, а также удобство использования одного ключа для нескольких сообщений, однако такие преимущества крайне ограничены и часто не перевешивают риски.

# Выводы

В ходе данной лабораторной работы мы освоили на практике применение режима однократного гаммирования
на примере кодирования различных исходных текстов одним ключом.

# Список литературы{.unnumbered}

::: {#refs}
:::
