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

</details>

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

section16 이상치, IQR
---
### 문제
1. 'views' 컬럼의 1사분위수, 3사분위수 그리고 IQR 을 계산하시오.

2. 이상치 조건에 맞는 데이터를 찾으시오. (이상치 : 1사분위수 - (IQR * 1.5) 보다 작거나, 3사분위수 + (IQR * 1.5) 보다 큰 값)

3. 이상치 데이터의 'views' 컬럼 합을 정수로 구하시오.

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
  quantile, IQR = 3사분위수 - 1사분위수
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 1사분위 / 3사분위
  q1 = df['views'].quantile(.25) 
  q3 = df['views'].quantile(.75)
  print(q1)
  print(q3)
```
- quantile() 함수를 모르면 describe() 함수를 사용해 사분위수 확인 가능
```python
q3 = df['views'].describe()['75%']  # 3사분위수
q1 = df['views'].describe()['25%']  # 1사분위수
```

> 결과
```python
  3031.0
  8473.5
```

<br>

> 코드
```python
  # IQR 계산
  IQR = q3 - q1
  IQR
```

> 결과
```python
  5442.5
```


<br>

> 코드
```python
  # 이상치 기준 찾기
  line1 = q1 - (IQR * 1.5)
  line2 = q3 + (IQR * 1.5)
  print(line1)
  print(line2)
```

> 결과
```python
  -5132.75
  16637.25
```

<br>

> 코드
```python
  # 이상치 조건에 만족하는 데이터 찾기
  cond1 = df['views'] < line1
  cond2 = df['views'] > line2
  df = df[cond1 | cond2]
  df
```
- 두 조건 중 하나의 조건이라도 부합하는 데이터를 찾기 위해 '또는(or)'을 의미하는 '|' 활용

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
  </tbody>
</table>
</div>


<br>

> 코드
```python
  # views 컬럼 합(정수)
  print(int(df['views'].sum()))
```

> 결과
```python
  77699
```

</details>

<br>

---

<br>

section17 이상치, 소수점 있는 데이터 찾기, 표준 편차
---
### 문제
1. 'views' 컬럼의 표준편차를 구하시오.

2. 'age' 컬럼의 이상치(소수점 나이, 음수 나이, 0살)를 제거하고, 'views' 컬럼의 표준편차를 구하시오.

3. 이상치 제거 전후의 'views' 컬럼의 표준편차를 더하여, 반올림 후 소수 둘째 자리까지 구하시오.

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
  std(), round()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 표준편차
  r1 = df['views'].std()
  r1
```
- std() : 표준편차를 구하는 함수

- 판다스는 기본적으로 표본 표준편차(ddof=1)를 계산

> 결과
```python
  4121.626455600414
```

<br>

> 코드
```python
  # 음수이거나 0 데이터 제외
  cond = df['age'] > 0
  df = df[cond]
  df
```
- 다른 방법
```python
  cond = df['age'] <= 0
  df = df[~cond]
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
<p>116 rows × 10 columns</p>
</div>


<br>

> 코드
```python
  # 소수점이 없는 값만 선택
  cond = df['age'] == round(df['age'], 0)
  df = df[cond]
  df
```
- 소수점이 있는 데이터를 찾기 위해 df['age'] == round(df['age'], 0) 조건 활용

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
<p>110 rows × 10 columns</p>
</div>

<br>

> 코드
```python
  # 표준편차
  r2 = df['views'].std()
  r2
```

> 결과
```python
  4175.681776173446
```

<br>

> 코드
```python
  print(round(r1 + r2, 2))
```

> 결과
```python
  8297.31
```

</details>

<br>

---

<br>

section18 데이터(행) 기준 평균값, 인덱싱
---
### 문제
1. index '2001' 데이터(행)에서 평균보다 큰 값의 개수를 구하시오.

2. index '2003' 데이터(행)에서 평균보다 작은 값의 개수를 구하시오.

3. 두 개수를 더하시오

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/type1_data2.csv', index_col = 'year')
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
      <th>190</th>
      <th>191</th>
      <th>192</th>
      <th>193</th>
      <th>194</th>
      <th>195</th>
      <th>196</th>
      <th>197</th>
      <th>198</th>
      <th>199</th>
    </tr>
    <tr>
      <th>year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000</th>
      <td>137</td>
      <td>74</td>
      <td>114</td>
      <td>140</td>
      <td>80</td>
      <td>150</td>
      <td>16</td>
      <td>133</td>
      <td>178</td>
      <td>181</td>
      <td>...</td>
      <td>124</td>
      <td>94</td>
      <td>118</td>
      <td>12</td>
      <td>50</td>
      <td>191</td>
      <td>137</td>
      <td>174</td>
      <td>56</td>
      <td>128</td>
    </tr>
    <tr>
      <th>2001</th>
      <td>176</td>
      <td>87</td>
      <td>64</td>
      <td>110</td>
      <td>128</td>
      <td>16</td>
      <td>8</td>
      <td>4</td>
      <td>123</td>
      <td>87</td>
      <td>...</td>
      <td>59</td>
      <td>22</td>
      <td>3</td>
      <td>108</td>
      <td>17</td>
      <td>104</td>
      <td>101</td>
      <td>161</td>
      <td>156</td>
      <td>43</td>
    </tr>
    <tr>
      <th>2002</th>
      <td>128</td>
      <td>132</td>
      <td>123</td>
      <td>112</td>
      <td>134</td>
      <td>160</td>
      <td>180</td>
      <td>47</td>
      <td>115</td>
      <td>155</td>
      <td>...</td>
      <td>160</td>
      <td>111</td>
      <td>116</td>
      <td>75</td>
      <td>48</td>
      <td>51</td>
      <td>81</td>
      <td>101</td>
      <td>194</td>
      <td>73</td>
    </tr>
    <tr>
      <th>2003</th>
      <td>78</td>
      <td>45</td>
      <td>26</td>
      <td>50</td>
      <td>177</td>
      <td>119</td>
      <td>47</td>
      <td>72</td>
      <td>163</td>
      <td>125</td>
      <td>...</td>
      <td>163</td>
      <td>88</td>
      <td>52</td>
      <td>79</td>
      <td>192</td>
      <td>83</td>
      <td>5</td>
      <td>75</td>
      <td>196</td>
      <td>119</td>
    </tr>
    <tr>
      <th>2004</th>
      <td>1</td>
      <td>162</td>
      <td>124</td>
      <td>12</td>
      <td>1</td>
      <td>126</td>
      <td>58</td>
      <td>123</td>
      <td>186</td>
      <td>161</td>
      <td>...</td>
      <td>100</td>
      <td>93</td>
      <td>86</td>
      <td>12</td>
      <td>115</td>
      <td>72</td>
      <td>29</td>
      <td>30</td>
      <td>88</td>
      <td>150</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 200 columns</p>
</div>

</details>

<br>

### 힌트
```python
  loc[], mean()
```

<br>

<details>
  <summary>풀이1</summary>

<br>

> 코드
```python
  # 2001, 평균보다 큰 값 합계
  m1 = df.loc[2001].mean()
  print(m1)
  
  cond1 = df.loc[2001] > m1
  print(cond1)
  
  r1 = sum(cond1)
  print(r1)
```
- sum() : 기본적으로 컬럼별 계산 진행

  - 행별로 계산하기 위해 loc 사용

> 결과
```python
  100.735
  0       True
  1      False
  2      False
  3       True
  4       True
         ...  
  195     True
  196     True
  197     True
  198     True
  199    False
  Name: 2001, Length: 200, dtype: bool
  100
```

<br>

> 코드
```python
  # 2003, 평균보다 작은 값 합계
  m2 = df.loc[2003].mean()
  print(m2)
  
  cond2 = df.loc[2003] < m2
  print(cond2)
  
  r2 = sum(cond2)
  print(r2)
```

> 결과
```python
  97.215
  0       True
  1       True
  2       True
  3       True
  4      False
         ...  
  195     True
  196     True
  197     True
  198    False
  199    False
  Name: 2003, Length: 200, dtype: bool
  102
```


<br>

> 코드
```python
  # 두 개수의 합
  print(r1 + r2)
```

> 결과
```python
  202
```

</details>

<br>

<details>
  <summary>풀이2</summary>

<br>

> 코드
```python
  # 행과 열 변경
  df = df.T
  df
```
- DataFrame.T 활용하여 행과 열을 변경한 후 계산 가능

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>year</th>
      <th>2000</th>
      <th>2001</th>
      <th>2002</th>
      <th>2003</th>
      <th>2004</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>137</td>
      <td>176</td>
      <td>128</td>
      <td>78</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>74</td>
      <td>87</td>
      <td>132</td>
      <td>45</td>
      <td>162</td>
    </tr>
    <tr>
      <th>2</th>
      <td>114</td>
      <td>64</td>
      <td>123</td>
      <td>26</td>
      <td>124</td>
    </tr>
    <tr>
      <th>3</th>
      <td>140</td>
      <td>110</td>
      <td>112</td>
      <td>50</td>
      <td>12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>80</td>
      <td>128</td>
      <td>134</td>
      <td>177</td>
      <td>1</td>
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
      <th>195</th>
      <td>191</td>
      <td>104</td>
      <td>51</td>
      <td>83</td>
      <td>72</td>
    </tr>
    <tr>
      <th>196</th>
      <td>137</td>
      <td>101</td>
      <td>81</td>
      <td>5</td>
      <td>29</td>
    </tr>
    <tr>
      <th>197</th>
      <td>174</td>
      <td>161</td>
      <td>101</td>
      <td>75</td>
      <td>30</td>
    </tr>
    <tr>
      <th>198</th>
      <td>56</td>
      <td>156</td>
      <td>194</td>
      <td>196</td>
      <td>88</td>
    </tr>
    <tr>
      <th>199</th>
      <td>128</td>
      <td>43</td>
      <td>73</td>
      <td>119</td>
      <td>150</td>
    </tr>
  </tbody>
</table>
<p>200 rows × 5 columns</p>
</div>


<br>

> 코드
```python
  # 평균보다 큰 값 합계
  m1 = df[2001].mean()
  cond1 = df[2001] > m1
  r1 = sum(cond1)
  print(r1)
```

> 결과
```python
  100
```

<br>

> 코드
```python
  # 평균보다 작은 값 합계
  m2 = df[2003].mean()
  cond2 = df[2003] < m2
  r2 = sum(cond2)
  print(r2)
```

> 결과
```python
  102
```

<br>

> 코드
```python
  # 두 값의 합
  print(r1 + r2)
```

> 결과
```python
  202
```

</details>

<br>

---

<br>

section19 결측치(뒤의 값으로 대체), 그룹합
---
### 문제
1. 결측치를 바로 뒤에 있는 값으로 대체하시오. (바로 뒤의 값도 결측치일 경우, 뒤에 있는 데이터 중 가장 가까운값으로 대체)

2. 'city'와 'f2' 컬럼을 기준으로 그룹합을 계산하시오.

3. 'views' 값이 세 번째로 큰 city 이름을 구하시오.

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
  fillna(), groupby(), reset_index(), sort_values()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 결측치 채우기
  df = df.fillna(method = 'bfill')
  df.isnull().sum()
```
- fillna() 의 method 는 결측치를 채울 방식을 말함

  - bfill : 결측치의 뒤에 있는 값으로 채움
 
  - fill : 결측치의 앞에 있는 값으로 채움

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
  views         0
  dtype: int64
```

<br>

> 코드
```python
  # city와 f2 기준 그룹합 계산
  df = df.groupby(['city', 'f2']).sum(numeric_only = True).reset_index()
  df
```
- reset_index() : groupby() 이후 만들어진 멀티인덱스를 컬럼으로 만들고, 인덱스는 새롭게 매겨짐

- 현재 판다스 최신 버전을 사용하고 있어 sum(numeric_only=True) 사용하지만

  - 시험환경에서는 sum() 사용

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>f2</th>
      <th>age</th>
      <th>f1</th>
      <th>f5</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>경기</td>
      <td>0</td>
      <td>1192.9</td>
      <td>1490.0</td>
      <td>1425.236647</td>
      <td>154066.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>경기</td>
      <td>1</td>
      <td>997.0</td>
      <td>1016.0</td>
      <td>935.958628</td>
      <td>91442.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>경기</td>
      <td>2</td>
      <td>296.0</td>
      <td>390.0</td>
      <td>430.186433</td>
      <td>42709.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>대구</td>
      <td>0</td>
      <td>664.0</td>
      <td>982.0</td>
      <td>371.184620</td>
      <td>100421.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>대구</td>
      <td>1</td>
      <td>393.6</td>
      <td>471.0</td>
      <td>404.779978</td>
      <td>49536.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>대구</td>
      <td>2</td>
      <td>185.0</td>
      <td>321.0</td>
      <td>79.667919</td>
      <td>22624.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>부산</td>
      <td>0</td>
      <td>525.0</td>
      <td>691.0</td>
      <td>395.272907</td>
      <td>80460.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>부산</td>
      <td>1</td>
      <td>475.7</td>
      <td>684.0</td>
      <td>460.657406</td>
      <td>51624.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>부산</td>
      <td>2</td>
      <td>38.5</td>
      <td>189.0</td>
      <td>101.195372</td>
      <td>17771.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>서울</td>
      <td>0</td>
      <td>241.0</td>
      <td>480.0</td>
      <td>484.809540</td>
      <td>61447.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>서울</td>
      <td>1</td>
      <td>433.3</td>
      <td>687.0</td>
      <td>506.371383</td>
      <td>59111.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>서울</td>
      <td>2</td>
      <td>165.3</td>
      <td>337.0</td>
      <td>179.328213</td>
      <td>22405.0</td>
    </tr>
  </tbody>
</table>
</div>


<br>

> 코드
```python
  # 내림차순 정렬
  df = df.sort_values('views', ascending = False)
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>f2</th>
      <th>age</th>
      <th>f1</th>
      <th>f5</th>
      <th>views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>경기</td>
      <td>0</td>
      <td>1192.9</td>
      <td>1490.0</td>
      <td>1425.236647</td>
      <td>154066.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>대구</td>
      <td>0</td>
      <td>664.0</td>
      <td>982.0</td>
      <td>371.184620</td>
      <td>100421.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>경기</td>
      <td>1</td>
      <td>997.0</td>
      <td>1016.0</td>
      <td>935.958628</td>
      <td>91442.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>부산</td>
      <td>0</td>
      <td>525.0</td>
      <td>691.0</td>
      <td>395.272907</td>
      <td>80460.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>서울</td>
      <td>0</td>
      <td>241.0</td>
      <td>480.0</td>
      <td>484.809540</td>
      <td>61447.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>서울</td>
      <td>1</td>
      <td>433.3</td>
      <td>687.0</td>
      <td>506.371383</td>
      <td>59111.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>부산</td>
      <td>1</td>
      <td>475.7</td>
      <td>684.0</td>
      <td>460.657406</td>
      <td>51624.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>대구</td>
      <td>1</td>
      <td>393.6</td>
      <td>471.0</td>
      <td>404.779978</td>
      <td>49536.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>경기</td>
      <td>2</td>
      <td>296.0</td>
      <td>390.0</td>
      <td>430.186433</td>
      <td>42709.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>대구</td>
      <td>2</td>
      <td>185.0</td>
      <td>321.0</td>
      <td>79.667919</td>
      <td>22624.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>서울</td>
      <td>2</td>
      <td>165.3</td>
      <td>337.0</td>
      <td>179.328213</td>
      <td>22405.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>부산</td>
      <td>2</td>
      <td>38.5</td>
      <td>189.0</td>
      <td>101.195372</td>
      <td>17771.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  # 3번째로 큰 값 출력
  print(df.iloc[2, 0])
```

> 결과
```python
  경기
```

</details>

<br>

---

<br>

section20 시계열 데이터, 월별 집계, 인덱스
---
### 문제
1. 연도 구분 없이 월별로 숫자형 컬럼의 합을 구하시오.

2. 합계 중 'views' 가 가장 작은 값을 가진 월을 정수로 구하시오.

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
  pd.to_datetime(), pd.month, groupby()
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
- pd.to_datetime() 활용해 자료형을 datetime 으로 변경

> 결과
```python
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
  # 파생변수 생성
  df['month'] = df['subscribed'].dt.month
  df
```
- dt.month 로 월을 별도 컬럼으로 만듦

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
      <td>2</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 11 columns</p>
</div>


<br>

> 코드
```python
  # 월별로 데이터 합 집계
  df = df.groupby('month').sum(numeric_only = True)
  df
```
- df.groupby('month').sum() 활용해 월별로 데이터 합 집계

  - 판다스 최신 버전 사용시 sum(numeric_only=True) 사용
 
  - 시험 환경에서는 sum() 으로 사용

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
      <th>month</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>441.8</td>
      <td>608.0</td>
      <td>1</td>
      <td>487.453162</td>
      <td>40013.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>860.7</td>
      <td>1301.0</td>
      <td>25</td>
      <td>460.248156</td>
      <td>165852.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>326.3</td>
      <td>457.0</td>
      <td>8</td>
      <td>352.729057</td>
      <td>39031.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>307.0</td>
      <td>268.0</td>
      <td>4</td>
      <td>312.187975</td>
      <td>41307.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>809.6</td>
      <td>822.0</td>
      <td>10</td>
      <td>855.287894</td>
      <td>110786.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>481.8</td>
      <td>244.0</td>
      <td>6</td>
      <td>387.206296</td>
      <td>31295.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>534.0</td>
      <td>399.0</td>
      <td>10</td>
      <td>630.370464</td>
      <td>67677.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>338.5</td>
      <td>119.0</td>
      <td>6</td>
      <td>520.223827</td>
      <td>51048.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>473.6</td>
      <td>356.0</td>
      <td>3</td>
      <td>379.121958</td>
      <td>66340.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>483.0</td>
      <td>437.0</td>
      <td>6</td>
      <td>595.737639</td>
      <td>48705.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>186.0</td>
      <td>181.0</td>
      <td>1</td>
      <td>278.410220</td>
      <td>15857.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>365.0</td>
      <td>373.0</td>
      <td>2</td>
      <td>515.672397</td>
      <td>28658.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 코드
```python
  # 오름차순 정렬 및 가장 작은 값 출력
  print(df.sort_values('views').index[0])
```
- df.sort_values('views') 활용해 'views' 기준으로 오름차순으로 정렬

- 가장 작은 값의 월(인덱스)을 index[0] 으로 출력

> 결과
```python
  11
```

</details>

<br>

---

<br>

section21 시간 간의 차이 계산(분), 필터링
---
### 문제
1. 예상 도착 시간보다 늦게 도착한 건수를 구하시오.

2. 이 중 거리가 7km 이상인 데이터의 수를 정수로 구하시오.

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/delivery_time.csv')
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
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 7 columns</p>
</div>

</details>

<br>

### 힌트
```python
  pd.datetime(), dt.total_seconds(), len()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # datetime 자료형 변환
  df['실제도착시간'] = pd.to_datetime(df['실제도착시간'])
  df['예상도착시간'] = pd.to_datetime(df['예상도착시간'])
  print(df['실제도착시간'], df['예상도착시간'])
```
- pd.datetime() 사용해 자료형을 datetime 으로 변경

> 결과
```python
  0     2023-07-26 09:14:06
  1     2022-11-07 10:44:04
  2     2023-04-18 06:12:46
  3     2023-08-18 11:16:25
  4     2023-08-11 11:27:57
                ...        
  995   2022-10-10 04:13:48
  996   2023-02-03 13:11:46
  997   2023-01-05 21:57:41
  998   2023-06-15 04:14:24
  999   2023-08-02 22:04:06
  Name: 실제도착시간, Length: 1000, dtype: datetime64[ns] 0     2023-07-26 08:39:42
  1     2022-11-07 10:50:15
  2     2023-04-18 05:32:53
  3     2023-08-18 11:08:33
  4     2023-08-11 10:51:57
                ...        
  995   2022-10-10 04:15:37
  996   2023-02-03 13:12:57
  997   2023-01-05 21:57:44
  998   2023-06-15 04:18:38
  999   2023-08-02 22:09:22
  Name: 예상도착시간, Length: 1000, dtype: datetime64[ns]
```

<br>

> 코드
```python
  # 지연 시간 계산(분)
  df['지연시간'] = (df['실제도착시간'] - df['예상도착시간']).dt.total_seconds()/60
  df
```
- 실제 도착 시간에서 예상 도착 시간을 뺀 값을 지연 시간으로 계산

- 지연 시간을 dt.total_seconds() 활용해 전체 시간을 초 단위로 변경

  - 60을 나눠 분 단위로 변경
 
- 예상 도착 시간보다 늦게 도착한 값은 지연 시간이 양수

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
      <th>지연시간</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
      <td>34.400000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
      <td>-6.183333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
      <td>39.883333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
      <td>7.866667</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
      <td>36.000000</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
      <td>-1.816667</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
      <td>-1.183333</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
      <td>-0.050000</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
      <td>-4.233333</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
      <td>-5.266667</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 8 columns</p>
</div>


<br>

> 코드
```python
  # 조건1 - 예상 도착 시간보다 늦게 도착한 건
  cond1 = df['지연시간'] > 0
  df[cond1]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
      <th>지연시간</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
      <td>34.400000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
      <td>39.883333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
      <td>7.866667</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
      <td>36.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2022-11-27 15:13:52</td>
      <td>2022-11-27 16:47:32</td>
      <td>2022-11-27 16:41:28</td>
      <td>배달왕</td>
      <td>14.85</td>
      <td>앱결제</td>
      <td>user_204</td>
      <td>6.066667</td>
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
    </tr>
    <tr>
      <th>986</th>
      <td>2023-03-15 20:57:13</td>
      <td>2023-03-15 21:39:48</td>
      <td>2023-03-15 21:24:23</td>
      <td>배고팡</td>
      <td>12.52</td>
      <td>카드</td>
      <td>user_85</td>
      <td>15.416667</td>
    </tr>
    <tr>
      <th>988</th>
      <td>2022-10-08 14:55:02</td>
      <td>2022-10-08 16:01:08</td>
      <td>2022-10-08 15:31:19</td>
      <td>여기여</td>
      <td>14.24</td>
      <td>카드</td>
      <td>user_207</td>
      <td>29.816667</td>
    </tr>
    <tr>
      <th>990</th>
      <td>2023-05-05 01:38:56</td>
      <td>2023-05-05 02:44:41</td>
      <td>2023-05-05 02:11:34</td>
      <td>여기여</td>
      <td>8.86</td>
      <td>현금</td>
      <td>user_378</td>
      <td>33.116667</td>
    </tr>
    <tr>
      <th>991</th>
      <td>2022-12-23 22:43:48</td>
      <td>2022-12-24 00:09:23</td>
      <td>2022-12-24 00:00:04</td>
      <td>배달왕</td>
      <td>5.95</td>
      <td>앱결제</td>
      <td>user_348</td>
      <td>9.316667</td>
    </tr>
    <tr>
      <th>992</th>
      <td>2022-09-18 06:21:27</td>
      <td>2022-09-18 07:34:52</td>
      <td>2022-09-18 06:55:28</td>
      <td>배달왕</td>
      <td>16.87</td>
      <td>현금</td>
      <td>user_181</td>
      <td>39.400000</td>
    </tr>
  </tbody>
</table>
<p>510 rows × 8 columns</p>
</div>

<br>

> 코드
```python
  # 조건2 - 거리가 7 이상인 건
  cond2 = df['거리'] >= 7
  df[cond2]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
      <th>지연시간</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
      <td>39.883333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
      <td>7.866667</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
      <td>36.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2022-11-27 15:13:52</td>
      <td>2022-11-27 16:47:32</td>
      <td>2022-11-27 16:41:28</td>
      <td>배달왕</td>
      <td>14.85</td>
      <td>앱결제</td>
      <td>user_204</td>
      <td>6.066667</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2022-09-25 16:27:43</td>
      <td>2022-09-25 17:52:23</td>
      <td>2022-09-25 18:13:21</td>
      <td>배달왕</td>
      <td>9.72</td>
      <td>현금</td>
      <td>user_343</td>
      <td>-20.966667</td>
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
    </tr>
    <tr>
      <th>992</th>
      <td>2022-09-18 06:21:27</td>
      <td>2022-09-18 07:34:52</td>
      <td>2022-09-18 06:55:28</td>
      <td>배달왕</td>
      <td>16.87</td>
      <td>현금</td>
      <td>user_181</td>
      <td>39.400000</td>
    </tr>
    <tr>
      <th>994</th>
      <td>2023-02-08 12:09:03</td>
      <td>2023-02-08 13:24:56</td>
      <td>2023-02-08 13:28:54</td>
      <td>여기여</td>
      <td>12.97</td>
      <td>현금</td>
      <td>user_418</td>
      <td>-3.966667</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
      <td>-1.183333</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
      <td>-0.050000</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
      <td>-4.233333</td>
    </tr>
  </tbody>
</table>
<p>629 rows × 8 columns</p>
</div>


<br>

> 코드
```python
  # 조건에 맞는 데이터(행) 수 출력
  print(len(df[cond1 & cond2]))
```

> 결과
```python
   311
```

</details>

<br>

---

<br>

section22 시간 간의 차이 계산(분), 그룹핑
---
### 문제
1. 주문 시간과 실제 도착 시간의 차이를 분 단위로 계산하시오.

2. 앱 종류별로 평균 도착 시간(분)을 계산하시오.

3. 평균적으로 가장 빠른 앱 종류를 찾고, 해당 앱의 평균 도착 시간을 분으로 반올림하여 정수로 구하시오.

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/delivery_time.csv')
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
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 7 columns</p>
</div>

</details>

<br>

### 힌트
```python
  pd.to_datetime(), dt.total_seconds(), groupby(), mean(), min()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # datetime 으로 자료형 변경
  df['실제도착시간'] = pd.to_datetime(df['실제도착시간'])
  print(df['실제도착시간'])
  df['주문시간'] = pd.to_datetime(df['주문시간'])
  print(df['주문시간'])
```
- pd.to_datetime() 사용해 자료형을 datetime() 으로 변경

> 결과
```python
  0     2023-07-26 09:14:06
  1     2022-11-07 10:44:04
  2     2023-04-18 06:12:46
  3     2023-08-18 11:16:25
  4     2023-08-11 11:27:57
                ...        
  995   2022-10-10 04:13:48
  996   2023-02-03 13:11:46
  997   2023-01-05 21:57:41
  998   2023-06-15 04:14:24
  999   2023-08-02 22:04:06
  Name: 실제도착시간, Length: 1000, dtype: datetime64[ns]
  0     2023-07-26 08:05:49
  1     2022-11-07 10:21:54
  2     2023-04-18 05:00:57
  3     2023-08-18 10:46:28
  4     2023-08-11 09:58:27
                ...        
  995   2022-10-10 03:13:30
  996   2023-02-03 12:47:19
  997   2023-01-05 21:28:58
  998   2023-06-15 03:56:42
  999   2023-08-02 20:53:53
  Name: 주문시간, Length: 1000, dtype: datetime64[ns]
```

<br>

> 코드
```python
  # 실제 도착 시간과 주문 시간 차이 계산(분)
  df['diff'] = (df['실제도착시간'] - df['주문시간']).dt.total_seconds()/60
  df['diff']
```
- 실제 도착 시간에서 주문 시간을 뺀 차이를 분으로 계산

> 결과
```python
  0      68.283333
  1      22.166667
  2      71.816667
  3      29.950000
  4      89.500000
           ...    
  995    60.300000
  996    24.450000
  997    28.716667
  998    17.700000
  999    70.216667
  Name: diff, Length: 1000, dtype: float64
```


<br>

> 코드
```python
  # 앱 종류별 도착 시간과 주문 시간 차이의 평균 계산
  df = df.groupby('앱종류')['diff'].mean()
  df
```
- 앱 종류를 기준으로 그룹핑

- 실제 도착 시간에서 주문 시간을 뺀 차이의 평균 구하기

> 결과
```python
  앱종류
  배고팡    61.818694
  배달왕    63.517864
  여기여    62.343110
  Name: diff, dtype: float64
```

<br>

> 코드
```python
  # 가장 작은 값을 찾고 반올림 후 출력
  print(round(df.min()))
```
- 가장 작은 값을 찾고 반올림 후 출력

> 결과
```python
  62
```

</details>

<br>

---

<br>

section23 시간 간의 차이 계산(분), 비율
---
### 문제
1. 각 결제 종류별로 실제 도착 시간이 예상 도착 시간보다 늦은 주문의 비율을 계산하시오.

2. 비율 중 가장 큰 값을 반올림하여 소수 둘째 자리까지 구하시오.

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/delivery_time.csv')
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
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 7 columns</p>
</div>

</details>

<br>

### 힌트
```python
  pd.to_datetime(), dt.total_seconds(), groupby(), mean(), max()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # datetime 자료형으로 변경
  df['실제도착시간'] = pd.to_datetime(df['실제도착시간'])
  print(df['실제도착시간'])
  df['예상도착시간'] = pd.to_datetime(df['예상도착시간'])
  print(df['예상도착시간'])
```
- pd.to_datetime() 활용해 자료형을 datetime 으로 변경

> 결과
```python
  0     2023-07-26 09:14:06
  1     2022-11-07 10:44:04
  2     2023-04-18 06:12:46
  3     2023-08-18 11:16:25
  4     2023-08-11 11:27:57
                ...        
  995   2022-10-10 04:13:48
  996   2023-02-03 13:11:46
  997   2023-01-05 21:57:41
  998   2023-06-15 04:14:24
  999   2023-08-02 22:04:06
  Name: 실제도착시간, Length: 1000, dtype: datetime64[ns]
  0     2023-07-26 08:39:42
  1     2022-11-07 10:50:15
  2     2023-04-18 05:32:53
  3     2023-08-18 11:08:33
  4     2023-08-11 10:51:57
                ...        
  995   2022-10-10 04:15:37
  996   2023-02-03 13:12:57
  997   2023-01-05 21:57:44
  998   2023-06-15 04:18:38
  999   2023-08-02 22:09:22
  Name: 예상도착시간, Length: 1000, dtype: datetime64[ns]
```

<br>

> 코드
```python
  # 지연 시간 계산(분)
  df['지연시간'] = (df['실제도착시간'] - df['예상도착시간']).dt.total_seconds()/60    # 분 단위로 게산
  df
```
- 지연 시간을 dt.total_seconds()/60 활용해 분으로 계산

> 결과

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
      <th>지연시간</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
      <td>34.400000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
      <td>-6.183333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
      <td>39.883333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
      <td>7.866667</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
      <td>36.000000</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
      <td>-1.816667</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
      <td>-1.183333</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
      <td>-0.050000</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
      <td>-4.233333</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
      <td>-5.266667</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 8 columns</p>
</div>


<br>

> 코드
```python
  # 실제 도착 시간이 예상 도착 시간보다 늦은 경우를 체크하는 컬럼 생성
  df['지연여부'] = df['지연시간'] > 0
  df
```
- df['지연시간'] > 0 활용해 지연 시간이 예측 시간보다 늦게 배달된 경우는 True

  - 빨리 배달된 경우는 False 

> 결과

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
      <th>지연시간</th>
      <th>지연여부</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
      <td>34.400000</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
      <td>-6.183333</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
      <td>39.883333</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
      <td>7.866667</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
      <td>36.000000</td>
      <td>True</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
      <td>-1.816667</td>
      <td>False</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
      <td>-1.183333</td>
      <td>False</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
      <td>-0.050000</td>
      <td>False</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
      <td>-4.233333</td>
      <td>False</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
      <td>-5.266667</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 9 columns</p>
</div>

<br>

> 코드
```python
  # 결제 종류별 지연된 주문 수의 비율 계산
  result = df.groupby('결제종류')['지연여부'].mean()
  result
```
- True = 1, False = 0

  - ex) 10개 중 3개가 1이고, 7개가 0일 때 평균 계산하면 0.3

- 결제 종류를 기준으로 그룹핑하고 지연 여부의 평균 구하기

  - 결제 종류별 지연된 주문 수의 비율이 계산됨

> 결과
```python
  결제종류
  앱결제    0.556634
  카드     0.489971
  현금     0.488304
  Name: 지연여부, dtype: float64
```


<br>

> 코드
```python
  # 가장 비율이 높은 값
  print(round(result.max(), 2))
```
- 비율이 높은 값을 찾고 반올림 후 출력

> 결과
```python
  0.56
```

</details>

<br>

---

<br>

section24 그룹핑, 값 찾기, 필터링
---
### 문제
1. 사용자별 주문 거리의 합계가 50km 이상인 사람들의 결제 방식을 구하시오.

2. 이 결제 방식 중 가장 빈도가 높은 수를 구하시오.

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/delivery_time.csv')
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
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 7 columns</p>
</div>

</details>

<br>

### 힌트
```python
  groupby(), isin(), value_counts()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 사용자별 주문 거리의 합계
  df_distance = df.groupby('user')['거리'].sum()
  df_distance
```
- user 기준으로 그룹핑

- 거리 컬럼의 합 구하기

  - 사용자별 거리 총합 계산

> 결과
```python
  user
  user_1      22.49
  user_10     21.27
  user_101    16.82
  user_103     6.54
  user_104     5.15
              ...  
  user_94      6.77
  user_95     49.68
  user_96      7.19
  user_98     10.31
  user_99      3.48
  Name: 거리, Length: 426, dtype: float64
```

<br>

> 코드
```python
  # 주문 거리의 합계가 50km 이상인 사용자만 필터링
  cond = df_distance >= 50
  df_distance = df_distance[cond]
  df_distance 
```
- 거리가 50 이상인 값 필터링

- 최종 df_distance 에는 50 이상인 user 값이 저장됨

> 결과
```python
  user
  user_116    67.98
  user_133    56.31
  user_157    51.15
  user_176    53.58
  user_19     52.44
  user_20     52.91
  user_204    54.16
  user_211    68.63
  user_251    52.73
  user_255    59.79
  user_311    51.02
  user_318    70.84
  user_338    50.32
  user_342    58.07
  user_360    82.77
  user_366    52.19
  user_368    56.78
  user_369    72.74
  user_383    56.91
  user_385    76.07
  user_397    58.12
  user_398    51.97
  user_430    51.92
  user_434    56.79
  user_441    58.20
  user_497    58.68
  user_80     55.14
  user_85     56.45
  Name: 거리, dtype: float64
```


<br>

> 코드
```python
  # 주문 거리의 합계가 50km 이상인 사용자들의 데이터 필터링
  filtered_data = df[df['user'].isin(df_distance.index)]
  filtered_data
```
- groupby() 함수를 활용해 그룹핑할 때 user 기준으로 그룹을 묶으면 user 가 index 가 됨

  - df_distance.index 를 했을 때 'user_116', 'user_133' 등과 같은 값을 반환받을 수 있음
 
- 이 user 값을 isin() 함수를 활용해 필터링

  - 조건식으로 찾으려면 user 수만큼 조건이 있어야 하지만, isin() 은 리스트 형태를 입력값으로 받음
 
    - 리스트에 있는 값을 한번에 찾을 수 있음

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2022-11-27 15:13:52</td>
      <td>2022-11-27 16:47:32</td>
      <td>2022-11-27 16:41:28</td>
      <td>배달왕</td>
      <td>14.85</td>
      <td>앱결제</td>
      <td>user_204</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2022-12-23 01:48:35</td>
      <td>2022-12-23 02:47:01</td>
      <td>2022-12-23 02:52:36</td>
      <td>배고팡</td>
      <td>5.35</td>
      <td>현금</td>
      <td>user_497</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2022-10-04 01:48:33</td>
      <td>2022-10-04 02:54:07</td>
      <td>2022-10-04 02:47:42</td>
      <td>배고팡</td>
      <td>8.99</td>
      <td>카드</td>
      <td>user_398</td>
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
    </tr>
    <tr>
      <th>959</th>
      <td>2023-01-25 02:39:41</td>
      <td>2023-01-25 04:10:54</td>
      <td>2023-01-25 03:27:17</td>
      <td>배달왕</td>
      <td>10.29</td>
      <td>앱결제</td>
      <td>user_157</td>
    </tr>
    <tr>
      <th>974</th>
      <td>2022-12-17 15:29:28</td>
      <td>2022-12-17 16:21:01</td>
      <td>2022-12-17 16:31:10</td>
      <td>배달왕</td>
      <td>15.52</td>
      <td>현금</td>
      <td>user_383</td>
    </tr>
    <tr>
      <th>981</th>
      <td>2023-03-08 10:51:00</td>
      <td>2023-03-08 12:29:03</td>
      <td>2023-03-08 11:54:56</td>
      <td>배고팡</td>
      <td>17.21</td>
      <td>현금</td>
      <td>user_311</td>
    </tr>
    <tr>
      <th>984</th>
      <td>2023-06-23 21:07:25</td>
      <td>2023-06-23 22:21:26</td>
      <td>2023-06-23 22:44:11</td>
      <td>배달왕</td>
      <td>10.30</td>
      <td>카드</td>
      <td>user_369</td>
    </tr>
    <tr>
      <th>986</th>
      <td>2023-03-15 20:57:13</td>
      <td>2023-03-15 21:39:48</td>
      <td>2023-03-15 21:24:23</td>
      <td>배고팡</td>
      <td>12.52</td>
      <td>카드</td>
      <td>user_85</td>
    </tr>
  </tbody>
</table>
<p>129 rows × 7 columns</p>
</div>

<br>

> 코드
```python
  # 해당 사용자들의 선호 결제 방식 중 큰 값
  payment_method = filtered_data['결제종류'].value_counts()
  print(payment_method[0])
```
- 필터링된 데이터프레임에서 결제 종류별로 빈도 수를 value_counts() 활용해 찾기

  - 가장 큰 값(상위에 있는 값이 가장 빈도 수가 높음)을 출력

> 결과
```python
  48  
```

</details>

<br>

---

<br>

section25 시간 간의 차이 계산(일)
---
### 문제
1. 각 사용자별로 첫 주문과 마지막 주문 사이의 시간 간격을 일 단위로 계산하시오.

2. 시간 간격이 1일 이하인 사용자를 제외하고, 나머지 사용자들의 평균 시간 간격(일 단위)을 계산하시오.

3. 평균 시간 간격보다 긴 시간 간격을 가진 사용자의 수를 정수로 구하시오.

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/delivery_time.csv')
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
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 7 columns</p>
</div>

</details>

<br>

### 힌트
```python
  to_datetime(), groupby(), min(), max(), dt.days
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 각 사용자별로 첫 주문과 마지막 주문 사이의 시간 간격(일 단위) 계산
  df['주문시간'] = pd.to_datetime(df['주문시간'])
  print(df['주문시간'])
  
  min_order_time = df.groupby('user')['주문시간'].min()
  print(min_order_time)
  
  max_order_time = df.groupby('user')['주문시간'].max()
  print(max_order_time)
  
  time_interval = (max_order_time - min_order_time).dt.days
  time_interval
```
- pd.to_datetime() 활용해 자료형을 datetime 으로 변경

- user 별로 2번 그룹핑

  - 최소값(첫 주문)
 
  - 최대값(마지막 주문)
 
- 첫 주문과 마지막 주문의 차이 계산

  - 한 번만 주문했다면, 첫 주문과 마지막 주문이 같아 0일(시간은 존재)
 
  - 문제에서는 일 단위를 묻고 있으므로 1일 미만은 무시
 
- dt.days 활용해 첫 주문과 마지막 주문의 차이를 일 단위로 계산

  - 전체 시간을 초로 변환하는 dt.total_seconds() 사용도 가능
 
    - 초 → 분 → 시간 → 일(소수점 버림) 로 변환
   
      - (시간 차이).dt.total_seconds()/60/60/24 에서 소수점을 버리면 일 단위
     
        - 일 단위에서는 24시가 지나지 않으면 똑같음
       
        - 내일 1시도 내일, 내일 23시도 내일

> 결과
```python
  0     2023-07-26 08:05:49
  1     2022-11-07 10:21:54
  2     2023-04-18 05:00:57
  3     2023-08-18 10:46:28
  4     2023-08-11 09:58:27
                ...        
  995   2022-10-10 03:13:30
  996   2023-02-03 12:47:19
  997   2023-01-05 21:28:58
  998   2023-06-15 03:56:42
  999   2023-08-02 20:53:53
  Name: 주문시간, Length: 1000, dtype: datetime64[ns]

  user
  user_1     2023-01-08 12:52:59
  user_10    2022-10-22 20:13:05
  user_101   2023-06-26 01:43:40
  user_103   2022-12-04 09:06:03
  user_104   2023-06-13 18:24:38
                     ...        
  user_94    2022-12-26 10:29:42
  user_95    2022-11-07 15:46:49
  user_96    2022-11-19 18:52:34
  user_98    2023-03-26 01:13:25
  user_99    2023-06-29 23:38:47
  Name: 주문시간, Length: 426, dtype: datetime64[ns]

  user
  user_1     2023-06-07 04:29:28
  user_10    2023-08-02 05:48:27
  user_101   2023-06-26 01:43:40
  user_103   2022-12-04 09:06:03
  user_104   2023-06-13 18:24:38
                     ...        
  user_94    2022-12-26 10:29:42
  user_95    2023-03-09 14:08:56
  user_96    2022-11-19 18:52:34
  user_98    2023-03-26 01:13:25
  user_99    2023-06-29 23:38:47
  Name: 주문시간, Length: 426, dtype: datetime64[ns]

  user
  user_1      149
  user_10     283
  user_101      0
  user_103      0
  user_104      0
             ... 
  user_94       0
  user_95     121
  user_96       0
  user_98       0
  user_99       0
  Name: 주문시간, Length: 426, dtype: int64
```

<br>

> 코드
```python
  # 1일 이하 주문 제외
  cond1 = time_interval > 0
  m = time_interval[cond1].mean()
  m
```
- 1번 이하 주문한 건을 제외하기 위해 time_interval 이 0인 값 제거 후 평균 구하기

> 결과
```python
  167.69463087248323
```


<br>

> 코드
```python
  # 평균보다 기간이 긴 유저 수를 계산하고 출력
  cond2 = time_interval > m
  print(len(time_interval[cond2]))
```
- 평균보다 기간이 긴 유저 수를 계산하고 출력

> 결과
```python
  146
```

</details>

<br>

---

<br>

section26 날짜와 시간 정보 변환, 비율
---
### 문제
1. 주문이 가장 많이 발생한 연-월을 찾으시오.

2. 해당 연-월에 '배고팡' 앱을 통한 주문 중 '앱결제'로 결제된 주문의 비율을 계산하시오. (반올림 후 소수 둘째 자리까지 계산)

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/delivery_time.csv')
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
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 7 columns</p>
</div>

</details>

<br>

### 힌트
```python
  dt.to_period('M'), idxmax()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 주문이 가장 많이 발생한 연-월 찾기
  df['주문시간'] = pd.to_datetime(df['주문시간'])
  print(df['주문시간'])
  
  df['주문월'] = df['주문시간'].dt.to_period('M')
  print(df['주문월'])
  
  year_month = df['주문월'].value_counts().idxmax()
  print(year_month)
```
- pd.to_datetime() 활용해 자료형을 datetime 으로 변경

- dt.to_period('M') 활용해 연도와 월을 묶어서 주문 월 컬럼 생성

  - ex) 2024-02
 
- 주문 월 빈도 수 중 주문이 가장 많이 발생한 연-월(최대값) 인덱스 찾기

> 결과
```python
  0     2023-07-26 08:05:49
  1     2022-11-07 10:21:54
  2     2023-04-18 05:00:57
  3     2023-08-18 10:46:28
  4     2023-08-11 09:58:27
                ...        
  995   2022-10-10 03:13:30
  996   2023-02-03 12:47:19
  997   2023-01-05 21:28:58
  998   2023-06-15 03:56:42
  999   2023-08-02 20:53:53
  Name: 주문시간, Length: 1000, dtype: datetime64[ns]
  
  0      2023-07
  1      2022-11
  2      2023-04
  3      2023-08
  4      2023-08
          ...   
  995    2022-10
  996    2023-02
  997    2023-01
  998    2023-06
  999    2023-08
  Name: 주문월, Length: 1000, dtype: period[M]
  
  2022-09
```

<br>

> 코드
```python
  # 해당 연-월에 배고팡 앱을 통한 주문
  cond1 = df['주문월'] == year_month
  cond2 = df['앱종류'] == '배고팡'
  filtered_df = df[cond1 & cond2]
  filtered_df
```
- 앱 종류가 배고팡이면서 주문 월이 가장 많은 조건을 통해 필터링

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
      <th>주문월</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>38</th>
      <td>2022-09-11 05:12:02</td>
      <td>2022-09-11 06:02:35</td>
      <td>2022-09-11 05:42:50</td>
      <td>배고팡</td>
      <td>17.10</td>
      <td>현금</td>
      <td>user_430</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>76</th>
      <td>2022-09-07 03:05:02</td>
      <td>2022-09-07 03:48:11</td>
      <td>2022-09-07 04:07:53</td>
      <td>배고팡</td>
      <td>1.10</td>
      <td>앱결제</td>
      <td>user_401</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>98</th>
      <td>2022-09-01 03:23:11</td>
      <td>2022-09-01 04:03:16</td>
      <td>2022-09-01 03:47:38</td>
      <td>배고팡</td>
      <td>4.28</td>
      <td>현금</td>
      <td>user_472</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>127</th>
      <td>2022-09-10 10:13:46</td>
      <td>2022-09-10 11:27:34</td>
      <td>2022-09-10 10:52:38</td>
      <td>배고팡</td>
      <td>10.95</td>
      <td>현금</td>
      <td>user_125</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>133</th>
      <td>2022-09-26 08:50:25</td>
      <td>2022-09-26 10:16:55</td>
      <td>2022-09-26 09:17:49</td>
      <td>배고팡</td>
      <td>19.60</td>
      <td>카드</td>
      <td>user_133</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>166</th>
      <td>2022-09-16 06:22:46</td>
      <td>2022-09-16 06:57:54</td>
      <td>2022-09-16 07:27:40</td>
      <td>배고팡</td>
      <td>3.44</td>
      <td>앱결제</td>
      <td>user_319</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>178</th>
      <td>2022-09-12 17:13:29</td>
      <td>2022-09-12 17:38:42</td>
      <td>2022-09-12 17:47:24</td>
      <td>배고팡</td>
      <td>13.78</td>
      <td>앱결제</td>
      <td>user_263</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>194</th>
      <td>2022-09-18 23:43:11</td>
      <td>2022-09-19 01:13:17</td>
      <td>2022-09-19 00:03:30</td>
      <td>배고팡</td>
      <td>12.75</td>
      <td>카드</td>
      <td>user_223</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>195</th>
      <td>2022-09-15 02:00:20</td>
      <td>2022-09-15 03:41:45</td>
      <td>2022-09-15 03:13:12</td>
      <td>배고팡</td>
      <td>7.34</td>
      <td>현금</td>
      <td>user_438</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>212</th>
      <td>2022-09-15 06:22:04</td>
      <td>2022-09-15 07:33:11</td>
      <td>2022-09-15 07:37:07</td>
      <td>배고팡</td>
      <td>7.48</td>
      <td>카드</td>
      <td>user_491</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>222</th>
      <td>2022-09-28 01:48:49</td>
      <td>2022-09-28 02:53:36</td>
      <td>2022-09-28 02:19:18</td>
      <td>배고팡</td>
      <td>19.28</td>
      <td>카드</td>
      <td>user_276</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>243</th>
      <td>2022-09-29 11:53:50</td>
      <td>2022-09-29 12:40:35</td>
      <td>2022-09-29 12:57:55</td>
      <td>배고팡</td>
      <td>1.43</td>
      <td>현금</td>
      <td>user_387</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>259</th>
      <td>2022-09-15 05:06:23</td>
      <td>2022-09-15 06:26:40</td>
      <td>2022-09-15 06:02:01</td>
      <td>배고팡</td>
      <td>9.86</td>
      <td>카드</td>
      <td>user_116</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>291</th>
      <td>2022-09-15 12:47:10</td>
      <td>2022-09-15 13:54:27</td>
      <td>2022-09-15 13:31:09</td>
      <td>배고팡</td>
      <td>4.36</td>
      <td>카드</td>
      <td>user_31</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>355</th>
      <td>2022-09-24 08:21:29</td>
      <td>2022-09-24 10:09:28</td>
      <td>2022-09-24 09:51:13</td>
      <td>배고팡</td>
      <td>2.04</td>
      <td>앱결제</td>
      <td>user_271</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>378</th>
      <td>2022-09-08 07:43:37</td>
      <td>2022-09-08 09:14:57</td>
      <td>2022-09-08 09:43:10</td>
      <td>배고팡</td>
      <td>6.84</td>
      <td>앱결제</td>
      <td>user_80</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>493</th>
      <td>2022-09-10 03:10:01</td>
      <td>2022-09-10 04:15:17</td>
      <td>2022-09-10 04:15:16</td>
      <td>배고팡</td>
      <td>14.39</td>
      <td>앱결제</td>
      <td>user_176</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>496</th>
      <td>2022-09-07 07:03:25</td>
      <td>2022-09-07 07:20:55</td>
      <td>2022-09-07 07:44:42</td>
      <td>배고팡</td>
      <td>14.48</td>
      <td>현금</td>
      <td>user_251</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>542</th>
      <td>2022-09-21 06:37:17</td>
      <td>2022-09-21 07:53:01</td>
      <td>2022-09-21 07:34:11</td>
      <td>배고팡</td>
      <td>2.05</td>
      <td>현금</td>
      <td>user_109</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>609</th>
      <td>2022-09-29 18:05:53</td>
      <td>2022-09-29 18:37:53</td>
      <td>2022-09-29 18:29:07</td>
      <td>배고팡</td>
      <td>18.32</td>
      <td>앱결제</td>
      <td>user_81</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>617</th>
      <td>2022-09-03 22:51:54</td>
      <td>2022-09-04 00:19:47</td>
      <td>2022-09-04 00:40:53</td>
      <td>배고팡</td>
      <td>3.83</td>
      <td>현금</td>
      <td>user_285</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>683</th>
      <td>2022-09-06 17:47:22</td>
      <td>2022-09-06 18:20:15</td>
      <td>2022-09-06 18:17:21</td>
      <td>배고팡</td>
      <td>15.22</td>
      <td>카드</td>
      <td>user_499</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>754</th>
      <td>2022-09-07 00:02:05</td>
      <td>2022-09-07 01:15:59</td>
      <td>2022-09-07 00:30:49</td>
      <td>배고팡</td>
      <td>6.08</td>
      <td>카드</td>
      <td>user_56</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>761</th>
      <td>2022-09-08 21:50:58</td>
      <td>2022-09-08 23:16:36</td>
      <td>2022-09-08 23:02:46</td>
      <td>배고팡</td>
      <td>6.46</td>
      <td>앱결제</td>
      <td>user_476</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>809</th>
      <td>2022-09-27 14:20:44</td>
      <td>2022-09-27 16:10:35</td>
      <td>2022-09-27 15:47:52</td>
      <td>배고팡</td>
      <td>10.61</td>
      <td>앱결제</td>
      <td>user_62</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>810</th>
      <td>2022-09-16 09:49:08</td>
      <td>2022-09-16 11:24:05</td>
      <td>2022-09-16 11:20:27</td>
      <td>배고팡</td>
      <td>19.43</td>
      <td>현금</td>
      <td>user_211</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>815</th>
      <td>2022-09-12 12:41:40</td>
      <td>2022-09-12 14:10:41</td>
      <td>2022-09-12 13:26:20</td>
      <td>배고팡</td>
      <td>6.79</td>
      <td>앱결제</td>
      <td>user_3</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>844</th>
      <td>2022-09-22 11:33:47</td>
      <td>2022-09-22 12:50:08</td>
      <td>2022-09-22 13:20:30</td>
      <td>배고팡</td>
      <td>15.73</td>
      <td>카드</td>
      <td>user_434</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>948</th>
      <td>2022-09-27 15:02:17</td>
      <td>2022-09-27 16:37:48</td>
      <td>2022-09-27 15:42:38</td>
      <td>배고팡</td>
      <td>16.42</td>
      <td>현금</td>
      <td>user_398</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>957</th>
      <td>2022-09-13 03:25:33</td>
      <td>2022-09-13 04:44:33</td>
      <td>2022-09-13 03:49:12</td>
      <td>배고팡</td>
      <td>0.92</td>
      <td>카드</td>
      <td>user_347</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>960</th>
      <td>2022-09-29 13:00:16</td>
      <td>2022-09-29 14:11:14</td>
      <td>2022-09-29 13:56:56</td>
      <td>배고팡</td>
      <td>7.33</td>
      <td>카드</td>
      <td>user_448</td>
      <td>2022-09</td>
    </tr>
    <tr>
      <th>968</th>
      <td>2022-09-07 12:02:51</td>
      <td>2022-09-07 12:22:15</td>
      <td>2022-09-07 12:28:03</td>
      <td>배고팡</td>
      <td>15.48</td>
      <td>카드</td>
      <td>user_153</td>
      <td>2022-09</td>
    </tr>
  </tbody>
</table>
</div>


<br>

> 코드
```python
  # 해당 연-월에 배고팡 앱을 통한 주문 중 '앱 결제'로 결제된 주문의 비율
  cond3 = filtered_df['결제종류'] == '앱결제'
  result = len(filtered_df[cond3]) / len(filtered_df)
  print(round(result, 2))
```
- 필터링된 데이터 중에서 앱 결제로 된 비율을 계산하기 위해 앱 결제 빈도 수/ 전체 빈도 수를 계산하고 반올림 후 출력

> 결과
```python
  0.31
```

</details>


<br>

---

<br>

section27 시간 범위, 속도(km/h)
---
### 문제
1. 점심시간(10시부터 13시 전까지)에 주문된 배달 데이터를 찾으시오.

2. 점심시간 주문 건 중 과속(평균 속도가 50km/h 이상)하는 주문 수를 정수로 구하시오.

   - 배달시간 = 실제도착시간 - 주문시간
  
   - 속도(km/h) = 거리(km) / 시간(h)

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/delivery_time.csv')
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
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 7 columns</p>
</div>

</details>

<br>

### 힌트
```python
  dt.hour, dt.total_seconds(), 배달시간 = 실제도착시간 - 주문시간, 속도(km/h) = 거리(km) / 시간(h)
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # datetime 자료형으로 변경
  df['주문시간'] = pd.to_datetime(df['주문시간'])
  print(df['주문시간'])
  df['실제도착시간'] = pd.to_datetime(df['실제도착시간'])
  print(df['실제도착시간'])
```

> 결과
```python
  0     2023-07-26 08:05:49
  1     2022-11-07 10:21:54
  2     2023-04-18 05:00:57
  3     2023-08-18 10:46:28
  4     2023-08-11 09:58:27
                ...        
  995   2022-10-10 03:13:30
  996   2023-02-03 12:47:19
  997   2023-01-05 21:28:58
  998   2023-06-15 03:56:42
  999   2023-08-02 20:53:53
  Name: 주문시간, Length: 1000, dtype: datetime64[ns]
  
  0     2023-07-26 09:14:06
  1     2022-11-07 10:44:04
  2     2023-04-18 06:12:46
  3     2023-08-18 11:16:25
  4     2023-08-11 11:27:57
                ...        
  995   2022-10-10 04:13:48
  996   2023-02-03 13:11:46
  997   2023-01-05 21:57:41
  998   2023-06-15 04:14:24
  999   2023-08-02 22:04:06
  Name: 실제도착시간, Length: 1000, dtype: datetime64[ns]
```

<br>

> 코드
```python
  # 점심시간 주문 선택
  df['시간'] = df['주문시간'].dt.hour
  print(df['시간'])
  
  cond1 = df['시간'] >= 10
  cond2 = df['시간'] < 13
  df = df[cond1 & cond2]
  df
```
- 점심시간(10 이상, 13 미만)의 조건을 필터링

> 결과
```python
0       8
1      10
2       5
3      10
4       9
       ..
995     3
996    12
997    21
998     3
999    20
Name: 시간, Length: 1000, dtype: int32
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
      <th>시간</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
      <td>10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
      <td>10</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2023-01-19 11:32:02</td>
      <td>2023-01-19 13:10:13</td>
      <td>2023-01-19 13:24:54</td>
      <td>여기여</td>
      <td>10.04</td>
      <td>카드</td>
      <td>user_337</td>
      <td>11</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2023-02-03 11:08:34</td>
      <td>2023-02-03 12:08:07</td>
      <td>2023-02-03 11:44:14</td>
      <td>여기여</td>
      <td>18.21</td>
      <td>현금</td>
      <td>user_198</td>
      <td>11</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2022-11-03 10:05:17</td>
      <td>2022-11-03 11:25:32</td>
      <td>2022-11-03 10:52:13</td>
      <td>배달왕</td>
      <td>4.25</td>
      <td>카드</td>
      <td>user_204</td>
      <td>10</td>
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
    </tr>
    <tr>
      <th>968</th>
      <td>2022-09-07 12:02:51</td>
      <td>2022-09-07 12:22:15</td>
      <td>2022-09-07 12:28:03</td>
      <td>배고팡</td>
      <td>15.48</td>
      <td>카드</td>
      <td>user_153</td>
      <td>12</td>
    </tr>
    <tr>
      <th>973</th>
      <td>2023-07-08 12:45:17</td>
      <td>2023-07-08 13:58:27</td>
      <td>2023-07-08 14:23:47</td>
      <td>배고팡</td>
      <td>1.60</td>
      <td>카드</td>
      <td>user_322</td>
      <td>12</td>
    </tr>
    <tr>
      <th>981</th>
      <td>2023-03-08 10:51:00</td>
      <td>2023-03-08 12:29:03</td>
      <td>2023-03-08 11:54:56</td>
      <td>배고팡</td>
      <td>17.21</td>
      <td>현금</td>
      <td>user_311</td>
      <td>10</td>
    </tr>
    <tr>
      <th>994</th>
      <td>2023-02-08 12:09:03</td>
      <td>2023-02-08 13:24:56</td>
      <td>2023-02-08 13:28:54</td>
      <td>여기여</td>
      <td>12.97</td>
      <td>현금</td>
      <td>user_418</td>
      <td>12</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
<p>120 rows × 8 columns</p>
</div>


<br>

> 코드
```python
  # 속도(km/h) = 거리(km) / 시간(h)
  df['배달시간'] = df['실제도착시간'] - df['주문시간']
  print(df['배달시간'])
  
  df['배달시간'] = df['배달시간'].dt.total_seconds() / 60 / 60    # 시간 단위로 변경
  print(df['배달시간'])
  
  df['속도'] = df['거리'] / df['배달시간']
  sum(df['속도'] >= 50)
```
- 속도 계산에는 거리와 시간이 필요

  - 실제 도착 시간과 주문 시간의 차이를 시간 단위로 변경
 
- 속도(km/h) = 거리(km) / 시간(h) 계산 후 속도가 50 이상인 값의 수 찾기

> 결과
```python
  1     0 days 00:22:10
  3     0 days 00:29:57
  7     0 days 01:38:11
  18    0 days 00:59:33
  22    0 days 01:20:15
              ...      
  968   0 days 00:19:24
  973   0 days 01:13:10
  981   0 days 01:38:03
  994   0 days 01:15:53
  996   0 days 00:24:27
  Name: 배달시간, Length: 120, dtype: timedelta64[ns]
  
  1      0.369444
  3      0.499167
  7      1.636389
  18     0.992500
  22     1.337500
           ...   
  968    0.323333
  973    1.219444
  981    1.634167
  994    1.264722
  996    0.407500
  Name: 배달시간, Length: 120, dtype: float64
  
  1
```

</details>

<br>

---

<br>

section28 날짜와 시간, 문자열
---
### 문제
1. 연도와 월을 기준으로 주문 수를 집계하시오.

2. 가장 많은 주문이 있었던 연도와 월을 예시와 같은 형식으로 숫자로만 구하시오.

   - 예 : 2024년 2월인 경우 : "202402", 2024년 10월인 경우 "202410"

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/delivery_time.csv')
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
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 7 columns</p>
</div>

</details>

<br>

### 힌트
```python
  groupby().size(), dt.to_period(), idxmax(), replace()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 주문 연월 추출(연도-월)
  df['주문시간'] = pd.to_datetime(df['주문시간'])
  df['주문월'] = df['주문시간'].dt.to_period('M')
  df['주문월']
```
- 주문 월을 dt.to_period('M') 으로 추출

  - dt.month 가 아니라 dt.to_period('M') 사용하는 이유
 
    - 2022년 8월과 2023년 8월을 구분하기 위함

> 결과
```python
  0      2023-07
  1      2022-11
  2      2023-04
  3      2023-08
  4      2023-08
          ...   
  995    2022-10
  996    2023-02
  997    2023-01
  998    2023-06
  999    2023-08
  Name: 주문월, Length: 1000, dtype: period[M]
```

<br>

> 코드
```python
  # 주문 월을 기준으로 빈도 수(주문 횟수) 계산
  count_month = df.groupby('주문월').size()
  count_month
```
- 주문 월별, 주문 횟수를 groupby('주문월').size() 로 구하기

> 결과
```python
  주문월
  2022-08    29
  2022-09    95
  2022-10    79
  2022-11    81
  2022-12    94
  2023-01    82
  2023-02    70
  2023-03    73
  2023-04    88
  2023-05    83
  2023-06    86
  2023-07    83
  2023-08    57
  Freq: M, dtype: int64
```


<br>

> 코드
```python
  # 주문 횟수가 가장 많은 월의 인덱스 추출
  year_month = count_month.idxmax()
  year_month
```
- 주문 횟수가 가장 많은 연도-월의 인덱스 추출

> 결과
```python
  Period('2022-09', 'M')
```

<br>

> 코드
```python
  # 문자열로 변경 및 하이픈(-) 제거
  year_month = str(year_month)
  result = year_month.replace('-','')
  print(result)
```
- 문자열로 변경하고 문제 조건에 맞는 형식으로 변경한 후 출력

> 결과
```python
  202209
```

</details>

<br>

---

<br>

section29 함수, 월별 집계
---
### 문제
1. 배달료 계산 기준표에 따라 각 주문에 대한 배달료를 계산하시오.

2. 월별로 배달료의 총합을 집계하시오.

3. 배달료가 가장 많이 발생한 월을 찾고, 그 월의 총 배달료를 정수로 구하시오.

|거리|배달료|
|:-:|:-:|
|5km 미만|2,000원|
|5km 이상 ~ 10km 미만|4,000원|
|10km 이상 ~ 15km 미만|6,000원|
|15km 이상 ~ 20km 미만|8,000원|

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/delivery_time.csv')
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
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 7 columns</p>
</div>

</details>

<br>

### 힌트
```python
  def, apply(), dt.to_period(), df.groupby()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 배달료 계산 함수 정의
  def delivery_fee(distance):
      if distance < 5 :
          return 2000
      elif distance < 10 :
          return 4000
      elif distance < 15 :
          return 6000
      elif distance < 20 :
          return 8000
```
- 배달료 계산을 위한 함수 만들기

<br>

> 코드
```python
  # 각 주문에 대한 배달료 계산
  df['배달료'] = df['거리'].apply(delivery_fee)
  df['배달료']  
```
- apply() 를 통해 주문별 배달료 계산 후 새로운 컬럼에 배달료 저장

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
      <th>배달료</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
      <td>4000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
      <td>6000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
      <td>6000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
      <td>6000</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
      <td>8000</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
      <td>4000</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
      <td>4000</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
      <td>4000</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 8 columns</p>
</div>


<br>

> 코드
```python
  # 월별로 배달료 총집합 집계
  df['주문시간'] = pd.to_datetime(df['주문시간'])
  period_M = df['주문시간'].dt.to_period('M')
  monthly = df.groupby(period_M)['배달료'].sum()
  monthly
```
- groupby() 활용해 월별로 배달료의 총합 집계

> 결과
```python
  주문시간
  2022-08    152000
  2022-09    446000
  2022-10    388000
  2022-11    384000
  2022-12    442000
  2023-01    386000
  2023-02    340000
  2023-03    408000
  2023-04    410000
  2023-05    420000
  2023-06    448000
  2023-07    434000
  2023-08    292000
  Freq: M, Name: 배달료, dtype: int64
```

<br>

> 코드
```python
  # 가장 많은 배달료가 발생한 월
  max_fee_month = monthly.idxmax()
  max_fee_month
```
- idxmax() 로 가장 많은 배달료가 발생한 월 찾기

> 결과
```python
  Period('2023-06', 'M')
```


<br>

> 코드
```python
  # 그 월의 총 배달료 찾기
  max_fee_value = monthly[max_fee_month]
  max_fee_value
```
- 인덱스(연도-월)로 월별 집계된 배달료 찾기

> 결과
```python
  448000
```

</details>

<br>

---

<br>

section30 주말, 평일 구분
---
### 문제
1. 주말 주문 건수와 평일 주문 건수를 구하시오. 

2. 주말 주문 건수와 평일 주문 건수의 차이를 절대값으로 구하고 정수형으로 구하시오.

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/delivery_time.csv')
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
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 7 columns</p>
</div>

</details>

<br>

### 힌트
```python
  dt.dayofweek
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 주말/평일 구분
  # 0 : 월, 1: 화, 2: 수, 3: 목, 4: 금, 5: 토, 6: 일
  df['주문시간'] = pd.to_datetime(df['주문시간'])
  df['dayofweek'] = df['주문시간'].dt.dayofweek
  df['주말'] = df['dayofweek'] >= 5
  df
```
- dt.dayofweek 사용해 해당 날짜의 요일을 숫자로 변경한 값 구하기

- 주말 여부를 파악하려면 숫자가 5 또는 6 인지 확인

  - df['dayofweek'] >= 5 조건을 사용해 참이면 주말 컬럼에 True, 거짓이면 False 대입

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
      <th>dayofweek</th>
      <th>주말</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
      <td>2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
      <td>4</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
      <td>4</td>
      <td>False</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
      <td>4</td>
      <td>False</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
      <td>2</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 9 columns</p>
</div>

<br>

> 코드
```python
  # 주말 개수, 평일 개수 계산
  weekend = sum(df['주말'])
  print(weekend)
  
  weekday = sum(~df['주말'])
  print(weekday)
```
- 주말과 평일의 행(레코드) 개수 구하기

> 결과
```python
  294
  706
```


<br>

> 코드
```python
  # 차이 절댓값 출력
  print(abs(weekend - weekday))
```
- 차이를 절대값으로 계산해 출력

> 결과
```python
  412
```

</details>

<br>

---

<br>

section31 문자열, 형 변환
---
### 문제
1. 'user' 컬럼에서 user 뒤에 있느 숫자 값만 추출하시오.

2. 추출된 숫자 값을 모두 합한 값을 정수로 구하시오.

<br>

```python
  import pandas as pd
  df = pd.read_csv('./data/delivery_time.csv')
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
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 7 columns</p>
</div>

</details>

<br>

### 힌트
```python
  str[:], astype()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python
  # 문자 슬라이싱
  df['user_int'] = df['user'].str[5:]
  df
```
- 특정 컬럼에서 행별로 user 뒷부분만 슬라이싱하기 위해 .str[구간] 설정

  - .str[5:] 5번째 인덱스부터 끝까지

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>주문시간</th>
      <th>실제도착시간</th>
      <th>예상도착시간</th>
      <th>앱종류</th>
      <th>거리</th>
      <th>결제종류</th>
      <th>user</th>
      <th>user_int</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2023-07-26 08:05:49</td>
      <td>2023-07-26 09:14:06</td>
      <td>2023-07-26 08:39:42</td>
      <td>여기여</td>
      <td>1.93</td>
      <td>카드</td>
      <td>user_275</td>
      <td>275</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-11-07 10:21:54</td>
      <td>2022-11-07 10:44:04</td>
      <td>2022-11-07 10:50:15</td>
      <td>배고팡</td>
      <td>5.19</td>
      <td>카드</td>
      <td>user_360</td>
      <td>360</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2023-04-18 05:00:57</td>
      <td>2023-04-18 06:12:46</td>
      <td>2023-04-18 05:32:53</td>
      <td>배고팡</td>
      <td>13.85</td>
      <td>카드</td>
      <td>user_36</td>
      <td>36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2023-08-18 10:46:28</td>
      <td>2023-08-18 11:16:25</td>
      <td>2023-08-18 11:08:33</td>
      <td>배고팡</td>
      <td>10.90</td>
      <td>앱결제</td>
      <td>user_65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2023-08-11 09:58:27</td>
      <td>2023-08-11 11:27:57</td>
      <td>2023-08-11 10:51:57</td>
      <td>여기여</td>
      <td>14.96</td>
      <td>카드</td>
      <td>user_176</td>
      <td>176</td>
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
    </tr>
    <tr>
      <th>995</th>
      <td>2022-10-10 03:13:30</td>
      <td>2022-10-10 04:13:48</td>
      <td>2022-10-10 04:15:37</td>
      <td>배고팡</td>
      <td>1.79</td>
      <td>현금</td>
      <td>user_186</td>
      <td>186</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2023-02-03 12:47:19</td>
      <td>2023-02-03 13:11:46</td>
      <td>2023-02-03 13:12:57</td>
      <td>배고팡</td>
      <td>15.55</td>
      <td>카드</td>
      <td>user_239</td>
      <td>239</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2023-01-05 21:28:58</td>
      <td>2023-01-05 21:57:41</td>
      <td>2023-01-05 21:57:44</td>
      <td>배고팡</td>
      <td>8.33</td>
      <td>현금</td>
      <td>user_264</td>
      <td>264</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2023-06-15 03:56:42</td>
      <td>2023-06-15 04:14:24</td>
      <td>2023-06-15 04:18:38</td>
      <td>여기여</td>
      <td>8.20</td>
      <td>앱결제</td>
      <td>user_229</td>
      <td>229</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2023-08-02 20:53:53</td>
      <td>2023-08-02 22:04:06</td>
      <td>2023-08-02 22:09:22</td>
      <td>여기여</td>
      <td>5.33</td>
      <td>카드</td>
      <td>user_148</td>
      <td>148</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 8 columns</p>
</div>

<br>

> 코드
```python
  # 자료형 변환
  df['user_int'] = df['user_int'].astype(int)
  df['user_int']
```
- astype() 활용해 문자열(str)을 정수(int) 자료형을 변경

> 결과
```python
  0      275
  1      360
  2       36
  3       65
  4      176
        ... 
  995    186
  996    239
  997    264
  998    229
  999    148
  Name: user_int, Length: 1000, dtype: int32
```


<br>

> 코드
```python
  # 합계
  print(df['user_int'].sum())
```
- 정수형으로 변경된 데이터의 총합 출력

> 결과
```python
  261387
```

</details>

<br>

---

<br>











