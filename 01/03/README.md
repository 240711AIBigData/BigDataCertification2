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



















