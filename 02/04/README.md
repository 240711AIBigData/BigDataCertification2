# CHAPTER04 머신러닝 실습(회귀)
- 회귀

  - X 데이터(독립변수, 피처)와 y 데이터(종속변수, 타깃) 간의 관계를 모델링
  
  - 새로 주어진 X 데이터에 대해 연속적인 값 예측
 
- 회귀, 분류 구분

  - 문제를 통해 파악

    - label(target) 이 어떤 컬럼인지 설명을 읽고 파악
   
    - ex) 확률값을 구하라 or 카테고리가 0 또는 1 로 구분 = 분류
   
    - ex) 수요량, 접속량, 사용량, 판매량 등 = 회귀

  - target(label) 값 확인
 
    - 데이터 샘플을 확인했을 때 연속형 숫자인지, 몇몇 값이 반복되는 카테고리인지 확인
   
    - df['target'].value_counts() 확인시 종류가 많으면 회귀, 한눈에 들어오면 분류
 
  - 평가지표 확인
 
    - 어떤 평가지표를 사용하는지에 따라 구분 가능
   
    - ex) MAE, MSE, RMSE 등 E(Error) 가 붙어있으면 회귀
   
<br>

SECTION01 문제 정의
---
- 10개의 아울렛 매장에서 1,500여 개의 제품에 대한 판매 데이터 수집

- 예측 모델을 만들고 아울렛 특정 매장에서 각 제품의 판매금액을 예측

  - 평가 기준은 RMSE 로 평가
 
  - label(target) 은 판매금액(Item_Outlet_Sale)
 
  - 제출 파일은 예측값만 result.csv 파일로 생성해 제출(컬럼명 : pred, 1개)

<br>

---

<br>

SECTION02 라이브러리 및 데이터 불러오기
---
- 판다스 라이브러리와 주어진 train 과 test 데이터셋 불러오기

> 코드
```python
  import pandas as pd
  
  train = pd.read_csv('./data/train.csv')
  test = pd.read_csv('./data/test.csv')
```

<br>

---

<br>

SECTION03 탐색적 데이터 분석(EDA)
---
#### (1) 데이터 크기 확인

> 코드
```python
  train.shape, test.shape
```

> 결과
```python
  ((6818, 12), (1705, 11))
```
- train 의 행(레코드)은 6,818개, 컬럼 12개

- test 의 행(레코드)은 1,708개, 컬럼 11개

<br>

#### (2) 데이터 샘플 확인

> 코드
```python
  train.head()
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item_Identifier</th>
      <th>Item_Weight</th>
      <th>Item_Fat_Content</th>
      <th>Item_Visibility</th>
      <th>Item_Type</th>
      <th>Item_MRP</th>
      <th>Outlet_Identifier</th>
      <th>Outlet_Establishment_Year</th>
      <th>Outlet_Size</th>
      <th>Outlet_Location_Type</th>
      <th>Outlet_Type</th>
      <th>Item_Outlet_Sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NCR06</td>
      <td>12.500</td>
      <td>Low Fat</td>
      <td>0.006760</td>
      <td>Household</td>
      <td>42.8112</td>
      <td>OUT013</td>
      <td>1987</td>
      <td>High</td>
      <td>Tier 3</td>
      <td>Supermarket Type1</td>
      <td>639.1680</td>
    </tr>
    <tr>
      <th>1</th>
      <td>FDW11</td>
      <td>12.600</td>
      <td>Low Fat</td>
      <td>0.048741</td>
      <td>Breads</td>
      <td>60.4194</td>
      <td>OUT013</td>
      <td>1987</td>
      <td>High</td>
      <td>Tier 3</td>
      <td>Supermarket Type1</td>
      <td>990.7104</td>
    </tr>
    <tr>
      <th>2</th>
      <td>FDH32</td>
      <td>12.800</td>
      <td>Low Fat</td>
      <td>0.075997</td>
      <td>Fruits and Vegetables</td>
      <td>97.1410</td>
      <td>OUT013</td>
      <td>1987</td>
      <td>High</td>
      <td>Tier 3</td>
      <td>Supermarket Type1</td>
      <td>2799.6890</td>
    </tr>
    <tr>
      <th>3</th>
      <td>FDL52</td>
      <td>6.635</td>
      <td>Regular</td>
      <td>0.046351</td>
      <td>Frozen Foods</td>
      <td>37.4506</td>
      <td>OUT017</td>
      <td>2007</td>
      <td>NaN</td>
      <td>Tier 2</td>
      <td>Supermarket Type1</td>
      <td>1176.4686</td>
    </tr>
    <tr>
      <th>4</th>
      <td>FDO09</td>
      <td>13.500</td>
      <td>Regular</td>
      <td>0.125170</td>
      <td>Snack Foods</td>
      <td>261.4910</td>
      <td>OUT013</td>
      <td>1987</td>
      <td>High</td>
      <td>Tier 3</td>
      <td>Supermarket Type1</td>
      <td>3418.8830</td>
    </tr>
  </tbody>
</table>
</div>

- 카테고리(문자)와 숫자 컬럼이 혼합되어 있음

- 마지막 컬럼인 Item)Outlet_Sales 는 target(label) 컬럼

  - 금액이고 소수점이 있는 숫자

<br>

#### (3) 데이터 자료형(타입) 확인

> 코드
```python
  train.info()
```

> 결과
```python
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 6818 entries, 0 to 6817
  Data columns (total 12 columns):
   #   Column                     Non-Null Count  Dtype  
  ---  ------                     --------------  -----  
   0   Item_Identifier            6818 non-null   object 
   1   Item_Weight                5656 non-null   float64
   2   Item_Fat_Content           6818 non-null   object 
   3   Item_Visibility            6818 non-null   float64
   4   Item_Type                  6818 non-null   object 
   5   Item_MRP                   6818 non-null   float64
   6   Outlet_Identifier          6818 non-null   object 
   7   Outlet_Establishment_Year  6818 non-null   int64  
   8   Outlet_Size                4878 non-null   object 
   9   Outlet_Location_Type       6818 non-null   object 
   10  Outlet_Type                6818 non-null   object 
   11  Item_Outlet_Sales          6818 non-null   float64
  dtypes: float64(4), int64(1), object(7)
  memory usage: 639.3+ KB
```
- float 4개, int 1개, object 7개

  - 7개의 컬럼은 인코딩 필요

<br>

#### (4) 기술통계 값 확인
- median(50%) > mean : 왼쪽 꼬리가 긴 분포(Negative Skew)

- median(50%) < mean : 오른쪽 꼬리가 긴 분포(Positive Skew)

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
      <th>Item_Weight</th>
      <th>Item_Visibility</th>
      <th>Item_MRP</th>
      <th>Outlet_Establishment_Year</th>
      <th>Item_Outlet_Sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>5656.000000</td>
      <td>6818.000000</td>
      <td>6818.000000</td>
      <td>6818.000000</td>
      <td>6818.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>12.872703</td>
      <td>0.066121</td>
      <td>140.419533</td>
      <td>1997.885890</td>
      <td>2190.941459</td>
    </tr>
    <tr>
      <th>std</th>
      <td>4.651034</td>
      <td>0.051383</td>
      <td>62.067861</td>
      <td>8.339795</td>
      <td>1706.131256</td>
    </tr>
    <tr>
      <th>min</th>
      <td>4.555000</td>
      <td>0.000000</td>
      <td>31.290000</td>
      <td>1985.000000</td>
      <td>33.290000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>8.785000</td>
      <td>0.026914</td>
      <td>93.610050</td>
      <td>1987.000000</td>
      <td>836.577700</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>12.600000</td>
      <td>0.053799</td>
      <td>142.448300</td>
      <td>1999.000000</td>
      <td>1806.648300</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>17.000000</td>
      <td>0.095273</td>
      <td>185.060150</td>
      <td>2004.000000</td>
      <td>3115.944000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>21.350000</td>
      <td>0.328391</td>
      <td>266.888400</td>
      <td>2009.000000</td>
      <td>13086.964800</td>
    </tr>
  </tbody>
</table>
</div>

- Item_Visibility 와 Item_Outlet_Sales 컬럼은 median(50%) < mean

  - 데이터 모양이 오른쪽 꼬리가 긴 분포의 모양

    - 시험에서는 시각화 출력 사용 불가

> 코드
```python
  train['Item_Outlet_Sales'].hist()
```

> 결과

![image](https://github.com/user-attachments/assets/e35ac912-2822-4968-8882-b14bbe14a73d)


<br>

#### (5) object 컬럼의 unique 개수 확인
- unique 개수에 따라 원-핫 인코딩 or 레이블 인코딩 사용

  - ex) 1,554개를 원-핫 인코딩했을 때 컬럼 수가 엄청나게 늘어나고 대부분의 값이 0으로 채워져 낭비 심함

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
      <th>Item_Identifier</th>
      <th>Item_Fat_Content</th>
      <th>Item_Type</th>
      <th>Outlet_Identifier</th>
      <th>Outlet_Size</th>
      <th>Outlet_Location_Type</th>
      <th>Outlet_Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>6818</td>
      <td>6818</td>
      <td>6818</td>
      <td>6818</td>
      <td>4878</td>
      <td>6818</td>
      <td>6818</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>1554</td>
      <td>5</td>
      <td>16</td>
      <td>10</td>
      <td>3</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>top</th>
      <td>FDW26</td>
      <td>Low Fat</td>
      <td>Snack Foods</td>
      <td>OUT046</td>
      <td>Medium</td>
      <td>Tier 3</td>
      <td>Supermarket Type1</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>9</td>
      <td>4092</td>
      <td>963</td>
      <td>763</td>
      <td>2228</td>
      <td>2664</td>
      <td>4474</td>
    </tr>
  </tbody>
</table>
</div>

- 3개부터 1,554개까지 있음

  - 1,554개 컬럼은 Item_Identifier
 
    - id 는 일반적으로 count 와 unique 수가 같지만, 이 경우 차이가 큼
   
      - 삭제하지 않았을 때와 삭제했을 때 둘 다 비교 필요
     
<br>

#### (6) test 데이터셋에 있는 object 컬럼 확인

> 코드
```python
  test.describe(include = 'O')
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item_Identifier</th>
      <th>Item_Fat_Content</th>
      <th>Item_Type</th>
      <th>Outlet_Identifier</th>
      <th>Outlet_Size</th>
      <th>Outlet_Location_Type</th>
      <th>Outlet_Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1705</td>
      <td>1705</td>
      <td>1705</td>
      <td>1705</td>
      <td>1235</td>
      <td>1705</td>
      <td>1705</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>1077</td>
      <td>5</td>
      <td>16</td>
      <td>10</td>
      <td>3</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>top</th>
      <td>FDG33</td>
      <td>Low Fat</td>
      <td>Fruits and Vegetables</td>
      <td>OUT013</td>
      <td>Medium</td>
      <td>Tier 3</td>
      <td>Supermarket Type1</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>4</td>
      <td>997</td>
      <td>272</td>
      <td>207</td>
      <td>565</td>
      <td>686</td>
      <td>1103</td>
    </tr>
  </tbody>
</table>
</div>

- Item_Identifier 제외하고 모두 train 데이터셋과 unique 개수 동일

<br>

#### (7) 결측치 여부 확인
- train 과 test 모두 2개의 컬럼에서 결측치 有

  - 데이터 전처리 단계에서 결측치 처리 필요
    
> 코드
```python
  train.isnull().sum()
```

> 결과
```python
  Item_Identifier                 0
  Item_Weight                  1162
  Item_Fat_Content                0
  Item_Visibility                 0
  Item_Type                       0
  Item_MRP                        0
  Outlet_Identifier               0
  Outlet_Establishment_Year       0
  Outlet_Size                  1940
  Outlet_Location_Type            0
  Outlet_Type                     0
  Item_Outlet_Sales               0
  dtype: int64
```

<br>

> 코드
```python
  test.isnull().sum()
```

> 결과
```python
  Item_Identifier                0
  Item_Weight                  301
  Item_Fat_Content               0
  Item_Visibility                0
  Item_Type                      0
  Item_MRP                       0
  Outlet_Identifier              0
  Outlet_Establishment_Year      0
  Outlet_Size                  470
  Outlet_Location_Type           0
  Outlet_Type                    0
  dtype: int64
```

<br>

---

<br>

SECTION04 데이터 전처리
---
#### (1) 인코딩 처리를 위해 object 컬럼 선택 

- 컬럼명 중 object 컬럼만 리스트로 만드는 방법

- 직접 object 컬럼 리스트를 만드는 방법

> 코드
```python
  list(train.columns[train.dtypes == object])
```

> 결과
```python
  ['Item_Identifier',
   'Item_Fat_Content',
   'Item_Type',
   'Outlet_Identifier',
   'Outlet_Size',
   'Outlet_Location_Type',
   'Outlet_Type']
```

<br>

#### (2) object 컬럼 모두 인코딩 진행

- 특정 컬럼을 제외하고 싶다면?

  - 모든 object 컬럼명을 선택하는 코드 작성 후 복사해 리스트를 직접 만든 다음 특정 컬럼 빼는 방법

> 코드
```python
  cols = ['Item_Fat_Content', 'Item_Type', 'Outlet_Identifier', 'Outlet_Size', 'Outlet_Location_Type', 'Outlet_Type']
  cols
```

> 결과
```python
  ['Item_Fat_Content',
   'Item_Type',
   'Outlet_Identifier',
   'Outlet_Size',
   'Outlet_Location_Type',
   'Outlet_Type']
```

<br>

#### (3) target 컬럼을 변수에 옮겨두고 데이터를 합쳐서 인코딩

- 인코딩을 위해 train 과 test 데이터셋을 병합

  - 합쳐서 진행하지 않을 경우 Item_Identifier 는 train 과 test 의 카테고리(종류)가 달라 모델 학습시 에러 발생
 
- Item_Identifier 제거하는 방법도 있음

<br>

> 코드
```python
  target = train.pop('Item_Outlet_Sales')
  print(train.shape, test.shape)
  df = pd.concat([train, test])
  print(df.shape)
```

> 결과
```python
  (6818, 11) (1705, 11)
  (8523, 11)
```

<br>

#### (4) 사이킷런에서 제공하는 LabelEncoder 로 레이블 인코딩 진행

- train 과 test 가 합쳐진 df 데이터만 레이블 인코딩

> 코드
```python
  # 레이블 인코딩
  from sklearn.preprocessing import LabelEncoder
  le = LabelEncoder()
  for col in cols:
      df[col] = le.fit_transform(df[col])
      
  df.head()
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item_Identifier</th>
      <th>Item_Weight</th>
      <th>Item_Fat_Content</th>
      <th>Item_Visibility</th>
      <th>Item_Type</th>
      <th>Item_MRP</th>
      <th>Outlet_Identifier</th>
      <th>Outlet_Establishment_Year</th>
      <th>Outlet_Size</th>
      <th>Outlet_Location_Type</th>
      <th>Outlet_Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NCR06</td>
      <td>12.500</td>
      <td>1</td>
      <td>0.006760</td>
      <td>9</td>
      <td>42.8112</td>
      <td>1</td>
      <td>1987</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>FDW11</td>
      <td>12.600</td>
      <td>1</td>
      <td>0.048741</td>
      <td>1</td>
      <td>60.4194</td>
      <td>1</td>
      <td>1987</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>FDH32</td>
      <td>12.800</td>
      <td>1</td>
      <td>0.075997</td>
      <td>6</td>
      <td>97.1410</td>
      <td>1</td>
      <td>1987</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>FDL52</td>
      <td>6.635</td>
      <td>2</td>
      <td>0.046351</td>
      <td>5</td>
      <td>37.4506</td>
      <td>2</td>
      <td>2007</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>FDO09</td>
      <td>13.500</td>
      <td>2</td>
      <td>0.125170</td>
      <td>13</td>
      <td>261.4910</td>
      <td>1</td>
      <td>1987</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>

<br>

#### 💡 레이블 인코딩하는 다른 방법(cat.codes)
- 사이킷런 레이블 인코딩이 아닌 다른 방법으로도 진행 가능

- 자료형을 category 로 변경 후 .cat.codes 붙여주면 레이블 인코딩 됨

- 반복문이 각 컬럼의 인코딩하는 과정을 파악할 수 있도록 print() 함수 추가함

  - 확인용으로 사용하지 않아도 괜찮음

> 코드
```python
  for col in cols:
      df[col] = df[col].astype('category').cat.codes
      print(f'{col} 레이블 인코딩 완료')
```

> 결과
```python
  Item_Fat_Content 레이블 인코딩 완료
  Item_Type 레이블 인코딩 완료
  Outlet_Identifier 레이블 인코딩 완료
  Outlet_Size 레이블 인코딩 완료
  Outlet_Location_Type 레이블 인코딩 완료
  Outlet_Type 레이블 인코딩 완료
```

<br>

#### (5) 인코딩 결과 확인 후 합친 데이터를 다시 train 과 test 로 분할 (iloc 활용)
- train index 번호는 처음부터 (train 개수 - 1)까지

- test index 번호는 train 행의 수부터 마지막까지

- iloc 뒤에 copy() 붙이면 복사본 생성

  - copy() 사용하지 않을 경우 판다스 버전에 따라 워닝 발생
 
> 코드
```python
  train = df.iloc[:len(train)].copy()
  test = df.iloc[len(train):].copy()
  train.shape, test.shape
```

> 결과
```python
  ((6818, 11), (1705, 11))
```

<br>

#### (6) 결측치 채우기(최소값, 최빈값)
- 왜 최소값과 최빈값을 선택했을까?

  - 연속형 컬럼의 경우 최소, 최대, 평균, 중앙 또는 그룹별 평균 중에서 편한 것으로 먼저 채우기
 
  - 첫 베이스라인(baseline) 결과 이후 변경
 
- 베이스라인은 작업형2 결과(csv)를 제출할 수 있는 최소한의 형태로 사용

  - 데이터를 불러오고 간단한 전처리와 빠르게 모델을 만들어 예측 결과를 제출할 수 있는 형태

- 전처리 중 스케일링, 이상치 등은 베이스라인을 만들기 위한 필수 요소가 아니므로 생략

- item_id 삭제

  - 삭제했을 때와 삭제하지 않았을 때의 모델 결과 비교 후 더 좋은 것 선택하는 것도 방법
 
> 코드
```python
  train['Item_Weight'] = train['Item_Weight'].fillna(train['Item_Weight'].min())
  train['Outlet_Size'] = train['Outlet_Size'].fillna(train['Outlet_Size'].mode()[0])
  
  test['Item_Weight'] = test['Item_Weight'].fillna(test['Item_Weight'].min())
  test['Outlet_Size'] = test['Outlet_Size'].fillna(test['Outlet_Size'].mode()[0])
  
  print(train.shape, test.shape)
  
  train.drop('Item_Identifier', axis=1, inplace=True)
  test.drop('Item_Identifier', axis=1, inplace=True)
  
  print(train.shape, test.shape)
```

> 결과
```python
  (6818, 11) (1705, 11)
  (6818, 10) (1705, 10)
```

<br>

---

<br>

SECTION05 검증 데이터 나누기
---
- 데이터를 학습용과 검증용으로 나눌 때 주의사항

  - X 데이터에서 타깃 변수 제외
 
    - 학습 데이터(X)에는 타깃 변수(y)를 포함시키지 않아야 함
   
    - 타깃 변수를 포함시키게 되면 모델은 이미 정답을 알고 있게 됨
   
    - 시험 문제지에 답이 이미 제공한 것과 같아 모델이 실제로 예측 능력을 갖췄는지 평가 불가
 
  - y 데이터는 시리즈 형태로
 
    - 타깃 데이터(y)는 데이터프레임에서 단일 컬럼을 선택해 시리즈 형태로 있어야 함
   
    - 데이터프레임 형태라도 나누는 것은 가능하지만, 머신러닝 모델에서 워닝 발생시킬 수 있음
 
  - random_state 고정
 
    - 데이터를 나눌 때 random_state 값을 설정해 고정시키면 코드 실행할 때마다 동일한 방식으로 데이터 나눠짐
   
    - 모델의 성능을 일관되게 평가
   
    - 다른 조건에서 실험했을 때 결과 재현 가능

> 코드
```python
  # 검증 데이터 나누기
  from sklearn.model_selection import train_test_split
  X_train, X_val, y_train, y_val = train_test_split(train, target, test_size=0.2, random_state=0)
  X_train.shape, X_val.shape, y_train.shape, y_val.shape
```

> 결과
```python
  ((5454, 10), (1364, 10), (5454,), (1364,))
```

<br>

---

<br>

SECTION06 머신러닝 학습 및 평가
---
 - 검증 데이터를 활용한 평가로 현 수준을 파악하고 모델을 더 개선할 수 있음

 - 시험에서 RMSE 계산에 어려움이 있다면 MAE 나 MSE 나 R² 로라도 평가 진행

   - 작업형2는 중간 과정이나 검증은 평가하지 않음

```python
  from sklearn.metrics import mean_squared_error
  from sklearn.metrics import mean_absolute_error
  from sklearn.metrics import r2_score
  
  def rmse(y_val, y_pred):
      return mean_squared_error(y_val, y_pred)**0.5
```

<br>

#### 💡 만약 아무 평가지표도 생각나지 않으면?
- 직접 비교

  - 검증 데이터의 예측 결과를 실제 결과 10개의 샘플만이라도 눈으로 확인
 
- ex) 분류에서 10개 샘플 모두 오답을 예측했거나, 회귀에서 숫자의 갭이 말도 안되게 크다면 잘못된 가능성 높음

<br>

### 01. 선형 회귀
- 기본적인 회귀 모델인 선형 회귀 모델로 학습하고 X_val 예측 결과값을 y_val 과 비교 평가

- 선형 회귀(Linear Regression) 모델은 random_state 하이퍼파라미터 값 없음

- MSE, MAE, RMSE 낮을 수록 좋음

  - 평가지표인 RMSE 는 오차 값을 나타내기 때문에 성능이 어느 정도인지 가늠하기 어려움
 
    - 첫 번째(베이스라인) 모델의 점수 기준
   
    - RMSE 결과값보다 더 좋은 성능을 내기 위해 노력하면 됨

- R² 1에 가까울수록 좋음

<br>

> 코드
```python
  # 선형 회귀
  from sklearn.linear_model import LinearRegression
  lr = LinearRegression()
  lr.fit(X_train, y_train)
  y_pred = lr.predict(X_val)
  
  result = mean_squared_error(y_val, y_pred)
  print('MSE :', result)
  
  result = mean_absolute_error(y_val, y_pred)
  print('MAE :', result)
  
  result = r2_score(y_val, y_pred)
  print('R2 :', result)
  
  result = rmse(y_val, y_pred)
  print('RMSE :', result)
```

> 결과
```python
  MSE : 1282923.0729833895
  MAE : 865.1968401416271
  R2 : 0.5058168396924843
  RMSE : 1132.6619411737067
```

<br>

---

<br>

SECTION07 예측 및 결과 파일 생성
---



<br>
