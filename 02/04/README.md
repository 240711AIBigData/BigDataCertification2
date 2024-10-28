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



<br>

---

<br>

SECTION05 검증 데이터 나누기
---



<br>

---

<br>

SECTION06 머신러닝 학습 및 평가
---



<br>

---

<br>

SECTION07 예측 및 결과 파일 생성
---



<br>
