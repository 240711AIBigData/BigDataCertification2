# CAHPTER05 머신러닝 실습(다중 분류)
- 이진 분류(Binary Classification) : 0 또는 1, 불량 또는 정상 등 클래스(class)가 2개

- 다중 분류(Multi-class Classification) : 클래스가 3개 이상

  - 평가지표에만 차이 有
 
- LightGBM 활용해 범주형 변수를 인코딩 없이 전처리

<br>

SECTION01 문제 정의
---
- 개인의 신용 관련 정보 데이터

- 개인의 신용 등급(Credit_Score) 예측

  - 평가 기준은 macro-f1 으로 평가
 
  - label(target) 은 신용 등급(Credit_Score) : 1, 2, 3
 
  - 제출 방식은 test 데이터로 예측한 class 1개 컬럼만 csv 로 제출
 
    - 컬럼명 : pred, 파일명 : result.csv

<br>

---

<br>

SECTION02 라이브러리 및 데이터 불러오기
---
- 판다스 라이브러리와 주어진 train, test 데이터셋 불러오기

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
  ((10000, 21), (10000, 20))
```
- train 행(레코드) : 10,000개, 컬럼 : 21개

- test 행(레코드) : 10,000개, 컬럼 : 20개

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
      <th>Delay_from_due_date</th>
      <th>Num_of_Delayed_Payment</th>
      <th>Num_Credit_Inquiries</th>
      <th>Credit_Utilization_Ratio</th>
      <th>Credit_History_Age</th>
      <th>Payment_of_Min_Amount</th>
      <th>Amount_invested_monthly</th>
      <th>Monthly_Balance</th>
      <th>Credit_Score</th>
      <th>Credit_Mix</th>
      <th>...</th>
      <th>Age</th>
      <th>Annual_Income</th>
      <th>Num_Bank_Accounts</th>
      <th>Num_Credit_Card</th>
      <th>Interest_Rate</th>
      <th>Num_of_Loan</th>
      <th>Monthly_Inhand_Salary</th>
      <th>Changed_Credit_Limit</th>
      <th>Outstanding_Debt</th>
      <th>Total_EMI_per_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>56.0</td>
      <td>16.0</td>
      <td>11.0</td>
      <td>35.598217</td>
      <td>120.0</td>
      <td>Yes</td>
      <td>229.093478</td>
      <td>252.385965</td>
      <td>1</td>
      <td>Bad</td>
      <td>...</td>
      <td>15.0</td>
      <td>36597.56</td>
      <td>8.0</td>
      <td>10.0</td>
      <td>29.0</td>
      <td>5.0</td>
      <td>3143.796667</td>
      <td>22.49</td>
      <td>2963.18</td>
      <td>122.900223</td>
    </tr>
    <tr>
      <th>1</th>
      <td>49.0</td>
      <td>23.0</td>
      <td>12.0</td>
      <td>25.553106</td>
      <td>120.0</td>
      <td>Yes</td>
      <td>104.613906</td>
      <td>219.105944</td>
      <td>1</td>
      <td>Bad</td>
      <td>...</td>
      <td>28.0</td>
      <td>32057.30</td>
      <td>9.0</td>
      <td>8.0</td>
      <td>16.0</td>
      <td>7.0</td>
      <td>2606.441667</td>
      <td>1.40</td>
      <td>1327.26</td>
      <td>164.859426</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34.0</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>40.039954</td>
      <td>174.0</td>
      <td>Yes</td>
      <td>338.626965</td>
      <td>251.265589</td>
      <td>1</td>
      <td>Bad</td>
      <td>...</td>
      <td>46.0</td>
      <td>75868.80</td>
      <td>6.0</td>
      <td>10.0</td>
      <td>32.0</td>
      <td>7.0</td>
      <td>6074.400000</td>
      <td>3.60</td>
      <td>1432.71</td>
      <td>297.547446</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21.0</td>
      <td>13.0</td>
      <td>8.0</td>
      <td>25.711678</td>
      <td>143.0</td>
      <td>NM</td>
      <td>116.816864</td>
      <td>259.927960</td>
      <td>2</td>
      <td>Standard</td>
      <td>...</td>
      <td>46.0</td>
      <td>17092.69</td>
      <td>7.0</td>
      <td>3.0</td>
      <td>19.0</td>
      <td>7.0</td>
      <td>1695.390833</td>
      <td>16.40</td>
      <td>1417.06</td>
      <td>62.794260</td>
    </tr>
    <tr>
      <th>4</th>
      <td>19.0</td>
      <td>13.0</td>
      <td>6.0</td>
      <td>39.140463</td>
      <td>138.0</td>
      <td>Yes</td>
      <td>87.262887</td>
      <td>626.212330</td>
      <td>1</td>
      <td>Bad</td>
      <td>...</td>
      <td>45.0</td>
      <td>81471.96</td>
      <td>6.0</td>
      <td>6.0</td>
      <td>25.0</td>
      <td>5.0</td>
      <td>6763.330000</td>
      <td>27.09</td>
      <td>2679.69</td>
      <td>202.857783</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 21 columns</p>
</div>

- 카테고리(문자)와 숫자 컬럼이 혼합되어 있는 것 확인

<br>

#### (3) 데이터 자료형(타입) 확인

> 코드
```python
  train.info()
```

> 결과
```python
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 10000 entries, 0 to 9999
  Data columns (total 21 columns):
   #   Column                    Non-Null Count  Dtype  
  ---  ------                    --------------  -----  
   0   Delay_from_due_date       10000 non-null  float64
   1   Num_of_Delayed_Payment    10000 non-null  float64
   2   Num_Credit_Inquiries      10000 non-null  float64
   3   Credit_Utilization_Ratio  10000 non-null  float64
   4   Credit_History_Age        10000 non-null  float64
   5   Payment_of_Min_Amount     10000 non-null  object 
   6   Amount_invested_monthly   10000 non-null  float64
   7   Monthly_Balance           10000 non-null  float64
   8   Credit_Score              10000 non-null  int64  
   9   Credit_Mix                10000 non-null  object 
   10  Payment_Behaviour         10000 non-null  object 
   11  Age                       10000 non-null  float64
   12  Annual_Income             10000 non-null  float64
   13  Num_Bank_Accounts         10000 non-null  float64
   14  Num_Credit_Card           10000 non-null  float64
   15  Interest_Rate             10000 non-null  float64
   16  Num_of_Loan               10000 non-null  float64
   17  Monthly_Inhand_Salary     10000 non-null  float64
   18  Changed_Credit_Limit      10000 non-null  float64
   19  Outstanding_Debt          10000 non-null  float64
   20  Total_EMI_per_month       10000 non-null  float64
  dtypes: float64(17), int64(1), object(3)
  memory usage: 1.6+ MB
```
- float : 17개, int : 1개, object : 3개

  - object 컬럼은 인코딩 필요

<br>

#### (4) object 컬럼의 unique 개수 확인

> 코드
```python
  train.describe(include='O')
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Payment_of_Min_Amount</th>
      <th>Credit_Mix</th>
      <th>Payment_Behaviour</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>10000</td>
      <td>10000</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>3</td>
      <td>3</td>
      <td>6</td>
    </tr>
    <tr>
      <th>top</th>
      <td>Yes</td>
      <td>Standard</td>
      <td>Low_spent_Small_value_payments</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>5269</td>
      <td>4591</td>
      <td>3416</td>
    </tr>
  </tbody>
</table>
</div>

- 작게는 3개부터 많게는 6개까지

- Payment_of_Min_Amount 컬럼은 Yes 가 데이터의 절반 이상 차지

- Credit_Mix 컬럼은 Standard 가 절반에 가까운 빈도수

<br>

#### (5) test 데이터셋에 있는 object 컬럼 확인

> 코드
```python
  test.describe(include='O')
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Payment_of_Min_Amount</th>
      <th>Credit_Mix</th>
      <th>Payment_Behaviour</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>10000</td>
      <td>10000</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>3</td>
      <td>3</td>
      <td>6</td>
    </tr>
    <tr>
      <th>top</th>
      <td>Yes</td>
      <td>Standard</td>
      <td>Low_spent_Small_value_payments</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>5167</td>
      <td>4590</td>
      <td>3498</td>
    </tr>
  </tbody>
</table>
</div>

- train 과 유사한 형태

<br>

#### (6) 결측치 확인
- 컬럼 수가 많고 유무만을 파악하기 위해 끝에 .sum() 하나 더 붙임

  - 총 결측 수 확인 가능
 
> 코드
```python
  print(train.isnull().sum().sum())
  print(test.isnull().sum().sum())
```

> 결과
```python
  0
  0
```
- 0 으로 train 과 test 데이터에는 결측치가 없음

<br>

#### (7) target(label) 값 확인

> 코드
```python
  train['Credit_Score'].value_counts()
```

> 결과
```python
  Credit_Score
  2    5237
  1    2978
  3    1785
  Name: count, dtype: int64
```
- 1, 2, 3 클래스 존재

  - 2 > 1 > 3 순으로 빈도 수 확인 가능

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































































