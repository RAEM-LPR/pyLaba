# Set.

Множество `set` в Python имеет тот же смысл, что понятие множества в математике. `Множество` содержит неупорядоченный набор элементов. Множества поддерживают стандартные математические операции над ними: *объединение, пересечение, разность*. Возможно также добавление и удаление элементов, проверка их принадлежности множеству с помощью оператора `in`. При этом все элементы входят в `set` только один раз, добавление существующего элемента не изменяет множество. Элементами множества могут быть только `неизменяемые` типы, например, его элементами не могут быть списки.

### Таблица по взаимодействию элемента и множества
Операция  | Значение 
---|---
`x in A`  | $x \in A$, принадлежит ли элемент x множеству A 
`x not in A`  | $x \notin A$ — то же, что `not (x in A)`
`A.add(x)`  | добавить элемент x в множество A 
`A.discard(x)`  | удалить элемент x из множества A 
`A.remove(x)`  | удалить элемент x из множества A 
`A.pop()`  | удаляет из множества один случайный элемент и возвращает его 


```python
a = {1, 2, 3}
a.add(4)
print(a)
```


```python
a.add(1)
print(a)
```


```python
print(0 in a, 1 in a)
```

Для удаления элементов из множества можно использовать `discard` и `remove`, их поведение различается тогда, когда удаляемый элемент отсутствует в множестве: `discard` не делает ничего, а метод `remove` генерирует исключение `KeyError`, которое вы увидите в одной из ячеек ниже.


```python
a.remove(1)
print(a)
```


```python
a.remove(0)
print(a)
```


```python
print(a)
```


```python
a.discard(2)
print(a)
```


```python
a.discard(0)
print(a)
```

Для создания пустого множества или для получения множества из *итерируемого* объекта можно использовать конструктор множеств `set`:


```python
a = set()
print(a)
a.add(1)
print(a)
```

Конструкция ниже не работает, потому что фигурные скобки используются для создания пустых словарей `dict`, о которых будет сказано ниже.


```python
a = {}
print(a)
a.add(1)
print(a)
```


```python
a = [1, 2, 3, 4]
print(set(a))
```


```python
a = [1, 2, 3, 4, 1]
print(set(a))
```


```python
a = "abcd"
print(set(a))
```


```python
a = "abcda"
print(set(a))
```

Операции над множествами можно записывать как коротко символами, так и названиями соответствующих функций:


```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
print(a.union(b))
print(a | b)
```


```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
print(a.intersection(b))
print(a & b)
```


```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
print(a.difference(b))
print(a - b)
```

Симметрическая разность двух множеств - множество, состоящее из элементов, входящих в одно и только одно из данных множеств:


```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
print(a.symmetric_difference(b))
print(a ^ b)
```


```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
print(a <= b)
print(a.issubset(b))

c = {3, 4}
d = {3, 4, 5, 6}
print(c <= d)
print(c.issubset(d))
```


```python
a = {3, 4, 5, 6}
b = {3, 4, 5, 6}
print(a <= b)
print(a < b)
```

Существуют также операции наподобие `+=`, `-=`, `*=`, `/=`, `//=`:


```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
a &= b
print(a)
```


```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
a.intersection_update(b)
print(a)
```


```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
a |= b
print(a)
```


```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
a.update(b)
print(a)
```


```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
a -= b
print(a)
```


```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
a.difference_update(b)
print(a)
```

### Сводная таблица операций с множествами:
Операция  | Альтернатива | Значение 
---|---|---
`A \| B` | `A.union(B)`  | Возвращает множество, являющееся объединением множеств A и B. 
`A \|= B` | `A.update(B)` | Записывает в A объединение множеств A и B. 
`A & B` | `A.intersection(B)`  | Возвращает множество, являющееся пересечением множеств A и B. 
`A &= B` | `A.intersection_update(B)`  | Записывает в A пересечение множеств A и B. 
`A - B` | `A.difference(B)`  | Возвращает разность множеств A и B (элементы, входящие в A, но не входящие в B). 
`A -= B` | `A.difference_update(B)`  | Записывает в A разность множеств A и B. 
`A ^ B` | `A.symmetric_difference(B)`  | Возвращает симметрическую разность множеств A и B (элементы, входящие в A или в B, но не в оба из них одновременно). 
`A ^= B` | `A.symmetric_difference_update(B)`  | Записывает в A симметрическую разность множеств A и B. 
`A <= B` | `A.issubset(B)`  | Возвращает True, если A является подмножеством B. 
`A >= B` | `A.issuperset(B)`  | Возвращает True, если B является подмножеством A. 
`A < B`  | | Эквивалентно A <= B and A != B 
`A > B`  | | Эквивалентно A >= B and A != B 




**Упражнение 0**. Вывести на экран все элементы множества A, которых нет в множестве B. Дописать код ниже.


```python
A = set('bqlpzlkwehrlulsdhfliuywemrlkjhsdlfjhlzxcovt')
B = set('zmxcvnboaiyerjhbziuxdytvasenbriutsdvinjhgik')
```

**Упражнение 1.** Считать через `input` строку, состоящую из 3 слов и найти буквы, входящие в каждое из слов.


```python

```

**Упражнение 2.** Считать через `input` строку, состоящую из произвольного числа слов и найти буквы, входящие в каждое из слов.


```python

```

**Упражнение 3\*.** Считать через `input` несколько чисел через пробел и найти цифры, входящие в каждое из чисел. Использовать `while`.


```python

```

# Dict.

Кроме множеств также часто используются словари. Элемент словаря `dict` - это пара `ключ: значение`.
Ключи позволяют обращаться к данным не по индексу, как это реализовано в списках, а по любому удобному значению.

### Сводная таблица по операциям со словарями:
Операция  | Значение 
---|---
`value = A[key]` | Получение элемента по ключу. Если элемента с заданным ключом в словаре нет, то возникает исключение KeyError. 
`value = A.get(key)` | Получение элемента по ключу. Если элемента в словаре нет, то get возвращает None. 
`value = A.get(key, default_value)` | То же, но вместо None метод get возвращает default_value. 
`key in A` | Проверить принадлежность ключа словарю. 
`key not in A` | То же, что not key in A. 
`A[key] = value` | Добавление нового элемента в словарь. 
`del A[key]` | Удаление пары ключ-значение с ключом key. Возбуждает исключение KeyError, если такого ключа нет. 
`if key in A: del A[key]` | Удаление пары ключ-значение с предварительной проверкой наличия ключа. 
`value = A.pop(key)` | Удаление пары ключ-значение с ключом key и возврат значения удаляемого элемента.Если такого ключа нет, то возбуждается KeyError. 
`value = A.pop(key, default_value)` | То же, но вместо генерации исключения возвращается default_value. 
`A.pop(key, None)` | Это позволяет проще всего организовать безопасное удаление элемента из словаря. 
`len(A)` | Возвращает количество пар ключ-значение, хранящихся в словаре. 



```python
d = {"Россия": "Москва", "Франция": "Париж", "Германия": "Берлин"}
print(d["Германия"])
```

Такой способ хранения данных в данном случае является более естественным и удобным. Создание словаря и добавление элементов:


```python
d = dict()
d["Россия"] = "Москва"
print(d)
```

    {'Россия': 'Москва'}
    

Можно обращаться к ключам словаря, к значениям словаря, итерировать по ключам и по парам ключ-значение.


```python
d = {"Россия": "Москва", "Франция": "Париж", "Германия": "Берлин"}
print(d.keys())
print(list(d.values()))
```

    dict_keys(['Россия', 'Франция', 'Германия'])
    ['Москва', 'Париж', 'Берлин']
    


```python
for k in d.keys():
    print(d[k])
```


```python
for k, v in d.items():
    print(k, v)
```


```python
print(d.items())
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    Input In [1], in <cell line: 1>()
    ----> 1 print(d.items())
    

    NameError: name 'd' is not defined



```python
print(list(d.items()))
```

Можем сортировать такие объекты, например, по странам в лексикографическом порядке:


```python
d = list(d.items())
d = sorted(d, key = lambda x: x[0])
print(d)
```

# Set comprehensions. Dict comprehensions.

Можно генерировать множества и словари по аналогии со списками:


```python
a = [i for i in range(-5, 5)]
print(a)
a = {i for i in range(-5, 5)}
print(a)
a = [abs(i) for i in range(-5, 5)]
print(a)
a = {abs(i) for i in range(-5, 5)}
print(a)
```

Для определения порядкового номера символа в таблице символов ASCII используется функция `ord`:


```python
s = "a"
print(ord(s))
print(ord('A'), ord('Z'), ord('a'), ord('z'))
```

Обратная к ней функция, возвращающая символ по его порядковому номеру - `chr`:


```python
print(chr(65), chr(90), chr(97), chr(122))
```

Создадим словарь, состоящий из пар элементов `номер буквы в таблице ASCII`: `буква`.


```python
d = {i: chr(i) for i in range(65, 91)}
print(d)
print(d[70])
```

**Упражнение 4.** Создайте аналогичный словарь для маленьких букв, выведите его, затем добавьте в него большие буквы и выведите итоговый словарь.


```python

```

**Упражнение 5.** Создайте словарь, в котором каждой букве (как ключу) будет соответствовать ее порядковый номер в алфавите (значение). Рекомендация: использовать функции `keys`, `values` или `items` для словаря из предыдущего упражнения, чтобы создать новый.


```python

```

**Упражнение 6.** Считайте слово с клавиатуры и найдите для него сумму номеров букв. Если некоторые буквы в слове повторяются (используйте такое слово), нужно считать только по уникальным буквам. Например, для строк 'abc' и 'abcbc' сумма будет 1+2+3=6, для xyz или zyxyz 24+25+26=75


```python

```

**Упражнение 7.** Считайте с клавиатуры количество пар синонимов, затем сами пары синонимов, затем одно из слов среди этих пар. Выведите его синоним. Допишите код, заменив все TODO. Пример ввода:

    3
    Hello Hi
    Bye Goodbye
    List Array
    Goodbye


```python
n = int(input())
d = dict()
for i in range(n):
    s = input()
    # TODO completing a dictionary
s = input()
# TODO search for the desired synonym
```

# Частотный анализ.

Вместо использования метода `count` для подсчета числа вхождений символа в большой текст лучше использовать `dict`. Для многократного поиска это будет работать быстрее, так как мы заполним словарь за один проход по данному тексту.


```python
s = "abracadabra"
d = dict()
for i in s:
    if i in d:
        d[i] += 1
    else:
        d[i] = 1
print(d)
```


```python
print(s.count('a'))
print(d['a'])
```


```python
s = "abracadabra" * 1000000
print(s[:100])
```


```python
import time
d = dict()
for i in s:
    if i in d:
        d[i] += 1
    else:
        d[i] = 1
t1 = time.time()
print(d['a'])
t2 = time.time()
print(t2 - t1)
```


```python
t3 = time.time()
print(s.count('a'))
t4 = time.time()
print(t4 - t3)
```

**Упражнение 8**. Считайте с клавиатуры строку, удалите из нее все цифры и пробелы. Создайте словарь, в котором ключами будут уникальные символы, а значениями их частота вхождения. Частотой вхождения называется отношение числа вхождений данного символа в исходную строку к числу символов в исходной строке.


```python

```

# Collections.

Существуют также другие стандартные коллекции, которые позволяют решать некоторые задачи еще проще.


```python
import collections
cnt = collections.Counter()
for word in ['red', 'blue', 'red', 'green', 'blue', 'blue']:
    cnt[word] += 1
cnt
```


```python
cnt['red']
```

Можно сократить запись, переимпортировав из библиотеки конкретный модуль:


```python
from collections import Counter
c = Counter(a=4, b=2, c=0, d=-2)
print(sorted(c.elements()))
```


```python
print(collections.Counter('abracadabra').most_common(3))
```


```python
c = Counter(a=4, b=2, c=0, d=-2)
d = Counter(a=1, b=2, c=3, d=4)
c.subtract(d)
print(c)
```


```python
c = Counter(a=10, b=5, c=0)
c.total() # new for Python 3.10+
```

С другими коллекциями вы можете познакомиться самостоятельно, их использование выходит за рамки упражнений и контеста.


```python

```