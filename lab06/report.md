---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе №6"
author: "Сырцов Александр Юрьевич"

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
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
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

Научится находить частичные и полные суммы рядов, значения пределов и интегралов в Octave.

# Задание

• Сделать отчёт по лабораторной работе в формате Markdown.

• В качестве ответа предоставить отчёты в 3 форматах: pdf, docx и md (в архиве, поскольку он должен содержать скриншоты, Makefile и т.д.)

# Выполнение лабораторной работы

## Пределы, последовательности и ряды

1. Реализую функцию для оценки некоторого предела.

Функция реализована в функциональном стиле и представляет собой анонимное лямбда-выражение, присвоенное объекту `f`, которое в качестве своего терма принимает вектор значений `n`. Вместе с тем сразу задаём вектор `k` и меняем формат отображения чисел для следующего шага (рис. -@fig:001).

![Анонимная функция и вектор *k*](pictures/pic1.png){ #fig:001 width=70% }

Замечание 1: вектор `k` задан как транспонированный конвектор, что крайне удобно и быстро в сочетании с range-оператором.

Замечание 2: Реализованная функция чистая и является функцией первого класса, однако перестаёт быть анонимной после присвоения объекту `f`, так как он становится "allias" для изначального выражения.

2. Вектор индексов `k` определил собой количество итераций для вектора `n` (рис. -@fig:002), представляя собой степени от 0 до 9. Итоговый вектор значений – это вектор чисел от 1 до 1000000000. При его подстановке в функцию `f` мы постепенно приближаемся к окрестности нужного значения и по закономерности чисел можно сказать, к какому значению стремиться предел, а именно к значению числа *e*, так как это второй замечательный предел (рис. -@fig:003).

![Инициалзация вектора значений](pictures/pic2.png){ #fig:002 width=70% }

![Подстановка значений в функцию](pictures/pic3.png){ #fig:003 width=70% }

замечание: можно было не инициализировать отдельно `k`, а сразу подставить вектор для экономии памяти.

## Частичные суммы

3. Необходимо рассчитать частичные суммы ряда от второго до одинадцатого элемента включительно.

Для этого я инициализирую вектор индексов и подставляю в n-й член ряда, получая десять элементов ряда (рис. -@fig:004).

![Значения для нахождения частичных сумм](pictures/pic4.png){ #fig:004 width=70% }

4. Частичные суммы расчитываются, как суммы от одного элемента до другого, не покрывая исходный ряд. Следуя такой логике, реализую цикл от 1 до 10, где в конвектор частичных сумм записывается сумма от первого элемента вектора `a` до i-го с помощью функции `sum()`. В конце выодим все значения через транспонированный конвектор (рис. -@fig:005).

![Частичные суммы](pictures/pic5.png){ #fig:005 width=70% }

5. Визуализирую резултаты и очевидно получаю обратную корелляцию между значениями ряда и значением частичных сумм (рис. -@fig:006)(рис. -@fig:007).

![Граафик значений элементов ряда и частичных сумм ряда](pictures/pic6.png){ #fig:006 width=70% }
![Граафик](pictures/pic7.png){ #fig:007 width=70% }
## Сумма ряда

6. Найду сумму элеметов горманического ряда.

Аналогично задав вектор индексов, находим элементы ряда и используем стандартную функцию `sum()` (рис. -@fig:007).

![Сумма ряда](pictures/pic7.png){ #fig:007 width=70% }

## Численное интегрирование

7. Нахожу значение определённого интеграла.

Для этого явно задаю функцию `f` и использую стандартную функцию `quad()` (рис. -@fig:008).

![определённый интеграл функцией *quad()*](pictures/pic8.png){ #fig:008 width=70% }

## Аппроксимированние суммами

8. Рассчитаем тот же интеграл, но по правилу средней точки.

Из комментариев к коду понятно, как работает правило и как работает код. Сначала реализация программы с использованием циклов `midpoint` (рис. -@fig:009).

![Реализация *midpoint*](pictures/midpoint1.png){ #fig:009 width=70% }

9. Запускаю код (рис. -@fig:010).

![Запуск *midpoint*](pictures/pic9.png){ #fig:010 width=70% }

10. Теперь аналогично реализую векторизованную программу `midpoint_v` (рис. -@fig:011) и запускаю (рис. -@fig:012).

![Реализация *midpoint_v*](pictures/midpoint2.png){ #fig:011 width=70% }

![Запуск *midpoint_v*](pictures/pic10.png){ #fig:012 width=70% }

11. Сравниваю результаты выполнения двух программ с помощью макросов (команд) `tic` и `toc`. Из результатов видно, что векторизванный код работает быстрее подобно тому, что мы наблюдали в одной из прошлых лабораторных (рис. -@fig:013).

![Сравнение скорости исполнения кода](pictures/pic11.png){ #fig:013 width=70% }

# Выводы

Я успешно пополнил опыт вычисления приближённых и точных значений рядов, пределов, сумм и интегралов, научившись этому в языке программирования Octave.