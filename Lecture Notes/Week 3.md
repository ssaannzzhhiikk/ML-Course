What about?
- Learning Methods
- Supervised Learning
- Classification
- Regression
- Linear Regression
- Unsupervised learning
- Logistiic Regression
- Support Vector Machines (SVM)
- kNN: NEAREST NEIGHBOR CLASSIFIER
- Decision Tree Classifier


# 1. Learning Methods

**Machine Learning** — это методы, позволяющие компьютеру **учиться из данных без явного программирования**.

Основные типы обучения:

|Type|Description|
|---|---|
|Supervised Learning|модель учится на размеченных данных|
|Unsupervised Learning|модель ищет структуру в данных|
|Semi-supervised|частично размеченные данные|
|Reinforcement Learning|обучение через награды|

В этой теме рассматриваются **Supervised и Unsupervised Learning**.

---

# 2. Supervised Learning

**Supervised Learning** — это обучение модели на **размеченных данных**.

Dataset содержит:

```
(X, y)
```

где

```
X → features (признаки)
y → label / target (ответ)
```

### Пример

|House Size|Price|
|---|---|
|50|100000|
|80|150000|

Модель учится предсказывать:

```
price = f(size)
```

---

## Основные задачи supervised learning

### Classification

Предсказание **категории**.

Примеры:

|Input|Output|
|---|---|
|email|spam / not spam|
|image|cat / dog|
|transaction|fraud / normal|

---

### Regression

Предсказание **числового значения**.

Примеры:

|Problem|Output|
|---|---|
|house price|200000|
|temperature|21.5|
|stock price|100.2|

---

# 3. Linear Regression

**Linear Regression** — один из самых простых алгоритмов regression.

Модель:
$$
y = w_0 + w_1 x
$$
где

|Symbol|Meaning|
|---|---|
|(w_0)|bias|
|(w_1)|weight|
|x|feature|

---

### Множественная регрессия
$$
y = w_0 + w_1 x_1 + w_2 x_2 + ... + w_n x_n
$$
---

### Цель обучения

Найти веса, минимизирующие ошибку:
$$
MSE = \frac{1}{n}\sum_{i=1}^{n}(y_i - \hat{y}_i)^2
$$
---

### Применения

- prediction
    
- forecasting
    
- economics
    
- finance


---

# 4. Logistic Regression

Несмотря на название, **Logistic Regression используется для classification**.

Функция:
$$
P(y=1|x) = \frac{1}{1+e^{-(w_0 + w_1 x)}}
$$
---

### Что делает sigmoid

- переводит значение в диапазон
    

```
0 — 1
```

---

### Интерпретация

|Probability|Prediction|
|---|---|
|> 0.5|class 1|
|< 0.5|class 0|

---

# 5. Support Vector Machines (SVM)

**SVM** — мощный алгоритм classification.

Цель:

Найти **гиперплоскость**, которая максимально разделяет классы.

---

### Гиперплоскость
$$
w \cdot x + b = 0
$$
---

### Основная идея

SVM выбирает границу, которая **максимизирует margin**.

```
distance between classes
```

---

### Support vectors

Это **точки данных, ближайшие к границе**.

Именно они определяют модель.

---

# 6. Kernel Methods

Иногда данные **не линейно разделимы**.

Решение:

отобразить данные в **более высокое пространство**.

```
φ(x)
```

---

## Kernel Trick

Вместо вычисления φ(x) напрямую используем kernel:

```
K(x,z)
```

---

### Kernel Function

K(x,z) = \phi(x) \cdot \phi(z)

---

### Популярные kernels

|Kernel|Formula|
|---|---|
|Linear|(x·z)|
|Polynomial|((x·z + c)^d)|
|RBF|(e^{-γ|

---

# 7. k-Nearest Neighbor (kNN)

**kNN** — простой алгоритм classification.

Алгоритм:

1. взять точку
    
2. найти **k ближайших соседей**
    
3. выбрать **самый частый класс**
    

---

### Distance metric

Чаще всего используется **Euclidean distance**:
$$
d(x,y) = \sqrt{\sum_{i=1}^{n}(x_i - y_i)^2}
$$
---

### Особенности

Плюсы

- простой
    
- не требует обучения
    

Минусы

- медленный на больших данных
    
- чувствителен к шуму
    

---

# 8. Decision Tree

**Decision Tree** — алгоритм, который принимает решения в виде дерева.

Пример:

```
Age < 30?
 ├ yes → student?
 │      ├ yes → buy
 │      └ no → no buy
 └ no → buy
```

---

### Основные элементы

|Element|Meaning|
|---|---|
|Root|начало дерева|
|Node|условие|
|Leaf|результат|

---

### Метрики разделения

|Metric|Formula|
|---|---|
|Gini impurity|используется в CART|
|Entropy|используется в ID3|

---

### Entropy
$$
H(S) = - \sum_{i=1}^{n} p_i \log_2 p_i
$$
---

# 9. Unsupervised Learning

**Unsupervised learning** работает **без меток (labels)**.

Цель:

найти **структуру данных**.

---

### Примеры задач

|Task|Example|
|---|---|
|Clustering|customer segmentation|
|Dimensionality reduction|PCA|
|Association rules|market basket|

---

# 10. Dimensionality Reduction

**Dimensionality reduction** — уменьшение количества признаков.

Цели:

- ускорить обучение
    
- уменьшить шум
    
- визуализировать данные
    

---

# 11. Principal Component Analysis (PCA)

**PCA** — метод уменьшения размерности.

Цель:

сохранить **максимальную variance** данных.

---

### Основная идея

Найти **новые оси**, вдоль которых variance максимальна.

Эти оси называются:

```
principal components
```

---

### Алгоритм PCA

1️⃣ Центрирование данных

```
Xcentered = X − mean
```

---

2️⃣ Вычисление covariance matrix

```
Σ
```

---

3️⃣ Eigen decomposition

\Sigma w = \lambda w

---

### Интерпретация

|Element|Meaning|
|---|---|
|eigenvectors|направления principal components|
|eigenvalues|количество variance|

---

### Пример

```
100 features → 10 principal components
```

с сохранением

```
95% информации
```

---

# 12. Applications

|Field|Example|
|---|---|
|Computer Vision|face recognition|
|Finance|stock analysis|
|Medicine|gene data|
|Marketing|customer segmentation|

---

# Короткое резюме

|Method|Type|
|---|---|
|Linear Regression|regression|
|Logistic Regression|classification|
|SVM|classification|
|kNN|classification|
|Decision Tree|classification|
|PCA|dimensionality reduction|

---

💡 Если хочешь, я могу ещё сделать **супер-конспект для экзамена (1 страница)** или **Obsidian note с callouts, links и graph structure**, который будет выглядеть **как настоящая knowledge base ML**.