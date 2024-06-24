# autism
Comparative analysis of patients with autism and healthy people based on NGS data


## Какой анализ мы проводим?

1. Сравнение больных и здорорых

- Хи-квадрат. Сравниваем каждую позицию: миллионы тестов -> Порправка на множественное сравнение -> Мощность? 
- Проблема множественного сравнения
- Проблема рассчета мощности
- Мы берем все гены или только 1000. (Если 1000 тогда какой научный интерес)
- Мы ищем различия или доказываем идентичность? (Если  идентичность, надо искать методику теста)

2.  Сравнение детей и взрослых
- Мощность?

3.  Сравнение иллюмины и генолаба
- Можно добавить людей из иллюмины, это повысит мощность. 
- Нужно провоодить дополнительное исследование. Доказывать репрезентативность
- Есть риск получить отличия

4.  Поиск подтипов болезни
- Кластеризация
- Нужно больше людей для мощности
- Проблема субпопуляция, надо кластеризировать каждую субпопуляцию

Пример структуры данных
Если у вас есть данные по двум группам и каждому варианту, таблица может выглядеть так:

## 1.1 Пример сводной таблицы для Хи-квадрат

| Variant ID | Group   | Present | Absent | Total |
|------------|---------|---------|--------|-------|
| rs123456   | Sick    | 40      | 60     | 100   |
| rs123456   | Healthy | 10      | 90     | 100   |
| rs789101   | Sick    | 30      | 70     | 100   |
| rs789101   | Healthy | 15      | 85     | 100   |
...
Примерно 10000 - 100000 на экзом.

## 1.2 Рассчет объема выборки для хи квадрат

```R
library(pwr)
# Задаем параметры
effect_size <- 0.3  # Средний эффект
alpha <- 0.05  # Уровень значимости
power <- 0.8  # Мощность теста
df <- 2   # Степени свободы для 3x2 таблицы
# Расчет объема выборки
sample_size <- pwr.chisq.test(w = effect_size, df = df, sig.level = alpha, power = power)
sample_size
```

Chi squared power calculation
w = 0.3
N = 107.0521
df = 2
sig.level = 0.05
power = 0.8
NOTE: N is the number of observations

107 человек для среднего эффекта без учета поправок

```R
library(pwr)
# Задаем параметры
effect_size <- 0.3  # Средний эффект https://www.utstat.toronto.edu/~brunner/oldclass/378f16/readings/CohenPower.pdf (p. 227, p.249)
alpha <- 0.05 / 10000  # Скоррекрированный уровень значимости
power <- 0.8  # Мощность теста
df <- 2   # Степени свободы для 3x2 таблицы
# Расчет объема выборки
sample_size <- pwr.chisq.test(w = effect_size, df = df, sig.level = alpha, power = power)
sample_size
```



Chi squared power calculation
w = 0.3
N = 359.4392
df = 2
sig.level = 5e-06
power = 0.8
NOTE: N is the number of observations

360 человек для среднего эффекта с учетом поправки Бонферони

## 2 Сравнение детей и взрослых

## 3 Сравнение иллюмины и генолаба
- Провести анализ конкордантности. Нужны ли контрольные библиотеки?
concordance rate
https://github.com/glebus-sasha/autism/edit/main/README.md
- или просто GC. Этого достаточно?
