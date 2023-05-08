## Двумерные списки

"Двумерный список" — это обычный список, элементами которого являются списки. Такой термин удобен для нас, но для Python нет разницы между одномерными и двумерными списками. В частности, нечто такое вообще будет являться промежуточным: `[1, [2, 3, 4], 5]`

Создадим список и рассмотрим обращение к элементам.


```python
a = [[1, 2, 3], [4, 5, 6]]
print(*a)
print(a[1])
print(a[1][0])
print(a[-1][-1])
```


```python
for i in range(len(a)):
    print(*a[i])
```

Для создания списка можем использовать генераторы:


```python
a = [[1, 2, 3] for i in range(4)]
for i in range(len(a)):
    print(*a[i])
```


```python
a = [[i, i+1, i+2] for i in range(4)]
for i in range(len(a)):
    print(*a[i])
```


```python
for x in a:
    print(*x)
```


```python
print(a)
```

Вот пример создания списка списков при помощи генератора списка, *вложенного* в генератор списка:


```python
a = [[j for j in range(5)] for i in range(5)]
for x in a:
    print(*x)
```

**Упражнение:** создайте двумерный список. Заполните его следующим образом: значение элемента - номер его строки.


```python

```

**Пример.** Напечатаем таблицу умножения $10*10$:


```python
n, m = 10, 10
a = [[i * j for j in range(1, m + 1)] for i in range(1, n + 1)]
for x in a:
    print(*x)
```

## Тип bool. Оператор in. Еще раз про if.

Еще один базовый тип данных — это `bool`. Переменные такого типа могут принимать только 2 значения: `True` и `False`.


```python
print(1 > 0)
```


```python
a = 1 > 0
print(a)
```


```python
b = 1 < 0
print(b)
```


```python
print(a * 5)
print(b * 3)
```

Именно тип `bool` используется в каскадной конструкции `if elif ... else`:


```python
if 1 > 0:
    print(2)
```

Существует приведение типов. Любое число, отличное от нуля с логической точки зрения — `True`, нуль воспринимается как `False`


```python
if 5:
    print(2)
else:
    print("!")
```


```python
if 0:
    print(4)
else:
    print("!")
```


```python
for i in [1, 2, 3, 4, 5]:
    print(i)
```

### Оператор `in`
Лексема `in` может быть использована не только как часть синтаксической конструкции цикла `for`, но и как *оператор* для проверки принадлежности элемента итерируемому объекту:


```python
print(4 in [1, 2, 3, 4, 5])
print(6 in [1, 2, 3, 4, 5])
```


```python
print(4 in range(1, 6))
print(6 in range(1, 6))
```


```python
print("b" in "abc")
print("B" in "abc")
```

## Функции, возвращающие значение
Функции — это вспомогательные алгоритмы. 

###  Логическое значение как результат работы функции
Ниже описаны три аналогичных функции. Прочитайте их тела и объясните почему они работают одинаково.
Какая из них вам больше нравится?


```python
def is_positive(x):
    if x > 0:
        return True
    else:
        return False
    
print(is_positive(5))
print(is_positive(-5))
```


```python
def is_positive(x):
    if x > 0:
        return True
    return False

print(is_positive(5))
print(is_positive(-5))
```


```python
def is_positive(x):
    return x > 0

print(is_positive(5))
print(is_positive(-5))
```

## Функции как аргументы функций map и filter
Для поэлементной обработки любого итерируемого объекта можно использовать функции `map` и `filter`:


```python
a = "1 2 -3 4 -5".split()
print(a)
a = list(map(int, a))
print(a)
```


```python
a = "1 2 -3 4 -5".split()
print(a)
a = list(map(float, a))
print(a)
```


```python
a = "1 2 -3 4 -5 0".split()
print(a)
a = list(map(bool, a))
print(a)
```


```python
a = "1 2 -3 4 -5 0".split()
print(a)
a = list(map(int, a))
print(a)
a = list(map(bool, a))
print(a)
```

Как параметр для `map` можно передавать не только стандартные функции, но и свои собственные:


```python
def my_function(x):
    return x * 2

a = "1 2 -3 4 -5".split()
print(a)
a = list(map(my_function, a))
print(a)
```

Такие "одноразовые функции" загрязняют пространство имён, поэтому есть возможность создать **безымянную функцию** при помощи слова `lambda`. Вычисляясь, лямбда-выражение "изготавливает" новую функцию и передаёт её как объект туда, где она нужна — в функцию `map`. Затем она сразу забывается.


```python
a = "1 2 -3 4 -5".split()
print(a)
a = list(map(lambda x: x * 2, a))
print(a)
```


```python
a = [1, 2, -3, 4, -5]
b = list(map(is_positive, a))
c = list(filter(is_positive, a))
print(b)
print(c)
```


```python
a = [1, 2, -3, 4, -5]
b = list(map(lambda x: x > 0, a))
c = list(filter(lambda x: x > 0, a))
print(b)
print(c)
```

Можем делать "сложную" лямбда-функцию:


```python
a = "1 2 -3 4 -5".split()
print(a)
a = list(map(lambda x: abs(int(x)), a))
print(a)
```

**Упражнение:** считайте список с клавиатуры. С помощью функции `filter` удалите из него те элементы, которые *не* являются квадратами однозначных натуральных чисел.


```python

```

Можно использовать `map` для обработки считанного списка. Считываем с помощью функции `input()` объект типа `str`, к нему применяем метод `split()` и получаем `list`, ко всем его элементам функция `map` применяет функцию `int`, а конструктор списка `list` сохраняет результат в список:


```python
a = list(map(int, input().split()))
print(a)
```


```python
a = [list(map(int, input().split())) for i in range(5)]
```


```python
for x in a:
    print(*x)
```

Пример: удалить из матрицы строки с отрицательной суммой


```python
a = [[5, -2, 3], [-1, 2, -3], [-8, 4, 5]]
for x in a:
    print(*x)
```


```python
a = list(filter(lambda x: sum(x) >= 0, a))
print(a)
```


```python
print(sum(a[0]), sum(a[1]))
```

И еще примеры:


```python
a = [1, 2, 3, 4, 5]
print(list(map(lambda x: x ** 2, a)))
```


```python
a = [1, 2, -3, 4, -5]
print(list(map(lambda x: x if x >= 0 else 0, a)))
```

## Цикл while. Целочисленная арифметика

Кроме цикла `for` в Python используется цикл `while`. Например, он удобен, если нужно указать условие выхода через условие типа `bool`


```python
i = 0
while i < 5:
    print(i ** 2)
    i += 1
```


```python
for i in range(5):
    print(i ** 2)
```

Еще две арифметические операции, которые потребуются в примере ниже: деление с остатком и целочисленное деление.


```python
print(16 % 3)
print(16 // 3)
```

С помощью цикла `while` удобно обращаться к отдельным цифрам числа. Например, можно сохранить их в массив:


```python
a = []
n = 2345
while n > 0:
    a.append(n % 10)
    n = n // 10
print(a)
```

**Упражнение:** напишите функцию, которая вычисляет сумму цифр числа, считайте число с клавиатуры и примените эту функцию.


```python

```

Можно запустить "бесконечный цикл" (он ничем не отличается от обычного). Внутри циклов можно использовать конструкции `break` и `continue`:


```python
while True:
    a = int(input())
    print(a)
```

Для прерывания работы ячейки можно нажать на квадратик.


```python
while True:
    a = int(input())
    if a > 0:
        print(a)
    else:
        break
```


```python
while True:
    a = int(input())
    if a > 0:
        continue
    else:
        break
```

## Работа с файлами

Пример: создайте файл input.txt, скопируйте туда таблицу с числами ниже:

    1 2 3
    4 5 6


```python
with open("input.txt", "r") as f:
    print(f.read())
```


```python
with open("input.txt", "r") as f:
    s = f.read()
    print(s)
    
```


```python
s, type(s)
```

Так выглядит внутреннее представление строки `s`. Когда мы вызываем функцию `print` символ переноса строки `\n` переводит курсор на новую строку:


```python
print("1\n2")
```


```python
with open("input.txt", "r") as f:
    a = f.readlines()
print(a)
```

Напомним, что `rstrip()` удаляет пробельные элементы из конца строки, в частности, символ переноса строки


```python
with open("input.txt", "r") as f:
    a = f.readlines()
    a = list(map(lambda x: x.rstrip(), a))
print(a)
```


```python
with open("input.txt", "r") as f:
    a = f.readlines()
    a = list(map(lambda x: x.rstrip().split(), a))
print(a)
```


```python
with open("input.txt", "r") as f:
    a = f.readlines()
    a = list(map(lambda x: [int(y) for y in x.rstrip().split()], a))
print(a)
```

Или проще:


```python
with open("input.txt", "r") as f:
    a = f.readlines()
    a = list(map(lambda x: x.rstrip().split(), a))
    for i in range(len(a)):
        for j in range(len(a[i])):
            a[i][j] = int(a[i][j])
print(a)
```

**Пример:** в созданный файл запишем вместо чисел, которые там были, новые числа, равные квадратам исходных


```python
b = [[a[i][j] ** 2 for j in range(len(a[i]))] for i in range(len(a))]
print(b)
```


```python
with open("output.txt", "w") as f:
    f.writelines([" ".join(x) for x in b])
```


```python
b = [[str(x) for x in b[i]] for i in range(len(b))]
with open("output.txt", "w") as f:
    f.writelines([" ".join(x) for x in b])
```

Посмотрите, что записалось в файл. Не совсем то, что нужно, не хватает символов переноса строки


```python
b = [[str(x) for x in b[i]] for i in range(len(b))]
with open("output.txt", "w") as f:
    f.writelines([" ".join(x) + "\n" for x in b])
```

Файлы можно открывать не только на запись, но и на дозапись. Обратите внимание, что в предыдущей ячейке предыдущее сожержимое файла стерлось запуском `open`, для этого используем флажок `a` вместо `w`


```python
b = [[str(x) for x in b[i]] for i in range(len(b))]
with open("output.txt", "a") as f:
    f.write("done!")
```

## Сортировка списков

Не углубляясь в алгоритмы, разберем, как можно сортировать списки в Python. Для этого есть функции `sort` и `sorted`. Первая изменяет сортируемый объект, вторая создает новый, а исходный остается:


```python
a = [3, 1, 5, 4, 2]
a.sort()
print(a)
```


```python
a = [3, 1, 5, 4, 2]
print(sorted(a))
print(a)
```

Но можем использовать вторую вместо первой:


```python
a = [3, 1, 5, 4, 2]
a = sorted(a)
print(a)
```

Сортировка по ключу. key - это второй параметр функции `sorted` и он часто записывает в виде лямбда-функции, которая возвращает функции от объектов, которые мы используем в качестве меры этих объектов для сортировки


```python
a = [3, 1, 5, 4, 2]
a = sorted(a, key = lambda x: -x)
print(a)
```


```python
a = [[1, 5], [3, 3], [5, 5], [3, 0]]
print(sorted(a, key = lambda x: sum(x)))
```


```python
a = [[1, 5], [3, 3], [5, 5], [3, 0]]
print(sorted(a, key = lambda x: x[0] ** 2 + x[1] ** 2))
```

Можем сортировать по нескольким параметрам в порядке убывания приоритета:


```python
a = [[1, 6], [2, 5], [3, 4]]
print(sorted(a, key = lambda x: (sum(x), x[1])))
```

`(sum(x), x[1])` - это кортеж. Кортежи похожи на списки, но они неизменяемы (нельзя присваивать по индексу и добавлять элементы)


```python
a = [1, 2]
a[1] = 3
print(a)
```


```python
a = (1, 2)
a[1] = 3
print(a)
```


```python
a = [1, 2]
a.append(3)
print(a)
```


```python
a = (1, 2)
a.append(3)
print(a)
```


```python
a = [1, 2]
a = [3, 4]
print(a)
```


```python
a = (1, 2)
a = (3, 4)
print(a)
```

Строки сортируются в лексикографическом порядке:


```python
a = ["100", "11", "12", "120", "119"]
print(sorted(a))
```


```python
a = ["100", "11", "12", "120", "119"]
print(sorted(a, key = lambda x: int(x)))
```

## Снова к файлам

**Пример:** дана таблица результатов олимпиады в формате "Фамилия Имя Класс Балл". Нужно скопировать ее в текстовый файл и считать в двумерный массив. Задача - определить фамилию и имя победителя олимпиады. Если их несколько, вывести первого в лексикографическом порядке.

Решение: считаем данные в двумерный список. Отсортируем его по убыванию балла и по возрастанию ФИ.

Таблица:

    Иванов Сергей 9 90
    Сергеев Петр 10 85
    Петров Иван 11 90


```python
with open("input.txt", "r", encoding="utf-8") as f:
    a = list(map(lambda x: x.rstrip().split(), f.readlines()))
    print(a)
```


```python
print(sorted(a, key = lambda x: (-int(x[3]), x[0], x[1])))
```


```python
print(" ".join(sorted(a, key = lambda x: (-int(x[3]), x[0], x[1]))[0][:2]))
```

## Генераторы и отложенные вычисления


```python
def foo(x):
    print(f"foo called for {x}")
    return x * 10

for x in map(foo, [1, 2, 3]):
    print(x)
```


```python
def foo(x):
    print(f"foo called for {x}")
    return x * 10

def boo(x):
    print(f"foo called for {x}")
    return x + 1000

A = [1, 2, 3]
B = map(foo, A)
C = map(boo, B)
print("Iterations start:")
for x in C:
    print(x)
```

## Итерируемые объекты

Часто бывает удобно использовать *распаковку* переменных:


```python
a, b = 1, 2
print(a)
print(b)
```


```python
a, b, c = [1, 2, 3]
print(a)
print(b)
print(c)
```


```python
a, b, c = [1, 2, 3, 4, 5]
```


```python
*a, b, c = [1, 2, 3, 4, 5]
print(a, b, c)
```


```python
a, *b, c = [1, 2, 3, 4, 5]
print(a, b, c)
```


```python
a, b, *c = [1, 2, 3, 4, 5]
print(a, b, c)
```


```python
for a, b, c in [(1, 2, 3), (4, 5, 6), (7, 8, 9)]:
    print(a, b, c)
```


```python
for a, *b in [(1, 2, 3, 4), (10, 20), (100, 200, 300)]:
    print(a, b)
```


```python
a, (b, c) = [1, (2, 3)]
print(a, b, c)
```

### enumerate, zip, for с распаковкой 

В цикле `for` также можно использовать распаковку:


```python
a = [[1, 2], [3, 4], [5, 6]]
for x, y in a:
    print(x, y, x + y)
```

Часто такая распаковка используется не сама по себе, а вместе с использованием удобных функций `zip` и `enumerate`, которые позволяют удобнее работать со списками:


```python
a = [[1, 2, 3], [4, 5, 6], [7, 8, 9], [0, 0, 0]]
for i, x in enumerate(a):
    print(i, x, sum(x))
```

    0 [1, 2, 3] 6
    1 [4, 5, 6] 15
    2 [7, 8, 9] 24
    3 [0, 0, 0] 0
    


```python
with open("1.txt", "w") as f:
    f.writelines([word + "\n" for word in ["dog", "cat", "mouse", "duck", "goose"]])
for line in open("1.txt"):
    print(line.strip())
```


```python
for i, x in enumerate(open("1.txt")):
    print(i, x.rstrip())
```


```python
a = ["ab", "cd", "ef"]
b = [1, 2, 3]
print(list(zip(a, b)))
```


```python
for a, b in zip("abcde", range(5)):
    print(a, b)
```

    a 0
    b 1
    c 2
    d 3
    e 4
    


```python
for a, b in zip("abcde", range(10)):
    print(a, b)
```

## itertools

Для более удобной работы с итерируемыми объектами мы можем использовать библиотеку `itertools`. Для этого нужно ее импортировать:


```python
import itertools as it

```


```python
for x, y, z in it.permutations("ABC"):
    print(x, y, z, sep='')
```


```python
for x, y, z in it.permutations("ABCD", 3):
    print(x, y, z, sep='', end=' ')
```

**Упражнение:**
Вычислите с помощью `it.permutation` $C_{12}^{5}$


```python

```


```python
for x, y in it.combinations("ABCDE", 2):
    print(x, y, sep='', end=' ')
```


```python
for x, y in it.combinations_with_replacement("ABCDE", 2):
    print(x, y, sep='', end=' ')
```


```python
for a in it.chain("мама", "мыла", "раму"):
    print(a, end=' ')
```


```python
for a in it.chain([5, 4, 3], [3, 4, 5], [[3, 4, 5]]):
    print(a, end=' ')
```


```python
for n, s in it.product("wxyz", "ABC"):
    print(n, s)
```

**Упражнение:**
Введите 2 списка (координаты вектора `a` и координаты вектора `b`) и найдите скалярное произведение этих векторов, используя `zip` или что-нибудь из `itertools`.


```python

```
