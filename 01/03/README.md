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
  fillna(), sort_values(), iloc[], sum()
```

<br>

<details>
  <summary>풀이</summary>

<br>

> 코드
```python

```

> 결과


<br>

> 코드
```python

```

<br>

> 코드
```python

```

> 결과
```python

```

</details>

<br>

---

<br>























