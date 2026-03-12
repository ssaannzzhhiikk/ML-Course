What about?
 - General about Data
 - Data Preprocessing:
 - Handling Missing Data
 - Outliers
 - Data Reduction and Transformation
 - Normalization & Standartization
 - Discretization and Binarization
 - Sampling & Aggregation


Data analytics = Turning Raw Data into Gold

Different names in literature: 
- Feature → machine learning
- Attribute → data mining, databases
- Variable → statistics
- Dimension → data warehousing

Golden Rule of Data (Short):
1. Accurate
2. Stored according to data type
3. Integrity
4. Consistent
5. Not be redundant
6. be timely
7. be well understood
8. Complete


## Types of Data:
|Category|Type|Description|Example|My Example|
|---|---|---|---|---|
|Categorical (qualitative)|Nominal|Labels, no order|City {Almaty, Astana}|Programming language {Python, Java, C++}|
|Categorical (qualitative)|Ordinal|Ordered categories|Education level {Bachelor, Master}|Satisfaction level {Low, Medium, High}|
|Numeric (quantitative)|Discrete|Countable values|Number of students|Number of GitHub repositories|
|Numeric (quantitative)|Continuous|Any value in a range|Temperature in Astana|Network latency (ms)|

## Data Preprocessing:
**Data preprocessing** — это этап **подготовки данных перед анализом или обучением модели**. Его цель — **очистить, исправить и привести данные в удобный формат**, чтобы алгоритмы могли работать правильно.

### Проблемы сырых данных

В реальных задачах данные часто бывают:

1. **Incomplete (неполные)**  
    Есть пропущенные значения или неизвестные атрибуты.  
    Пример:
    
    ```
    Name | Age | City
    Ali  | 21  | Almaty
    Dana | —   | Astana
    ```
    
2. **Noisy (шумные)**  
    Содержат ошибки, выбросы или случайные отклонения.  
    Пример:
    
    ```
    Age: 21, 22, 23, 500
    ```
    
    500 — очевидная ошибка.
    
3. **Inconsistent (несогласованные)**  
    Данные записаны по-разному или содержат противоречия.  
    Пример:
    
    ```
    Country: KZ
    Country: Kazakhstan
    Country: Kazakstan
    ```
    

### Почему это важно

Есть правило:

**Garbage in → Garbage out**

Если в модель подать плохие данные, результат тоже будет плохим.  
Поэтому **качество модели напрямую зависит от качества входных данных**.

### Сколько времени занимает

В реальных проектах **60–80% времени** уходит именно на preprocessing, а не на построение модели.

### Основные этапы Data Preprocessing

|Step|Что делают|Пример|
|---|---|---|
|Data Cleaning|удаление ошибок, заполнение пропусков|заменить пустой Age на среднее|
|Data Integration|объединение данных из разных источников|база пользователей + база заказов|
|Data Transformation|изменение формата данных|нормализация чисел|
|Data Reduction|уменьшение размера данных|убрать лишние признаки|

### Простой пример

Сырые данные:

|Name|Age|Salary|
|---|---|---|
|Ali|21|500|
|Dana|—|520|
|Tim|22|50000|

После preprocessing:

|Name|Age|Salary|
|---|---|---|
|Ali|21|500|
|Dana|21.5|520|
|Tim|22|550|

(заполнили пропуск и исправили выброс)

---

## Methods of Data Preprocessing (ALL):
Вот **более расширенная версия этих 5 методов Data Preprocessing** с дополнительными деталями, которые обычно требуют на экзаменах по **Data Mining / Machine Learning**.

---

# 1. Handling Missing Values

**Missing values** появляются когда данные **не были записаны, потеряны или неизвестны**.

### Причины

- ошибка ввода данных
    
- пользователь не заполнил поле
    
- сенсор не смог измерить значение
    
- данные не применимы
    

### Основные методы
### Pros and Cons:
| Technique                                            | How it works                                                                   | Pros                                                 | Cons                                                              | When to use                                                               |
| ---------------------------------------------------- | ------------------------------------------------------------------------------ | ---------------------------------------------------- | ----------------------------------------------------------------- | ------------------------------------------------------------------------- |
| Ignore (Delete rows/columns)                         | Remove records that contain missing values                                     | Very simple, no artificial data added                | Loss of data, smaller dataset, possible bias if many rows removed | When missing data is **very small (<5%)**                                 |
| Fill with constants                                  | Replace missing values with a fixed value like **0**, **-1**, or **"Unknown"** | Fast, keeps dataset size the same, easy to implement | Can distort statistics, may create unrealistic values             | When missing value has a **logical default** (e.g., Unknown category)     |
| Fill with Mean / Median / Mode                       | Replace missing values with a **statistical measure** of the column            | Maintains dataset size, better than random filling   | Reduces variability, weakens relationships between variables      | Mean → numeric normal data; Median → skewed data; Mode → categorical data |
| Predictive filling (Regression, kNN, Decision Trees) | Predict missing value using other features in dataset                          | More accurate, keeps relationships between variables | Complex, slower, risk of model error                              | When dataset is **large and features are correlated**                     |

### Когда использовать

- **Mean** → данные распределены нормально
    
- **Median** → есть выбросы
    
- **Mode** → категориальные данные


---

# 2. Encoding Categorical Data

Алгоритмы ML **не понимают текст**, поэтому категории нужно перевести в **числа**.

### 1. Label Encoding

Каждая категория получает **уникальный номер**.

|Color|Encoded|
|---|---|
|Red|0|
|Blue|1|
|Green|2|

**Проблема:**  
модель может подумать что **Green > Blue > Red**, хотя порядка нет.

---

### 2. One-Hot Encoding

Каждая категория становится **отдельной колонкой**.

|Red|Blue|Green|
|---|---|---|
|1|0|0|
|0|1|0|

**Плюсы**

- нет ложного порядка
    

**Минусы**

- увеличивает количество признаков
    

---

### Когда использовать

|Situation|Method|
|---|---|
|Ordinal data|Label Encoding|
|Nominal data|One-Hot Encoding|
|Many categories|Target / Frequency encoding|

---

# 3. Normalization

**Normalization** масштабирует данные в диапазон **0 – 1** или **-1 – 1**.

Это нужно когда признаки имеют **разные масштабы**.

Пример без normalization:

|Feature|Value|
|---|---|
|Age|25|
|Salary|50000|

Алгоритм может считать **Salary важнее**, потому что числа больше.

После normalization:

|Age|Salary|
|---|---|
|0.25|0.50|

Формула:
min max normalization
 x' = x - min) / (max - min)

### Где используется

- kNN
    
- Neural Networks
    
- Gradient Descent algorithms
    

---

# 4. Standardization (Z-score scaling)

В отличие от normalization, **standardization не ограничивает диапазон**.

Она приводит данные к:

- **mean = 0**
    
- **standard deviation = 1**
    

Формула:
Z-score Normalization
[  
z = X - mu / sigma
]

### Пример

|Value|Standardized|
|---|---|
|10|-1|
|15|0|
|20|1|

### Используется в

- Logistic Regression
    
- Support Vector Machines
    
- PCA
    
- Neural Networks
    

---

### Normalization vs Standardization

|Feature|Normalization|Standardization|
|---|---|---|
|Range|0–1|no fixed range|
|Sensitive to outliers|Yes|Less|
|Common in|Neural nets, kNN|Linear models, SVM|

---

# 5. Outlier Detection

**Outliers** — это значения, которые **сильно отличаются от остальных данных**.
Graphical, Statistical, Distance Based, Model Based
Пример:

|Age|
|---|
|20|
|21|
|22|
|400|

400 — очевидный **outlier**.

---

### Почему это проблема

Outliers могут:

- искажать **mean**
    
- ухудшать **model accuracy**
    
- ломать **distance-based algorithms**
    

---

### Методы обнаружения

#### 1. IQR (Interquartile Range)

[  
IQR = Q3 - Q1  
]

Outlier если:

[  
x < Q1 - 1.5IQR  
]

или

[  
x > Q3 + 1.5IQR  
]

---

#### 2. Z-score

Если

[  
|z| > 3  
]

то значение считается **outlier**.

---

#### 3. Boxplot

Визуальный способ обнаружения выбросов.

---

### Что делать с outliers

|Method|Description|
|---|---|
|Remove|удалить значение|
|Transform|логарифмирование|
|Cap|ограничить максимум|

---

# Почему preprocessing критически важен

Без него:

- модель обучается **дольше**
    
- accuracy **ниже**
    
- возможны **ошибки алгоритмов**
    

В индустрии:

**60–80% времени Data Scientist тратит именно на preprocessing.**

---
### 7. Discretization и Binarization — методы Data Preprocessing

|Method|Definition|How it works|Example|Pros|Cons|
|---|---|---|---|---|---|
|Discretization|Преобразование **continuous (числовых)** данных в **категории**|Разделяет диапазон значений на интервалы (bins)|Age → Young / Middle / Old|Упрощает данные, легче интерпретировать|Потеря точности|
|Equal-width discretization|Делит диапазон на **равные интервалы**|width = (max − min) / k|0–30, 31–60, 61–90|Простая реализация|Может давать неравномерные группы|
|Equal-frequency discretization|Каждый интервал содержит **одинаковое количество объектов**|сортируем данные и делим на k частей|10 объектов → 5 в каждом bin|Балансированные группы|Интервалы могут иметь разную ширину|
|Entropy-based discretization|**Supervised метод**, использует information gain|выбирает границы, которые лучше разделяют классы|используется в decision trees|Высокая точность|Более сложный|
|Binarization|Преобразование значения в **0 или 1**|Используется **threshold**|Age > 30 → 1, иначе 0|Очень простая обработка|Потеря информации|
|One-hot encoding (binarization for categorical)|Преобразует категорию в **набор бинарных признаков**|каждая категория → отдельный бинарный столбец|Red → (1,0,0)|Нет ложного порядка между категориями|Увеличивает размер данных|

---

### Пример Discretization

Исходные данные (Age):

|Age|
|---|
|22|
|25|
|29|
|35|
|42|
|55|
|63|
|70|

После discretization (3 bins):

|Category|Ages|
|---|---|
|Young (0–30)|22, 25, 29|
|Middle-aged (31–50)|35, 42|
|Old (51+)|55, 63, 70|

---

### Пример Binarization

Threshold = 30

|Age|Age > 30|
|---|---|
|22|0|
|25|0|
|35|1|
|42|1|

---

### Разница

|Feature|Discretization|Binarization|
|---|---|---|
|Output|несколько категорий|только 0 или 1|
|Data type|continuous → categorical|numeric/categorical → binary|
|Information|больше информации|сильное упрощение|

---

💡 **Коротко для экзамена:**

- **Discretization** — преобразует continuous данные в **категории (bins)**.
    
- **Binarization** — преобразует данные в **0/1** на основе **threshold** или **one-hot encoding**.


## Sampling:

### Sampling — метод Data Reduction в Data Preprocessing

**Sampling** — это техника, при которой из большого набора данных **выбирается меньшая случайная выборка**, которая представляет весь dataset.

Используется чтобы:

- уменьшить **размер данных**
    
- ускорить **обучение моделей**
    
- снизить **вычислительные затраты**
    

Например:

|Full dataset|Sample|
|---|---|
|1,000,000 records|10,000 records|

Если sample выбран правильно, он **сохраняет статистические свойства данных**.

---

# Основные методы Sampling

|Method|Definition|How it works|Example|Pros|Cons|
|---|---|---|---|---|---|
|Simple Random Sampling Without Replacement (SRSWOR)|случайная выборка **без повторений**|выбранный элемент больше не возвращается в dataset|из 1000 записей выбираем 100 уникальных|нет повторов, хорошее представление данных|нельзя выбрать тот же объект дважды|
|Simple Random Sampling With Replacement (SRSWR)|случайная выборка **с повторениями**|после выбора запись возвращается обратно|запись может появиться несколько раз|проще для математических моделей|возможны дубликаты|
|Stratified Sampling|выборка из **подгрупп (strata)**|данные делятся на категории и sampling делается внутри каждой|male/female sampling|сохраняет пропорции групп|сложнее реализовать|
|Cluster Sampling|выборка **целых групп (clusters)**|dataset делится на группы и выбираются некоторые группы целиком|выбрать несколько школ из всех школ|быстрее и дешевле|может быть менее точным|

---

# Разница Stratified vs Cluster

|Feature|Stratified Sampling|Cluster Sampling|
|---|---|---|
|Groups|homogeneous внутри|heterogeneous внутри|
|Sampling|из каждой группы|выбираются целые группы|
|Goal|сохранить пропорции|уменьшить стоимость сбора данных|

---

# Пример

Dataset студентов:

|Student|Gender|
|---|---|
|A|Male|
|B|Female|
|C|Male|
|D|Female|

### Stratified Sampling

Берем одинаковую долю из каждой группы:

|Sample|
|---|
|A|
|B|

---

### Cluster Sampling

Если студенты разделены по классам:

|Class|Students|
|---|---|
|Class 1|A,B,C|
|Class 2|D,E,F|

Выбираем **Class 1 полностью**.

---

# Когда используется Sampling

- **Big Data**
    
- **Machine Learning training**
    
- **Streaming data**
    
- **Data reduction**
    

---

✔ **Коротко для экзамена:**

Sampling — это **data reduction technique**, которая уменьшает dataset, выбирая **репрезентативную случайную выборку данных**.

Основные методы:

- **SRSWOR** — random sample без повторений
    
- **SRSWR** — random sample с повторениями
    
- **Stratified sampling** — sampling из каждой подгруппы
    
- **Cluster sampling** — sampling целых групп.




### Aggregation — метод Data Preprocessing (Data Transformation / Reduction)

**Aggregation** — это техника, при которой данные **объединяются и суммируются по определённым признакам**, чтобы получить **сводную информацию**.

Используется для:

- уменьшения **размеров данных**
    
- подготовки **подробных признаков** для анализа
    
- выявления **паттернов на уровне групп**
    

---

# Основные идеи

|Term|Description|Example|
|---|---|---|
|Aggregation|Суммирование, усреднение или подсчёт значений по группам|подсчитать среднюю зарплату по департаментам|
|Grouping|Разделение данных на категории перед агрегированием|все сотрудники по отделам|
|Roll-up|Аггрегирование по более **высокому уровню**|City → Region → Country|
|Drill-down|Противоположное roll-up: агрегированные данные → детализация|Country → Region → City|

---

# Методы Aggregation

|Method|How it works|Example|
|---|---|---|
|Sum|Складывает значения|Total sales per month|
|Average / Mean|Среднее значение|Average age per department|
|Count|Количество объектов|Number of orders per customer|
|Min / Max|Минимум или максимум|Max temperature per city|
|Median|Медиана|Median income per neighborhood|

---

# Пример

Исходные данные:

|Employee|Department|Salary|
|---|---|---|
|A|IT|5000|
|B|IT|6000|
|C|HR|4000|
|D|HR|4500|

После Aggregation (average salary per department):

|Department|Average Salary|
|---|---|
|IT|5500|
|HR|4250|

---

# Когда используется

- Big Data: **уменьшение объёма данных**
    
- Feature Engineering: создание **сводных признаков**
    
- OLAP (Online Analytical Processing)
    

---

✔ **Коротко для экзамена:**  
**Aggregation** — это **объединение данных по группам**, с подсчётом **сумм, средних, минимумов, максимумов** и других статистик, чтобы уменьшить размер данных и подготовить их для анализа или моделей.

