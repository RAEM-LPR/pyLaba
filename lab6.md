```python
import pandas as pd
import numpy as np
```

## Обзор данных

Для считывания данных используется функция `pd.read_csv`. У этой функции много аргументов (см. документацию), первый из которых - название считываемого файла с данными, второй - sep - разделитель, по умолчанию это запятая. Данные в csv файлах (обычно, но не всегда) записаны в виде "таблицы". Одна запись - одна строка, данные столбцов разделяются запятыми.

Для работы с файлом его, как и обычный текстовый файл (впрочем, это и есть обычный текстовый файл!), удобнее положить в ту же директорию, где лежит ноутбук. Затем вы можете прямо через jupyter открыть файл `csv` и увидеть, как он выглядит.


```python
f = pd.read_csv("telecom_churn.csv")
```

Посмотреть начало и конец таблицы (по умолчанию 5 строк, но это настраиваемый параметр) - функции `head` и `tail`. Описание данных - `describe`, `info`. Размер таблицы - `shape`, названия колонок - `columns`. Обратите внимание, что `columns` возвращает итерируемый объект.


```python
f.head()
```


```python
f.head(7)
```


```python
f.tail()
```


```python
f.tail(7)
```


```python
f.tail(100)
```


```python
f.shape
```


```python
f.columns
```


```python
f.describe()
```


```python
f.info()
```

Небольшое, но важное отступление. Глубоко понимать это пока не обязательно. Обратите внимание, что функция `print` возвращает строковое представление объекта и она не необходима, чтобы вывести объект. 2 ячейки сработают одинаково:


```python
a = 1
print(a)
```


```python
a = 1
a
```

При этом для некоторых объектов (для которых стандартные функции `__str__` и `__repr__` возвращают разные значения) два способа вывода сработают несколько по-разному:


```python
a = np.array([1.0, 2.0])
print(a)
```


```python
a = np.array([1.0, 2.0])
a
```

Такая же ситуация с pandas dataframe'ами. Без print получится красивее, чем с ним, но фактически это одно и то же:


```python
print(f)
```


```python
f
```

2 варианта синтаксиса для просмотра содержимого столбца:


```python
f.State
```


```python
f['State']
```

Обратите внимание, что таблица и столбцы имеют разный тип:


```python
type(f), type(f.State), type(f['State'])
```

Тем не менее, мы можем сделать именно датафрейм из одного столбца следующим образом:


```python
f[['State']]
```


```python
type(f[['State']]), type(f['State'])
```

Это способ обращения к "срезам" таблицы по названиям столбцов. Еще пример:


```python
f[['State', 'Churn']]
```

Просмотр уникальных значений в столбце и их числа:


```python
f.State.unique()
```


```python
f.State.nunique()
```

Обращение к элементу ообъекта `pd.Series`:


```python
f.State[0]
```

Полный набор функций, применимых к столбцу можно посмотреть следующим образом. Здесь используется стандартная функция `__dir__()`, которая выводит список атрибутов и методов объекта.


```python
f.State.__dir__()
```

С `pd.DataFrame` привычный способ обращения по индексам не сработает:


```python
f[0][0]
```

Основной способ - использование `loc` и `iloc`. `loc` дает индексацию по "настоящим" индексам - названиям столбцов и названиям строк. В нашем случае, названия строк - целые числа, как обычные индексы. `iloc` позволяет осуществлять стандартную численную индексацию, как для `numpy` массивов.


```python
f.iloc[0] # первая строка
```


```python
f.iloc[0][0]
```


```python
f.iloc[0, 0]
```


```python
f.iloc[[0, 0]]
```


```python
f.iloc[[1, 2, 5, 1]]
```


```python
f.loc[[1, 2, 5, 1]]
```


```python
f.loc[[1, 2, 5, 1], ["State", "Account length"]]
```


```python
f.iloc[[1, 2, 5, 1], [0, 1]]
```

Следующая ячейка вернет ошибку:


```python
f.iloc[[1, 2, 5, 1], ["State", "Account length"]]
```


```python
f.iloc[:5, :4]
```


```python
f.loc[:, ["State", "Account length"]]
```


```python
f.loc[4:9, ["State", "Account length", "Area code", "International plan"]]
```

Обратите внимание, что `loc` включает и строки соответствующие и начальному, и конечному индексам.

Сохраним этот датафрейм в новую переменную и рассмотрим отличие loc и iloc в работе по целочисленным индексам строк


```python
new_f = f.loc[4:9, ["State", "Account length", "Area code", "International plan"]]
```


```python
new_f.iloc[:5]
```


```python
new_f.loc[:5]
```

**Упражнение 1.** Объясните различие поведения `loc` и `iloc` для `new_f`.

#### Создание датафрейма и присваивание по индексам


```python
df = pd.DataFrame({"A": [1, 2, 3], "B": [4, 5, 6]}, index = ["first", "second", "third"])
df
```


```python
df.iloc[0, 0] = 100
df
```


```python
df.loc["second", "B"] = 31
df
```


```python
df.iloc[2] = 5
df
```


```python
df.loc["B"] = 0
df
```


```python
df.loc[:, "B"] = 0
df
```


```python
df = pd.DataFrame({"A": [1, 2, 3, 4], "B": [5, 6, 7, 8]})
df
```


```python
df.iloc[1:2, :] = -1
df
```


```python
df.loc[1:2, :] = -2
df
```

Еще раз убеждаемся, что `loc` включает оба конца "среза", а `iloc` - полуинтервал, как например обычные срезы.

#### Создание нового столбца


```python
df["C"] = 1
df
```


```python
df["D"] = df["A"] + df["B"]
df
```


```python
df["E"] = df["D"].apply(lambda x: x ** 2)
df
```


```python
df["F"] = df[["A", "C", "E"]].apply(lambda x: x.sum(), axis=1)
df
```

**Упражнение 2.** Объясните последний результат.

## Срезы с условиями и аггрегация


```python
f[f.Churn == True]
```


```python
f[f["Area code"] == 408]
```


```python
f[f["Area code"] == 408].loc[3]
```


```python
f[f["Area code"] == 408].loc[3] == f[f["Area code"] == 408].iloc[0]
```


```python
f[f.Churn == True]
```


```python
f[f.Churn == True].mean()
```


```python
f[f.Churn == True].sum()
```

Выборка по нескольким условиям требует скобок, т.к. операции `&`, `|`, `~` (и, или, не) имеют более высокий приоритет, чем `==`, `>=`, `<=` и арифметические:


```python
f[(f.Churn == True) & (f["Area code"] == 408)]
```

Можем посмотреть средние показатели лояльных и нелояльных клиентов (столбец "Churn" показывает, ушел клиент от нас как от оператора связи или нет).


```python
loyal = f[f.Churn == False].mean()
unloyal = f[f.Churn == True].mean()
pd.DataFrame({"loyal": loyal, "unloyal": unloyal})
```

`groupby` позволяет делать группировку по уникальным значениям столбца, которые будут играть роль индекса в полученном датафрейме. При этом также нужна функция агрегации (`mean`, `sum`, `max` и прочие), чтобы отобразить полученный объект.


```python
f.groupby("Churn")
```


```python
f.groupby("Churn").mean()
```

Здесь мы сделали агрегацию всех столбцов функцией `mean`. Часто нам нужна агрегация по конкретному или конкретным столбцам. Посмотрим, например, в каком штате больше всего разговаривают по телефону:


```python
f.groupby(["State"]).agg({"Total day minutes": "mean"})
```

Максимальное значение времени:


```python
f.groupby(["State"]).agg({"Total day minutes": "mean"}).max()
```

Чтобы найти сам штат, можем отсортировать данные:


```python
f.groupby(["State"]).agg({"Total day minutes": "mean"}).sort_values(by="Total day minutes", ascending = False)
```

**Пример.** Как распределен отток клиентов по штатам? В каких штатах он больше среднего?


```python
f.groupby(["State"]).agg({"Churn": "mean"})
```


```python
f.groupby(["State"]).agg({"Churn": "mean"}).loc["LA"]
```


```python
f.groupby(["State"]).agg({"Churn": "mean"}).mean()
```


```python
f.groupby(["State"]).agg({"Churn": "mean"}).mean()[0]
```


```python
m = f.groupby(["State"]).agg({"Churn": "mean"}).mean()[0]
new_dataframe = f.groupby(["State"]).agg({"Churn": "mean"})
new_dataframe[new_dataframe.Churn > m]
```

## Упражнения.

**Упражнение 3.** Найдите среднее количество звонков `Total day calls` для всего датафрейма.


```python

```

**Упражнение 4.** Найдите среднее количество звонков `Total day calls` для любого выбранного вами штата.


```python

```

**Упражнение 5.** Создайте датафрейм, в котором будет среднее количество звонков `Total day calls` для каждого штата.


```python

```

**Упражнение 6.** Оставьте в созданном датафрейме строки только с теми штатами, где количество звонков `Total day calls` больше среднего по исходному датафрейму.


```python

```

**Упражнение 7.** Создайте датафрейм, в котором будует средние количества звонков `Total day calls` и `Total eve calls` для каждого штата.


```python

```

**Упражнение 8.** Создайте датафрейм, в котором будует средние количества звонков `Total day calls` и `Total eve calls` для каждого штата, а также столбец со значениями True и False - ответом на вопрос, больше ли дневных звонков, чем вечерних.


```python

```

**Упражнение 9.** Найти долю клиентов (отношение их числа к общему количеству клиентов) с `international plan` и `voice mail plan`.


```python

```

**Упражнение 10.** Найти число уникальных значений `Area code`.


```python

```

**Упражнение 11.** Вывести DataFrame из 2 столбцов: число звонков в поддержку; число клиентов, звонивших столько раз. Подсказка: используйте функцию агрегации `count`.


```python

```

**Упражнение 12.** Вывести DataFrame из 2 столбцов: число звонков в поддержку; доля оттока (`Churn`). Построить график.


```python

```


```python

```

**Упражнение 13.** Найти среднюю длительность международного (`intl`) звонка.


```python

```

**Упражнение 14*.** Какие звонки дольше - дневные, вечерние или ночные? Ответ привести в формате DataFrame $3*3$: строки - число минут, число звонков, среднее время звонка. Столбцы - день, вечер, ночь


```python

```

**Упражнение 15.** Сравнить `Total day charge` для оставшихся и ушедших клиентов.


```python

```

**Упражнение 16.** Отсортриуйте штаты по `Total day charge` (по возрастанию).


```python

```

**Упражнение 17.** Сделайте агрегацию по средним показателям для каждой `Area code`.


```python

```

**Упражнение 18.** Выведите датафрейм размера $3*2$: столбцы State, Churn для 100, 102 и 104 строк исходного датафрейма.


```python

```

**Упражнение 19.** Создайте датафрейм из 2 столбцов, заполненных произвольными числами. Добавьте третий столбец, равный их сумме квадратов.


```python

```

**Упражнение 20.** Добавьте к созданному датафрейму четвертый столбец, равный среднему значению первых трех, *используя* функцию `mean`.


```python

```
