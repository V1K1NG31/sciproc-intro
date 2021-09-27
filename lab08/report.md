---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе №8"
subtitle: "Собственные значения"
author: "Юрченко С.В. группа НФИбд-03-19"

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

Научится вычислять собственные значения и векторы и научится оперировать ими для решения смежных задач.

# Задание

- Сделать отчёт по лабораторной работе в формате Markdown.
- В качестве ответа предоставить отчёты в 3 форматах: pdf, docx и md (в архиве, поскольку он должен содержать скриншоты, Makefile и т.д.).

# Выполнение лабораторной работы

## Собственные значения и векторы

1. Необходимо найти собственные векторы и значения матрицы `A`. Для этого после включения журналирования задаю матрицу (рис. -@fig:001).

![Матрица *A*](pics/1.png){ #fig:001 width=70% }

2. Теперь использую встроенную функцию `eig()`, которая возвращает матрицу из собственных векторов и матрицу с собственными значениями на главной диагонали, при условии, что определён список из двух объектов. (рис. -@fig:002).

![Функция для нахождения собственных значений и векторов](pics/2.png){ #fig:002 width=70% }

3. По результатам видно, что были получены комплексные числа, поэтому для получения действительных чисел задаю симметричную матрицу вида

$$ C = A^{T} A $$

и нахожу собственные векторы и значения этой матрицы функцией `eig()` (рис. -@fig:003).

![Результат в действительных числах](pics/3.png){ #fig:003 width=70% }

## Марковские цепи

4. Цепь Маркова – последовательность событий, образующая дискретное распределение, где все состояния имеют зависимость. Рассматривается следующий пример:

Пусть у нас есть 5 состояний для описания перемещения по дороге. В состояниях 2, 3 и 4 совершается поворот влево или вправо, а на концах дороги происходит остановка.

Задача – предсказать, где мы окажемся через `k`-e количество шагов блуждания. В первую очередь я задал транспонированную матрицу переходов `T` (рис. -@fig:004).

![Матрица переходов](pics/4.png){ #fig:004 width=70% }

5. После задал 4 вектора вероятностей начальных состояний: `a` - начальное состояние неизвестно, `b` - начальное состояние может быть на концах дороги, `c` - почти наверно мы находимся в состоянии 2, `d` - почти наверно находимся в состоянии 3 (рис. -@fig:005).

![Векторы начальных состояний](pics/5.png){ #fig:005 width=70% }

6. Чтобы выяснить состояния через несколько шагов необходимо умножить матрицу переходов в степени, соответствующей количеству шагов, на вектор начальных состояний. В нашем случае всего 5 шагов. Выясним состояния после пяти шагов в зависимости от начальных условий. Я получил следующий результат (рис. -@fig:006).

![Векторы вероятности через 5 шагов блуждания](pics/6.png){ #fig:006 width=70% }

7. Теперь нужно найти равновесное состояние, то есть состояние, которое не приведёт ни к каким изменениям системы. Вектор такого равновесного состояния представляет из себя собственный вектор сумма элементов которого равна единице, чтобы собственное значение было равно единице. Сначала задаю новую матрицу переходов `Т` и нахожу его собственные векторы. Далее беру первый собственный вектор и записываю элементы в виде частного значения элемента и суммы всех элементов вектора, чтобы сумма элементов вектора `x` (вектор равновесного состояния) была равна единице (рис. -@fig:007).

![Равновесный вектор *x*](pics/7.png){ #fig:007 width=70% }

8. Проверяю вектор, проводя с ним разное количество шагов (10 и 50), в обоих случаях значения одинаковы. Кроме того, вычитаю результаты от разного количества шагов, результат отличается лишь через десяток знаков после запятой вследствие погрешности алгоритмов нахождения собственных векторов, так что можно говорить о том, что разница при разном количестве шагов стремится к нулю, что говорит о том, что значения и вправду одинаковые, а найденный вектор является равновесным состоянием (рис. -@fig:008).

![Проверка равновесности вектора *x*](pics/8.png){ #fig:008 width=70% }


# Выводы

Мне удалось научится находить собственные векторы и значения матриц, а также удалось применить их для решения задач на цепи Маркова.