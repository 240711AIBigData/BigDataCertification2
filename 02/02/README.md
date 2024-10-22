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

















