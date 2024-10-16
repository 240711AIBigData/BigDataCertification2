# 작업형1 연습문제
section01 필터링, 최솟값, 중앙값
---
### 문제
1. 'f5' 컬럼이 0이 아닌 데이터(행) 구하시오.

2. 앞에서 구한 데이터에 'views' 컬럼 결측치를 'views' 컬럼의 최솟값으로 채워주시오.

3. 그리고 'views' 컬럼의 중앙값을 계산해 정수로 구하시오.

<br>

```python
  improt pandas as pd
  df = pd.read_csv('./data/type1_data1.csv')
```

<details>
  <summary>df 확인</summary>

<br>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  min(), fillna(), median()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # f5 컬럼에 0 제외
  cond = df['f5'] != 0
  df[cond]
```
- 0 값을 제외한 데이터 찾기

  - df['f5']!=0 이 아닌 값을 찾는 방법
 
  - df['f5']==0 인 값을 찾고 df[~cond]로 데이터 선택하는 방법
 
    - ~ : not 연산자
   
- not 연산자는 True 면 False, False 면 True

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>97</th>
      <td>id97</td>
      <td>100.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>INFP</td>
      <td>67.886373</td>
      <td>2024-03-18</td>
      <td>6687.0</td>
    </tr>
    <tr>
      <th>98</th>
      <td>id98</td>
      <td>39.0</td>
      <td>경기</td>
      <td>58.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>98.429899</td>
      <td>2024-10-02</td>
      <td>865.0</td>
    </tr>
    <tr>
      <th>99</th>
      <td>id99</td>
      <td>1.0</td>
      <td>경기</td>
      <td>47.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFJ</td>
      <td>97.381034</td>
      <td>2024-12-02</td>
      <td>6090.0</td>
    </tr>
    <tr>
      <th>100</th>
      <td>id100</td>
      <td>47.0</td>
      <td>경기</td>
      <td>53.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ESFP</td>
      <td>33.308999</td>
      <td>2024-02-21</td>
      <td>15535.0</td>
    </tr>
    <tr>
      <th>101</th>
      <td>id68</td>
      <td>35.0</td>
      <td>경기</td>
      <td>45.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>67.886373</td>
      <td>2024-07-29</td>
      <td>8599.0</td>
    </tr>
  </tbody>
</table>
<p>102 rows × 10 columns</p>
</div>

<br>

> 코드
```python
  # views 컬럼 결측치를 최소값으로 대체
  min = df['views'].min()
  df['views'].fillna(min, inplace=True)
```
- 결측치를 채울 때는 fillna() 활용

  - 채운 데이터를 저장하기 위해 inplace 사용하거나 대입 연산자 사용
 
    - df['views'] = df['views'].fillna(min)
      
<br>

> 코드
```python
  # views 컬럼의 중앙값 정수로
  print(int(df['views'].median()))
```

> 결과
```python
  5924
```

</details>

<br>

---

<br>

section02 카테고리, 인덱스 문자열 슬라이싱
---
### 문제
1. 'subscribed' 컬럼에서 가장 빈도수가 많은 날짜를 구하시오.

2. 앞에서 구한 날짜의 일(day) 값을 정수로 구하시오

<br>

```python
  improt pandas as pd
  df = pd.read_csv('./data/type1_data1.csv')
```

<details>
  <summary>df 확인</summary>
  
<br>
  
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  value_counts(), index[], str[:]
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # subscribed 종류 중 가장 많은 날짜 구하기
  df = df['subscribed'].value_counts()
  df
```
- 카테고리별 개수를 확인하기 위해서 value_counts() 사용

  - 가장 빈도 수가 많은 순부터 나열
 
- 원하값만 출력하기 위해 value_counts() 결과를 데이터프레임으로 저장

> 결과
```
  subscribed
  2025-02-17    16
  2024-06-21     3
  2024-04-03     2
  2024-07-29     2
  2024-05-28     2
                ..
  2024-07-08     1
  2024-07-20     1
  2024-06-10     1
  2024-02-01     1
  2024-05-20     1
  Name: count, Length: 96, dtype: int64
```

<br>

> 코드
```python
  # 일(day) 값을 찾고, 정수형으로 변경
  int(df.index[0][-2:])
```
- 첫 번째 행(row)이 빈도 수가 많은 데이터

  - 날짜 카테고리가 인덱스로 ⇒ index[0] 사용해 날짜 얻기 가능
 
- day 만 출력하기 위해 문자열 슬라이싱

  - index[0]은 문자열 형태이므로 바로 문자열 슬라이싱 적용 가능
 
  - index[0][-2:] : 첫 번째 행에서 문자열의 가장 마지막 두 자리 추출

> 결과
```python
  17
```

</details>

<br>

---

<br>

section03 파생변수, 정렬, 인덱싱
---
### 문제
1. 결측치가 있는 데이터(행)을 제거하시오.

2. 'views' 컬럼을 'f1' 컬럼으로 나눈 값을 새로운 컬럼으로 추가하시오.

3. 새로운 컬럼 값 중 가장 큰 값을 가진 행의 age를 정수로 구하시오.

<br>

```python
  improt pandas as pd
  df = pd.read_csv('./data/type1_data1.csv')
```

<details>
  <summary>df 확인</summary>

<br>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  dropna(), sort_values(), iloc[]
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 결측치 제거
  df =df.dropna()
  df
```
- 데이터프레임에서 결측치가 있는 데이터를 제거하기 위해서 dropna() 활용

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>id06</td>
      <td>22.0</td>
      <td>서울</td>
      <td>57.0</td>
      <td>0</td>
      <td>vip</td>
      <td>INTP</td>
      <td>20.129444</td>
      <td>2024-09-12</td>
      <td>21550.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>id08</td>
      <td>38.0</td>
      <td>서울</td>
      <td>101.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFJ</td>
      <td>83.685380</td>
      <td>2024-03-06</td>
      <td>3260.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>id10</td>
      <td>95.0</td>
      <td>서울</td>
      <td>74.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>98.429899</td>
      <td>2024-04-03</td>
      <td>9992.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>id100</td>
      <td>47.0</td>
      <td>경기</td>
      <td>53.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ESFP</td>
      <td>33.308999</td>
      <td>2024-02-21</td>
      <td>15535.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>70 rows × 10 columns</p>
</div>

<br>

> 코드
```python
  # 검증
  df.isnull().sum()
```
- dropna()가 잘 적용되었는지 확인하기 위해 df.isnull().sum() 으로 검증

> 결과
```
  id            0
  age           0
  city          0
  f1            0
  f2            0
  f3            0
  f4            0
  f5            0
  subscribed    0
  views         0
  dtype: int64
```

<br>

> 코드
```python
  # 새로운 컬럼 계산
  df['new'] = df['views']/df['f1']
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
      <th>new</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
      <td>119.868852</td>
    </tr>
    <tr>
      <th>5</th>
      <td>id06</td>
      <td>22.0</td>
      <td>서울</td>
      <td>57.0</td>
      <td>0</td>
      <td>vip</td>
      <td>INTP</td>
      <td>20.129444</td>
      <td>2024-09-12</td>
      <td>21550.0</td>
      <td>378.070175</td>
    </tr>
    <tr>
      <th>7</th>
      <td>id08</td>
      <td>38.0</td>
      <td>서울</td>
      <td>101.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFJ</td>
      <td>83.685380</td>
      <td>2024-03-06</td>
      <td>3260.0</td>
      <td>32.277228</td>
    </tr>
    <tr>
      <th>9</th>
      <td>id10</td>
      <td>95.0</td>
      <td>서울</td>
      <td>74.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>98.429899</td>
      <td>2024-04-03</td>
      <td>9992.0</td>
      <td>135.027027</td>
    </tr>
    <tr>
      <th>10</th>
      <td>id100</td>
      <td>47.0</td>
      <td>경기</td>
      <td>53.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ESFP</td>
      <td>33.308999</td>
      <td>2024-02-21</td>
      <td>15535.0</td>
      <td>293.113208</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
      <td>423.782609</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
      <td>86.584615</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
      <td>105.583333</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
      <td>100.661538</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
      <td>25.063830</td>
    </tr>
  </tbody>
</table>
<p>70 rows × 11 columns</p>
</div>

<br>

> 코드
```python
  # 내림차순 정렬
  df = df.sort_values('new', ascending = False)
  df
```
- df['new'] 중 가장 큰 값의 age 를 찾기 위해 new 컬럼 기준으로 내림차순(ascending = False) 정렬

  - sort_values() 기본값은 오름차순

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
      <th>new</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
      <td>423.782609</td>
    </tr>
    <tr>
      <th>83</th>
      <td>id83</td>
      <td>73.0</td>
      <td>경기</td>
      <td>50.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>80.138280</td>
      <td>2024-09-26</td>
      <td>19139.0</td>
      <td>382.780000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>id06</td>
      <td>22.0</td>
      <td>서울</td>
      <td>57.0</td>
      <td>0</td>
      <td>vip</td>
      <td>INTP</td>
      <td>20.129444</td>
      <td>2024-09-12</td>
      <td>21550.0</td>
      <td>378.070175</td>
    </tr>
    <tr>
      <th>105</th>
      <td>id104</td>
      <td>21.0</td>
      <td>서울</td>
      <td>13.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>4556.0</td>
      <td>350.461538</td>
    </tr>
    <tr>
      <th>106</th>
      <td>id105</td>
      <td>21.0</td>
      <td>경기</td>
      <td>24.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>7654.0</td>
      <td>318.916667</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>109</th>
      <td>id108</td>
      <td>21.0</td>
      <td>서울</td>
      <td>54.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ESTJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2178.0</td>
      <td>40.333333</td>
    </tr>
    <tr>
      <th>57</th>
      <td>id57</td>
      <td>3.0</td>
      <td>대구</td>
      <td>111.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-01-12</td>
      <td>4421.0</td>
      <td>39.828829</td>
    </tr>
    <tr>
      <th>7</th>
      <td>id08</td>
      <td>38.0</td>
      <td>서울</td>
      <td>101.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFJ</td>
      <td>83.685380</td>
      <td>2024-03-06</td>
      <td>3260.0</td>
      <td>32.277228</td>
    </tr>
    <tr>
      <th>108</th>
      <td>id107</td>
      <td>21.0</td>
      <td>부산</td>
      <td>76.0</td>
      <td>1</td>
      <td>silver</td>
      <td>ESTJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2346.0</td>
      <td>30.868421</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
      <td>25.063830</td>
    </tr>
  </tbody>
</table>
<p>70 rows × 11 columns</p>
</div>

<br>

> 코드
```python
  # age 값 찾아서 출력
  int(df.iloc[0, 1])
```
- 첫 번째 데이터(행)의 age를 iloc 또는 loc를 활용해 출력

  - iloc[행, 열]

> 결과
```python
  22
```

</details>

<br>

---

<br>

section04 값 변경, 정렬, 합계
---
### 문제
1. 'views' 컬럼의 결측 데이터를 0으로 대체하시오. 

2. 'views' 컬럼에서 상위 10번째 값을 구하시오.

3. 'views' 컬럼에서 상위 10개의 값을 상위 10번째 값으로 대체하시오.

4. 'views' 컬럼의 전체 합을 정수로 구하시오.

<br>

```python
  improt pandas as pd
  df = pd.read_csv('./data/')
```

<details>
  <summary>df 확인</summary>

<br>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  fillna(), sort_values(), iloc[], sum()
```

<br>

<details>
  <summary>풀이1</summary>

<br>

> 코드
```python
  # 결측 데이터를 0으로 대체
  df['views'].fillna(0, inplace = True)
  df
```
- fillna()를 활용해 결측치를 0으로 대체

- inplace = True : 기존 데이터프레임을 변경하겠다는 뜻

  - 새로운 객체를 생성하지 않고, 바로 df 에 적용

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

<br>

> 코드
```python
  # 내림차순 정렬, 상위 10번째 값 확인
  df = df.sort_values('views', ascending = False)
  df.head(10)
```
- views 를 기준으로 내림차순 정렬

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>id06</td>
      <td>22.0</td>
      <td>서울</td>
      <td>57.0</td>
      <td>0</td>
      <td>vip</td>
      <td>INTP</td>
      <td>20.129444</td>
      <td>2024-09-12</td>
      <td>21550.0</td>
    </tr>
    <tr>
      <th>56</th>
      <td>id56</td>
      <td>59.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>1</td>
      <td>vip</td>
      <td>ESTJ</td>
      <td>73.586397</td>
      <td>2024-04-05</td>
      <td>19589.0</td>
    </tr>
    <tr>
      <th>83</th>
      <td>id83</td>
      <td>73.0</td>
      <td>경기</td>
      <td>50.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>80.138280</td>
      <td>2024-09-26</td>
      <td>19139.0</td>
    </tr>
    <tr>
      <th>32</th>
      <td>id32</td>
      <td>25.0</td>
      <td>부산</td>
      <td>64.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ISFJ</td>
      <td>13.049921</td>
      <td>2024-05-24</td>
      <td>17421.0</td>
    </tr>
    <tr>
      <th>100</th>
      <td>id100</td>
      <td>47.0</td>
      <td>경기</td>
      <td>53.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ESFP</td>
      <td>33.308999</td>
      <td>2024-02-21</td>
      <td>15535.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>id100</td>
      <td>47.0</td>
      <td>경기</td>
      <td>53.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ESFP</td>
      <td>33.308999</td>
      <td>2024-02-21</td>
      <td>15535.0</td>
    </tr>
    <tr>
      <th>104</th>
      <td>id103</td>
      <td>21.0</td>
      <td>부산</td>
      <td>53.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ISFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>13543.0</td>
    </tr>
    <tr>
      <th>114</th>
      <td>id113</td>
      <td>22.0</td>
      <td>경기</td>
      <td>34.0</td>
      <td>2</td>
      <td>silver</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>10346.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>id10</td>
      <td>95.0</td>
      <td>서울</td>
      <td>74.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>98.429899</td>
      <td>2024-04-03</td>
      <td>9992.0</td>
    </tr>
    <tr>
      <th>113</th>
      <td>id112</td>
      <td>22.0</td>
      <td>서울</td>
      <td>45.0</td>
      <td>2</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9877.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  # views 상위 10개 데이터에 상위 10번째 값(최소값) 대입
  views_min = df.iloc[:10]['views'].min()
  df.iloc[:10, -1] = views_min
  df['views'].head(10)
```
- 상위 10개의 데이터 값을 변경하기 위해 iloc 활용

- df의 상위 10개의 행을 선택하고, 그 중 'views' 열에서 최소값(상위 10번째 값)을 추출

  - 변경할 범위는 iloc[행 인덱스 범위, 컬럼 인덱스]로 지정
 
    - iloc[:10] : 인덱스 0에서 9까지(상위 10개의 행)를 선택
   
  - 선택된 상위 10개 행의 'views' 열에서 최소값을 찾아 views_min 변수에 저장
 
- df 데이터프레임의 상위 10개의 행과 마지막 열을 선택한 뒤, 그 값을 views_min으로 설정

  - iloc[:10, -1] : 상위 10개의 행과 마지막 열을 의미(-1은 마지막 컬럼 의미)

    - 이 위치에 있는 값을 모두 views_min 으로 변경

> 결과
```
  5      9877.0
  56     9877.0
  83     9877.0
  32     9877.0
  100    9877.0
  10     9877.0
  104    9877.0
  114    9877.0
  9      9877.0
  113    9877.0
  Name: views, dtype: float64
```

<br>

> 코드
```python
  int(df['views'].sum())
```

> 결과
```
  652812
```

</details>

<br>

<details>
  <summary>풀이2</summary>

<br>

> 코드
```python
  # 결측 데이터를 0으로 대체
  df['views'].fillna(0, inplace = True)
  df['views'].isna().sum()
```

> 결과
```
  0
```

<br>

> 코드
```python
  # views 컬럼에서 10번째로 큰 값 구하기
  value = df['views'].nlargest(10).iloc[-1]
  value
```
- nlargest() : 시리즈에서 사용 가능한 함수(메소드)

  - 데이터를 정렬하지 않고도 큰 값을 빠르게 찾을 수 있음
 
- df['views'].nlargest(10) 으로 views 컬럼에서 가장 큰 값 10개가 큰 순으로 정령되어 반환

  - 가장 마지막 값(=10번째 값)을 iloc[-1] 로 선택

> 결과
```
  9877.0
```

<br>

> 코드
```python
  # views 컬럼에서 가장 큰 9개의 값을 10번째로 큰 값으로 대체
  df.loc[df['views'] > value, 'views'] = value
  df['views'].nlargest(10)
```
- loc[행, 열] 사용시 조건 대입 가능

  - df['views'] > value : 가장 큰 9개의 값을 10번째 큰 값으로 대체

> 결과
```
  5      9877.0
  9      9877.0
  10     9877.0
  32     9877.0
  56     9877.0
  83     9877.0
  100    9877.0
  104    9877.0
  113    9877.0
  114    9877.0
  Name: views, dtype: float64
```

<br>

> 코드
```python
  # views 컬럼의 합
  print(int(df['views'].sum()))
```

> 결과
```
  652812
```

</details>

<br>

---

<br>

section05 문자열 슬라이싱, 파생변수, 평균값
---
### 문제
1. 'f4' 컬럼 데이터에 'FJ' 가 포함된 데이터를 찾으시오.

2. 찾은 데이터 중에서 'f2' 컬럼의 평균값을 구하시오. (반올림 후 소수 둘째 자리까지 계산)

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/type1_data1.csv');
  df
```

<details>
  <summary>df 확인</summary>

<br>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  DataFrame['컬럼명'].str[범위], mean()
```

<br>

<details>
  <summary>풀이1</summary>

<br>

> 코드
```python
  # f4 컬럼에서 뒤의 2개 값 슬라이싱
  df['new'] = df['f4'].str[2:]
  df['new']
```
- 데이터프레임의 특정 값을 문자열 슬라이싱하기 위해서는 우선 문자열로 변경

- df['f4'].str[슬라이싱 범위] 로 문자열로 변경한 후 슬라이싱 범위 지정

> 결과
```
  0      FJ
  1      FJ
  2      TJ
  3      FP
  4      FJ
         ..
  115    TP
  116    TP
  117    FP
  118    FP
  119    FJ
  Name: new, Length: 120, dtype: object
```

<br>

> 코드
```python
  # FJ 데이터만 찾기
  cond = df['new'] == 'FJ'
  df = df[cond]
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
      <th>new</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>6</th>
      <td>id07</td>
      <td>36.3</td>
      <td>서울</td>
      <td>60.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>9.796378</td>
      <td>2024-01-11</td>
      <td>61.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>7</th>
      <td>id08</td>
      <td>38.0</td>
      <td>서울</td>
      <td>101.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFJ</td>
      <td>83.685380</td>
      <td>2024-03-06</td>
      <td>3260.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>8</th>
      <td>id09</td>
      <td>3.3</td>
      <td>서울</td>
      <td>35.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ESFJ</td>
      <td>17.252986</td>
      <td>2024-03-21</td>
      <td>2764.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>13</th>
      <td>id13</td>
      <td>15.0</td>
      <td>서울</td>
      <td>68.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFJ</td>
      <td>83.685380</td>
      <td>2024-12-30</td>
      <td>5643.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>18</th>
      <td>id18</td>
      <td>41.0</td>
      <td>서울</td>
      <td>87.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ISFJ</td>
      <td>80.138280</td>
      <td>2024-03-03</td>
      <td>7933.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>24</th>
      <td>id24</td>
      <td>80.0</td>
      <td>부산</td>
      <td>44.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INFJ</td>
      <td>73.586397</td>
      <td>2024-09-11</td>
      <td>5976.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>31</th>
      <td>id31</td>
      <td>86.0</td>
      <td>부산</td>
      <td>77.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFJ</td>
      <td>73.586397</td>
      <td>2024-02-11</td>
      <td>8014.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>32</th>
      <td>id32</td>
      <td>25.0</td>
      <td>부산</td>
      <td>64.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ISFJ</td>
      <td>13.049921</td>
      <td>2024-05-24</td>
      <td>17421.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>33</th>
      <td>id33</td>
      <td>47.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ENFJ</td>
      <td>17.252986</td>
      <td>2024-04-02</td>
      <td>3880.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>39</th>
      <td>id39</td>
      <td>56.0</td>
      <td>부산</td>
      <td>50.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>INFJ</td>
      <td>33.308999</td>
      <td>2024-12-22</td>
      <td>NaN</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>41</th>
      <td>id41</td>
      <td>81.0</td>
      <td>대구</td>
      <td>55.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>37.113739</td>
      <td>2024-10-04</td>
      <td>8640.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>45</th>
      <td>id45</td>
      <td>97.0</td>
      <td>대구</td>
      <td>88.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>13.049921</td>
      <td>2024-06-21</td>
      <td>8317.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>52</th>
      <td>id52</td>
      <td>97.0</td>
      <td>대구</td>
      <td>82.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISFJ</td>
      <td>90.496999</td>
      <td>2024-05-20</td>
      <td>8518.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>54</th>
      <td>id54</td>
      <td>53.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>1</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>69.730313</td>
      <td>2024-06-21</td>
      <td>5872.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>57</th>
      <td>id57</td>
      <td>3.0</td>
      <td>대구</td>
      <td>111.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-01-12</td>
      <td>4421.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>59</th>
      <td>id59</td>
      <td>64.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>1</td>
      <td>silver</td>
      <td>ESFJ</td>
      <td>20.129444</td>
      <td>2024-06-23</td>
      <td>4994.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>63</th>
      <td>id63</td>
      <td>88.0</td>
      <td>경기</td>
      <td>86.0</td>
      <td>1</td>
      <td>silver</td>
      <td>ISFJ</td>
      <td>73.586397</td>
      <td>2024-12-01</td>
      <td>4053.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>67</th>
      <td>id67</td>
      <td>66.0</td>
      <td>경기</td>
      <td>52.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>73.586397</td>
      <td>2024-06-17</td>
      <td>1159.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>73</th>
      <td>id73</td>
      <td>90.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>73.586397</td>
      <td>2024-08-12</td>
      <td>512.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>81</th>
      <td>id81</td>
      <td>86.0</td>
      <td>경기</td>
      <td>50.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>37.113739</td>
      <td>2024-09-14</td>
      <td>244.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>85</th>
      <td>id85</td>
      <td>83.6</td>
      <td>경기</td>
      <td>55.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INFJ</td>
      <td>80.138280</td>
      <td>2024-09-24</td>
      <td>6719.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>99</th>
      <td>id99</td>
      <td>1.0</td>
      <td>경기</td>
      <td>47.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFJ</td>
      <td>97.381034</td>
      <td>2024-12-02</td>
      <td>6090.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>105</th>
      <td>id104</td>
      <td>21.0</td>
      <td>서울</td>
      <td>13.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>4556.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>106</th>
      <td>id105</td>
      <td>21.0</td>
      <td>경기</td>
      <td>24.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>7654.0</td>
      <td>FJ</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
      <td>FJ</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  # f2 평균 구하기
  print(round(df['f2'].mean(), 2))
```
- 조건에 맞는 데이터를 찾고, mean() 함수로 평균 구하기

> 결과
```python
  0.61
```

</details>

<br>

<details>
  <summary>풀이2</summary>

<br>

> 코드
```python
  # FJ 인 데이터 찾기
  cond = df['f4'].str.contains('FJ')
  df = df[cond]
  df
```
- str.contains() 로 특정 문자 찾기 가능

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>id07</td>
      <td>36.3</td>
      <td>서울</td>
      <td>60.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>9.796378</td>
      <td>2024-01-11</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>id08</td>
      <td>38.0</td>
      <td>서울</td>
      <td>101.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFJ</td>
      <td>83.685380</td>
      <td>2024-03-06</td>
      <td>3260.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>id09</td>
      <td>3.3</td>
      <td>서울</td>
      <td>35.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ESFJ</td>
      <td>17.252986</td>
      <td>2024-03-21</td>
      <td>2764.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>id13</td>
      <td>15.0</td>
      <td>서울</td>
      <td>68.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFJ</td>
      <td>83.685380</td>
      <td>2024-12-30</td>
      <td>5643.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>id18</td>
      <td>41.0</td>
      <td>서울</td>
      <td>87.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ISFJ</td>
      <td>80.138280</td>
      <td>2024-03-03</td>
      <td>7933.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>id24</td>
      <td>80.0</td>
      <td>부산</td>
      <td>44.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INFJ</td>
      <td>73.586397</td>
      <td>2024-09-11</td>
      <td>5976.0</td>
    </tr>
    <tr>
      <th>31</th>
      <td>id31</td>
      <td>86.0</td>
      <td>부산</td>
      <td>77.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFJ</td>
      <td>73.586397</td>
      <td>2024-02-11</td>
      <td>8014.0</td>
    </tr>
    <tr>
      <th>32</th>
      <td>id32</td>
      <td>25.0</td>
      <td>부산</td>
      <td>64.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ISFJ</td>
      <td>13.049921</td>
      <td>2024-05-24</td>
      <td>17421.0</td>
    </tr>
    <tr>
      <th>33</th>
      <td>id33</td>
      <td>47.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ENFJ</td>
      <td>17.252986</td>
      <td>2024-04-02</td>
      <td>3880.0</td>
    </tr>
    <tr>
      <th>39</th>
      <td>id39</td>
      <td>56.0</td>
      <td>부산</td>
      <td>50.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>INFJ</td>
      <td>33.308999</td>
      <td>2024-12-22</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>41</th>
      <td>id41</td>
      <td>81.0</td>
      <td>대구</td>
      <td>55.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>37.113739</td>
      <td>2024-10-04</td>
      <td>8640.0</td>
    </tr>
    <tr>
      <th>45</th>
      <td>id45</td>
      <td>97.0</td>
      <td>대구</td>
      <td>88.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>13.049921</td>
      <td>2024-06-21</td>
      <td>8317.0</td>
    </tr>
    <tr>
      <th>52</th>
      <td>id52</td>
      <td>97.0</td>
      <td>대구</td>
      <td>82.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISFJ</td>
      <td>90.496999</td>
      <td>2024-05-20</td>
      <td>8518.0</td>
    </tr>
    <tr>
      <th>54</th>
      <td>id54</td>
      <td>53.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>1</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>69.730313</td>
      <td>2024-06-21</td>
      <td>5872.0</td>
    </tr>
    <tr>
      <th>57</th>
      <td>id57</td>
      <td>3.0</td>
      <td>대구</td>
      <td>111.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-01-12</td>
      <td>4421.0</td>
    </tr>
    <tr>
      <th>59</th>
      <td>id59</td>
      <td>64.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>1</td>
      <td>silver</td>
      <td>ESFJ</td>
      <td>20.129444</td>
      <td>2024-06-23</td>
      <td>4994.0</td>
    </tr>
    <tr>
      <th>63</th>
      <td>id63</td>
      <td>88.0</td>
      <td>경기</td>
      <td>86.0</td>
      <td>1</td>
      <td>silver</td>
      <td>ISFJ</td>
      <td>73.586397</td>
      <td>2024-12-01</td>
      <td>4053.0</td>
    </tr>
    <tr>
      <th>67</th>
      <td>id67</td>
      <td>66.0</td>
      <td>경기</td>
      <td>52.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>73.586397</td>
      <td>2024-06-17</td>
      <td>1159.0</td>
    </tr>
    <tr>
      <th>73</th>
      <td>id73</td>
      <td>90.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>73.586397</td>
      <td>2024-08-12</td>
      <td>512.0</td>
    </tr>
    <tr>
      <th>81</th>
      <td>id81</td>
      <td>86.0</td>
      <td>경기</td>
      <td>50.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>37.113739</td>
      <td>2024-09-14</td>
      <td>244.0</td>
    </tr>
    <tr>
      <th>85</th>
      <td>id85</td>
      <td>83.6</td>
      <td>경기</td>
      <td>55.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INFJ</td>
      <td>80.138280</td>
      <td>2024-09-24</td>
      <td>6719.0</td>
    </tr>
    <tr>
      <th>99</th>
      <td>id99</td>
      <td>1.0</td>
      <td>경기</td>
      <td>47.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFJ</td>
      <td>97.381034</td>
      <td>2024-12-02</td>
      <td>6090.0</td>
    </tr>
    <tr>
      <th>105</th>
      <td>id104</td>
      <td>21.0</td>
      <td>서울</td>
      <td>13.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>4556.0</td>
    </tr>
    <tr>
      <th>106</th>
      <td>id105</td>
      <td>21.0</td>
      <td>경기</td>
      <td>24.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>7654.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  # f2 평균 구하기
  print(round(df['f2'].mean(), 2))
```

> 결과
```
  0.61
```

</details>

<br>

---

<br>

section06 필터링, 분산
---
### 문제
1. 'f3' 컬럼이 gold 이면서 'f2' 컬럼이 2인 데이터를 찾으시오.

2. 찾은 데이터에서 'f1' 컬럼의 분산을 구하시오. (반올림 후 소수 둘째 자리까지 계산)

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/type1_data1.csv')
  df
```

<details>
  <summary>df 확인</summary>

<br>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  var(), round()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 조건에 맞는 데이터
  cond1 = df['f3'] == 'gold'
  cond2 = df['f2'] == 2
  df = df[cond1 & cond2]
  df
```
- 조건 2개 만들기 : f3 이 gold 면서 f2 가 2 인 데이터 필터링

  - 문자와 숫자로 동시에 조건을 만들 때 문자는 따옴표 필요, 숫자는 따옴표 필요 X

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>18</th>
      <td>id18</td>
      <td>41.0</td>
      <td>서울</td>
      <td>87.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ISFJ</td>
      <td>80.138280</td>
      <td>2024-03-03</td>
      <td>7933.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>id29</td>
      <td>-13.5</td>
      <td>부산</td>
      <td>47.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ENTP</td>
      <td>67.886373</td>
      <td>2024-08-28</td>
      <td>6793.0</td>
    </tr>
    <tr>
      <th>42</th>
      <td>id42</td>
      <td>65.0</td>
      <td>대구</td>
      <td>48.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ESTP</td>
      <td>33.308999</td>
      <td>2024-02-09</td>
      <td>5999.0</td>
    </tr>
    <tr>
      <th>55</th>
      <td>id55</td>
      <td>75.0</td>
      <td>대구</td>
      <td>63.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ENTP</td>
      <td>13.049921</td>
      <td>2024-02-06</td>
      <td>6042.0</td>
    </tr>
    <tr>
      <th>64</th>
      <td>id64</td>
      <td>43.0</td>
      <td>경기</td>
      <td>62.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ESFP</td>
      <td>73.586397</td>
      <td>2024-02-22</td>
      <td>5995.0</td>
    </tr>
    <tr>
      <th>68</th>
      <td>id68</td>
      <td>35.0</td>
      <td>경기</td>
      <td>45.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>67.886373</td>
      <td>2024-07-29</td>
      <td>8599.0</td>
    </tr>
    <tr>
      <th>71</th>
      <td>id71</td>
      <td>35.0</td>
      <td>경기</td>
      <td>84.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>52.667078</td>
      <td>2024-07-15</td>
      <td>8087.0</td>
    </tr>
    <tr>
      <th>101</th>
      <td>id68</td>
      <td>35.0</td>
      <td>경기</td>
      <td>45.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>67.886373</td>
      <td>2024-07-29</td>
      <td>8599.0</td>
    </tr>
    <tr>
      <th>112</th>
      <td>id111</td>
      <td>22.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>7894.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  # 분산
  result = df['f1'].var()
  
  # 출력
  round(result, 2)
```
- var() 로 f1 컬럼의 분산을 구하고 출력

> 결과
```python
  235.43
```

</details>

<br>

---

<br>

section07 값 변경(연산), 필터링 절댓값
---
### 문제
1. 모든 나이(age)에 1을 더하시오.

2. 20대의 'views' 평균과 30대의 'views' 평균의 절댓값 차이를 구하시오. (반올림 후 소수 둘째 자리까지 계산)

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/type1_data1.csv')
  df
```

<details>
  <summary>df 확인</summary>

<br>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  abs(), mean()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 나이 + 1
  df['age'] = df['age'] + 1
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>3.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>10.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>28.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>76.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>25.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>23.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>24.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>24.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>24.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>25.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

<br>

> 코드
```python
  # 나이 + 1
  df['age'] = df['age'] + 1
  df
```
- 판다스에서 df['age'] + 1 로 해달 컬럼의 모든 데이터에 연산 가능

> 결과
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>3.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>10.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>28.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>76.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>25.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>23.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>24.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>24.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>24.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>25.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

<br>

> 코드
```python
  # 20대 조건
  cond1 = (df['age'] >= 20) & (df['age'] < 30)
  df[cond1]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>28.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>25.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>id06</td>
      <td>23.0</td>
      <td>서울</td>
      <td>57.0</td>
      <td>0</td>
      <td>vip</td>
      <td>INTP</td>
      <td>20.129444</td>
      <td>2024-09-12</td>
      <td>21550.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>id12</td>
      <td>21.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>ESTP</td>
      <td>91.297791</td>
      <td>2024-11-30</td>
      <td>1367.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>id15</td>
      <td>23.0</td>
      <td>서울</td>
      <td>67.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ENTP</td>
      <td>9.796378</td>
      <td>2024-05-26</td>
      <td>7676.0</td>
    </tr>
    <tr>
      <th>32</th>
      <td>id32</td>
      <td>26.0</td>
      <td>부산</td>
      <td>64.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ISFJ</td>
      <td>13.049921</td>
      <td>2024-05-24</td>
      <td>17421.0</td>
    </tr>
    <tr>
      <th>43</th>
      <td>id43</td>
      <td>24.0</td>
      <td>대구</td>
      <td>60.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ISTP</td>
      <td>29.269869</td>
      <td>2024-05-18</td>
      <td>3878.0</td>
    </tr>
    <tr>
      <th>65</th>
      <td>id65</td>
      <td>27.5</td>
      <td>경기</td>
      <td>NaN</td>
      <td>0</td>
      <td>silver</td>
      <td>ISFP</td>
      <td>91.297791</td>
      <td>2024-01-10</td>
      <td>3336.0</td>
    </tr>
    <tr>
      <th>87</th>
      <td>id87</td>
      <td>20.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>1</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>97.381034</td>
      <td>2024-08-30</td>
      <td>6516.0</td>
    </tr>
    <tr>
      <th>93</th>
      <td>id93</td>
      <td>22.8</td>
      <td>경기</td>
      <td>57.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>ISFP</td>
      <td>73.586397</td>
      <td>2024-06-07</td>
      <td>42.0</td>
    </tr>
    <tr>
      <th>104</th>
      <td>id103</td>
      <td>22.0</td>
      <td>부산</td>
      <td>53.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ISFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>13543.0</td>
    </tr>
    <tr>
      <th>105</th>
      <td>id104</td>
      <td>22.0</td>
      <td>서울</td>
      <td>13.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>4556.0</td>
    </tr>
    <tr>
      <th>106</th>
      <td>id105</td>
      <td>22.0</td>
      <td>경기</td>
      <td>24.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>7654.0</td>
    </tr>
    <tr>
      <th>107</th>
      <td>id106</td>
      <td>22.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>4212.0</td>
    </tr>
    <tr>
      <th>108</th>
      <td>id107</td>
      <td>22.0</td>
      <td>부산</td>
      <td>76.0</td>
      <td>1</td>
      <td>silver</td>
      <td>ESTJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2346.0</td>
    </tr>
    <tr>
      <th>109</th>
      <td>id108</td>
      <td>22.0</td>
      <td>서울</td>
      <td>54.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ESTJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2178.0</td>
    </tr>
    <tr>
      <th>110</th>
      <td>id109</td>
      <td>22.0</td>
      <td>경기</td>
      <td>78.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESTJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6790.0</td>
    </tr>
    <tr>
      <th>111</th>
      <td>id110</td>
      <td>23.0</td>
      <td>대구</td>
      <td>45.0</td>
      <td>2</td>
      <td>silver</td>
      <td>ESTJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2112.0</td>
    </tr>
    <tr>
      <th>112</th>
      <td>id111</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>7894.0</td>
    </tr>
    <tr>
      <th>113</th>
      <td>id112</td>
      <td>23.0</td>
      <td>서울</td>
      <td>45.0</td>
      <td>2</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9877.0</td>
    </tr>
    <tr>
      <th>114</th>
      <td>id113</td>
      <td>23.0</td>
      <td>경기</td>
      <td>34.0</td>
      <td>2</td>
      <td>silver</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>10346.0</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>23.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>24.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>24.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>24.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>25.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  # 20대 views
  result20 = abs(df[cond1]['views'].mean())
  result20
```
- 절대값 게산을 위해서 abs() 함수 활용

> 결과
```python
  6441.7307692307695
```

<br>

> 코드
```python
  # 30대 조건
  cond2 = (df['age'] >= 30) & (df['age'] < 40)
  df[cond2]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>id07</td>
      <td>37.3</td>
      <td>서울</td>
      <td>60.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>9.796378</td>
      <td>2024-01-11</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>id08</td>
      <td>39.0</td>
      <td>서울</td>
      <td>101.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFJ</td>
      <td>83.685380</td>
      <td>2024-03-06</td>
      <td>3260.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>id23</td>
      <td>35.0</td>
      <td>부산</td>
      <td>75.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTP</td>
      <td>69.730313</td>
      <td>2024-05-21</td>
      <td>6236.0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>id25</td>
      <td>35.0</td>
      <td>부산</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ESTP</td>
      <td>60.339826</td>
      <td>2024-07-12</td>
      <td>8954.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>id27</td>
      <td>38.0</td>
      <td>부산</td>
      <td>60.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ESTP</td>
      <td>73.586397</td>
      <td>2024-10-13</td>
      <td>4255.0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>id28</td>
      <td>39.0</td>
      <td>부산</td>
      <td>34.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ENTP</td>
      <td>80.138280</td>
      <td>2024-10-31</td>
      <td>5068.0</td>
    </tr>
    <tr>
      <th>35</th>
      <td>id35</td>
      <td>31.0</td>
      <td>부산</td>
      <td>NaN</td>
      <td>2</td>
      <td>silver</td>
      <td>ESTJ</td>
      <td>33.308999</td>
      <td>2024-06-10</td>
      <td>3084.0</td>
    </tr>
    <tr>
      <th>47</th>
      <td>id47</td>
      <td>35.6</td>
      <td>대구</td>
      <td>75.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ESTJ</td>
      <td>90.496999</td>
      <td>2024-05-28</td>
      <td>8628.0</td>
    </tr>
    <tr>
      <th>51</th>
      <td>id51</td>
      <td>37.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>83.685380</td>
      <td>2024-08-20</td>
      <td>7217.0</td>
    </tr>
    <tr>
      <th>68</th>
      <td>id68</td>
      <td>36.0</td>
      <td>경기</td>
      <td>45.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>67.886373</td>
      <td>2024-07-29</td>
      <td>8599.0</td>
    </tr>
    <tr>
      <th>71</th>
      <td>id71</td>
      <td>36.0</td>
      <td>경기</td>
      <td>84.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>52.667078</td>
      <td>2024-07-15</td>
      <td>8087.0</td>
    </tr>
    <tr>
      <th>79</th>
      <td>id79</td>
      <td>31.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>INTJ</td>
      <td>80.138280</td>
      <td>2024-08-14</td>
      <td>8777.0</td>
    </tr>
    <tr>
      <th>89</th>
      <td>id89</td>
      <td>35.0</td>
      <td>경기</td>
      <td>66.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ENTJ</td>
      <td>33.308999</td>
      <td>2024-10-14</td>
      <td>6119.0</td>
    </tr>
    <tr>
      <th>101</th>
      <td>id68</td>
      <td>36.0</td>
      <td>경기</td>
      <td>45.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>67.886373</td>
      <td>2024-07-29</td>
      <td>8599.0</td>
    </tr>
    <tr>
      <th>102</th>
      <td>id101</td>
      <td>37.0</td>
      <td>경기</td>
      <td>65.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ISFP</td>
      <td>0.000000</td>
      <td>2025-01-29</td>
      <td>5735.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  # 30대 view
  result30 = abs(df[cond2]['views'].mean())
  result30
```
- 절대값 게산을 위해서 abs() 함수 활용

> 결과
```python
  6178.6
```

<br>

> 코드
```python
  # 20대 views 와 30대 views 절댓값 차이
  result = result20 - result30
  print(round(result, 2))
```

> 결과
```python
  263.13
```

<br>

---

<br>

section08 시계열 데이터, 필터링, 데이터 개수
---
### 문제
1. 'subscribed' 컬럼이 2024년 2월인 데이터를 찾으시오.

2. 위에서 찾은 데이터 중 'f3' 컬럼이 gold 인 데이터의 개수를 구하시오.

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/type1_data1.csv')
  df
```

<details>
  <summary>df 확인</summary>

<br>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  to_datetime(), dt.year(), dt.month(), len()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 자료형 변환
  df['subscribed'] = pd.to_datetime(df['subscribed'])
  df['subscribed']
```
- object 자료형을 datetime 자료형으로 변경

  - pd.to_datetime() 활용

> 결과
```
  0     2024-07-16
  1     2024-05-12
  2     2024-03-16
  3     2024-07-21
  4     2024-03-07
           ...    
  115   2025-02-17
  116   2025-02-17
  117   2025-02-17
  118   2025-02-17
  119   2025-02-17
  Name: subscribed, Length: 120, dtype: datetime64[ns]
```

<br>

> 코드
```python
  # 파생 변수 생성(연, 월)
  df['year'] = df['subscribed'].dt.year
  df['month'] = df['subscribed'].dt.month
  df
```
- 연, 월을 dt 활용하여 새로운 컬럼(파생변수) 생성

  - dt.year, dt.month, dt.day 는 괄호 X

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
      <th>year</th>
      <th>month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
      <td>2024</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
      <td>2024</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
      <td>2024</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
      <td>2024</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
      <td>2024</td>
      <td>3</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
      <td>2025</td>
      <td>2</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
      <td>2025</td>
      <td>2</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
      <td>2025</td>
      <td>2</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
      <td>2025</td>
      <td>2</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
      <td>2025</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 12 columns</p>
</div>

<br>

> 코드
```python
  # 2024년 2월이고, 'f3'이 gold 인 데이터
  cond1 = df['year']  == 2024
  cond2 = df['month']  == 2
  cond3 = df['f3'] == 'gold'
  df = df[cond1 & cond2 & cond3]
  df
```
- 여러 조건에 부합하는 데이터 선택

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
      <th>year</th>
      <th>month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>22</th>
      <td>id22</td>
      <td>-6.3</td>
      <td>부산</td>
      <td>72.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ENFP</td>
      <td>52.667078</td>
      <td>2024-02-09</td>
      <td>6147.0</td>
      <td>2024</td>
      <td>2</td>
    </tr>
    <tr>
      <th>31</th>
      <td>id31</td>
      <td>86.0</td>
      <td>부산</td>
      <td>77.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFJ</td>
      <td>73.586397</td>
      <td>2024-02-11</td>
      <td>8014.0</td>
      <td>2024</td>
      <td>2</td>
    </tr>
    <tr>
      <th>42</th>
      <td>id42</td>
      <td>65.0</td>
      <td>대구</td>
      <td>48.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ESTP</td>
      <td>33.308999</td>
      <td>2024-02-09</td>
      <td>5999.0</td>
      <td>2024</td>
      <td>2</td>
    </tr>
    <tr>
      <th>55</th>
      <td>id55</td>
      <td>75.0</td>
      <td>대구</td>
      <td>63.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ENTP</td>
      <td>13.049921</td>
      <td>2024-02-06</td>
      <td>6042.0</td>
      <td>2024</td>
      <td>2</td>
    </tr>
    <tr>
      <th>64</th>
      <td>id64</td>
      <td>43.0</td>
      <td>경기</td>
      <td>62.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ESFP</td>
      <td>73.586397</td>
      <td>2024-02-22</td>
      <td>5995.0</td>
      <td>2024</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  print(len(df))
```
- len() 함수로 데이터 개수 구하기

> 결과
```
   5
```

</details>

<br>

---

<br>

section09 필터링, 카테고리, 최빈값
---
### 문제
1. 'views' 컬럼 값이 1000 이하인 데이터(결측치 제외)를 찾으시오.

2. 앞에서 구한 데이터 중 'f4' 컬럼의 최빈값을 구하시오.

<br>

```python
  import pandas as pd 
  df = pd.read_csv('./data/type1_data1.csv')
  df
```

<details>
  <summary>df 확인</summary>

<br>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  value_counts(), index[]
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # views 수가 1000 이하
  cond = df['views'] <= 1000
  df = df[cond]
  df
```
- views 수가 1000 이하의 데이터 선택

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>id07</td>
      <td>36.3</td>
      <td>서울</td>
      <td>60.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>9.796378</td>
      <td>2024-01-11</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>30</th>
      <td>id30</td>
      <td>16.0</td>
      <td>부산</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>ESTJ</td>
      <td>17.252986</td>
      <td>2024-05-28</td>
      <td>240.0</td>
    </tr>
    <tr>
      <th>44</th>
      <td>id44</td>
      <td>44.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>INTP</td>
      <td>16.283854</td>
      <td>2024-11-10</td>
      <td>546.0</td>
    </tr>
    <tr>
      <th>61</th>
      <td>id61</td>
      <td>87.0</td>
      <td>경기</td>
      <td>62.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>INTP</td>
      <td>69.730313</td>
      <td>2024-02-03</td>
      <td>218.0</td>
    </tr>
    <tr>
      <th>72</th>
      <td>id72</td>
      <td>8.0</td>
      <td>경기</td>
      <td>97.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>ESTJ</td>
      <td>97.381034</td>
      <td>2024-01-30</td>
      <td>602.0</td>
    </tr>
    <tr>
      <th>73</th>
      <td>id73</td>
      <td>90.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>73.586397</td>
      <td>2024-08-12</td>
      <td>512.0</td>
    </tr>
    <tr>
      <th>81</th>
      <td>id81</td>
      <td>86.0</td>
      <td>경기</td>
      <td>50.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>37.113739</td>
      <td>2024-09-14</td>
      <td>244.0</td>
    </tr>
    <tr>
      <th>93</th>
      <td>id93</td>
      <td>21.8</td>
      <td>경기</td>
      <td>57.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>ISFP</td>
      <td>73.586397</td>
      <td>2024-06-07</td>
      <td>42.0</td>
    </tr>
    <tr>
      <th>98</th>
      <td>id98</td>
      <td>39.0</td>
      <td>경기</td>
      <td>58.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>98.429899</td>
      <td>2024-10-02</td>
      <td>865.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  # f4 컬럼 종류별 개수
  df = df['f4'].value_counts()
  df
```
- f4 컬럼의 종류별 개수를 value_counts() 활용해 구한 뒤 데이터프레임으로 만듦

  - df['f4'].value_counts() 를 데이터프레임으로 변경하면 f4 컬럼 데이터가 인덱스가 됨
 
  - value_counts() 는 기본적으로 내림차순 정렬되어 첫 번째 행이 최빈값

> 결과
```python
  f4
  ISFJ    3
  INFP    2
  ESTJ    2
  INTP    2
  ISFP    1
  Name: count, dtype: int64
```

<br>

> 코드
```python
  # f4 컬럼 최빈값
  print(df.index[0])
```
- 첫 번째 인덱스 출력

> 결과
```python
  ISFJ
```

</details>

<br>

<details>
  <summary>풀이2</summary>

<br>

> 코드
```python
  # views 수가 1000 이하
  cond = df['views'] <= 1000
  df = df[cond]
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>id07</td>
      <td>36.3</td>
      <td>서울</td>
      <td>60.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>9.796378</td>
      <td>2024-01-11</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>30</th>
      <td>id30</td>
      <td>16.0</td>
      <td>부산</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>ESTJ</td>
      <td>17.252986</td>
      <td>2024-05-28</td>
      <td>240.0</td>
    </tr>
    <tr>
      <th>44</th>
      <td>id44</td>
      <td>44.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>INTP</td>
      <td>16.283854</td>
      <td>2024-11-10</td>
      <td>546.0</td>
    </tr>
    <tr>
      <th>61</th>
      <td>id61</td>
      <td>87.0</td>
      <td>경기</td>
      <td>62.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>INTP</td>
      <td>69.730313</td>
      <td>2024-02-03</td>
      <td>218.0</td>
    </tr>
    <tr>
      <th>72</th>
      <td>id72</td>
      <td>8.0</td>
      <td>경기</td>
      <td>97.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>ESTJ</td>
      <td>97.381034</td>
      <td>2024-01-30</td>
      <td>602.0</td>
    </tr>
    <tr>
      <th>73</th>
      <td>id73</td>
      <td>90.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>73.586397</td>
      <td>2024-08-12</td>
      <td>512.0</td>
    </tr>
    <tr>
      <th>81</th>
      <td>id81</td>
      <td>86.0</td>
      <td>경기</td>
      <td>50.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>37.113739</td>
      <td>2024-09-14</td>
      <td>244.0</td>
    </tr>
    <tr>
      <th>93</th>
      <td>id93</td>
      <td>21.8</td>
      <td>경기</td>
      <td>57.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>ISFP</td>
      <td>73.586397</td>
      <td>2024-06-07</td>
      <td>42.0</td>
    </tr>
    <tr>
      <th>98</th>
      <td>id98</td>
      <td>39.0</td>
      <td>경기</td>
      <td>58.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>98.429899</td>
      <td>2024-10-02</td>
      <td>865.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  # f4 컬럼 최빈값
  print(df['f4'].mode()[0])
```
- 최빈값을 구하기 위해 mode() 활용

  - sum() 이나 mean() 과 달리, 시리즈(Series) 형태로 반환
 
  - mode() 뒤에 [0] 을 붙여 첫 번째 값 출력
 
- 최빈값은 여러 개일 수도 있음

  - 시험에서는 정답을 1개만 입력해야 하므로 최빈값이 2개일 가능성은 낮음

> 결과
```python 
   ISFJ
```

</details>

<br>

---

<br>

section10 그룹핑, 최댓값, 정렬
---
### 문제
1. 결측치가 있는 행을 삭제하시오.

2. 결측치가 삭제된 데이터를 사용하여 지역별(city) 평균을 계산하시오.

3. 앞에서 계산한 지역적 평균 데이터에서 'f2' 컬럼 값이 가장 큰 지역을 구하시오.

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/type1_data1.csv')
  df
```

<details>
  <summary>df 확인</summary>

<br>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  dropna(), groupby(), mean(), sort_values() or idxmax()
```

<br>

<details>
  <summary>풀이1</summary>

<br>

> 코드
```python
  # 결측치가 있는 행 삭제
  df.dropna(inplace=True)
  df
```
- 결측치가 있는 행을 dropna() 로 삭제

  - inplace=True : 해당 메서드가 원본 데이터프레임을 수정할지 여부를 결정

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>id06</td>
      <td>22.0</td>
      <td>서울</td>
      <td>57.0</td>
      <td>0</td>
      <td>vip</td>
      <td>INTP</td>
      <td>20.129444</td>
      <td>2024-09-12</td>
      <td>21550.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>id08</td>
      <td>38.0</td>
      <td>서울</td>
      <td>101.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFJ</td>
      <td>83.685380</td>
      <td>2024-03-06</td>
      <td>3260.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>id10</td>
      <td>95.0</td>
      <td>서울</td>
      <td>74.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>98.429899</td>
      <td>2024-04-03</td>
      <td>9992.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>id100</td>
      <td>47.0</td>
      <td>경기</td>
      <td>53.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ESFP</td>
      <td>33.308999</td>
      <td>2024-02-21</td>
      <td>15535.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>70 rows × 10 columns</p>
</div>

<br>

> 코드
```python
  # 지역별 평균 계산
  df = df.groupby(['city']).mean(numeric_only=True)    # 시험 환경은 mean() 사용
  df
```
- numeric_only=True : 데이터 프레임이나 시리즈에서 숫자 데이터에만 연산을 적용하도록 하는 설정

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>f1</th>
      <th>f2</th>
      <th>f5</th>
      <th>views</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>경기</th>
      <td>48.704000</td>
      <td>61.360000</td>
      <td>0.760000</td>
      <td>52.106731</td>
      <td>8127.880000</td>
    </tr>
    <tr>
      <th>대구</th>
      <td>49.773333</td>
      <td>66.200000</td>
      <td>0.666667</td>
      <td>27.370166</td>
      <td>6819.133333</td>
    </tr>
    <tr>
      <th>부산</th>
      <td>35.075000</td>
      <td>65.875000</td>
      <td>0.687500</td>
      <td>38.638715</td>
      <td>6945.437500</td>
    </tr>
    <tr>
      <th>서울</th>
      <td>38.000000</td>
      <td>60.142857</td>
      <td>0.785714</td>
      <td>41.122705</td>
      <td>7369.142857</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  # f2 컬럼이 가장 큰 지역 출력
  print(df.sort_values('f2', ascending=False).index[0])
```
- f2 컬럼이 가장 큰 지역을 구하기 위해 내림차순으로 정렬하고 인덱스 값 출력

> 결과
```python
  서울
```

</details>

<br>

<details>
  <summary>풀이2</summary>

<br>

> 코드
```python
  # 결측치가 있는 행 삭제
  df.dropna(inplace=True)
```

<br>

> 코드
```python
  # 지역별 평균 계산
  df = df.groupby(['city']).mean(numeric_only = True)  # 시험 환경은 mean() 사용
  df
```
- df.groupby() 활용시 컬럼이 1개면 groupby('city') 처럼 대괄호 없이 사용 가능

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>f1</th>
      <th>f2</th>
      <th>f5</th>
      <th>views</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>경기</th>
      <td>48.704000</td>
      <td>61.360000</td>
      <td>0.760000</td>
      <td>52.106731</td>
      <td>8127.880000</td>
    </tr>
    <tr>
      <th>대구</th>
      <td>49.773333</td>
      <td>66.200000</td>
      <td>0.666667</td>
      <td>27.370166</td>
      <td>6819.133333</td>
    </tr>
    <tr>
      <th>부산</th>
      <td>35.075000</td>
      <td>65.875000</td>
      <td>0.687500</td>
      <td>38.638715</td>
      <td>6945.437500</td>
    </tr>
    <tr>
      <th>서울</th>
      <td>38.000000</td>
      <td>60.142857</td>
      <td>0.785714</td>
      <td>41.122705</td>
      <td>7369.142857</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  # f2 컬럼이 가장 큰 지역 출력
  print(df['f2'].idxmax())
```
- df.sort_values('f2', ascending=False).index[0] 대신 df['f2'].idxmax() 활용해도 같은 결과 도출

  - idxmax() : 최댓값의 인덱스 반환
 
  - idxmin() : 최솟값의 인덱스 반환

> 결과
```python
   서울
```

</details>

<br>

---

<br>

section11 슬라이싱, 사분위수, 결측치 제거
---
### 문제
1. 데이터에서 결측치가 있는 데이터(행)을 모두 제거하시오.

2. 결측치가 제거된 데이터를 사용하여 앞에서부터 70% 데이터를 구하시오. (단, 데이터 70% 지점의 index 가 소수점으로 계산될 경우 소수점 이하는 버림)

3. 앞에서 구한 70% 데이터 중 'views' 컬럼의 3사분위수에서 1사분위수를 뺀 값을 정수로 구하시오.

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/type1_data1.csv')
  df
```

<details>
  <summary>df 확인</summary>

<br>

<div>
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  int(), dropna(), quantile()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 결측치가 있는 행 제거
  df.dropna(inplace=True)
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>id06</td>
      <td>22.0</td>
      <td>서울</td>
      <td>57.0</td>
      <td>0</td>
      <td>vip</td>
      <td>INTP</td>
      <td>20.129444</td>
      <td>2024-09-12</td>
      <td>21550.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>id08</td>
      <td>38.0</td>
      <td>서울</td>
      <td>101.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFJ</td>
      <td>83.685380</td>
      <td>2024-03-06</td>
      <td>3260.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>id10</td>
      <td>95.0</td>
      <td>서울</td>
      <td>74.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>98.429899</td>
      <td>2024-04-03</td>
      <td>9992.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>id100</td>
      <td>47.0</td>
      <td>경기</td>
      <td>53.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ESFP</td>
      <td>33.308999</td>
      <td>2024-02-21</td>
      <td>15535.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>70 rows × 10 columns</p>
</div>

<br>

> 코드
```python
  # 70% 지점
  end = int(len(df) * 0.7)
  end
```
- 앞에서부터 70% 데이터를 찾기 위해 70% index 지점 찾기

  - index 는 반드시 정수형이어야 하므로 int() 사용

> 결과
```python
  49
```

<br>

> 코드
```python
  # 70% 데이터 슬라이싱
  df = df.iloc[:end]
  df
```
- 70% 지점 인덱스까지 iloc() 활용하여 슬라이싱

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>id06</td>
      <td>22.0</td>
      <td>서울</td>
      <td>57.0</td>
      <td>0</td>
      <td>vip</td>
      <td>INTP</td>
      <td>20.129444</td>
      <td>2024-09-12</td>
      <td>21550.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>id08</td>
      <td>38.0</td>
      <td>서울</td>
      <td>101.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFJ</td>
      <td>83.685380</td>
      <td>2024-03-06</td>
      <td>3260.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>id10</td>
      <td>95.0</td>
      <td>서울</td>
      <td>74.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>98.429899</td>
      <td>2024-04-03</td>
      <td>9992.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>id100</td>
      <td>47.0</td>
      <td>경기</td>
      <td>53.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ESFP</td>
      <td>33.308999</td>
      <td>2024-02-21</td>
      <td>15535.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>id11</td>
      <td>40.0</td>
      <td>서울</td>
      <td>68.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFP</td>
      <td>98.429899</td>
      <td>2024-10-29</td>
      <td>6752.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>id13</td>
      <td>15.0</td>
      <td>서울</td>
      <td>68.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFJ</td>
      <td>83.685380</td>
      <td>2024-12-30</td>
      <td>5643.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>id14</td>
      <td>77.0</td>
      <td>서울</td>
      <td>50.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ENTJ</td>
      <td>67.886373</td>
      <td>2024-09-19</td>
      <td>5700.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>id15</td>
      <td>22.0</td>
      <td>서울</td>
      <td>67.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ENTP</td>
      <td>9.796378</td>
      <td>2024-05-26</td>
      <td>7676.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>id16</td>
      <td>68.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFP</td>
      <td>16.283854</td>
      <td>2024-07-25</td>
      <td>9472.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>id18</td>
      <td>41.0</td>
      <td>서울</td>
      <td>87.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ISFJ</td>
      <td>80.138280</td>
      <td>2024-03-03</td>
      <td>7933.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>id22</td>
      <td>-6.3</td>
      <td>부산</td>
      <td>72.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ENFP</td>
      <td>52.667078</td>
      <td>2024-02-09</td>
      <td>6147.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>id23</td>
      <td>34.0</td>
      <td>부산</td>
      <td>75.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTP</td>
      <td>69.730313</td>
      <td>2024-05-21</td>
      <td>6236.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>id24</td>
      <td>80.0</td>
      <td>부산</td>
      <td>44.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INFJ</td>
      <td>73.586397</td>
      <td>2024-09-11</td>
      <td>5976.0</td>
    </tr>
    <tr>
      <th>26</th>
      <td>id26</td>
      <td>55.0</td>
      <td>부산</td>
      <td>57.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ENFP</td>
      <td>83.685380</td>
      <td>2024-05-01</td>
      <td>5857.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>id27</td>
      <td>37.0</td>
      <td>부산</td>
      <td>60.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ESTP</td>
      <td>73.586397</td>
      <td>2024-10-13</td>
      <td>4255.0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>id28</td>
      <td>38.0</td>
      <td>부산</td>
      <td>34.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ENTP</td>
      <td>80.138280</td>
      <td>2024-10-31</td>
      <td>5068.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>id29</td>
      <td>-13.5</td>
      <td>부산</td>
      <td>47.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ENTP</td>
      <td>67.886373</td>
      <td>2024-08-28</td>
      <td>6793.0</td>
    </tr>
    <tr>
      <th>31</th>
      <td>id31</td>
      <td>86.0</td>
      <td>부산</td>
      <td>77.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFJ</td>
      <td>73.586397</td>
      <td>2024-02-11</td>
      <td>8014.0</td>
    </tr>
    <tr>
      <th>32</th>
      <td>id32</td>
      <td>25.0</td>
      <td>부산</td>
      <td>64.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ISFJ</td>
      <td>13.049921</td>
      <td>2024-05-24</td>
      <td>17421.0</td>
    </tr>
    <tr>
      <th>33</th>
      <td>id33</td>
      <td>47.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ENFJ</td>
      <td>17.252986</td>
      <td>2024-04-02</td>
      <td>3880.0</td>
    </tr>
    <tr>
      <th>36</th>
      <td>id36</td>
      <td>68.0</td>
      <td>부산</td>
      <td>77.0</td>
      <td>1</td>
      <td>gold</td>
      <td>INTP</td>
      <td>13.049921</td>
      <td>2024-07-20</td>
      <td>9713.0</td>
    </tr>
    <tr>
      <th>40</th>
      <td>id40</td>
      <td>56.0</td>
      <td>대구</td>
      <td>75.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFP</td>
      <td>17.252986</td>
      <td>2024-01-22</td>
      <td>8481.0</td>
    </tr>
    <tr>
      <th>41</th>
      <td>id41</td>
      <td>81.0</td>
      <td>대구</td>
      <td>55.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>37.113739</td>
      <td>2024-10-04</td>
      <td>8640.0</td>
    </tr>
    <tr>
      <th>42</th>
      <td>id42</td>
      <td>65.0</td>
      <td>대구</td>
      <td>48.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ESTP</td>
      <td>33.308999</td>
      <td>2024-02-09</td>
      <td>5999.0</td>
    </tr>
    <tr>
      <th>43</th>
      <td>id43</td>
      <td>23.0</td>
      <td>대구</td>
      <td>60.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ISTP</td>
      <td>29.269869</td>
      <td>2024-05-18</td>
      <td>3878.0</td>
    </tr>
    <tr>
      <th>45</th>
      <td>id45</td>
      <td>97.0</td>
      <td>대구</td>
      <td>88.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>13.049921</td>
      <td>2024-06-21</td>
      <td>8317.0</td>
    </tr>
    <tr>
      <th>47</th>
      <td>id47</td>
      <td>34.6</td>
      <td>대구</td>
      <td>75.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ESTJ</td>
      <td>90.496999</td>
      <td>2024-05-28</td>
      <td>8628.0</td>
    </tr>
    <tr>
      <th>49</th>
      <td>id49</td>
      <td>75.0</td>
      <td>대구</td>
      <td>88.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>37.113739</td>
      <td>2024-03-31</td>
      <td>9737.0</td>
    </tr>
    <tr>
      <th>52</th>
      <td>id52</td>
      <td>97.0</td>
      <td>대구</td>
      <td>82.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISFJ</td>
      <td>90.496999</td>
      <td>2024-05-20</td>
      <td>8518.0</td>
    </tr>
    <tr>
      <th>53</th>
      <td>id53</td>
      <td>52.0</td>
      <td>대구</td>
      <td>50.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESTP</td>
      <td>20.129444</td>
      <td>2024-09-09</td>
      <td>7012.0</td>
    </tr>
    <tr>
      <th>55</th>
      <td>id55</td>
      <td>75.0</td>
      <td>대구</td>
      <td>63.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ENTP</td>
      <td>13.049921</td>
      <td>2024-02-06</td>
      <td>6042.0</td>
    </tr>
    <tr>
      <th>57</th>
      <td>id57</td>
      <td>3.0</td>
      <td>대구</td>
      <td>111.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-01-12</td>
      <td>4421.0</td>
    </tr>
    <tr>
      <th>63</th>
      <td>id63</td>
      <td>88.0</td>
      <td>경기</td>
      <td>86.0</td>
      <td>1</td>
      <td>silver</td>
      <td>ISFJ</td>
      <td>73.586397</td>
      <td>2024-12-01</td>
      <td>4053.0</td>
    </tr>
    <tr>
      <th>64</th>
      <td>id64</td>
      <td>43.0</td>
      <td>경기</td>
      <td>62.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ESFP</td>
      <td>73.586397</td>
      <td>2024-02-22</td>
      <td>5995.0</td>
    </tr>
    <tr>
      <th>68</th>
      <td>id68</td>
      <td>35.0</td>
      <td>경기</td>
      <td>45.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>67.886373</td>
      <td>2024-07-29</td>
      <td>8599.0</td>
    </tr>
    <tr>
      <th>70</th>
      <td>id70</td>
      <td>-9.0</td>
      <td>경기</td>
      <td>96.0</td>
      <td>1</td>
      <td>silver</td>
      <td>ISTP</td>
      <td>48.431184</td>
      <td>2024-11-17</td>
      <td>4442.0</td>
    </tr>
    <tr>
      <th>71</th>
      <td>id71</td>
      <td>35.0</td>
      <td>경기</td>
      <td>84.0</td>
      <td>2</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>52.667078</td>
      <td>2024-07-15</td>
      <td>8087.0</td>
    </tr>
    <tr>
      <th>74</th>
      <td>id74</td>
      <td>45.0</td>
      <td>경기</td>
      <td>98.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESTP</td>
      <td>52.667078</td>
      <td>2024-05-27</td>
      <td>7739.0</td>
    </tr>
    <tr>
      <th>75</th>
      <td>id75</td>
      <td>63.0</td>
      <td>경기</td>
      <td>47.0</td>
      <td>0</td>
      <td>gold</td>
      <td>ESTP</td>
      <td>20.129444</td>
      <td>2024-06-12</td>
      <td>6779.0</td>
    </tr>
    <tr>
      <th>78</th>
      <td>id78</td>
      <td>92.0</td>
      <td>경기</td>
      <td>96.0</td>
      <td>1</td>
      <td>gold</td>
      <td>INTJ</td>
      <td>69.730313</td>
      <td>2024-10-27</td>
      <td>7565.0</td>
    </tr>
    <tr>
      <th>80</th>
      <td>id80</td>
      <td>67.0</td>
      <td>경기</td>
      <td>60.0</td>
      <td>0</td>
      <td>silver</td>
      <td>ISFP</td>
      <td>83.685380</td>
      <td>2024-01-14</td>
      <td>4381.0</td>
    </tr>
    <tr>
      <th>83</th>
      <td>id83</td>
      <td>73.0</td>
      <td>경기</td>
      <td>50.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>80.138280</td>
      <td>2024-09-26</td>
      <td>19139.0</td>
    </tr>
    <tr>
      <th>84</th>
      <td>id84</td>
      <td>66.0</td>
      <td>경기</td>
      <td>44.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>83.685380</td>
      <td>2024-12-19</td>
      <td>5650.0</td>
    </tr>
    <tr>
      <th>85</th>
      <td>id85</td>
      <td>83.6</td>
      <td>경기</td>
      <td>55.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INFJ</td>
      <td>80.138280</td>
      <td>2024-09-24</td>
      <td>6719.0</td>
    </tr>
    <tr>
      <th>89</th>
      <td>id89</td>
      <td>34.0</td>
      <td>경기</td>
      <td>66.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ENTJ</td>
      <td>33.308999</td>
      <td>2024-10-14</td>
      <td>6119.0</td>
    </tr>
    <tr>
      <th>91</th>
      <td>id91</td>
      <td>6.0</td>
      <td>경기</td>
      <td>72.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>9.796378</td>
      <td>2024-08-23</td>
      <td>8988.0</td>
    </tr>
    <tr>
      <th>92</th>
      <td>id92</td>
      <td>97.0</td>
      <td>경기</td>
      <td>78.0</td>
      <td>1</td>
      <td>gold</td>
      <td>INFP</td>
      <td>97.381034</td>
      <td>2024-05-08</td>
      <td>9625.0</td>
    </tr>
    <tr>
      <th>95</th>
      <td>id95</td>
      <td>77.0</td>
      <td>경기</td>
      <td>43.0</td>
      <td>1</td>
      <td>gold</td>
      <td>INTJ</td>
      <td>91.297791</td>
      <td>2024-05-21</td>
      <td>8697.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  # 3사분위수, 1사분위수
  q3 = df['views'].quantile(.75)
  q1 = df['views'].quantile(.25)
  print(q3)
  print(q1)
```
- quantile() : 데이터의 분위수를 계산하는 데 사용

  - 0.5 분위수는 중앙값(median), 0.25는 1사분위수(25%), 0.75는 3사분위수(75%)
 
> 결과
```python
  8628.0
  5857.0
```

<br>

> 코드
```python
  # 결과 출력
  print(int(q3 - q1))
```

> 결과
```python
   2771
```

<br>

#### 💡 
- 시험에서 quantile() 함수를 기억하지 못한다면 df['views'].describe() 를 활용해 25%, 75% 확인 가능

> 코드
```python
  df['views'].describe()
```

> 결과
```python
  count       49.000000
  mean      7804.795918
  std       3700.967328
  min       3260.000000
  25%       5857.000000
  50%       7012.000000
  75%       8628.000000
  max      21550.000000
  Name: views, dtype: float64
```

</details>

<br>

---

<br>

section12 결측치 처리, 최빈값, 데이터 개수
---
### 문제
1. 결측치가 가장 많은 두 컬럼을 찾으시오.

2. 첫 번째로 결측치가 많은 컬럼에서 결측치가 있는 데이터(행)을 삭제하시오.

3. 두 번째로 결측치가 많은 컬럼을 최빈값으로 대체하시오.

4. 'f3' 컬럼의 'gold' 값을 가진 데이터의 수를 정수형으로 구하시오.

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/type1_data1.csv')
  df
```

<details>
  <summary>df 확인</summary>

<br>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  dropna(), mode(), sum()
```

<br>

<details>
  <summary>풀이1</summary>

<br>

> 코드
```python
  # 결측치가 가장 많은 컬럼 확인
  df.isnull().sum()
```
- df.isnull().sum() 으로 결측치가 가장 많은 컬럼이 f1 임을 확인

> 결과
```python
  id             0
  age            0
  city           0
  f1            31
  f2             0
  f3            29
  f4             0
  f5             0
  subscribed     0
  views          4
  dtype: int64
```

<br>

> 코드
```python
  # 첫 번째로 결측치가 많은 컬럼에서 결측치가 있는 데이터 제거
  df = df.dropna(subset=['f1'])
  df
```
- df.dropna(subset=['f1']) 으로 결측치가 가장 많은 컬럼 제거

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>id06</td>
      <td>22.0</td>
      <td>서울</td>
      <td>57.0</td>
      <td>0</td>
      <td>vip</td>
      <td>INTP</td>
      <td>20.129444</td>
      <td>2024-09-12</td>
      <td>21550.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>id07</td>
      <td>36.3</td>
      <td>서울</td>
      <td>60.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>9.796378</td>
      <td>2024-01-11</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>89 rows × 10 columns</p>
</div>

<br>

> 코드
```python
  # 두 번째로 결측치가 많은 컬럼 최빈값 확인
  freq = df['f3'].mode()[0]
  freq
```
- mode()[0] 으로 최빈값 찾고, 두 번째로 결측치가 많은 컬럼 채우기

> 결과
```python
  'gold'
```

<br>

> 코드
```python
  # 최빈값 대체
  df['f3'].fillna(freq, inplace=True)
  df.isnull().sum()
```

> 결과
```python
  id            0
  age           0
  city          0
  f1            0
  f2            0
  f3            0
  f4            0
  f5            0
  subscribed    0
  views         2
  dtype: int64
```

<br>

> 코드
```python
  # f3 컬럼이 gold 인 데이터의 수
  print(sum(df['f3'] == 'gold'))
```
- df['f3'] == 'gold' 는 True(1) or False(0) 반환

- sum(조건) 은 True(1) 의 합

  - 조건에 부합하는 데이터 개수

> 결과
```python
  63
```

</details>

<br>

<details>
  <summary>풀이2</summary>

<br>

> 코드
```python
  # 결측치가 가장 많은 컬럼
  col = df.isnull().sum().idxmax()
  col
```

> 결과
```python
  'f1'
```
- df.isnull().sum() : 컬럼별 결측 수를 시리즈 형태로 반환

  - 인덱스는 컬럼명
 
- .idxmax() 활용해 결측 수가 가장 큰 값의 인덱스를 col 변수에 담기

<br>

> 코드
```python
  # 결측치가 가장 많은 컬럼 제거
  df = df.dropna(subset = [col])
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>id06</td>
      <td>22.0</td>
      <td>서울</td>
      <td>57.0</td>
      <td>0</td>
      <td>vip</td>
      <td>INTP</td>
      <td>20.129444</td>
      <td>2024-09-12</td>
      <td>21550.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>id07</td>
      <td>36.3</td>
      <td>서울</td>
      <td>60.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>9.796378</td>
      <td>2024-01-11</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>89 rows × 10 columns</p>
</div>

<br>

> 코드
```python
  # 두 번째로 결측치가 많은 컬럼 최빈값 확인
  freq = df['f3'].mode()[0]
  freq
```

> 결과
```python
  'gold'
```

<br>

> 코드
```python
  # 최빈값 대체
  df['f3'] = df['f3'].fillna(freq)
  df.isnull().sum()
```

> 결과
```python
  id            0
  age           0
  city          0
  f1            0
  f2            0
  f3            0
  f4            0
  f5            0
  subscribed    0
  views         2
  dtype: int64
```

<br>

> 코드
```python
  # f3 컬럼이 gold 인 데이터 수
  print(len(df[df['f3'] == 'gold']))
```
- 데이터 수를 구할 때 활용법

  - sum() 활용
 
  - len() 활용
 
- df['f3'] == 'gold'

  - 데이터프레임 df의 열 f3에서 값이 'gold'와 같은지 확인하는 조건 생성
  
  - True 또는 False 값을 포함하는 불리언 시리즈를 반환
 
- df[df['f3'] == 'gold']

  - 조건을 만족하는 행들을 필터링하여 새로운 데이터프레임 생성
 
  - df['f3'] 열의 값이 'gold'인 행들만 반환
 
- len()

  - 필터링된 데이터프레임의 행의 개수 계산
 
  - 'gold'라는 값을 가진 행이 몇 개인지 세는 것

> 결과
```python
  63
```

</details>

<br>

---

<br>

section13 결측 데이터 찾기, 필터링, 평균값
---
### 문제
1. 'f1' 컬럼에 결측치가 있는 데이터만 선택하시오.

2. 선택된 데이터에서 'age' 컬럼의 평균값을 구하시오. (반올림 후 소수 첫째 자리까지 계산)

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/type1_data1.csv')
  df
```

<details>
  <summary>df 확인</summary>

<br>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  isnull(), mean()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 결측치가 있는 데이터 True/False
  cond = df['f1'].isnull()
  cond
```
- 결측치가 있는 데이터를 찾기 위해 df['f1'].insull() 활용

  - NaN 이라면 True, 데이터가 있다면 False 반환

> 결과
```python
  0       True
  1      False
  2      False
  3       True
  4      False
         ...  
  115    False
  116    False
  117    False
  118    False
  119    False
  Name: f1, Length: 120, dtype: bool
```

<br>

> 코드
```python
  # 결측치가 있는 데이터 선택
  df = df[cond]
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>id12</td>
      <td>20.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>ESTP</td>
      <td>91.297791</td>
      <td>2024-11-30</td>
      <td>1367.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>id17</td>
      <td>74.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTP</td>
      <td>67.886373</td>
      <td>2024-10-26</td>
      <td>9441.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>id19</td>
      <td>53.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>83.685380</td>
      <td>2024-12-24</td>
      <td>5287.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>id21</td>
      <td>90.0</td>
      <td>부산</td>
      <td>NaN</td>
      <td>1</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>29.269869</td>
      <td>2024-05-03</td>
      <td>9690.0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>id25</td>
      <td>34.0</td>
      <td>부산</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ESTP</td>
      <td>60.339826</td>
      <td>2024-07-12</td>
      <td>8954.0</td>
    </tr>
    <tr>
      <th>30</th>
      <td>id30</td>
      <td>16.0</td>
      <td>부산</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>ESTJ</td>
      <td>17.252986</td>
      <td>2024-05-28</td>
      <td>240.0</td>
    </tr>
    <tr>
      <th>34</th>
      <td>id34</td>
      <td>65.0</td>
      <td>부산</td>
      <td>NaN</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>48.431184</td>
      <td>2024-02-01</td>
      <td>3163.0</td>
    </tr>
    <tr>
      <th>35</th>
      <td>id35</td>
      <td>30.0</td>
      <td>부산</td>
      <td>NaN</td>
      <td>2</td>
      <td>silver</td>
      <td>ESTJ</td>
      <td>33.308999</td>
      <td>2024-06-10</td>
      <td>3084.0</td>
    </tr>
    <tr>
      <th>37</th>
      <td>id37</td>
      <td>100.0</td>
      <td>부산</td>
      <td>NaN</td>
      <td>0</td>
      <td>silver</td>
      <td>ESTP</td>
      <td>33.308999</td>
      <td>2024-07-08</td>
      <td>4068.0</td>
    </tr>
    <tr>
      <th>38</th>
      <td>id38</td>
      <td>87.0</td>
      <td>부산</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>ESTP</td>
      <td>83.685380</td>
      <td>2024-06-21</td>
      <td>1048.0</td>
    </tr>
    <tr>
      <th>44</th>
      <td>id44</td>
      <td>44.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>INTP</td>
      <td>16.283854</td>
      <td>2024-11-10</td>
      <td>546.0</td>
    </tr>
    <tr>
      <th>46</th>
      <td>id46</td>
      <td>93.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ESTJ</td>
      <td>67.886373</td>
      <td>2024-05-23</td>
      <td>9711.0</td>
    </tr>
    <tr>
      <th>48</th>
      <td>id48</td>
      <td>18.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>ENFP</td>
      <td>20.129444</td>
      <td>2024-03-25</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>51</th>
      <td>id51</td>
      <td>36.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>83.685380</td>
      <td>2024-08-20</td>
      <td>7217.0</td>
    </tr>
    <tr>
      <th>54</th>
      <td>id54</td>
      <td>53.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>1</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>69.730313</td>
      <td>2024-06-21</td>
      <td>5872.0</td>
    </tr>
    <tr>
      <th>56</th>
      <td>id56</td>
      <td>59.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>1</td>
      <td>vip</td>
      <td>ESTJ</td>
      <td>73.586397</td>
      <td>2024-04-05</td>
      <td>19589.0</td>
    </tr>
    <tr>
      <th>59</th>
      <td>id59</td>
      <td>64.0</td>
      <td>대구</td>
      <td>NaN</td>
      <td>1</td>
      <td>silver</td>
      <td>ESFJ</td>
      <td>20.129444</td>
      <td>2024-06-23</td>
      <td>4994.0</td>
    </tr>
    <tr>
      <th>60</th>
      <td>id60</td>
      <td>56.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ESFP</td>
      <td>52.667078</td>
      <td>2024-11-24</td>
      <td>6794.0</td>
    </tr>
    <tr>
      <th>62</th>
      <td>id62</td>
      <td>52.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>INTP</td>
      <td>60.339826</td>
      <td>2024-04-10</td>
      <td>2100.0</td>
    </tr>
    <tr>
      <th>65</th>
      <td>id65</td>
      <td>26.5</td>
      <td>경기</td>
      <td>NaN</td>
      <td>0</td>
      <td>silver</td>
      <td>ISFP</td>
      <td>91.297791</td>
      <td>2024-01-10</td>
      <td>3336.0</td>
    </tr>
    <tr>
      <th>66</th>
      <td>id66</td>
      <td>87.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>1</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>17.252986</td>
      <td>2024-08-05</td>
      <td>8471.0</td>
    </tr>
    <tr>
      <th>73</th>
      <td>id73</td>
      <td>90.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>73.586397</td>
      <td>2024-08-12</td>
      <td>512.0</td>
    </tr>
    <tr>
      <th>79</th>
      <td>id79</td>
      <td>30.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>INTJ</td>
      <td>80.138280</td>
      <td>2024-08-14</td>
      <td>8777.0</td>
    </tr>
    <tr>
      <th>82</th>
      <td>id82</td>
      <td>48.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>ENTJ</td>
      <td>37.113739</td>
      <td>2024-10-17</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>86</th>
      <td>id86</td>
      <td>2.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>ESTP</td>
      <td>29.269869</td>
      <td>2024-02-16</td>
      <td>2155.0</td>
    </tr>
    <tr>
      <th>87</th>
      <td>id87</td>
      <td>19.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>1</td>
      <td>gold</td>
      <td>ISFP</td>
      <td>97.381034</td>
      <td>2024-08-30</td>
      <td>6516.0</td>
    </tr>
    <tr>
      <th>90</th>
      <td>id90</td>
      <td>54.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>0</td>
      <td>silver</td>
      <td>ENTP</td>
      <td>29.269869</td>
      <td>2024-04-03</td>
      <td>3818.0</td>
    </tr>
    <tr>
      <th>94</th>
      <td>id94</td>
      <td>84.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>1</td>
      <td>silver</td>
      <td>ESTJ</td>
      <td>90.496999</td>
      <td>2024-08-16</td>
      <td>3774.0</td>
    </tr>
    <tr>
      <th>97</th>
      <td>id97</td>
      <td>100.0</td>
      <td>경기</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>INFP</td>
      <td>67.886373</td>
      <td>2024-03-18</td>
      <td>6687.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  # age 평균값
  result = df['age'].mean()
  result
```
- f1 에 결측치가 있는 데이터를 선택하고, 그 데이터에서 age 의 평균값 계산

> 결과
```python
  53.596774193548384
```

<br>

> 코드
```python
  # 소수 첫째 자리까지 출력
  print(round(result, 1))
```

> 결과
```python
   53.6
```

</details>

<br>

---

<br>

section14 중복 데이터 제거, 값 변경, 데이터 개수
---
### 문제
1. 중복 데이터를 제거하시오.

2. 'f3' 컬럼의 결측치는 0, 'silver'는 1, 'gold'는 2, 'vip'는 3으로 변환하시오.

3. 변환된 'f3' 컬럼의 총합을 정수형으로 구하시오.

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/type1_data1.csv')
  df
```

<details>
  <summary>df 확인</summary>

<br>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  drop_duplicates(), replace(), map(), sum()
```

<br>

<details>
  <summary>풀이1</summary>

<br>

> 코드
```python
  # 중복 데이터 제거
  df.drop_duplicates(inplace = True)
  df
```
- drop_duplicates() : 중복 데이터를 제거하는 함수

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>118 rows × 10 columns</p>
</div>

<br>

> 코드
```python
  # 값 대체
  import numpy as np
  df['f3'] = df['f3'].replace(np.nan, 0).replace('silver', 1).replace('gold', 2).replace('vip', 3)
  df['f3']
```
- replace(변경 전, 변경 후)를 활용해 값 변경

- 딕셔너리와 map() 활용도 가능
```python
  dict_list = {np.nan : 0, 'silver' : 1, 'gold' : 2, 'vip' : 3}
  df['f3'] = df['f3'].map(dict_list)
```

> 결과
```python
  0      2
  1      0
  2      2
  3      0
  4      0
        ..
  115    2
  116    3
  117    1
  118    2
  119    3
  Name: f3, Length: 118, dtype: int64
```

<br>

> 코드
```python
  # f3 컬럼의 총합(정수형으로 출력)
  print(int(df['f3'].sum()))
```

> 결과
```python
  167
```

</details>

<br>

<details>
  <summary>풀이2</summary>

<br>

> 코드
```python
  # 계산
  r1 = sum(df['f3'] == 'silver') * 1
  r2 = sum(df['f3'] == 'gold') * 2
  r3 = sum(df['f3'] == 'vip') * 3
  print(r1 + r2 + r3)
```
- sum() 함수를 사용해 'silver', 'gold', 'vip' 를 각각 구하고, 문제에서 제시한 가중치를 곱한 후 모두 합하기

> 결과
```python
   167
```

</details>

<br>

---

<br>

section15 컬럼 삭제, 행 단위 합계, 필터링
---
### 문제
1. 주어진 데이터에서 문자 자료형 컬럼을 삭제하시오.

2. 숫자 자료형 컬럼의 결측치를 0으로 대체하시오.

3. 각 행의 합이 3000 보다 큰 값의 개수를 정수로 구하시오. (각 행의 합: 'age' + 'f1' + 'f2' + 'f5' + 'views')

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/type1_data1.csv')
  df
```

<details>
  <summary>df 확인</summary>

<br>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>age</th>
      <th>city</th>
      <th>f1</th>
      <th>f2</th>
      <th>f3</th>
      <th>f4</th>
      <th>f5</th>
      <th>subscribed</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id01</td>
      <td>2.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>0</td>
      <td>gold</td>
      <td>ENFJ</td>
      <td>91.297791</td>
      <td>2024-07-16</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id02</td>
      <td>9.0</td>
      <td>서울</td>
      <td>70.0</td>
      <td>1</td>
      <td>NaN</td>
      <td>ENFJ</td>
      <td>60.339826</td>
      <td>2024-05-12</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id03</td>
      <td>27.0</td>
      <td>서울</td>
      <td>61.0</td>
      <td>1</td>
      <td>gold</td>
      <td>ISTJ</td>
      <td>17.252986</td>
      <td>2024-03-16</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id04</td>
      <td>75.0</td>
      <td>서울</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>INFP</td>
      <td>52.667078</td>
      <td>2024-07-21</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id05</td>
      <td>24.0</td>
      <td>서울</td>
      <td>85.0</td>
      <td>2</td>
      <td>NaN</td>
      <td>ISFJ</td>
      <td>29.269869</td>
      <td>2024-03-07</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>id114</td>
      <td>22.0</td>
      <td>대구</td>
      <td>23.0</td>
      <td>0</td>
      <td>gold</td>
      <td>INTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>id115</td>
      <td>23.0</td>
      <td>부산</td>
      <td>65.0</td>
      <td>0</td>
      <td>vip</td>
      <td>ENTP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>id116</td>
      <td>23.0</td>
      <td>서울</td>
      <td>12.0</td>
      <td>1</td>
      <td>silver</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>id117</td>
      <td>23.0</td>
      <td>대구</td>
      <td>65.0</td>
      <td>2</td>
      <td>gold</td>
      <td>INFP</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>id118</td>
      <td>24.0</td>
      <td>부산</td>
      <td>94.0</td>
      <td>1</td>
      <td>vip</td>
      <td>ESFJ</td>
      <td>0.000000</td>
      <td>2025-02-17</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 10 columns</p>
</div>

</details>

<br>

### 힌트
```python
  select_dtypes, drop, fillna, DataFrame.T
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 자료형이 object 컬림 제외
  cols = df.select_dtypes(exclude = 'object').columns
  df = df[cols]
  df
```
- select_dtypes() : 데이터프레임에서 특정 데이터 타입을 기반으로 열을 선택하는 함수

- exclude='object' : 문자열 데이터 타입 제외, 숫자형이나 날짜형 등의 다른 타입들만 선택

- .columns : 데이터프레임의 열 이름들을 반환

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>f1</th>
      <th>f2</th>
      <th>f5</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2.0</td>
      <td>NaN</td>
      <td>0</td>
      <td>91.297791</td>
      <td>6820.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9.0</td>
      <td>70.0</td>
      <td>1</td>
      <td>60.339826</td>
      <td>2534.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>27.0</td>
      <td>61.0</td>
      <td>1</td>
      <td>17.252986</td>
      <td>7312.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>75.0</td>
      <td>NaN</td>
      <td>2</td>
      <td>52.667078</td>
      <td>493.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>24.0</td>
      <td>85.0</td>
      <td>2</td>
      <td>29.269869</td>
      <td>1338.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>115</th>
      <td>22.0</td>
      <td>23.0</td>
      <td>0</td>
      <td>0.000000</td>
      <td>9747.0</td>
    </tr>
    <tr>
      <th>116</th>
      <td>23.0</td>
      <td>65.0</td>
      <td>0</td>
      <td>0.000000</td>
      <td>5628.0</td>
    </tr>
    <tr>
      <th>117</th>
      <td>23.0</td>
      <td>12.0</td>
      <td>1</td>
      <td>0.000000</td>
      <td>1267.0</td>
    </tr>
    <tr>
      <th>118</th>
      <td>23.0</td>
      <td>65.0</td>
      <td>2</td>
      <td>0.000000</td>
      <td>6543.0</td>
    </tr>
    <tr>
      <th>119</th>
      <td>24.0</td>
      <td>94.0</td>
      <td>1</td>
      <td>0.000000</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 5 columns</p>
</div>

<br>

> 코드
```python
  # 결측치 0 대체
  df = df.fillna(0)
  df.isnull().sum()
```

> 결과
```python
  age      0
  f1       0
  f2       0
  f5       0
  views    0
  dtype: int64
```


<br>

> 코드
```python
# 행과 열 변경
df = df.T
df
```
- 행과 열 변경이 필요할 때는 DataFrame.T 활용

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>...</th>
      <th>110</th>
      <th>111</th>
      <th>112</th>
      <th>113</th>
      <th>114</th>
      <th>115</th>
      <th>116</th>
      <th>117</th>
      <th>118</th>
      <th>119</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>age</th>
      <td>2.000000</td>
      <td>9.000000</td>
      <td>27.000000</td>
      <td>75.000000</td>
      <td>24.000000</td>
      <td>22.000000</td>
      <td>36.300000</td>
      <td>38.00000</td>
      <td>3.300000</td>
      <td>95.000000</td>
      <td>...</td>
      <td>21.0</td>
      <td>22.0</td>
      <td>22.0</td>
      <td>22.0</td>
      <td>22.0</td>
      <td>22.0</td>
      <td>23.0</td>
      <td>23.0</td>
      <td>23.0</td>
      <td>24.0</td>
    </tr>
    <tr>
      <th>f1</th>
      <td>0.000000</td>
      <td>70.000000</td>
      <td>61.000000</td>
      <td>0.000000</td>
      <td>85.000000</td>
      <td>57.000000</td>
      <td>60.000000</td>
      <td>101.00000</td>
      <td>35.000000</td>
      <td>74.000000</td>
      <td>...</td>
      <td>78.0</td>
      <td>45.0</td>
      <td>65.0</td>
      <td>45.0</td>
      <td>34.0</td>
      <td>23.0</td>
      <td>65.0</td>
      <td>12.0</td>
      <td>65.0</td>
      <td>94.0</td>
    </tr>
    <tr>
      <th>f2</th>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.00000</td>
      <td>2.000000</td>
      <td>1.000000</td>
      <td>...</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>f5</th>
      <td>91.297791</td>
      <td>60.339826</td>
      <td>17.252986</td>
      <td>52.667078</td>
      <td>29.269869</td>
      <td>20.129444</td>
      <td>9.796378</td>
      <td>83.68538</td>
      <td>17.252986</td>
      <td>98.429899</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>views</th>
      <td>6820.000000</td>
      <td>2534.000000</td>
      <td>7312.000000</td>
      <td>493.000000</td>
      <td>1338.000000</td>
      <td>21550.000000</td>
      <td>61.000000</td>
      <td>3260.00000</td>
      <td>2764.000000</td>
      <td>9992.000000</td>
      <td>...</td>
      <td>6790.0</td>
      <td>2112.0</td>
      <td>7894.0</td>
      <td>9877.0</td>
      <td>10346.0</td>
      <td>9747.0</td>
      <td>5628.0</td>
      <td>1267.0</td>
      <td>6543.0</td>
      <td>2356.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 120 columns</p>
</div>

</details>

<br>

<details>
  <summary>풀이2</summary>

<br>

> 코드
```python
  # 행별 합이 3000 이상인 데이터 수
  print(sum(df.sum() >= 3000))
```
- 조건에 맞는 데이터 개수를 구하기 위해 sum() 활용

- df.sum()

  - sum() 함수는 기본적으로 열별 합계를 계산
    
    - df 의 각 열에 대해 모든 값의 합을 구함
 
- df.sum() >= 3000

  - 각 열의 합계가 3000 이상인지를 확인하는 조건을 적용
  
    - 열별로 True 또는 False의 불리언 값 시리즈 반환
 
- sum(df.sum() >= 3000)

  - True는 1로, False는 0으로 계산
  
    - 3000 이상인 열의 개수 계산

> 결과
```python
  88
```

</details>

<br>

---

<br>









