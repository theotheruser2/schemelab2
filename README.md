<!-- федеральное государственное автономное образовательное учреждение высшего образования
«Национальный исследовательский университет ИТМО» -->

# Лабораторная работа №2 &laquo;Функциональная схемотехника&raquo;

Выполнили студенты группы P33113:  Доморацкий Э.А., Юров М.А.

Преподаватель: Тищук Б.Ю.

Санкт-Петербург, 2021

Цель работы
=======

Получить навыки описания арифметических блоков на RTL-уровне с использованием языка описания аппаратуры Verilog HDL.

Вариант 7
=========

-   `y = a * √b`
-   2 сумматора и 2 умножителя

Схема и описание работы
=======================

![](./scheme.png)

1. После получения входных данных - переменных `a` и `b`, и сигнала о готовности к началу арифметических операций, `a` передается на блок умножения, ожидающего аргументов,  в то время как `b` отправляется на блок, высчитывающий его квадратный корень.
2. После вычисления квадратного корня `b` подается сигнал о готовности, результат данной операции передается в качестве второго аргумента в блоке умножения.
3. Вычисляется результат y = `a * √b`.
4. Вновь подается сигнал о готовности к вычислениям, схема получает входные данные.   

Область допустимых значений
===========================

Так как входные данные `a` и `b` - целые беззнаковые числа разрядностью восемь бит, то они принимают значения от 0 до 255. Следовательно, с учетом округления к меньшему целому полученное значение `√b ∈ [0; 15]` (4 бита). Максимально возможное значение функции `y = 255 * 15 = 3825`, для возвращения результата потребуется 12 бит.

Код разработанной схемы
========================

`multiplier.v` - блок умножения\
`sqrt.v` - блок вычисления квадратного корня\
`a_sqrtb.v` - схема для вычисления значения функции

Код разработанного тестового окружения 
=======================================

`ab_tb.v` - тестирование блока вычисления квадратного корня\
`s_test.v` - тестирование работы схемы в целом

Описание окружения и результаты тестирования
============================================

Для тестирования блока вычисления квадратного корня в качестве входного аргумента используется одно значение, указанное в коде. В терминал выводится результат вычислений.

При тестировании арифметического блока функции в цикле подаются входные значения `a` и `b`, где `b = a + 2`. На каждом шаге цикла значения входных аргументов увеличивается на 25. В терминал выводятся входные данные, результат вычислений.

Результаты тестирования для схемы:

![](./test1.png)

Временная диаграмма
===================

Сигналы подаются с частотой 100 МГц. На рассчёт одного значения уходит 580 нс.

![](./time1.png)


Потребление ресурсов
====================

Полученные на основе симуляции данные об использовании ресурсов устройства, энергопотреблении, температуре:

![](./stat.png)

Вывод
=====

В результате работы была создан арифметический блок для вычисления значений функции `y = a * √b`, описанный на RTL-уровне при помощи языка Verilog HDL, было разработано тестовое окружение.
