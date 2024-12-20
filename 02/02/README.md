# CHAPTER02 머신러닝 실습(분류)
SECTION01 문제 정의
---
- 미국 인구조사 데이터(1994)를 바탕으로 만들어진 데이터

- 각 사람의 소득 예측

- 나이, 결혼 여부, 직종 등의 컬럼 존재

  - 레이블(타깃)은 연소득이 $50,000 이상과 미만으로 구분됨(컬럼명 : income)
 
  - 소득 예측값($50,000 이상일 확률)을 csv 파일로 생성
 
  - 평가 기준은 ROC-AUC 로 평가
 
  - 제출 파일은 예측값만 result.csv 파일로 생성해 제출(컬럼명 : pred, 1개)

<br>

---

<Br>

SECTION02 라이브러리 및 데이터 불러오기
---
- 2개의 데이터가 주어짐

  - train 데이터
 
    - test 데이터보다 컬럼의 수가 1개 더 많음
   
    - y 데이터(label, target) 포함
 
  - test 데이터

<br>

> 데이터 불러오기
```python
  # 판다스 라이브러리
  import pandas as pd
  
  # 데이터 불러오기
  train = pd.read_csv('./data/train.csv')
  test = pd.read_csv('./data/test.csv')
```
- pd.read_csv() 활용해 csv 파일 불러오기

- 불러온 데이터를 train 과 test 변수에 담기

<br>

#### 💡 머신러닝에서 자주 나오는 용어
- 피처(feature) : 예측에 사용되는 입력 데이터를 의미

  - ex) 집 가격 예측시 '집의 크기', '방 개수', '위치' 등이 피처로 활용
 
  - '변수', '컬럼', '열', '독립변수' 등과 같은 용어로도 불림
 
- 타깃(target) : 예측의 목표가 되는 결과값을 지칭

  - ex) 집값 예측 문제에서 '실제 집의 가격'이 타깃 값에 해당
 
  - '레이블(label)', 'y', '종속변수' 등의 명칭으로도 불림
 
- '피처'는 예측을 위한 정보를 제공, '타깃'은 그 예측의 목표가 되는 구체적인 값

<br>

---

<br>

SECTION03 탐색적 데이터 분석(EDA)
---
- 탐색적 데이터 분석(Exploratory Data Analysis, EDA)

  - 데이터를 살펴보고 이해하기 위한 과정
 
  - 데이터의 크기, 자료형, 기초 통계 등 데이터가 어떻게 구성되었는지 파악
 
  - 결측치, 이상치 등 발견
 
  - 데이터의 패턴, 분포 등을 이해하기 위해 시각화를 많이 사용
 
    - 빅분기 실기 시험 환경은 시각화 지원 X

<br>

### 01. 데이터 샘플 head()

<br>

> 코드
```python
  train.head(3)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>workclass</th>
      <th>fnlwgt</th>
      <th>education</th>
      <th>education.num</th>
      <th>marital.status</th>
      <th>occupation</th>
      <th>relationship</th>
      <th>race</th>
      <th>sex</th>
      <th>capital.gain</th>
      <th>capital.loss</th>
      <th>hours.per.week</th>
      <th>native.country</th>
      <th>income</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3331</td>
      <td>34.0</td>
      <td>State-gov</td>
      <td>177331</td>
      <td>Some-college</td>
      <td>10</td>
      <td>Married-civ-spouse</td>
      <td>Prof-specialty</td>
      <td>Husband</td>
      <td>Black</td>
      <td>Male</td>
      <td>4386</td>
      <td>0</td>
      <td>40.0</td>
      <td>United-States</td>
      <td>&gt;50K</td>
    </tr>
    <tr>
      <th>1</th>
      <td>19749</td>
      <td>58.0</td>
      <td>Private</td>
      <td>290661</td>
      <td>HS-grad</td>
      <td>9</td>
      <td>Married-civ-spouse</td>
      <td>Craft-repair</td>
      <td>Husband</td>
      <td>White</td>
      <td>Male</td>
      <td>0</td>
      <td>0</td>
      <td>40.0</td>
      <td>United-States</td>
      <td>&lt;=50K</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1157</td>
      <td>48.0</td>
      <td>Private</td>
      <td>125933</td>
      <td>Some-college</td>
      <td>10</td>
      <td>Widowed</td>
      <td>Exec-managerial</td>
      <td>Unmarried</td>
      <td>Black</td>
      <td>Female</td>
      <td>0</td>
      <td>1669</td>
      <td>38.0</td>
      <td>United-States</td>
      <td>&lt;=50K</td>
    </tr>
  </tbody>
</table>
</div>

- id, age, workclass, ••• income 컬럼과 데이터 확인 가능

- 수치형(numerical) 변수와 범주형(categorical) 변수가 함께 존재

- income 컬럼이 target(y 또는 label) 컬럼

  - 일반적으로 train 데이터에 target 이 함께 있다면 가장 오른쪽 컬럼에 위치
 
  - 문제를 통해 target 컬럼 확인 or train 데이터와 test 데이터 컬럼의 차이를 보고 확인

<br>

### 02. 데이터 크기 shape

<br>

> 코드
```python
  train.shape, test.shape
```
- shape 에는 괄호 X

> 결과
```python
  ((29304, 16), (3257, 15))
```
- 컬럼 수가 1개 차이나는 이유

  - target 의 유무에 따른 것

<br>

#### (1) 자료형 info()
- info() : 자료형 확인

- 머신러닝의 입력 데이터로 활용하기 위해서는 object 형은 수치형(float, int) 데이터로 변경해야 함

  - 데이터 전처리 단계에서는 object 형을 인코딩

<br>

> 코드
```python
  train.info()
```

> 결과
```python
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 29304 entries, 0 to 29303
  Data columns (total 16 columns):
   #   Column          Non-Null Count  Dtype  
  ---  ------          --------------  -----  
   0   id              29304 non-null  int64  
   1   age             29292 non-null  float64
   2   workclass       27642 non-null  object 
   3   fnlwgt          29304 non-null  int64  
   4   education       29304 non-null  object 
   5   education.num   29304 non-null  int64  
   6   marital.status  29304 non-null  object 
   7   occupation      27636 non-null  object 
   8   relationship    29304 non-null  object 
   9   race            29304 non-null  object 
   10  sex             29304 non-null  object 
   11  capital.gain    29304 non-null  int64  
   12  capital.loss    29304 non-null  int64  
   13  hours.per.week  29291 non-null  float64
   14  native.country  28767 non-null  object 
   15  income          29304 non-null  object 
  dtypes: float64(2), int64(5), object(9)
  memory usage: 3.6+ MB
```
- train 데이터 타입 : float 형 2개, int 형 5개, object 형 9개 존재

<br>

#### (2) 기초 통계 describe() / 수치형
- describe() : 수치형 컬럼 기초 통계 값 확인

- 'age' 컬럼

  - train 데이터 : 평균 약 38, 최소값 -38, 최대값 90
 
    - 나이는 마이너스 값이 있을 수 없으나, train 데이터에는 마이너스 존재
    
    - 이상치로 의심 가능
 
  - test epdlxj : 최소값 17
 
    - train 데이터와는 달리 마이너스가 없음

<br>

> 코드
```python
  train.describe()
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>fnlwgt</th>
      <th>education.num</th>
      <th>capital.gain</th>
      <th>capital.loss</th>
      <th>hours.per.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>29304.000000</td>
      <td>29292.000000</td>
      <td>2.930400e+04</td>
      <td>29304.000000</td>
      <td>29304.000000</td>
      <td>29304.000000</td>
      <td>29291.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>16264.027880</td>
      <td>38.553223</td>
      <td>1.897488e+05</td>
      <td>10.080842</td>
      <td>1093.858722</td>
      <td>86.744506</td>
      <td>40.434229</td>
    </tr>
    <tr>
      <th>std</th>
      <td>9384.518323</td>
      <td>13.628811</td>
      <td>1.055250e+05</td>
      <td>2.570824</td>
      <td>7477.435640</td>
      <td>401.518928</td>
      <td>12.324036</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>-38.000000</td>
      <td>1.228500e+04</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>8145.750000</td>
      <td>28.000000</td>
      <td>1.177890e+05</td>
      <td>9.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>40.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>16253.500000</td>
      <td>37.000000</td>
      <td>1.783765e+05</td>
      <td>10.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>40.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>24374.250000</td>
      <td>48.000000</td>
      <td>2.370682e+05</td>
      <td>12.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>32560.000000</td>
      <td>90.000000</td>
      <td>1.484705e+06</td>
      <td>16.000000</td>
      <td>99999.000000</td>
      <td>4356.000000</td>
      <td>99.000000</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  test.describe()
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>fnlwgt</th>
      <th>education.num</th>
      <th>capital.gain</th>
      <th>capital.loss</th>
      <th>hours.per.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>3257.000000</td>
      <td>3251.000000</td>
      <td>3.257000e+03</td>
      <td>3257.000000</td>
      <td>3257.000000</td>
      <td>3257.000000</td>
      <td>3248.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>16423.704943</td>
      <td>38.802830</td>
      <td>1.900447e+05</td>
      <td>10.079214</td>
      <td>931.804728</td>
      <td>92.336199</td>
      <td>40.468288</td>
    </tr>
    <tr>
      <th>std</th>
      <td>9535.416746</td>
      <td>13.917588</td>
      <td>1.057902e+05</td>
      <td>2.590118</td>
      <td>6496.962999</td>
      <td>415.732721</td>
      <td>12.598546</td>
    </tr>
    <tr>
      <th>min</th>
      <td>3.000000</td>
      <td>17.000000</td>
      <td>1.882700e+04</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>8078.000000</td>
      <td>28.000000</td>
      <td>1.186520e+05</td>
      <td>9.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>40.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>16626.000000</td>
      <td>37.000000</td>
      <td>1.783190e+05</td>
      <td>10.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>40.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>24743.000000</td>
      <td>48.000000</td>
      <td>2.364360e+05</td>
      <td>12.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>32559.000000</td>
      <td>90.000000</td>
      <td>1.033222e+06</td>
      <td>16.000000</td>
      <td>99999.000000</td>
      <td>3900.000000</td>
      <td>99.000000</td>
    </tr>
  </tbody>
</table>
</div>

<br>

#### 💡 데이터 분포 describe() 해석
|구분|값|의미|
|:-:|:-:|-|
|분포의 대칭성|비슷하다|분포가 대칭|
|분포의 대칭성|mean > 50% (중앙값)|• 오른쪽 왜곡<br>대부분 값이 왼쪽에 몰려 있고, 갈수록 값이 희박해짐|
|분포의 대칭성|mean < 50% (중앙값)|• 왼쪽 왜곡<br>대부분 값이 오른쪽에 몰려 있고, 갈수록 값이 희박해짐| 
|데이터의 범위|min 과 max|최소값과 최대값으로 데이터의 전체 범위를 파악|
|데이터 분포|min ~ 25% 구간<br>25 ~ 50% 구간<br>50 ~ 75% 구간<br>75 ~ max 구간|간격이 좁다면 그 구간에 더 많은 데이터가 몰려 있음|

<br>

#### (3) 기초 통계 describe(include='object') / 범주형
- describe() 함수 안에 include='O'(대문자) or include='object'

  - 범주형 컬럼의 기초 통계 값 확인

<br>

> 코드
```python
  train.describe(include = 'O')
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>workclass</th>
      <th>education</th>
      <th>marital.status</th>
      <th>occupation</th>
      <th>relationship</th>
      <th>race</th>
      <th>sex</th>
      <th>native.country</th>
      <th>income</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>27642</td>
      <td>29304</td>
      <td>29304</td>
      <td>27636</td>
      <td>29304</td>
      <td>29304</td>
      <td>29304</td>
      <td>28767</td>
      <td>29304</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>8</td>
      <td>16</td>
      <td>7</td>
      <td>14</td>
      <td>6</td>
      <td>5</td>
      <td>2</td>
      <td>41</td>
      <td>2</td>
    </tr>
    <tr>
      <th>top</th>
      <td>Private</td>
      <td>HS-grad</td>
      <td>Married-civ-spouse</td>
      <td>Prof-specialty</td>
      <td>Husband</td>
      <td>White</td>
      <td>Male</td>
      <td>United-States</td>
      <td>&lt;=50K</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>20451</td>
      <td>9449</td>
      <td>13466</td>
      <td>3683</td>
      <td>11845</td>
      <td>25022</td>
      <td>19578</td>
      <td>26240</td>
      <td>22263</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  test.describe(include = 'object')
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>workclass</th>
      <th>education</th>
      <th>marital.status</th>
      <th>occupation</th>
      <th>relationship</th>
      <th>race</th>
      <th>sex</th>
      <th>native.country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>3083</td>
      <td>3257</td>
      <td>3257</td>
      <td>3082</td>
      <td>3257</td>
      <td>3257</td>
      <td>3257</td>
      <td>3211</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>8</td>
      <td>16</td>
      <td>7</td>
      <td>14</td>
      <td>6</td>
      <td>5</td>
      <td>2</td>
      <td>37</td>
    </tr>
    <tr>
      <th>top</th>
      <td>Private</td>
      <td>HS-grad</td>
      <td>Married-civ-spouse</td>
      <td>Prof-specialty</td>
      <td>Husband</td>
      <td>White</td>
      <td>Male</td>
      <td>United-States</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>2245</td>
      <td>1052</td>
      <td>1510</td>
      <td>457</td>
      <td>1348</td>
      <td>2794</td>
      <td>2212</td>
      <td>2930</td>
    </tr>
  </tbody>
</table>
</div>

- test 데이터의 native.country 컬럼

  - 전체 데이터 수 : 3,211개
 
  - 카테고리 종류 : 37개
 
    - train 과 차이 有
 
  - 최빈값 : United-States
 
  - 최빈값의 빈도 수 : 2,930
 
    - 카테고리 종류는 많지만 대부분의 데이터가 United-States 임을 확인 가능

<br>

#### (4) 결측치 isnull().sum()
- 결측치가 있다면 데이터 전처리 단계에서 처리

<br>

> 코드
```python
  train.isnull().sum()
```

> 결과
```python
  id                   0
  age                 12
  workclass         1662
  fnlwgt               0
  education            0
  education.num        0
  marital.status       0
  occupation        1668
  relationship         0
  race                 0
  sex                  0
  capital.gain         0
  capital.loss         0
  hours.per.week      13
  native.country     537
  income               0
  dtype: int64
```
- 5개 컬럼에 결측치 존재

  - age, workclass, occupation, hours.per.week, native.country

<br>

> 코드
```python
  test.isnull().sum()
```

> 결과
```python
  id                  0
  age                 6
  workclass         174
  fnlwgt              0
  education           0
  education.num       0
  marital.status      0
  occupation        175
  relationship        0
  race                0
  sex                 0
  capital.gain        0
  capital.loss        0
  hours.per.week      9
  native.country     46
  dtype: int64
```
- 5개 컬럼에 결측치 존재

  - age, workclass, occupation, hours.per.week, native.country

<br>

#### (5) 각 target 별 빌도 수 value_counts()
- value_counts() : target(카테고리)별 개수 확인

- target 에서 확인하고자 하는 것

  - 이진 분류인가?
 
  - 불균형 데이터인가?
 
    - 성능 좋은 머신러닝 모델을 만들기 어려움
   
    - ex) 제조업에서의 정상과 불량, 신용카드 회사의 정상 거래 및 비정상 거래 데이터 등

<br>

> 코드
```python
  train['income'].value_counts()
```

> 결과
```python
  income
  <=50K    22263
  >50K      7041
  Name: count, dtype: int64
```

<br>

---

<br>

SECTION04 데이터 전처리
---
- 머신러닝 입력 데이터 조건

  - 결측치가 있다면 채우거나 삭제 (데이터 클리닝)
 
  - 중복값은 제거 (데이터 클리닝)
 
  - 모든 데이터를 숫자 형태로 변경 (인코딩)

- 전처리를 최소화하고 싶다면 수치형 데이터만 선택해 모델 학습시킴

  - 범주형 데이터 함께 사용하려면 인코딩 필요
 
- 데이터를 일정한 범위로 작업하는 스케일링(데이터 정규화)과 이상치 처리(데이터 클리닝)는 선택

<br>

|데이터 전처리|필수/선택|
|:-:|-|
|결측치|(결측치가 있다면)**필수**|
|이상치|**선택**(문제에서 명시하지 않으면 생략)|
|인코딩|(범주형 데이터가 있다면)**필수**|
|스케일링|**선택**|

<br>

#### 💡 데이터 전처리 때 파생변수 생성 해야할까?
- 주요 퍄생변수(기존 변수를 조합해 새로운 변수 생성) 생성은 머신러닝 모델 성능 향상에 도움

  - ex) 나이(age)를 20대, 30대 등 범주형 변수로 변환
 
- 빅분기 시험에서는 고성능의 모델은 요구하는 것이 아니므로 생략

- 시계열 데이터가 있다면 연도, 월, 일 컬럼(변수) 생성 추천

<br>

### 01. 결측치(Missing Values) 처리
#### (1) 결측치 삭제
- 결측치를 처리하는 가장 쉬운 방법

- dropna() : 결측치가 있는 행(레코드) 제거 

  - 제거 후 데이터 크기 변경됨
 
    - 전과 후의 데이터 크기를 눈으로 확인하기
   
  - 전체 데이터를 대상으로 결측치가 하나라도 있는 행은 모두 제거됨
 
- dropna(subset = ['컬럼명']) : 결측치가 있는 특정 컬럼 데이터에서 결측이 있는 '행'을 제거

- dropna(axis = 1) : 결측치가 있는 컬럼 전체 삭제

  - 기본값 :  axis = 0
 
  - 1개의 결측치가 있는 컬럼도 삭제
 
- drop() : 특정 컬럼만 삭제

<br>

> 코드
```python
  print('처리전: ', train.shape)
  df = train.dropna()
  print('처리후: ', df.shape)
```
- 실제 결측치 처리에는 train = train.dropna() 사용

- df = train.dropna() 이유

  - 결측치 처리 결과를 df 변수에 대입하여 기존 train 데이터가 변경되지 않도록 하기 위함

> 결과
```python
  처리전:  (29304, 16)
  처리후:  (27096, 16)
```

<br>

- train 데이터의 특정 컬럼의 결측 행 제거

> 코드
```python
  train.isnull().sum()
```

> 결과
```python
  id                   0
  age                 12
  workclass         1662
  fnlwgt               0
  education            0
  education.num        0
  marital.status       0
  occupation        1668
  relationship         0
  race                 0
  sex                  0
  capital.gain         0
  capital.loss         0
  hours.per.week      13
  native.country     537
  income               0
  dtype: int64
```

<br>

> 코드
```python
  df = train.dropna(subset = ['native.country', 'workclass'])
  df.isnull().sum()
```
- 'native.country', 'workclass' 컬럼의 결측 행 제거 후 결과 확인

> 결과
```python
  id                 0
  age               12
  workclass          0
  fnlwgt             0
  education          0
  education.num      0
  marital.status     0
  occupation         6
  relationship       0
  race               0
  sex                0
  capital.gain       0
  capital.loss       0
  hours.per.week    13
  native.country     0
  income             0
  dtype: int64
```
- 두 컬럼은 결측이 있는 '행'이 삭제되어 결측치가 없어짐

<br>

- 결측치가 있는 컬럼 전체 삭제

> 코드
```python
  print('처리전: ', train.shape)
  df = train.dropna(axis = 1)
  print('처리후: ', df.shape)
```

> 결과
```python
  처리전:  (29304, 16)
  처리후:  (29304, 11)
```

<br>

- 특정 컬럼만 삭제

> 코드
```python
  print('처리전: ', train.shape)
  df = train.drop(['native.country', 'workclass'], axis = 1)
  print('처리후: ', df.shape)
```

> 결과
```python
  처리전:  (29304, 16)
  처리후:  (29304, 14)
```

<br>

#### 💡 결측치를 제거할 행과 값을 채울 행은 어떻게 정할까?
- 정답은 없지만 기준은 존재

- 머신러닝 결과를 기준으로 성능이 좋아지는 방향으로 데이터 전처리 진행

- 머신러닝 프로세스 중 데이터 전처리는 처음에는 빠른 진행을 위해 삭제하는 방향으로 진행

- 모델 성능 1차 확인 후 다시 데이터 전처리 단계로 와서 채우고 2차 결과 확인 추천

<br>

#### (2) 결측치 채우기(범주형)
- 범주형 데이터에서 결측치를 채울 때는 주로 최빈값으로 대체

- 특정 컬럼에서 mode()[0] 을 통해 최빈값을 찾고, fillna() 로 값을 채울 수 있음

- 결측치가 있는 이유 : 누락 or 해당 도메인 데이터에서 다른 이유로 결측치가 있을수도 있음

  - 결측치를 새로운 카테고리로 분류하는 것도 방법
 
  - ex) 임의의 표시로 결측 데이터를 'X'로 채울 수 있음
 
    - X 는 의미가 있는게 아니라 단순히 결측을 나타내는 유니크한 값으로 채운 것

- 데이터 전처리 시 train 뿐만 아니라 test 도 함께 적용

  - train 에 적용한 전처리를 test 에도 적용

> 코드
```python
  m = train['workclass'].mode()[0]
  print(m)
  train['workclass'] = train['workclass'].fillna(m)
  
  m = train['native.country'].mode()[0]
  print(m)
  train['native.country'] = train['native.country'].fillna(m)
  
  train.isnull().sum()
```

> 결과
```python
  Private
  United-States
  
  id                   0
  age                 12
  workclass            0
  fnlwgt               0
  education            0
  education.num        0
  marital.status       0
  occupation        1668
  relationship         0
  race                 0
  sex                  0
  capital.gain         0
  capital.loss         0
  hours.per.week      13
  native.country       0
  income               0
  dtype: int64
```

<br>

> 코드
```python
  train['occupation'] = train['occupation'].fillna('X')
  train.isnull().sum()
```

> 결과
```python
  id                 0
  age               12
  workclass          0
  fnlwgt             0
  education          0
  education.num      0
  marital.status     0
  occupation         0
  relationship       0
  race               0
  sex                0
  capital.gain       0
  capital.loss       0
  hours.per.week    13
  native.country     0
  income             0
  dtype: int64
```

<br>

> 코드
```python
  # test 데이터
  test['workclass'] = test['workclass'].fillna(train['workclass'].mode()[0])
  test['native.country'] = test['native.country'].fillna(train['native.country'].mode()[0])
  test['occupation'] = test['occupation'].fillna('X')
  test.isnull().sum()
```

> 결과
```python
  id                0
  age               6
  workclass         0
  fnlwgt            0
  education         0
  education.num     0
  marital.status    0
  occupation        0
  relationship      0
  race              0
  sex               0
  capital.gain      0
  capital.loss      0
  hours.per.week    9
  native.country    0
  dtype: int64
```

<br>

#### 💡 최빈값에는 왜 mode() 뒤에 [0] 이 붙을까?
- mode() : 최빈값을 구할 때 mean(), max(), min() 과 달리 시리즈 자료형으로 반환

  - 시리즈로 반환하는 이유
 
    - 빈도 수가 같은 값이 1개가 아니라 여러 개일 수 있기 때문
   
  - 갑ㅄ만 반환받기 위해서는 인덱스 [0] 필요

<br>

#### (3) 결측치 채우기(수치형)
- 결측치를 채울 컬럼의 평균값과 중앙값을 각각 train. 데이터에서 구해 train 과 test 에 채움

- 결측치 처리 후에는 결측치가 다 채워졌는지 확인 필수

<br>

> 코드
```python
  # 평균값으로 채우기
  value = int(train['age'].mean())
  print('평균값: ', value)
  train['age'] = train['age'].fillna(value)
  test['age'] = test['age'].fillna(value)
```
- 나이가 소수점으로 채워지지 않도록 int() 함수로 자료형 변환

  - ex) 31.23세라면 내림해 31세로 변경

> 결과
```python
  평균값:  38
```

<br>

> 코드
```python
  # 중앙값으로 채우기
  value = int(train['hours.per.week'].median())
  print('중앙값: ', value)
  train['hours.per.week'] = train['hours.per.week'].fillna(value)
  test['hours.per.week'] = test['hours.per.week'].fillna(value)
```

> 결과
```python
  중앙값:  40
```

<br>

> 코드
```python
  train.isnull().sum()
```

> 결과
```python
  id                0
  age               0
  workclass         0
  fnlwgt            0
  education         0
  education.num     0
  marital.status    0
  occupation        0
  relationship      0
  race              0
  sex               0
  capital.gain      0
  capital.loss      0
  hours.per.week    0
  native.country    0
  income            0
  dtype: int64
```

<br>

### 02. 이상치(Outliers) 처리
- 이상치 : 일반적인 데이터 패턴에서 벗어난 값

- IQR 활용 or 도메인(해당 분야) 전문가라면 판단 가능

- 빅분기 시험에서는 이상치 처리를 명시한 것이 아니라면 생략 가능

> 코드
```python
  train.describe()
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>fnlwgt</th>
      <th>education.num</th>
      <th>capital.gain</th>
      <th>capital.loss</th>
      <th>hours.per.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>29304.000000</td>
      <td>29304.000000</td>
      <td>2.930400e+04</td>
      <td>29304.000000</td>
      <td>29304.000000</td>
      <td>29304.000000</td>
      <td>29304.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>16264.027880</td>
      <td>38.552996</td>
      <td>1.897488e+05</td>
      <td>10.080842</td>
      <td>1093.858722</td>
      <td>86.744506</td>
      <td>40.434036</td>
    </tr>
    <tr>
      <th>std</th>
      <td>9384.518323</td>
      <td>13.626025</td>
      <td>1.055250e+05</td>
      <td>2.570824</td>
      <td>7477.435640</td>
      <td>401.518928</td>
      <td>12.321306</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>-38.000000</td>
      <td>1.228500e+04</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>8145.750000</td>
      <td>28.000000</td>
      <td>1.177890e+05</td>
      <td>9.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>40.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>16253.500000</td>
      <td>37.000000</td>
      <td>1.783765e+05</td>
      <td>10.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>40.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>24374.250000</td>
      <td>48.000000</td>
      <td>2.370682e+05</td>
      <td>12.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>32560.000000</td>
      <td>90.000000</td>
      <td>1.484705e+06</td>
      <td>16.000000</td>
      <td>99999.000000</td>
      <td>4356.000000</td>
      <td>99.000000</td>
    </tr>
  </tbody>
</table>
</div>

- train 데이터의 'age' 컬럼의 음수를 이상치로 판단하고 제거해보기

<br>

- train 데이터의 'age' 컬럼에서 음수 값 데이터 확인

> 코드
```python
  train[train['age'] < 0]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>workclass</th>
      <th>fnlwgt</th>
      <th>education</th>
      <th>education.num</th>
      <th>marital.status</th>
      <th>occupation</th>
      <th>relationship</th>
      <th>race</th>
      <th>sex</th>
      <th>capital.gain</th>
      <th>capital.loss</th>
      <th>hours.per.week</th>
      <th>native.country</th>
      <th>income</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <td>29188</td>
      <td>-33.0</td>
      <td>Private</td>
      <td>263561</td>
      <td>Some-college</td>
      <td>10</td>
      <td>Married-civ-spouse</td>
      <td>Craft-repair</td>
      <td>Husband</td>
      <td>White</td>
      <td>Male</td>
      <td>0</td>
      <td>0</td>
      <td>60.0</td>
      <td>United-States</td>
      <td>&gt;50K</td>
    </tr>
    <tr>
      <th>79</th>
      <td>14325</td>
      <td>-38.0</td>
      <td>Private</td>
      <td>22245</td>
      <td>HS-grad</td>
      <td>9</td>
      <td>Married-civ-spouse</td>
      <td>Exec-managerial</td>
      <td>Husband</td>
      <td>White</td>
      <td>Male</td>
      <td>0</td>
      <td>0</td>
      <td>60.0</td>
      <td>United-States</td>
      <td>&gt;50K</td>
    </tr>
    <tr>
      <th>26161</th>
      <td>4292</td>
      <td>-25.0</td>
      <td>Private</td>
      <td>200681</td>
      <td>Some-college</td>
      <td>10</td>
      <td>Never-married</td>
      <td>X</td>
      <td>Own-child</td>
      <td>White</td>
      <td>Male</td>
      <td>0</td>
      <td>0</td>
      <td>40.0</td>
      <td>United-States</td>
      <td>&lt;=50K</td>
    </tr>
  </tbody>
</table>
</div>

<br>

-  test 데이터의 'age' 컬럼에는 음수 값 데이터가 없음

> 코드
```python
  test[test['age'] < 0]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>workclass</th>
      <th>fnlwgt</th>
      <th>education</th>
      <th>education.num</th>
      <th>marital.status</th>
      <th>occupation</th>
      <th>relationship</th>
      <th>race</th>
      <th>sex</th>
      <th>capital.gain</th>
      <th>capital.loss</th>
      <th>hours.per.week</th>
      <th>native.country</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>

<br>

- age 가 1 이상인 데이터만 남기기

> 코드
```python
  print(train.shape)
  train = train[train['age'] > 0]
  print(train.shape)
```

> 결과
```python
  (29304, 16)
  (29301, 16)
```
- 전처리 전과 후의 크기 확인을 통해 3개가 줄어든 것 확인 가능

<br>

#### 💡 데이터 전처리 시 주의사항
- train 데이터에 적용한 것을 test 데이터에도 똑같이 적용해야 함

  - 입문자가 흔히 하는 실수
 
    - train 데이터에는 적용하고 test 데이터에는 적용하지 않아 train 데이터와 test 데이터의 형태가 달라지는 것
   
- train 데이터에서의 행(레코드) 삭제는 test 데이터에는 적용 X

  - train 데이터 중 행(레코드)는 일부 삭제할 수 있지만, test 데이터의 행은 삭제하면 안됨
 
    - ex) 100개의 행이 있는 test 데이터라면 결과도 100개 값이 예측되어야 함
   
    - 임의로 삭제시 채점 불가

<br>

### 03. 인코딩(Encoding)
- 컴퓨터가 이해하고 처리할 수 있는 형식으로 변환하는 과정

- 범주형(텍스트) 데이터를 숫자로 변환하는 과정

  - 머신러닝 모델에 입력 데이터로 사용하기 위한 필수 과정
 
- 인코딩 또는 스케일링 전에 label 컬럼을 변수에 옮겨두기
 
<br>

> 코드
```python
  y_train = train.pop('income')
  y_train
```
- train 은 label 값 포함하고 있고, label 은 수치형 데이터가 아닌 범주형 데이터

  - 인코딩을 진행하기에 앞서 함께 원-핫 인코딩되는 것을 방지하기 위해 y_train 변수에 담아둠
 
- pop() : income 컬럼을 y_train 에 대입하고, income 컬럼을 삭제해 이 두 가지를 한 줄로 유용하게 처리할 수 있는 함수

> 결과
```python
  0         >50K
  1        <=50K
  2        <=50K
  3         >50K
  4        <=50K
           ...  
  29299    <=50K
  29300    <=50K
  29301    <=50K
  29302    <=50K
  29303    <=50K
  Name: income, Length: 29301, dtype: object
```

<br>

#### 💡 SettingWithCopyWarning 발생 시 해결 방법
- 데이터를 변경하는 인코딩, 스케일링 등 전처리에서 워닝 발생 가능성 有

- 워닝은 무시해도 되지만, 해결하는 것이 좋음

- 해결 방벙

  - .copy() 활용해 명시적으로 복사
 
    - train 변수를 스케일링하기 전에 코드 중에서 어떤 작업의 결과가 train 에 담겨있다면 .copy() 함수 붙여 해결

```python
  df_copy = df[df['A'] > 10].copy()
  df_copy['B'] = 20
```

<br>

#### (1) 원-핫 인코딩
- 판다스에서 기본적으로 제공

- pd.get_dummies(train) 을 train 데이터 전체에 넣어주면 인코딩이 필요한 컬럼(object)만 자동으로 인코딩 진행된 후 결과값 반환

- train 과 test 의 컬럼이 다르면 머신러닝 입력 데이터로 사용 불가

<br>

> 코드
```python
  train_oh = pd.get_dummies(train)
  test_oh = pd.get_dummies(test)
  print(train.shape, test.shape, train_oh.shape, test_oh.shape)
```

> 결과
```python
  (29301, 15) (3257, 15) (29301, 107) (3257, 103)
```
- train 데이터의 15개 컬럼이 107개 컬럼으로 변경된 것 확인

- test 데이터의 15개 컬럼이 103개 컬럼으로 변경된 것 확인

- train 과 test 데이터의 native.country 컬럼에서 카테고리 차이가 있었음

  - 원핫 인코딩 시 컬럼 수의 불일치로 나타남

<br>

#### 💡 데이터를 합쳐서 인코딩하는 방법
- 머신러닝을 통해 학습하고 예측하기 위해서는 train 컬럼와 test 컬럼이 일치해야 함

- ex) train 에는 과자가 빼빼로, 고래밥, 콘칩 세 가지 종류 / test 에는 고래밥, 콘칩 두 가지 종류

  - 원-핫 인코딩 후 컬럼수가 달라짐
 
    - 데이터를 합치고 원-핫 인코딩 진행 후 다시 train 과 test 로 분할

<br>

> pd.concat() 통해 데이터를 위아래(axis=0)로 합침
```python
  print(train.shape, test.shape)
  data = pd.concat([train, test], axis = 0)
  print(data.shape)
```

> 결과
```python
  (29301, 15) (3257, 15)
  (32558, 15)
```

<br>

> get_dummies(data)f 로 합친 데이터를 원-핫 인코딩
```python
  data_oh = pd.get_dummies(data)
  print(data_oh.shape)
```

> 결과
```python
  (32558, 107)
```

<br>

> iloc 활용해 데이터 분할
```python
  train_oh = data_oh.iloc[:len(train)].copy()
  test_oh = data_oh.iloc[len(train):].copy()
  print(train_oh.shape, test_oh.shape)
```
- train 데이터 수는 len() 으로 찾기

- 선택된 데이터를 새로운 변수에 옮겨 담을 때는 copy() 붙이기

  - 'SettingWithCopyWarning' : copy() 사용하지 않아 발생한 문제

> 결과
```python
  (29301, 107) (3257, 107)
```

<br>

<br>

#### (2) 레이블 인코딩
- 사이킷런(scikit-learn) : 머신러닝과 데이터 분석을 위한 파이썬 라이브러리

  - 사이킷런에서 제공하는 LabelEncoder 활용
 
- 여러 컬럼에 레이블 인코딩을 적용하려면 각 컬럼에 대해 레이블 인코딩을 개별적으로 적용해야 함

  - ex) 8개의 컬럼을 레이블 인코딩한다면 레이블 인코딩 코드를 컬럼명만 달리해서 8번 작성하거나 반복문 활욜
 
    - for col in cols : 리스트(cols)에서 차례대로 컬럼명을 불러와col 변수에 담기
   
    - le = LabelEncoder() : 레이블 인코더 불러오기
   
    - train[col] = le.fit_transform(train[col])
   
      - fit : 매핑 사전 만들기 (ex) 빼빼로: 1, 고래밥: 2, 콘칩: 3
     
      - transform : 매핑 사전에 따라 데이터 변환
     
      - fit_transform : 이 두 작업을 한번에 처리
     
    - test[col] = le.transform(test[col])
   
      - test 에는 train 과 같은 숫자로 데이터를 변환하기 위해 fit 과정없이 transform 만 적용
     
    - 들여쓰기로 작성된 코드까지가 반복문의 범위
   
      - 처음으로 돌아가 cols 에서 다음 값 불러오기

- 레이블 인코딩할 object 컬럼명을 리스트 형태로 만들기

  - object 형만 선택하는 코드 활용 or cols 변수에 직접 리스트 형태로 만들

    - 컬럼 수가 많지 않으면 후자 추천 : 직관적이고 오류 줄일 수 있음
   
      - 컬럼명 오타 주의(데이터 직접 입력 X, 컬럼명 복사-붙여넣기)

> 코드
```python
  # cols = train.select_dtypes(include = 'object').columns      # 방법1
  # cols = train.columns[train.dtypes == object]        # 방법2
  cols = ['workclass', 'education', 'marital.status', 'occupation', 'relationship', 'race', 'sex', 'native.country']
  cols
```

> 결과
```python
  ['workclass',
   'education',
   'marital.status',
   'occupation',
   'relationship',
   'race',
   'sex',
   'native.country']
```

<br>

> 코드
```python
  from sklearn.preprocessing import LabelEncoder
  
  for col in cols :
      le = LabelEncoder()
      train[col] = le.fit_transform(train[col])
      test[col] = le.transform(test[col])
      
  train.head()
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>workclass</th>
      <th>fnlwgt</th>
      <th>education</th>
      <th>education.num</th>
      <th>marital.status</th>
      <th>occupation</th>
      <th>relationship</th>
      <th>race</th>
      <th>sex</th>
      <th>capital.gain</th>
      <th>capital.loss</th>
      <th>hours.per.week</th>
      <th>native.country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3331</td>
      <td>34.0</td>
      <td>6</td>
      <td>177331</td>
      <td>15</td>
      <td>10</td>
      <td>2</td>
      <td>9</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>4386</td>
      <td>0</td>
      <td>40.0</td>
      <td>38</td>
    </tr>
    <tr>
      <th>1</th>
      <td>19749</td>
      <td>58.0</td>
      <td>3</td>
      <td>290661</td>
      <td>11</td>
      <td>9</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>4</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>40.0</td>
      <td>38</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1157</td>
      <td>48.0</td>
      <td>3</td>
      <td>125933</td>
      <td>15</td>
      <td>10</td>
      <td>6</td>
      <td>3</td>
      <td>4</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>1669</td>
      <td>38.0</td>
      <td>38</td>
    </tr>
    <tr>
      <th>3</th>
      <td>693</td>
      <td>58.0</td>
      <td>3</td>
      <td>100313</td>
      <td>15</td>
      <td>10</td>
      <td>2</td>
      <td>10</td>
      <td>0</td>
      <td>4</td>
      <td>1</td>
      <td>0</td>
      <td>1902</td>
      <td>40.0</td>
      <td>38</td>
    </tr>
    <tr>
      <th>4</th>
      <td>12522</td>
      <td>41.0</td>
      <td>3</td>
      <td>195661</td>
      <td>15</td>
      <td>10</td>
      <td>2</td>
      <td>13</td>
      <td>0</td>
      <td>4</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>54.0</td>
      <td>38</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 04. 스케일링
- 수치형 데이터의 범위를 조정하는 작업

- 사이킷런 : 민맥스(최소-최대) 스케일링(Min-Max Scaling), 스탠더드 스케일링(Standard Scaling), 로버스트 스케일링(Robust Scaling) 등

  - 추후 검증 데이터를 평가할 때 더 좋은 쪽 선택

- 트리 기반 모델에서 큰 효과 보기 어려움

  - 선형 회귀나 로지스틱 회귀와 같은 선형 모델은 스케일링의 영향 받음
 
- 스케일링은 선택이기 때문에 1차 제출 후 시간적 여유가 있다면 적용해 비교하는 것을 추천함

<br>

> 스케일링 적용할 원본 데이터가 필요하므로 사본을 불러오는 함수 생성
```python
  cols = ['age', 'fnlwgt', 'education.num', 'capital.gain', 'capital.loss', 'hours.per.week']
  
  def get_data() :
      train_copy = train.copy()
      test_copy = test.copy()
      return train_copy, test_copy
```
- 스케일링을 적용할 수치형 컬럼명을 리스트로 작성

<br>

#### 💡 display() 활용
- print() 와 같은 출력 함수

- 스케일링 전과 후의 가독성을 높이기 위해 display() 활용해 표 형태로 출력

  - 시험 환경에서는 display() 사용 불가로 print() 활용

<br>

#### (1) 민맥스 스케일링
- 데이터를 0과 1 사이로 변환

  - 최소값이 0, 최대값이 1, 나머지 값들은 범위 안에서 매핑

> 코드
```python
  train_copy, test_copy = get_data()
  
  from sklearn.preprocessing import MinMaxScaler
  scaler = MinMaxScaler()
  display(train_copy[cols].head(2))
  train_copy[cols] = scaler.fit_transform(train_copy[cols])
  test_copy[cols] = scaler.transform(test_copy[cols])
  display(train_copy[cols].head(2))
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>fnlwgt</th>
      <th>education.num</th>
      <th>capital.gain</th>
      <th>capital.loss</th>
      <th>hours.per.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>34.0</td>
      <td>177331</td>
      <td>10</td>
      <td>4386</td>
      <td>0</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>58.0</td>
      <td>290661</td>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>40.0</td>
    </tr>
  </tbody>
</table>
</div>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>fnlwgt</th>
      <th>education.num</th>
      <th>capital.gain</th>
      <th>capital.loss</th>
      <th>hours.per.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.232877</td>
      <td>0.112092</td>
      <td>0.600000</td>
      <td>0.04386</td>
      <td>0.0</td>
      <td>0.397959</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.561644</td>
      <td>0.189060</td>
      <td>0.533333</td>
      <td>0.00000</td>
      <td>0.0</td>
      <td>0.397959</td>
    </tr>
  </tbody>
</table>
</div>

<br>

#### 💡 코딩에서 스케일링과 레이블 인코딩의 차이점
- train 데이터에 fit_transform 과 test 데이터에 transform 을 적용하는 것은 유사함

  - 스케일링 : 다수의 컬럼에 한번에 적용 가능
 
  - 레이블 인코딩 : 각 컬럼마다 적용
 
    -여러 컬럼에 적용하기 위해서는 반복문 필수

<br>

#### (2) 스탠더드 스케일링
- 데이터를 평균이 0이고 표준편차가 1인 분포로 변환하는 방벙

> 코드
```python
  train_copy, test_copy = get_data()
  
  from sklearn.preprocessing import StandardScaler
  scaler = StandardScaler()
  display(train_copy[cols].head(2))
  train_copy[cols] = scaler.fit_transform(train_copy[cols])
  test_copy[cols] = scaler.transform(test_copy[cols])
  display(train_copy[cols].head(2))
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>fnlwgt</th>
      <th>education.num</th>
      <th>capital.gain</th>
      <th>capital.loss</th>
      <th>hours.per.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>34.0</td>
      <td>177331</td>
      <td>10</td>
      <td>4386</td>
      <td>0</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>58.0</td>
      <td>290661</td>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>40.0</td>
    </tr>
  </tbody>
</table>
</div>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>fnlwgt</th>
      <th>education.num</th>
      <th>capital.gain</th>
      <th>capital.loss</th>
      <th>hours.per.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.335121</td>
      <td>-0.117705</td>
      <td>-0.031462</td>
      <td>0.440247</td>
      <td>-0.216056</td>
      <td>-0.035121</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.428590</td>
      <td>0.956277</td>
      <td>-0.420430</td>
      <td>-0.146298</td>
      <td>-0.216056</td>
      <td>-0.035121</td>
    </tr>
  </tbody>
</table>
</div>

<br>

#### (3) 로버스트 스케일링(Robust Scaling)
- 각 값의 중앙값을 빼고 1사분위수(Q1)와 3사분위수(Q3)의 차이(IQR)로 나누는 방법

  - 다른 스케일링에 비해 이상치의 영향을 덜받음

> 코드
```python
  from sklearn.preprocessing import RobustScaler
  scaler = RobustScaler()
  display(train[cols].head(2))
  train[cols] = scaler.fit_transform(train[cols])
  test[cols] = scaler.transform(test[cols])
  display(train[cols].head(2))
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>fnlwgt</th>
      <th>education.num</th>
      <th>capital.gain</th>
      <th>capital.loss</th>
      <th>hours.per.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>34.0</td>
      <td>177331</td>
      <td>10</td>
      <td>4386</td>
      <td>0</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>58.0</td>
      <td>290661</td>
      <td>9</td>
      <td>0</td>
      <td>0</td>
      <td>40.0</td>
    </tr>
  </tbody>
</table>
</div>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>fnlwgt</th>
      <th>education.num</th>
      <th>capital.gain</th>
      <th>capital.loss</th>
      <th>hours.per.week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.15</td>
      <td>-0.008711</td>
      <td>0.000000</td>
      <td>4386.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.05</td>
      <td>0.941438</td>
      <td>-0.333333</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>

- 대부분의 사람들이 자본 이득(capital.gain)은 얻지 못했고 대부분 0에 가까움

- capital.gain 의 Q1 과 Q3 이 0에 가깝다면 이 컬럼의 대부분의 값들이 변하지 않을 수 있음

<br>

#### 💡 target 변수가 숫자가 아닌 문자에서 레이블 인코딩이 필요하다면?
- target 은 문자도 인식

  - 일부 머신러닝 모델(Xgboost)에서는 숫자 형태의 target(label) 요구
 
- 타깃을 레이블 인코딩하는 방법

> 코드
```python
  y_train.value_counts()
```

> 결과
```python
  income
  <=50K    22262
  >50K      7039
  Name: count, dtype: int64
```

<br>

> map() 이용
```python
  target = y_train.map({'<=50K':0, '>50K':1})
  target.value_counts()
```

> 결과
```python
  income
  0    22262
  1     7039
  Name: count, dtype: int64
```

<br>

> replace() 이용
```python
  target = y_train.replace('<=50K', 0).replace('>50K', 1)
  target.value_counts()
```

> 결과
```python
  income
  0    22262
  1     7039
  Name: count, dtype: int64
```

<br>

---

<br>

SECTION05 검증 데이터 나누기
---
- 학습된 모델의 성능을 평가하고 개선하기 위해 진행

- 검증 데이터를 활용해 모델의 성능을 평가, 데이터 전처리 단계 또는 하이퍼파라미터 튜닝을 통해 개선 가능

- 사이킷런의 train_test_split() 활용해 데이터 분리

  - train 과 validation 나누는 용도로 활용
 
  - test 데이터와는 관계 X
 
- train_test_split(train, target, test_size=0.2, random_state=0)

  - train : X 데이터, 데이터프레임 형태로 입력
 
  - target : label(y) 데이터, 시리즈 형태로 입력
 
  - test_size=0.2 : 검증용 데이터 비율, 0.2 는 전체 데이터 중에서 20% 의미
 
  - random_state=0 : 랜덤적인 요소 고정, 작성하지 않으면 실행할 때마다 다른 값으로 나눠짐
 
    - 실행할 때마다 같은 데이터로 나누기 위해 고정 필요
   
    - 숫자는 정수로 자유롭게 입력
   
- 반환값 4개

  - X_train, X_val, y_train, y_val
  
    - X, X, y, y 로 암기

> 코드
```python
  from sklearn.model_selection import train_test_split
  
  X_train, X_val, y_train, y_val = train_test_split(train, y_train, test_size=0.2, random_state=0)
  
  X_train.shape, X_val.shape, y_train.shape, y_val.shape
```

> 결과
```python
  ((23440, 15), (5861, 15), (23440,), (5861,))
```

<br>

#### 💡 데이터 분할 이후 shape 보는 방법
- X_train.shape, X_val.shape, y_train.shape, y_val.shape 값에서 두 가지 확인

  - 데이터 분할 이후 X_train.shape, X_val.shape 의 컬럼 수(열 수) 일치
 
  - 데이터 분할 이후 y_train.shape, y_val.shape 에서 컬럼(열) 부분에 1이 나타나지 않는 시리즈 형태
 
- (23440,), (5861,) : 시리즈 형태, 머신러닝에서 타깃 변수 입력 형태

  - (23440,1), (5861,1) : 데이터프레임 형태
 
    - 머신러닝 모델에 입력될 경우 DataConversionWarning 경고 메시지 발생
   
    - train_test_split(train, target) 사용 시 target 이 시리즈가 아니라 데이터프레임으로 입력된 결과

- 다중 변수 할당 : 파이썬은 다중 변수 할당 가능

  - 변수 대입시에도 'a, b, c, d = 1, 2, 3, 4' 로 사용 가능
 
  - 함수에서 4개의 결과를 반활할 때도 a, b, c, d = train_test_split() 으로 사용

<br>

---

<br>

SECTION06 머신러닝 학습  및 평가
---
- 의사결정 나무(Decision Tree) 모델은 학습을 통해 트리 구조 만듦

  - 어떤 과정을 통해 결과가 도출되었는지 설명하기 쉬움
 
  - 과적합되기 쉬워 성능에 한계 有
 
- 과적합 보완

  - 앙상블 기법 : 여러 개의 모델을 학습시켜 사용
 
    - 배깅(bagging)
   
      - 랜덤포레스트(Random Forest)
   
    - 부스팅(boosting)
   
      - 라이트지비엠(LightGBM)

|다이어트 성공과 실패를 알려주는 모델을 나타낸 의사결정 나무 예시|
|-|
|![이미지](./img/01.png)|

<br>

### 01. 랜덤포레스트(Random Forest)
- 여러 개의 의사결정 나무를 기반으로 한 앙상블 학습 알고리즘

- 사이킷런(sklearn.ensemble)에서 랜덤포레스트 분류 모델 불러와 3단계로 사용

  - rf = RandomForestClassifier()  # 모델 선택
 
  - rf.fit(X_train, y_train)       # 학습 진행
 
  - pred = rf.predict_proba(X_val) # 예측
 
    - predict : 예측된 각 레이블(클래스) 반환('<=50K', '>50K')
   
    - predict_proba : 각 레이블에 속할 확률값 반환
   
    - 첫 번째 값 : '<=50K' 인 확률
   
    - 두 번째 값 : '>50K' 인 확률

> 코드
```python
  # 랜덤포레스트
  from sklearn.ensemble import RandomForestClassifier
  rf = RandomForestClassifier(random_state = 0)
  rf.fit(X_train, y_train)
  pred = rf.predict_proba(X_val)      # 각 레이블에 속할 확률값 반환
  
  print(rf.classes_)
  pred[:10]
```

> 결과
```python
  ['<=50K' '>50K']
  array([[1.  , 0.  ],
         [1.  , 0.  ],
         [0.9 , 0.1 ],
         [0.63, 0.37],
         [1.  , 0.  ],
         [0.99, 0.01],
         [0.98, 0.02],
         [0.94, 0.06],
         [0.12, 0.88],
         [0.88, 0.12]])
```

<br>

### 02. 평가지표
- 머신러닝 모델을 학습하고 나서 제대로 학습이 되었고, 예측 하고 있는지 검증 데이터로 평가 필요

- 분류 모델의 평가 지표

  - 정확도(Accuracy)
 
  - 정밀도(Precision)
 
  - 재현율(Recall)
 
  - F1 스코어
 
  - ROC_AUC

<br>

#### (1) ROC_AUC
- 점수를 평가할 때는 확률값 필요

- 머신러닝에서 예측할 때 확률값을 예측할 수 있는 predict_proba() 사용

  - 각 클래스의 확률을 각각 예측 ⇒ 2차원 구조 결과 반환
 
  - 반환된 결과, pred 첫 번째 열인 [0] 불러오면 '<=50K' 확률, 두 번째 열인 [1] 불러오면 '>50K' 확률

<br>

|구분(분류 모델)|평가지표|결과 및 설명|
|:-:|:-:|-|
|predict_proba()|roc_auc|2차원 형태: [[0.4, 0.6], [0.7, 0.3], [0.3, 0.7]]<br>각 클래스의 예측 확률 반환|
|predict()|정확도, F1 Score, 정밀도, 재현율 등|1차원 형태: [1, 0, 1]<br>예측된 클래스(레이블) 반환|

<br>

> 코드
```python
  from sklearn.metrics import roc_auc_score
  roc_auc = roc_auc_score(y_val, pred[:, 1])
  print('roc_auc :', roc_auc)
```

> 결과
```python
  roc_auc : 0.9173623004487484
```

<br>

#### (2) Accuracy(정확도)
- 전체 데이터 중 올바르게 예측된 데이터의 비율

  - 100개 중 86개 맞췄으면 0.86
 
    - 1에 가까울수록 좋음
      
- predict() 활용

  - 예측된 각 클래스(레이블) 반환

> 코드
```python
  pred = rf.predict(X_val)
  pred[:10]
```

> 결과
```python
  array(['<=50K', '<=50K', '<=50K', '<=50K', '<=50K', '<=50K', '<=50K',
         '<=50K', '>50K', '<=50K'], dtype=object)
```
- '<=50K' 또는 '>50K' 인 예측값 확인 가능

<br>

> 코드
```python
  from sklearn.metrics import accuracy_score
  accuracy = accuracy_score(y_val, pred)
  print('accuracy_score :', accuracy)
```

> 결과
```python
  accuracy_score : 0.8694761986009213
```

<br>

#### (3) F1 스코어
- 정밀도(Precision)와 재현율(Recall)의 조화평균으로 계싼되는 평가지표

  - 높을 수록 좋음
 
- 양성 클래스를 1로 가정, target 이 <=50K, >50K 문자로 구성

  - 어떤 값이 양성 클래스인지 pos_laver='>50K' 사용해 지정
 
  - 만약 타깃이 0, 1 로 변환된 숫자였다면 f1_score(y_val, pred) 만 작성 가능

> 코드
```python
  from sklearn.metrics import f1_score
  f1 = f1_score(y_val, pred, pos_label = '>50K')
  print('f1_score :', f1)
```

> 결과
```python
  f1_score : 0.6926476496584973
```

<br>

### 03. 라이트지비엠(LightGBM)
- 그래디언트 부스팅(Gradient Boosting) 기반의 앙상블 학습 알고리즘

  - 머신러닝 모델 중 정형 데이터를 다룰 때 인기있는 모델
 
- 사이킷런이 아닌 별도 라이브러리 활용

  - fit(X, y) 로 학습
 
  - predict(predict_proba) 로 예측
 
- 평가지표 ROC_AUC, Accuracy, F1 스코어 모두 랜덤포레스트 모델 예측 결과보다 성능이 조금씩 향상됨

<br>

#### (1) random_state
- 모델을 학습할 때 랜덤적인 요소가 존재하기 때문에 매번 성능 결과가 달라짐

  - 랜덤적인 요소를 고정하기 위해서는 random_state = 0 설정해 사용
 
    - 이 값이 같다고 해서 다른 환경에서도 같은 값이 나오는 것은 아님
   
    - 작업 중인 환경에서 여러 번 실행했을 때 동일한 결과가 나옴

<br>

#### (2) verbose
- LightGBM 버전에 따라 출력 결과에 로그 메시지(세부사항) 함께 나타남

  - 에러는 아니지만 신경쓰인다면 verbose=-1 사용해 로그 메시지 숨기기 가능

> 코드
```python
  # !pip install lightgbm
  
  import lightgbm as lgb
  lgbmc = lgb.LGBMClassifier(random_state=0, verbose=-1)
  lgbmc.fit(X_train, y_train)
  pred = lgbmc.predict_proba(X_val)
  
  roc_auc = roc_auc_score(y_val, pred[:, 1])
  print('roc_auc :', roc_auc)
  
  pred = lgbmc.predict(X_val)
  accuracy = accuracy_score(y_val, pred)
  print('accuracy_score :', accuracy)
  
  f1 = f1_score(y_val, pred, pos_label='>50K')
  print('f1_score :', f1)
```

> 결과
```python
  roc_auc : 0.9279535666686397
  accuracy_score : 0.8771540692714553
  f1_score : 0.7158642462509865
```

<br>

---

<br>

SECTION07 예측 및 결과 파일 생성
---
- test 데이터 예측

- 학습된 LightGBM 모델을 활용해 test 데이터 넣고 predict_proba 실행시 예측 확률값 반환받음

> 코드
```python
  pred = lgbmc.predict_proba(test)
  pred
```

> 결과
```python
  array([[0.89924007, 0.10075993],
         [0.97622077, 0.02377923],
         [0.9853122 , 0.0146878 ],
         ...,
         [0.93528667, 0.06471333],
         [0.98996872, 0.01003128],
         [0.96723292, 0.03276708]])
```
- 첫 번째 값이 '<=50K' 확률, 두 번째 값이 '>50K' 확률

  - 두 번째 값을 pred[:, 1] 로 선택
 
- 확률값의 순서를 확인하려면 'lgbmc.classes_(모델변수.classes_)'

  - 문자가 아닌 0과 1이었다면 첫 번째가 0 확률값, 두 번째가 1 확률값

<br>

- 예측값을 데이터프레임으로 변경하고, 문제 요구사항대로 컬럼명을 'pred' 로 작성

- result.csv 파일로 저장

  - index = False 파라미터 적용 필수
 
    - 하지 않으면 기존 인덱스도 함께 저장됨

- pd.read_csv() 활용해 최종 확인 후 '제출' 버튼 클릭 (제출은 여러 번 가능)

> 코드
```python
  submit = pd.DataFrame({'pred':pred[:, 1]})
  submit.to_csv('result.csv', index=False)
  
  pd.read_csv('result.csv')
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pred</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.100760</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.023779</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.014688</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.798048</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.026542</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>3252</th>
      <td>0.009613</td>
    </tr>
    <tr>
      <th>3253</th>
      <td>0.321992</td>
    </tr>
    <tr>
      <th>3254</th>
      <td>0.064713</td>
    </tr>
    <tr>
      <th>3255</th>
      <td>0.010031</td>
    </tr>
    <tr>
      <th>3256</th>
      <td>0.032767</td>
    </tr>
  </tbody>
</table>
<p>3257 rows × 1 columns</p>
</div>

<br>






