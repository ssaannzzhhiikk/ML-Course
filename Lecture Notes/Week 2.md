What about?
 - Similarity
 - L(p) norm
 - Jaccard Coefficent
 - Cosine Siimilarity
 - Correlation
 - PEARSON’S & SPEARMAN’S correlation
 - Dimensionality Reduction
 - PCA 
 - Kernel Methods
 - Data Visualization (Not handled here)


## Similarity:
### Similarity и Distance в Data Mining

Во многих задачах **Data Mining** нужно определить, насколько объекты **похожи (similar)** или **различаются (dissimilar)**.  
Для этого используются **меры сходства (similarity)** и **меры расстояния (distance)**.

---

## Основная идея

Даны два объекта:

[  
O_1, O_2  
]

Нужно вычислить:

|Measure|Meaning|
|---|---|
|**Sim(O₁, O₂)**|степень сходства между объектами|
|**Dist(O₁, O₂)**|расстояние между объектами|

---

## Разница Similarity и Distance

|Feature|Similarity|Distance|
|---|---|---|
|Meaning|насколько объекты похожи|насколько объекты отличаются|
|Range|обычно **0 → 1**|**0 → ∞**|
|Interpretation|больше значение → более похожи|меньше значение → более похожи|

Пример:

|Object|Age|Salary|
|---|---|---|
|A|25|5000|
|B|27|5200|

Distance между ними **маленькая**, значит **similarity высокая**.

---

## Где используется Similarity

|Task|Why similarity is needed|
|---|---|
|Nearest Neighbor Search|найти самый похожий объект|
|Recommender Systems|рекомендовать похожие товары|
|Document similarity|поиск похожих текстов|
|Image recognition|поиск похожих изображений|

---

## Где используется Distance

|Task|Why distance is needed|
|---|---|
|Clustering|группировка похожих объектов|
|Outlier Detection|поиск аномалий|
|Classification (kNN)|определение ближайших соседей|

---

## Связь Similarity и Distance

Они **взаимозаменяемы**.

Например:

Similarity = 1 / (1 + Distance)  
или
Distance = 1 - Similarity  

То есть **similarity можно преобразовать в distance и наоборот**.

---

## Пример Distance (Euclidean)

Два объекта:

|Object|x|y|
|---|---|---|
|A|2|3|
|B|5|7|

Distance:

[  
d = \sqrt{(x_1-x_2)^2 + (y_1-y_2)^2}  
]

---

## Важное замечание

Иногда similarity **нельзя выразить точной формулой**, потому что:

- данные сложные
    
- домен специфический
    
- similarity зависит от контекста
    

Пример:

- similarity между **музыкальными вкусами**
    
- similarity между **текстами**
    

---

✔ **Коротко для экзамена**

Similarity — это **мера того, насколько два объекта похожи**.  
Distance — это **мера различия между объектами**.

Они используются в:

- clustering
    
- classification
    
- recommender systems
    
- anomaly detection.


## Lp norm
![[Pasted image 20260314003340.png]]

![[Pasted image 20260314003158.png]]

Для **quantitative (числовых) данных** сходство объектов обычно измеряется через **distance functions**.  
Самая общая форма — **Lp-norm distance**.

1. Euclidean Distance (p = 2)
Straight line between points
2. Manhattan Distance (p = 1)
Используется когда движение происходит **по сетке (grid)**, как улицы города.

|Distance|Used in|
|---|---|
|Euclidean|clustering, kNN, PCA|
|Manhattan|high-dimensional data, sparse data|

### Distance for Binary Data:
### Distances for Binary Data

Когда данные **binary (0/1)**, используются специальные меры сходства.  
Один из самых распространённых — **Simple Matching Coefficient (SMC)**.

---

## Simple Matching Coefficient (SMC)

**SMC** измеряет **долю совпадающих значений** между двумя бинарными объектами.

Он учитывает:

- совпадения **1–1**
    
- совпадения **0–0**
    

---

### Таблица сравнения бинарных признаков

||O₂ = 1|O₂ = 0|
|---|---|---|
|**O₁ = 1**|q|r|
|**O₁ = 0**|s|t|


Где:

|Symbol|Meaning|
|---|---|
|q|количество совпадений **1–1**|
|r|1–0|
|s|0–1|
|t|совпадения **0–0**|

Общее количество признаков:

[  
p = q + r + s + t  
]

---

### Формула Similarity (SMC)

[  
SMC = \frac{q + t}{p}  
]

где:

- (q+t) — количество совпадений
    
- (p) — общее число признаков
    

---

### Формула Distance

[  
Dist = 1 - SMC  
]

---
## Когда используется

|Use case|Example|
|---|---|
|Binary attributes|yes/no features|
|Market basket analysis|purchased / not purchased|
|Document classification|word present / absent|

---

## Jaccard Coefficient:
## 1. Основная идея Jaccard

Jaccard измеряет **насколько два множества похожи**.

Формула:

$J(A,B)=\frac{|A \cap B|}{|A \cup B|}$

|Symbol|Meaning|
|---|---|
|(A ∩ B)|пересечение (общие элементы)|
|(A ∪ B)|объединение (все уникальные элементы)|

---

## 2. Интерпретация

|Value|Meaning|
|---|---|
|1|объекты полностью одинаковые|
|0|нет общих элементов|
|0–1|частичное сходство|


## 4. Формула для бинарных векторов

Когда данные представлены **0 и 1**:

|Symbol|Meaning|
|---|---|
|(M_{11})|оба имеют 1|
|(M_{10})|первый 1, второй 0|
|(M_{01})|первый 0, второй 1|

Формула:

$$ 
J = \frac{M_{11}}{M_{11}+M_{10}+M_{01}}  
$$

Обрати внимание:

$$**(M_{00}) (0-0)
$$не учитывается.**

---

## 5. Почему игнорируется 0-0

Потому что **отсутствие признака обычно не информативно**.

Пример:

|Movie|User A|User B|
|---|---|---|
|Inception|1|0|
|Dune|1|1|
|Titanic|0|0|

Совпадение **Titanic = 0-0** не говорит о схожести вкусов.

---

## 6. Где используется Jaccard

|Task|Example|
|---|---|
|Recommender systems|похожие пользователи|
|Document similarity|общие слова|
|Market basket|общие покупки|
|Clustering binary data|grouping|

---

# 1. Cosine Similarity

Используется для **высокомерных и разреженных данных**, особенно **текстов**.

Идея:  
важна **не длина вектора**, а **угол между векторами**.

Если два документа используют похожие слова → их векторы направлены **в одну сторону**.

### Формула


$$
\cos(\theta)=\frac{A \cdot B}{||A|| \, ||B||}
$$



---

### Интерпретация

|Cosine value|Meaning|
|---|---|
|1|одинаковые направления|
|0|нет сходства|
|-1|противоположные направления|

---

### Где используется

|Application|Example|
|---|---|
|Text similarity|похожие документы|
|Search engines|поиск релевантных текстов|
|Recommender systems|похожие пользователи|

---

# 2. Correlation

**Correlation** показывает, **насколько две переменные связаны**.

Она отвечает на два вопроса:

|Question|Meaning|
|---|---|
|Direction|переменные растут вместе или противоположно|
|Strength|насколько сильная связь|

---

### Интерпретация

|Correlation value|Meaning|
|---|---|
|+1|идеальная положительная связь|
|0|нет связи|
|-1|идеальная отрицательная связь|

---

# 3. Correlation ≠ Causation

Очень важное правило:

**Correlation does NOT imply causation**

Пример:

- число утонувших в бассейнах
    
- количество фильмов с Nicolas Cage
    

Они могут **коррелировать**, но **не связаны причинно**.

Причина может быть **третья переменная** (lurking variable).

---

# 4. Pearson Correlation (r)

Самая популярная мера корреляции.

Используется для **линейных отношений между continuous variables**.

### Формула


$$
r=\frac{\sum (x_i-\bar{x})(y_i-\bar{y})}
{\sqrt{\sum (x_i-\bar{x})^2 \sum (y_i-\bar{y})^2}}
$$


---

### Когда использовать

|Condition|Reason|
|---|---|
|linear relationship|измеряет линейную связь|
|continuous data|требует числовых данных|
|normal distribution|лучше работает|

---

# 5. Spearman Rank Correlation

Используется когда связь **монотонная, но не линейная**.

То есть:

- одна переменная всегда растёт
    
- но **не обязательно по прямой линии**
    

Пример:

```
Exercise ↑ → Cholesterol ↓
```

Но связь **нелинейная**.

---

### Формула

$$
\rho = 1-\frac{6\sum d_i^2}{n(n^2-1)}
$$


где:

|Symbol|Meaning|
|---|---|
|(d_i)|разница рангов|
|(n)|количество наблюдений|

---

### Когда использовать

|Case|Reason|
|---|---|
|nonlinear monotonic relationship|лучше чем Pearson|
|ordinal data|работает с рангами|
|noisy data|более устойчив|

---

# 6. Mutual Information (MI)

**Mutual Information** измеряет **любую зависимость между переменными**, не только линейную.

Идея:

> Насколько знание одной переменной уменьшает неопределённость другой.

---

### Формула

$$
MI(X,Y)=\sum_{x,y} p(x,y)\log\frac{p(x,y)}{p(x)p(y)}
$$


---

### Когда используется

|Use case|Example|
|---|---|
|Feature Selection|выбрать лучшие признаки|
|Nonlinear relationships|сложные зависимости|
|Information theory|entropy analysis|

---

# Быстрое сравнение

|Measure|Detects|Data type|
|---|---|---|
|Cosine Similarity|угол между векторами|text / high-dim|
|Pearson|линейная зависимость|continuous|
|Spearman|монотонная зависимость|ranked|
|Mutual Information|любая зависимость|general|

---

✅ **Запомнить для экзамена:**

- **Cosine similarity** → текстовые данные
    
- **Pearson correlation** → линейная связь
    
- **Spearman correlation** → монотонная связь
    
- **Mutual information** → любая зависимость
    
---
Сделаю **чёткую структурированную шпаргалку** по твоему конспекту: **Dimensionality Reduction, PCA, Kernel Methods**. Это ровно тот формат, который обычно нужен **для экзамена или заметок в Obsidian**.

---

# Dimensionality Reduction

**Dimensionality reduction** — это уменьшение количества признаков (**features**) в dataset, при этом стараясь сохранить **максимум информации (variance)**.

### Основная идея

Много признаков часто:

- **коррелированы**
    
- содержат **повторяющуюся информацию**
    
- усложняют модель


Поэтому их можно заменить **меньшим набором новых переменных**.

---

## Зачем это нужно

|Problem|Benefit|
|---|---|
|слишком много признаков|упрощает модель|
|медленные вычисления|ускоряет обучение|
|шум в данных|уменьшает noise|
|скрытые закономерности|легче увидеть структуру|

---

# Principal Component Analysis (PCA)

**PCA** — самый популярный метод **dimensionality reduction**.

### Цель

Сократить количество признаков, **сохранив максимальную variance данных**.

---

## Основная идея PCA

PCA создаёт **новые признаки**, которые называются:

**Principal Components (PC)**

Они:

- **ортогональны (перпендикулярны)**
    
- **некоррелированы**
    
- расположены вдоль направлений **максимальной variance**
    

---

### Интуитивный пример

Представь **3D объект**.

Камера делает **2D фото**, но старается сохранить **максимум деталей**.

PCA делает то же самое:

```
High-dimensional data → Lower dimensional representation
```

---

# Алгоритм PCA (шаги)

### 1. Центрирование данных

Вычитаем среднее значение.

$$
X_{centered} = X - \bar{X}  
$$

---

### 2. Вычисляем covariance matrix

$$
\Sigma = \frac{1}{n-1}X^TX  
$$

Covariance показывает **как признаки изменяются вместе**.

---

### 3. Решаем eigenproblem

$$ 
\Sigma w = \lambda w  
$$

|Symbol|Meaning|
|---|---|
|(w)|eigenvector|
|(\lambda)|eigenvalue|

---

# Что означают результаты

|Element|Meaning|
|---|---|
|Eigenvectors|направления новых осей (principal components)|
|Eigenvalues|сколько variance хранит компонент|

---

### Интерпретация

Большое eigenvalue → **важная компонента**

Маленькое eigenvalue → **мало информации**

---

# Итог PCA

```
100 features → 10 principal components
```

При этом сохраняется **90–95% variance**.

---

# Применения PCA

|Field|Example|Benefit|
|---|---|---|
|Image processing|MNIST digits|compression|
|Face recognition|eigenfaces|faster recognition|
|Finance|stock returns|find market factors|
|Medicine|gene data|visualize clusters|
|Marketing|customer behavior|segmentation|

---

# Kernel Methods

Многие алгоритмы работают хорошо **только если данные линейно разделимы**.

Но реальные данные обычно **нелинейные**.

### Идея

Отобразить данные в **более высокое пространство**:

$$
\phi(x): \mathbb{R}^d \rightarrow \mathbb{R}^D  
$$

где

$$
D > d  
$$

---

# Kernel Trick

Вместо явного вычисления

$$
\phi(x)  
$$

мы считаем **скалярное произведение** напрямую:

$$
K(x,z)=\phi(x)\cdot\phi(z)  
$$

---

# Kernel Function

Kernel — это функция, которая вычисляет **similarity** между объектами в новом пространстве.

---

## Популярные kernel функции

|Kernel|Formula|Use|
|---|---|---|
|Linear|(K(x,z)=x·z)|линейные данные|
|Polynomial|(K(x,z)=(x·z+c)^d)|сложные границы|
|RBF (Gaussian)|(K(x,z)=e^{-\gamma||
|Sigmoid|(tanh(ax·z+b))|нейросетевые модели|

---

# Kernel Matrix

Матрица всех попарных similarity:

$$  
K_{ij}=K(x_i,x_j)  
$$

---

# Почему kernel trick важен

Без kernel:

```
explicit mapping → очень дорого
```

С kernel:

```
compute similarity directly
```

---

# Где используются Kernel Methods

|Algorithm|
|---|
|Support Vector Machines (SVM)|
|Kernel PCA|
|Kernel Ridge Regression|
|Gaussian Processes|

---

# Коротко для экзамена

### Dimensionality Reduction

Уменьшение числа признаков с сохранением информации.

---

### PCA

Метод, который:

- ищет **направления максимальной variance**
    
- создаёт **principal components**
    
- уменьшает dimensionality
    

---

### Kernel Methods

Методы, которые:

- отображают данные в **высокое пространство**
    
- используют **kernel trick**
    
- позволяют линейным алгоритмам решать **нелинейные задачи**

