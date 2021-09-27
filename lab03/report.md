---
# Front matter
lang: ru-RU
title: "Лабораторная работа №3"
subtitle: "Введение в Octave"
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

Познакомиться с языком Octave, изучить основные инструменты работы с векторами и матрцами.

# Задание

Подготовить отчёт.


# Выполнение лабораторной работы

1. Включаю журналирование сессии команд и записываю всё в файл `diary`. Сам файл и его содержимое (рис. -@fig:001)

2. Использую Octave для вычисления математического выражения (рис. -@fig:001)
3.  Задаю конвектор `u`, или вектор-строку, двумя способами . Также создаю вектор с теми же значениями, переопределяя `u`, и матрицу `A` (рис. -@fig:001)

![1](pictures/Pic1.png){ #fig:001 width=70% }

4. Задав два вектора `u` и `v`, нашёл значение выражения `2v + 3u`, затем скалярное (в ответе число), векторное произведение (в ответе вектор) двух векторов и норму вектора `u` (рис. -@fig:002)

```octave
  u = [1; -4; 6]
  v = [2; 1; -1]
```

![2](Pictures/Pic2.png){ #fig:002 width=70% }

5. Вычисляю проекцию вектора `u` на `v`, перед этим переопределив их (рис. -@fig:003)

Стандартный инструмент для решения не задан, поэтому пользуемся выведением формулы проекции через формулу скалярного произведения.

![3](pictures/Pic4.png){ #fig:003 width=70% }

6. Задаём матрицы `A` и `B` (рис. -@fig:004)

7. Вычислил их произведение, произведение с транспонированной матрицей `B` и выражение вида `2A - 4I, I - единичная матрица` (рис. -@fig:004) (рис. -@fig:005)

![4](pictures/Pic5.png){ #fig:004 width=70% }

![5](pictures/Pic6.png){ #fig:005 width=70% }

Пример единичной матрицы 5x5 (рис. -@fig:005)

8. Вычисляем определитель и ранг матрицы `A` (рис. -@fig:006)

![6](pictures/Pic7.png){ #fig:006 width=70% }

9. Построим график, задав все значения `х` через range-функцию `linspace()` и определим нашу переменную `y` со всеми значениями во всех точках `x`. Чтобы получить график, используем функцию `plot()`, которая выводит неприрывную линию по умолчанию (рис. -@fig:007)

10. Улучшим внешний вид графика, определив параметр цвета `'r'` (можно было задать его через параметр `'r-'`, явно задав отображение в виде линии) и параметр ширины линии. Кроме того функцией `axis()` подраниваем значения осей, то есть меняем масштаб изображения, включаем сетку, добавляем подписи к осям и легенду (рис. -@fig:007)

Функция `plot()` принимает множественные параметры, поэтому, считывая параметр `'linewidth'`, считывает следующий за ним параметр, как значение ширины линии. По сути это своеобразная замена инструмента ключевых параметров.

![7](pictures/Pic8.png){ #fig:007 width=70% }
![8](pictures/PicGr.png){ #fig:009 width=70% }
![9](pictures/PicGr2.png){ #fig:010 width=70% }
![10 итоговый график](pictures/PicGr3.png){ #fig:010 width=70% }
```octave
  % предварительно отчистим фигуру
  clf
```
11.  Теперь изображаем две диаграммы: точки и прямую линейной регрессии, задав нужные значения (рис. -@fig:011)

![11](pictures/Pic9.png){ #fig:011 width=70% }

```octave
  % аналогично можно было
  % отобразить две диаграммы на одной фигуре так

  plot(x, y, 'o', x, 1.2 * x, '-')
```

Итоговое изображение выглядит так (рис. -@fig:012)

![12](pictures/PicGr4.png){ #fig:012 width=70% }

12. Изобразим третий график, который потом сохраним двумя способами. для начала зададим `x` (рис. -@fig:014), далее отобразим график и сохраним в формате png (рис. -@fig:013)

![13](pictures/Pic10.png){ #fig:013 width=70% }


```octave
  % второй способ отличается тем,
  % что вместо макроса,
  % мы используем print в качестве функции

  % конкретно тут сохраняем в формате pdf
  print('graph2.pdf','-dpdf')
```

Сам график выглядит так (рис. -@fig:016)

![14](Graph2.png){ #fig:016 width=70% }

1.  Сравним работу двух алгоритмов вычисления суммы элементов последовательности от 1 до 100000: через range-цикл `for` с итератором и векторную форму (то есть через векторы и орифметические операторы с точкой)

Код с циклом `for` (рис. -@fig:015)

![15](pictures/LoopFor.png){ #fig:017 width=70% }

Код с векторами (рис. -@fig:016)

![16](pictures/LoopVec.png){ #fig:016 width=70% }

Результаты оказались ожидаемыми – векторная форма отработала  быстрее (рис. -@fig:017)

![17](pictures/Pic11.png){ #fig:019 width=70% }

Скорее всего, дело в реализации инструментов языка. По аналогии с Python, где цикл `for` реализован через язык C, поэтому работает быстрее, чем более нативный цикл `while`, можно предположить, что в Octave присутствует реализация на языках более низкого уровня абстракции.

# Выводы

Мне удалось освоить начальные навыки владения языка Octave, с помощью его инструментов произвести операции с векторами, конвекторами, матрицами: создать и сохранить в разных форматах диаграммы и понять некоторые принципы его работы.