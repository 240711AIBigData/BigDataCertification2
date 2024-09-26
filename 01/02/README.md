# CHAPTER2 판다스(pandas)
- 데이터 분석을 위한 파이썬 라이브러리

- 파이썬에서 데이터를 만들고 수정하고 정렬하고 채우고 집계하고 분석하는 것을 쉽게 할 수 있음

<br>

SECTION01 데이터프레임(DataFrame)과 시리즈(Series)
---
> 시리즈는 1차원 형태, 데이터프레임은 행(rows)과 열(columns)이 있는 2차원(표) 형태

<br>

### 01. 행과 열
- 행 : 각 데이터/레코드(가로)

- 열 : 컬럼 전체(세로)

- 판다스에서 축(axis)을 숫자로 나타낼 때, 행은 0, 열은 1로 표시

  - "행(0)렬(1)"로 기억

<br>

### 02. 판다스 별칭
- pd 라는 별칭(alias, 줄여서 as)으로 사용
```python
  import pandas as pd
```

<Br>

### 03. 시리즈(Series)
- pd.Series(데이터) 로 생성 가능

  - 데이터는 리스트를 활용해 만들 수 있음
 
- 출력해보면 인덱스와 값이 출력되고, 자료형은 'object'

  - 판다스에서 object형은 주로 문자열 데이터를 나타내는데 사용

- 숫자를 리스트 형태로 만든 후 pd.Series()로 감싸면 시리즈로 변경

  - 시리즈 값의 자료형(타입)은 int
 
- 판다스는 리스트에 포함된 데이터 타입을 기반으로 시리즈의 데이터 타입을 자동으로 결정


```python
  menu = pd.Series(['아메리카노', '카페라떼', '카페모카'])
  menu
```

> 결과
```python
  0    아메리카노
  1     카페라떼
  2     카페모카
  dtype: object
```

<br>

```python
  price = pd.Series([4500, 5000, 5500])
  price
```

> 결과
```python
  0    4500
  1    5000
  2    5500
  dtype: int64
```

<br>

#### 💡 int 뒤의 숫자는?
```python
    비트(bit) 수
    2의 64승인 매우 큰 정수 범위 표현 가능
    비트 수를 변경해 데이터 용량을 줄이기도 함
```

<br>

### 04. 데이터프레임(DataFrame)
- pd.DataFrame({"컬럼명":데이터}) 로 생성 가능

  - 소괄호 안에 중괄호로 묶여 있음
 
  - 컬럼명의 "menu"는 문자(따옴표 있음) 그 자체, 데이터의 menu는 변수명(따옴표 없음)

```python
  pd.DataFrame({
    "menu" : menu,
    "price" : price
  })
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>menu</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
    </tr>
  </tbody>
</table>
</div>

- 데이터프레임을 만들 때 시리즈를 꼭 거치지 않아도 ok

  - 데이터프레임을 담는 변수명은 DataFrame의 약자인 df를 주로 사용
 
```python
  df = pd.DataFrame({
    "메뉴" : ['아메리카노', '카페라떼', '카페모카'],
    "가격" : [4500, 5000, 5500],
    "원두" : ["케냐", "콜롬비아", "케냐"]
  })

  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>원두</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>케냐</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>케냐</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 05. 컬럼 선택
- df['컬럼명'] or df["컬럼명"] : 데이터프레임에서 특정 컬럼만 선택해 표시

  - 1개의 컬럼명만 선택하면 시리즈 형태로 출력
 
```python
  print(df['메뉴'])
  type(df['메뉴'])
```

> 결과
```python
  0    아메리카노
  1     카페라떼
  2     카페모카
  Name: 메뉴, dtype: object

  pandas.core.series.Series
```

<br>

#### 💡 데이터프레임에서 컬럼명 선택 시 주의사항
- df['컬럼명'] 외에도 df.컬럼명 처럼 '.'를 사용하는 방법도 있지만 권장 X

  - 컬럼명에 공백이 있으면 에러 발생 가능성 有
 
<br>

### 06. 데이터프레임과 시리즈 자료형
- 데이터프레임에서 특정 컬럼 1개만 선택하면 시리즈 형태

- 1개의 컬럼을 시리즈 형태가 아닌 데이터프레임으로 필요할 경우

  - 한번 더 [대괄호]로 묶어주기
 
- 복수의 컬럼을 선택할 때는 대괄호 2개 사용

  - 결과는 데이터프레임 자료형

- 컬럼을 복수로 선택할 때는 주로 리스트 활용

  - 변수에 컬럼명을 담고 df[변수] 실행시, 변수에 있는 컬럼이 선택되어 데이터프레임 출력
 
  - 대괄호가 하나처럼 보이지만 df[['컬럼1', '컬럼2']]와 동일
 
```python
  print(df[['메뉴']])
  type(df[['메뉴']])
```

> 결과
```python
        메뉴
  0  아메리카노
  1   카페라떼
  2   카페모카
  
  pandas.core.frame.DataFrame
```

<br>

```python
  print(df[['메뉴', '가격']])
  type(df[['메뉴', '가격']])
```

> 결과
```python
        메뉴    가격
  0  아메리카노  4500
  1   카페라떼  5000
  2   카페모카  5500

  pandas.core.frame.DataFrame
```

<br>

```python
  cols = ['메뉴', '가격']
  print(df[cols])
  type(df[cols])
```

> 결과
```python
        메뉴    가격
  0  아메리카노  4500
  1   카페라떼  5000
  2   카페모카  5500

  pandas.core.frame.DataFrame
```

<br>

#### 💡 정리
|구분|반환된 자료형|설명|예|
|:-:|:-:|:-:|:-:|
|df[]|시리즈|1개 컬럼 선택|df['컬럼1']|
|df[[]]|데이터프레임|1개 이상의 컬럼 선택|df[['컬럼1']]<br>df[['컬럼1', '컬럼2']]|

<br>

### 07. 자료형 비교
- type() 함수로 자료형 확인 가능

  - df : 데이터프레임
 
  - df['컬럼명'] : 시리즈
 
  - df[['컬럼명']] " 데이터프레임
 
- 머신러닝(작업형2)에서 입력 데이터로 특정 컬럼을 데이터프레임으로 넣어야 할 때 활용

```python
  print('df          : ', type(df))
  print("df['가격']   : ", type(df['가격']))
  print("df[['가격']] : ", type(df[['가격']]))
```

> 결과
```python
  df          :  <class 'pandas.core.frame.DataFrame'>
  df['가격']   :  <class 'pandas.core.series.Series'>
  df[['가격']] :  <class 'pandas.core.frame.DataFrame'>
```

<br>

---

<br>

SECTION02 데이터 저장 및 불러오기
---
> 예제 데이터 생성
```python
  import pandas as pd

  # 예제 데이터 생성
  df = pd.DataFrame({
      '메뉴' : ['아메리카노', '카페라떼', '카페모카', '카푸치노', '에스프레소', '밀크티', '녹차'],
      '가격' : [4500, 5000, 5500, 5000, 4000, 5900, 5300],
      '칼로리' : [10, 110, 250, 110, 20, 210, 0]
  })

  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
    </tr>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
    </tr>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 01. csv로 저장
- df.to_csv('파일명.csv') : 데이터프레임을 csv 파일로 저장

```python
  df.to_csv('./data/temp.csv')
```

<br>

### 02. csv 불러오기
- pd.read_csv('파일명') ㅣ csv 데이터 불러오기

- 출력 결과에 나타나는 'Unnamed: 0' 컬럼

  - 데이터를 저장할 때 기본 설정으로 기존 인덱스가 값으로 함께 저장된 것
 
- 가장 왼쪽에 있는 인덱스는 pd.read_csv()로 데이터를 불러올 때 새로 생성된 인덱스

```python
  temp_df = pd.read_csv('./data/temp.csv')
  temp_df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 03. csv 저장 옵션
- index = Flase : 인덱스를 제외하고 저장

  - 작업형2의 필수 사용 기능
 
```python
  df.to_csv('./data/cafe.csv', index = False)
  df = pd.read_csv('./data/cafe.csv')
  df.head()
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 04. 데이터 불러오기 옵션
- 데이터를 불러올 때 사용하는 판다스의 read_csv() 함수는 주요 파라미터

#### (1) index_col
- 인덱스로 사용할 컬럼명 또는 열의 번호 지정

```python
  pd.read_csv('data.csv', index_col = '컬럼명')
  pd.read_csv('data.csv', index_col = 0)
```

<br>

#### (2) usecols
- 불러올 컬럼명 또는 열의 번호 지정

```python
  pd.read_csv('data.csv', usecols = ['컬럼명1', '컬럼명2', ...])
  pd.read_csv('data.csv', usecols = [열 번호1, 열 번호2, ...])
```

<br>

#### (3) parse_dates
- 컬럼명 지정시 문자열로 된 컬럼을 날짜 datetime으로 변경 가능 (=파싱, parsing)

```python
  pd.read_csv('data.csv', parse_dates = ['컬럼명'])
```

<br>

#### (4) encoding
- 일반적으로 판다스의 기본 인코딩 방식은 'UTF-8'

  - 한국어가 포함된 텍스트 파일이 UTF-8이 아닌 경우 글자가 깨는 현상 발생
 
    - 데이터를 불러올 때 'cp949' or 'euc-kr' 설정
   
```python
  pd.read_csv('data.csv', encoding = 'cp949')
  pd.read_csv('data.csv', encoding = 'euc-kr')
```

<br>

---

<br>

SECTION03 탐색적 데이터 분석(EDA, Exploratory Data Analysis)
---
- 데이터를 탐색하고 이해하기 위해 수행

- 일반적으로 데이터는 한 눈에 관찰 불가

  - EDA 과정을 통해 데이터를 다양한 각도에서 관찰하고 이해해야 함
 
  - 결측치, 이상치, 패턴, 변수 파악 등 데이터 전처리 하기 전 데이터에 대한 이해를 돕는 단계
 
- 주로 시각화 많이 사용

  - 다만, 빅분기 실기 환경에서는 시각화 지원 X
 
<br>

### 01. 데이터프레임 샘플 확인
- 데이터프레임의 일부 확인

  - head(N)
 
    - 데이터프레임의 상위 N개 행 반환
   
    - N은 양의 정수로 기본값은 5
   
    - 데이터를 불러온 후 가장 많이 사용하는 함수(메소드)
 
  - tail(N)
 
    - 데이터프레임의 하위 N개 행 반환
   
    - N은 양의 정수로 기본값은 5
 
  - sample(N)
 
    - 데이터프레임에서 임의로 샘플링해 N개 행 반환
   
    - N은 양의 정수로 기본값은 1
   
    - head, tail 과는 달리, 실행할 때마다 다른 결과를 샘플링

```python
  df.head(2)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  df.tail(3)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
    </tr>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
    </tr>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  df.sample(3)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 02. 데이터프레임의 크기
- df.shape : 전체 데이터의 크기 확인

  - 뒤에 괄호가 없는 속성을 가짐

```python
  df.shape
```

> 결과
```python
  (7, 3)
```

<br>

#### 💡 속성과 함수(메소드)
- shape : 데이터프레임의 속성이어서 괄호 X

- head(), tail() : 함수(메소드) 형태라서 괄호 O

<br>

### 03. 컬럼별 자료형
- info() : 데이터프레임 안 컬럼의 자료형(type) 확인

  - Dtype
 
    - object : 문자
   
    - int : 숫자
   
  - int or float 뒤의 숫자 : 비트 

```python
  df.info()
```

> 결과
```python
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 7 entries, 0 to 6
  Data columns (total 3 columns):
   #   Column  Non-Null Count  Dtype 
  ---  ------  --------------  ----- 
   0   메뉴      7 non-null      object
   1   가격      7 non-null      int64 
   2   칼로리     7 non-null      int64 
  dtypes: int64(2), object(1)
  memory usage: 300.0+ bytes
```

<br>

### 04. 상관관계
- corr() : 상관관계 확인

```python
  df.corr(numeric_only = True)
```

> 결과
```python
  	가격	칼로리
  가격	1.000000	0.713227
  칼로리	0.713227	1.000000
```
▲ 가격과 칼로리는 0.7의 양의 상관관계

<br>

#### 💡 코랩에서 발생하는 에러와 해결방법
- 데이터프레임에 숫자형과 문자형 컬럼이 혼합되어 있을 때

  - corr(), mean(), sum() 등 함수 사용시 에러 발생
 
    - 문자열 데이터를 숫자로 변환할 수 없기 때문

```python
  # 에러 예
  ValueError : Could not convert string to float: '아메리카노'
```

<br>

- 해결방법

  - 해당 함수에 numeric_only = True 옵션 추가
 
    - 함수가 숫자형 데이터에만 적용되도록 함
   
  - ex
 
    - 상관계수 계산시
   
      - 코랩 환경 : corr(numeric_only = True)
     
      - 시험 환경 : corr()

```python
  df.corr(numeric_only = True)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>가격</th>
      <td>1.000000</td>
      <td>0.713227</td>
    </tr>
    <tr>
      <th>칼로리</th>
      <td>0.713227</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 05. 범주형 데이터 탐색
```python
  # 자동차의 종류와 크기를 나타낸 중복 값이 있는 데이터
  df_car = pd.DataFrame({
      'car' : ['Sedan', 'SUV', 'Sedan', 'SUV', 'SUV', 'SUV', 'Sedan', 'Sedan', 'Sedan', 'Sedan', 'Sedan'],
      'size' : ['S', 'M', 'S', 'S', 'M', 'M', 'L', 'S', 'S', 'M', 'S']
  })
  df_car.head(3)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>car</th>
      <th>size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sedan</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SUV</td>
      <td>M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sedan</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 06. 고유한 값의 개수
- nunique() : 데이터프레임에서 컬럼별로 고유한 값의 개수 확인

  - 종류의 수는 파악 가능하지만, 어떤 데이터인지는 확인 불가

```python
  df_car.nunique()
```

> 결과
```python
  car     2
  size    3
  dtype: int64
```

#### (1) 고유한 값
- unique() : 고유한 값(구체적인 항목) 파악

```python
  print(df_car['car'].unique())
  print(df_car['size'].unique())
```

> 결과
```python
  ['Sedan' 'SUV']
  ['S' 'M' 'L']
```

<br>

#### (2) 고유한 값과 개수
- value_counts() : 고유한 값과 개수(nunique()와 unique() 결과 내용 한번에 파악)

  - 항목별로 개수를 출력해 데이터 탐색하는데 유용함

```python
  print(df_car['car'].value_counts())
  print(df_car['size'].value_counts())
```

> 결과
```python
  car
  Sedan    7
  SUV      4
  Name: count, dtype: int64
  size
  S    6
  M    4
  L    1
  Name: count, dtype: int64
```

<br>

#### 💡 value_counts()
- 작업형2에서 빈번하게 사용

- 주로 시리즈(데이터프레임 특정 컬럼)에 적용

  - 데이터프레임에서 특정 컬럼 1개만 선택하면 시리즈 형태
 
- df['컬럼명'].value_counts()

- 판다스 1.1.0 이상에서는 데이터프레임에도 df.value_counts() 사용 가능

  - 결과 보기가 불편하므로 시리즈에서 사용하기를 추천함

<br>

#### (3) 기술통계
- describe() : 데이터의 기술통계량 확인

  - 기본적으로 수치형 데이터(int, float)만 적용해 기술통계 결과 확인 가능
 
    - count : 값이 있는 데이터 수
   
    - mean : 평균
   
    - std : 표준편차
   
    - min : 최솟값
   
    - 00% : 백분위수에서 00%
   
    - max : 최댓값

- 실습시 변수 활용 관련
  
  - 수치형 데이터를 확인할 때 : 기존에 사용했던 df 변수 활용
 
  - 범주형 데이터를 확인할 때 : 새로 만들었던 df_car 변수 활용

```python
  df.describe()
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>7.000000</td>
      <td>7.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>5028.571429</td>
      <td>101.428571</td>
    </tr>
    <tr>
      <th>std</th>
      <td>631.702160</td>
      <td>99.402980</td>
    </tr>
    <tr>
      <th>min</th>
      <td>4000.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>4750.000000</td>
      <td>15.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>5000.000000</td>
      <td>110.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>5400.000000</td>
      <td>160.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>5900.000000</td>
      <td>250.000000</td>
    </tr>
  </tbody>
</table>
</div>

<br>

#### (4) 기술통계(object 자료형)
- include 파라미터 활용 : 데이터 타입이 object인 기술통계 확인

  - "O"(대문자) or "object" 입력
 
    - count : 값이 있는 데이터 수
   
    - unique : 고유한 데이터 수(종류)
   
    - top : 가장 많이 나오는 값(최빈값)
   
    - freq : 가장 많이 나오는 값의 빈도 수

```python
  df_car.describe(include = 'O')
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>car</th>
      <th>size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>11</td>
      <td>11</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>top</th>
      <td>Sedan</td>
      <td>S</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>7</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  df.describe(include = 'object')
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>7</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>7</td>
    </tr>
    <tr>
      <th>top</th>
      <td>아메리카노</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>

▲ '메뉴' 컬럼 데이터 전체가 고유값을 가졌기 때문에 top과 freq는 큰 의미 X

<br>

---

<br>

SECTION04 자료형 변환
---
- 판다스에서 주로 볼 수 있는 자료형 : int(정수), float(실수), object(문자)

  - 문제 상황에 따라 문자를 숫자로 변환하거나 실수형을 정수형으로 변환

<br>

> 가격은 float형, 칼로리는 object형인 예제 데이터 생성
```python
  import pandas as pd
  
  # 가격은 float형, 칼로리는 object형인 예제 데이터 생성
  data = {
      '메뉴' : ['아메리카노', '카페라떼', '카페모카', '카푸치노', '에스프레소', '밀크티', '녹차'],
      '가격' : [4500.0, 5000.0, 5500.0, 5000.0, 4000.0, 5900.0, 5300.0],
      '칼로리' : ['10', '110', '250', '110', '20', '210', '0']
  }
  df = pd.DataFrame(data)
  df.info()
```

> 결과
```python
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 7 entries, 0 to 6
  Data columns (total 3 columns):
   #   Column  Non-Null Count  Dtype  
  ---  ------  --------------  -----  
   0   메뉴      7 non-null      object 
   1   가격      7 non-null      float64
   2   칼로리     7 non-null      object 
  dtypes: float64(1), object(2)
  memory usage: 300.0+ bytes
```

<br>

### 01. int로 변환
- astype('변경할 자료형')

```python
  df['가격'] = df['가격'].astype('int')
  df.info()
```

> 결과
```python
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 7 entries, 0 to 6
  Data columns (total 3 columns):
   #   Column  Non-Null Count  Dtype 
  ---  ------  --------------  ----- 
   0   메뉴      7 non-null      object
   1   가격      7 non-null      int32 
   2   칼로리     7 non-null      object
  dtypes: int32(1), object(2)
  memory usage: 272.0+ bytes
```

<br>

### 02. float로 변환
- object 자료형을 float 자료형으로 변경

  - object가 정수형으로 변경 가능한 데이터라면 문제 x
 
  - object가 문자형 데이터라면 에러 발생
 
```python
  df['칼로리'] = df['칼로리'].astype('float')
  df.info()
```

> 결과
```python
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 7 entries, 0 to 6
  Data columns (total 3 columns):
   #   Column  Non-Null Count  Dtype  
  ---  ------  --------------  -----  
   0   메뉴      7 non-null      object 
   1   가격      7 non-null      int32  
   2   칼로리     7 non-null      float64
  dtypes: float64(1), int32(1), object(1)
  memory usage: 272.0+ bytes
```

<br>

---

<br>

SECTION05 새로운 컬럼 추가
---
> cafe.csv 데이터프레임 불러오기
```python
import pandas as pd

df = pd.read_csv('./data/cafe.csv')
df.head(2)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 01. 새로운 컬럼 추가
-  df['새 컬럼명']
```python
  df['new'] = 0
  df.head(2)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>new</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 02. 기존 컬럼을 사용한 계산
```python
  # 새로운 컬럼에 메뉴별 정상가에서 20% 할인한 금액 대입
  discount = 0.2
  df['할인가'] = df['가격'] * (1 - discount)
  df.head(2)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>new</th>
      <th>할인가</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>0</td>
      <td>3600.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>0</td>
      <td>4000.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

---

<br>

SECTION06 데이터 삭제
---
- 축(axis) : 데이터의 방향을 나타매녀 0과 1의 두 가지 값 사용

  - axis = 0 : 행(row) - 특정 행을 삭제하고 싶을 때
 
  - axis = 1 : 열(column) - 특정 열을 삭제하고 싶을 때

```python
  import pandas as pd
  
  df = pd.read_csv('./data/cafe.csv')
  df.head(3)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
    </tr>
  </tbody>
</table>
</div>

<br>

#### 💡 행 또는 열 삭제시 주의사항
- 행 또는 열을 삭제하는 코드(셸) 실행 후 재실행시 에러 발생

  - 행 : "KeyError: ['인덱스'] not found in axis"
 
  - 열 : "KeyError: ['컬럼명'] not found in axis"

  - 위 에러 내용은 이미 삭제했기 때문에 특정 컬럼명(인덱스)를 찾을 수 없다는 의미
 
- 현재 셀부터 다시 실행하고 싶다면 "런타임 → 이전 셀 실행"

  - 처음부터 현재 셀 이전까지 모두 실행
 
<br>

### 01. 행 삭제
- DataFrame.drop('index명', axis = 0)

  - 삭제된 결과값이 자동 저장되지는 않음
 
  - 저장하는 방법으로 drop에 있는 inplace 파라미터 활용
 
    - False :  기본값, drop 결과값 저장 X
   
    - True : drop 결과값 저장 O

```python
  df.drop(1, axis = 0, inplace = True)
  df.head(3)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 02. 컬럼(열) 삭제
- DataFrame.drop('컬럼명', axis = 1)

  - inplace 대신 대입(=) 연산자로 결과 저장 가능

```python
  df = df.drop('칼로리', axis = 1)
  df.head(3)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 03. 삭제 후 저장 방법
- inplace 사용시 반환값 X, 사용하지 않으면 반환값으로 대입 가능

  - 함께 사용 불가
 
<br>

|구분|예|반환값|
|:-:|:-:|:-:|
|inplace 활용|df.drop('가격', axis=1, inplace=True)|없음|
|대입 연산자 활용|df = df.drop('가격', axis=1)|있음|

<br>

#### 💡 삭제 전후의 데이터 크기 확인
- 삭제할 때는 실수를 방지하기 위해 삭제 전후의 데이터 크기를 df.shape로 확인

```python
  df.shape  # 삭제 전
  df.drop(1, axis = 0, inplace = True)  # 행 또는 열 삭제 코드
  df.shape  # 삭제 후
```

<br>

---

<br>

SECTION07 인덱싱/슬라이싱(loc)
---
- 인덱스로 값을 찾거나 슬라이싱으로 특정 영역 추출

> cafe.csv 데이터프레임 불러오기

```python
  import pandas as pd
  
  df = pd.read_csv('./data/cafe.csv')
  df.head(2)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 01. 인덱싱
- df.loc[인덱스명] : 해당 인덱스 데이터에 접근

  - loc는 location의 약자로 인덱스명 또는 컬럼명을 통해 데이터에 접근
 
  - 인덱스명이 숫자(loc[숫자]) : 그대로 작성
  
  - 인덱스명이 문자(loc['문자']) : 따옴표로 묶기

- df.loc[인덱스명, 컬럼명] : 특정 행과 특정 컬럼(열)의 교차점에 있는 단일값 출력

```python
  df.loc[0]
```

> 결과
```python
  메뉴     아메리카노
  가격      4500
  칼로리       10
  Name: 0, dtype: object
```

<br>

```python
  df.loc[1, '가격']
```

> 결과
```python
  5000
```

<br>

### 02. 슬라이싱
- loc[행 범위 또는 특정 행, 컬럼(열)의 범위 또는 특정 컬럼]

  - 범위 : '시작 인덱스:끝 인덱스'
 
    - 시작 인덱스 생략시 처음부터
   
    - 끝 인덱스 생략시 마지막까지
   
    - 시작 인덱스와 끝 인덱스 모두 생략 : 전체
   
  - 특정 컬럼을 선택해 슬라이싱하고 싶으면 컬럼을 리스트 형태로 작성

```python
  df.loc[:, '가격']
```

> 결과
```python
  0    4500
  1    5000
  2    5500
  3    5000
  4    4000
  5    5900
  6    5300
  Name: 가격, dtype: int64
```

<br>

```python
  df.loc[2, '메뉴':'칼로리']
```

> 결과
```python
  메뉴     카페모카
  가격     5500
  칼로리     250
  Name: 2, dtype: object
```

<br>

```python
  df.loc[2, ['메뉴', '칼로리']]
```

> 결과
```python
  메뉴     카페모카
  칼로리     250
  Name: 2, dtype: object
```

<br>

```python
  df.loc[1:3, '메뉴':'가격']
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
    </tr>
  </tbody>
</table>
</div>

<br>

---

<br>

SECTION08 인덱싱/슬라이싱(iloc)
---
- df.iloc[]

  - iloc는 interger location의 약자
 
  - 데이터프레임의 행이나 열의 순서에 따른 인덱스 번호로 값 슬라이싱

<br>

> cafe.csv 데이터 불러와 인덱스가 0인 첫 번째 행 삭제
```python
  import pandas as pd
  
  df = pd.read_csv('./data/cafe.csv')
  df.drop(0, axis = 0, inplace = True)    # 첫 번째 행 삭제
  df.head(2)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 01. 인덱싱
- iloc에서 대괄호 안의 숫자는 순서를 의미

  - 0은 첫 번째 행(또는 컬럼), 1은 두 번째 행(또는 컬럼)
 
  - 비교 : loc에서 대괄호는 인덱스명을 의미해 순서가 변경되더라도 상관X

- cafe.csv 데이터에서 카페라떼 선택하는 방법

  - loc[1, '메뉴']
 
  - iloc[0, 0]

```python
  df.iloc[0]
```

> 결과
```python
  메뉴     카페라떼
  가격     5000
  칼로리     110
  Name: 1, dtype: object
```

<br>

### 02. 슬라이싱
- 특정 컬럼 값만 출력할 때도 인덱스 번호 활용

- iloc[행 인덱싱, 열 슬라이싱] : 1개의 행과 2개의 열을 추출할 때

  - 슬라이싱 범위 : 마지막 인덱스 번호 앞까지 결과 반환

- iloc 대괄호 안에 번위가 1개만 있다면 행 인덱스 범위

  - 컬럼 범위는 전체를 의미
 
  - df.iloc[1:3] 과 결과가 같음

```python
  df.iloc[:, 1]
```

> 결과
```python
  1    5000
  2    5500
  3    5000
  4    4000
  5    5900
  6    5300
  Name: 가격, dtype: int64
```

<br>

```python
  df.iloc[2, 0:2]
```

> 결과
```python
  메뉴    카푸치노
  가격    5000
  Name: 3, dtype: object
```

<br>

```python
  df.iloc[1:3]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> loc로 위와 같은 결과 출력해보기
```python
  df.loc[2:3, '메뉴':'칼로리']    # 컬럼 범위는 전체이므로 생략 가능
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
    </tr>
  </tbody>
</table>
</div>

<br>

#### 💡 loc와 iloc 범위 차이
|구분|방식|범위|예시|
|:-:|:-:|:-:|:-:|
|loc|인덱스명, 컬럼명|끝 인덱스 포함|[0:2] 일 때 2 포함<br>(0, 1, 2 선택)|
|iloc|인덱스 번호(위치 숫자),<br>컬럼 번호(위치 숫자)<br>*번호는 0부터 시작|끝 인덱스 포함 X<br>(끝 인덱스 - 1)|[0:2] 일 때 2 미포함<br>(0, 1 선택)|

<br>

---

<br>

SECTION09 데이터 추가/변경
---
> cafe.csv 데이터프레임 불러오기

```python
  import pandas as pd
  
  df = pd.read_csv('./data/cafe.csv')
  df.head(2)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
    </tr>
  </tbody>
</table>
</div>

<br>

#### 💡 넘파이(numpy)
- 판다스와 같은 파이썬 라이브러리

- 판다스보다 빠르게 수치 연산

- 연산량이 많은 딥러닝에서 주로 활용

<br>

### 01. 결측치(NaN) 대입
- NaN(Not a Number) : '값 없음' 의미, 결측치

  - 넘파이 라이브러리를 통해 만들 수 있음
 
```python
  import numpy as np
  
  df['원산지'] = np.nan
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 02. loc를 활용한 값 변경
- 특정 위치에 값 대입

  - loc[인덱스명(범위), 컬럼명(범위)] : 작업형1에서 특정 컬럼 범위의 값을 대체할 때 사용

```python
  df.loc[0, '원산지'] = '콜롬비아'
  df.loc[2:3, '원산지'] = '과테말라'
  df.head(4)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
      <td>과테말라</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 03. loc를 활용한 값 추가
- 새로운 데이터 행(row) 추가

  - loc의 대괄호 안에 새 인덱스명을 넣고 값 대입
 
    - 인덱스명은 숫자, 문자 둘 다 가능

```python
  df.loc['시즌'] = ['크리스마스라떼', 6000, 300, '한국']
  df.tail(3)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>시즌</th>
      <td>크리스마스라떼</td>
      <td>6000</td>
      <td>300</td>
      <td>한국</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 04. loc와 딕셔너리를 활용한 값 추가
- 리스트가 아닌 딕셔너리 형태로도 새로운 데이터 행(row) 추가 가능

  - 리스트 : 반드시 행의 컬럼 수와 리스트의 데이터 수 일치
 
  - 딕셔너리 : 특정 컬럼이 없다면 결측치(NaN)로 입력됨

```python
  df.loc[7] = {'메뉴':'딸기라떼', '가격':5700, '칼로리':280}
  df.tail(3)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>시즌</th>
      <td>크리스마스라떼</td>
      <td>6000</td>
      <td>300</td>
      <td>한국</td>
    </tr>
    <tr>
      <th>7</th>
      <td>딸기라떼</td>
      <td>5700</td>
      <td>280</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 인덱스의 '시즌' 데이터(행) 삭제 후 cafe2.csv 파일로 저장
```python
  df.drop('시즌', axis=0, inplace=True)
  df.to_csv('./data/cafe2.csv', index=False)
```

<br>

---

<br>

SECTION10 정렬
---
- 데이터를 오름차순 또는 내림차순으로 정렬 가능

  - 오름차순 : 작은 수에서 큰 수로 정렬
 
  - 내림차순 : 큰 수에서 작은 수로 정렬
 
> cafe2.csv 데이터프레임 불러오기

```python
  import pandas as pd
  
  df = pd.read_csv('./data/cafe2.csv')
  df.head(2)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 01. 정렬 방법
- 인덱스 기준 : sort_index()

- 데이터 값 기준 : sort_values()

- 기본 설정은 오름차순

  - 내림차순 : ascending 값을 False 로 대입
 
<br>

|정렬|파라미터|기본값|
|:-:|:-:|:-:|
|오름차순|ascending = True|기본값(생략 가능)|
|내림차순|ascending = False|-|

<br>

### 02. 인덱스 기준 정렬
```python
  df.sort_index(ascending = False)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7</th>
      <td>딸기라떼</td>
      <td>5700</td>
      <td>280</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 03. 데이터 값 기준 정렬
- by = '컬럼명' : 반드시 들어가야 할 파라미터

  - 'by =' 는 생략하고 컬럼명만 작성해도 OK
 
```python
  df.sort_values(by='메뉴', ascending = False)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>딸기라떼</td>
      <td>5700</td>
      <td>280</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 04. 2개 이상의 기준 정렬
- 정렬하고자 하는 컬럼이 2개 이상일 때, 각 컬럼마다 오름차순/내림차순 다를 때

  - 순서에 맞게 리스트 형태로 대입
 
  - 먼저 작성된 컬럼이 우선순위가 높음
 
  - inplace 로 변경 사항 저장

```python
  df.sort_values(['가격', '메뉴'], ascending = [False, True], inplace = True)
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>딸기라떼</td>
      <td>5700</td>
      <td>280</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 05. 인덱스 초기화
- reset_index()

  - sort_values()로 정렬된(변경된) 상태에서 인덱스를 새로 만들고 싶을 때
 
  - 인덱스가 0부터 새롭게 만들어진
 
  - 단, 기존 인덱스는 새로운 컬럼에 저장됨
 
    - 기존 인덱스가 필요없다면 drop = True 설정
   
```python
  df.reset_index(drop = True)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>딸기라떼</td>
      <td>5700</td>
      <td>280</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>3</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>6</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>7</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

---

<br>

SECTION11 필터링
---
> cafe2.csv 데이터프레임 불러오기

```python
  import pandas as pd
  
  df = pd.read_csv('./data/cafe2.csv')
  df.head(2)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 01. 1개 조건 필터링
- 특정 컬럼에 조건식(<, >, ==, != 등)을 적용하면 True/False 반환 (불리언 자료형)

  - 불리언 결과를 데이터프레임의 대괄호 안에 넣으면 True로 표시된 행들만 선택됨

```python
  df['칼로리'] < 50
```

> 결과
```python
  0     True
  1    False
  2    False
  3    False
  4     True
  5    False
  6     True
  7    False
  Name: 칼로리, dtype: bool
```

<br>

> 방법1
```python
  df[df['칼로리'] < 50]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 방법2
```python
  cond = df['칼로리'] < 50
  df[cond]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

▲ 방법1은 조건이 2개 이상일 때 괄호 수가 많아지고 가독성 좋지 않으므로 방법2 추천

<br>

### 02. NOT 연산자
- ~ 연산자 : 조건의 반대를 필터링하는데 사용

  - True(1)를 False(0)으로, False(0)를 True(1)로 변경
 
  - 조건의 반대 결과 출력

```python
  cond = df['칼로리'] < 50
  df[~cond]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>딸기라떼</td>
      <td>5700</td>
      <td>280</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 03. 복수 조건 필터링
- 조건이 2개 이상일 때는 합집합(AND)이거나 교집합(OR)인지 구분

|2개 이상의 조건|설명|판다스에서 활용하는 기호|
|:-:|:-:|:-:|
|교집합|두 조건이 모두 참일 때<br>True 반환|&|
|합집합|두 조건 중 하나 이상이 참일 때<br>True 반환|\||

<br>

#### 💡 언제 and/or 또는 &/| 연산자를 사용?
- and/or

  - 파이썬 조건문

- &/|

  - 판다스 데이터프레임을 필터링할 때

  - 시험에서는 판다스로 데이터를 다루는 일이 많으므로 &/| 연산자 기억
 
  - 파이썬 비트(0과 1) 연산

 <br>

 |구분|설명|예|
 |:-:|:-:|-|
 |파이썬|and : 교집합<br>or : 합집합|if 조건1 and 조건2 :<br> &nbsp;&nbsp; print('두 조건 모두 참')<br>if 조건1 or 조건2 :<br> &nbsp;&nbsp; print('두 조건 중 하나 이상 참')|
 |판다스|& : 교집합<br>\| : 합집합|df[조건1 & 조건2]<br>df[조건1 \| 조건2]| 

<br>

```python
  # 가격이 5,000원 이하면서 칼로리가 100보다 큰 데이터
  cond1 = df['가격'] <= 5000
  cond2 = df['칼로리'] > 100
  df[cond1 & cond2]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
      <td>과테말라</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  # 가격이 5,000원 이하거나 칼로리가 100보다 큰 데이터
  cond1 = df['가격'] <= 5000
  cond2 = df['칼로리'] > 100
  df[cond1 | cond2]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>딸기라떼</td>
      <td>5700</td>
      <td>280</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 04. isin()을 사용한 필터링
- isin() : 주어진 값이 있는지 확인

  - 데이터프레임이나 시리즈의 값 중에 포함되어 있는지 체크

    - 포함되어 있으면 True
   
    - 포함되어 있지 않으면 False
   
  - 여러 개의 값을 한번에 찾을 수 있음
 
    - 리스트에 찾는 값 넣고, 그 리스트를 isin() 괄호 안에 작성
   
  - 주어진 값과의 완전한 일치를 검사함

```python
  df['메뉴'].isin(['녹차'])
```

> 결과
```python
  0    False
  1    False
  2    False
  3    False
  4    False
  5    False
  6     True
  7    False
  Name: 메뉴, dtype: bool
```

<br>

```python
  # 데이터프레임에 불리언 대입시 조건 만족 데이터(행)만 조회 가능
  cond = df['메뉴'].isin(['녹차'])
  df[cond]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  box = ['녹차', '카푸치노', '카페라떼']
  cond = df['메뉴'].isin(box)
  df[cond]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

---

<br>

SECTION12 결측치 처리
---
> cafe2.csv 데이터프레임 불러오기

```python
  import pandas as pd
  
  df = pd.read_csv('./data/cafe2.csv')
  df.head(2)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 01. 결측치 탐색
- df.isnull() : 결측치 확인

  - 각 값마다 True/False 반환
 
    - 결측치(NaN)면 True
   
    - 값이 있다면 False
   
  - sum() 붙이면 컬럼별 합산 가능
 
    - True = 1, False = 0
   
    - 컬럼별로 더하면 결측치 수 확인 가능
   
    - df.isna().sum() 도 같은 결과

```python
  df.isnull()
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>5</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>6</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>7</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  df.isnull().sum()
```

> 결과
```python
  메뉴     0
  가격     0
  칼로리    0
  원산지    5
  dtype: int64
```

<br>

```python
  df.isna().sum()
```

> 결과
```python
  메뉴     0
  가격     0
  칼로리    0
  원산지    5
  dtype: int64
```

<br>

### 02. 결측치 채우기
- fillna() : 컬럼에 있는 결측치를 임의의 값으로 채우기

```python
  df['원산지'].fillna('코스타리카', inplace = True)
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>코스타리카</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
      <td>코스타리카</td>
    </tr>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>코스타리카</td>
    </tr>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>코스타리카</td>
    </tr>
    <tr>
      <th>7</th>
      <td>딸기라떼</td>
      <td>5700</td>
      <td>280</td>
      <td>코스타리카</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 결측치가 처리된 결과값을 cafe3.csv로 저장
```python
  df.to_csv('./data/cafe3.csv', index = False)
```

<br>

---

<br>

SECTION13 값 변경
---
- replace() : 특정 값을 찾아 변경

<br>

> cafe2.csv 데이터프레임 불러오기

```python
  import pandas as pd
  
  df = pd.read_csv('./data/cafe3.csv')
  df.head(2)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>코스타리카</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 01. replace() 활용
- replace(변경 전 값, 변경 후 값)

- 여러 개의 값을 변경하려면?

  - replace() 여러 번 사용

  - '변경 전 값 : 변경 후 값' 형태로 딕셔너리 생성 후 replace() 괄호 안에 넣어주기

```python
  df.replace('아메리카노', '룽고', inplace = True)
  df.replace('녹차', '그린티', inplace = True)
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>룽고</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>코스타리카</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
      <td>코스타리카</td>
    </tr>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>코스타리카</td>
    </tr>
    <tr>
      <th>6</th>
      <td>그린티</td>
      <td>5300</td>
      <td>0</td>
      <td>코스타리카</td>
    </tr>
    <tr>
      <th>7</th>
      <td>딸기라떼</td>
      <td>5700</td>
      <td>280</td>
      <td>코스타리카</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  change = {'룽고':'아메리카노', '그린티':'녹차'}
  df.replace(change, inplace = True)
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>코스타리카</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
      <td>과테말라</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
      <td>코스타리카</td>
    </tr>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>코스타리카</td>
    </tr>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>코스타리카</td>
    </tr>
    <tr>
      <th>7</th>
      <td>딸기라떼</td>
      <td>5700</td>
      <td>280</td>
      <td>코스타리카</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 02. loc/iloc 활용
- loc는 인덱스 사용

- 새로운 컬럼을 만들고 값을 대입하지 않으면 자동으로 'NaN' 적용

```python
  df.loc[6, '원산지'] = '대한민국'
  df.tail(3)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>코스타리카</td>
    </tr>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>대한민국</td>
    </tr>
    <tr>
      <th>7</th>
      <td>딸기라떼</td>
      <td>5700</td>
      <td>280</td>
      <td>코스타리카</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  df.loc[1:2, '이벤트가'] = 1000
  df.head(3)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
      <th>이벤트가</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>코스타리카</td>
      <td>1000.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
      <td>과테말라</td>
      <td>1000.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

> 변경된 데이터 프레임을 cafe4.csv로 저장
```python
  df.to_csv('./data/cafe4.csv', index = False)
```

<br>

---

<br>

SECTION14 문자열
---
- 문자열(string) : 일련의 문자로 구성된 데이터 유형

  - 문자, 숫자, 구두점, 공백, 특수 문자 등의 문자를 포함
 
  - 파이썬에서는 문자열을 큰따옴표 또는 작은따옴표로 둘러싸서 표현
 
- 판다스에서는 str 접근자를 사용해 문자열 데이터를 다룸

<br>

> 예제 데이터 생성
```python
  import pandas as pd
  
  df = pd.DataFrame({
      'A' : ['데이터 분석', '웹 프로그래밍', '앱 개발'],
      'B' : [10, 20, 30],
      'C' : ['ab cd', 'AB CD', 'ab cd ']  # 의도적으로 마지막 데이터 뒤에 공백 추가
  })
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>데이터 분석</td>
      <td>10</td>
      <td>ab cd</td>
    </tr>
    <tr>
      <th>1</th>
      <td>웹 프로그래밍</td>
      <td>20</td>
      <td>AB CD</td>
    </tr>
    <tr>
      <th>2</th>
      <td>앱 개발</td>
      <td>30</td>
      <td>ab cd</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 01. 문자열 변경(치환)
- 예제 데이터에서 replace()를 이용해 A컬럼 '분석' 단어를 '시각화'로 변경

  - 결과 : 변경되지 않음
 
  - 이유 : 0행 0열에 있는 전체 문자열은 '데이터 분석'
 
    - replace()만으로 전체 단어인 '데이터 분석'을 다른 단어로 변경 가능
   
    - '데이더 분석'이라는 문자열에서 '분석'이라는 일부 단어만 변경 불가
   
- str : 전체 문자열 중 일부만 변경할 때 사용

  - 데이터프레임의 값을 문자열로 인식
 
  - str.replace('변경 전 단어', '변경 후 단어')

- 데이터가 숫자일 때 str 접근자 사용시 에러 발생

  - 숫자 데이터는 replace()로 변경

- 정리

  - replace() : 문자열 뿐만 아니라 다른 유형도 변경 가능
 
  - str.replace() : 문자열만 적용 가능

```python
  df['A'] = df['A'].replace('분석', '시각화')
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>데이터 분석</td>
      <td>10</td>
      <td>ab cd</td>
    </tr>
    <tr>
      <th>1</th>
      <td>웹 프로그래밍</td>
      <td>20</td>
      <td>AB CD</td>
    </tr>
    <tr>
      <th>2</th>
      <td>앱 개발</td>
      <td>30</td>
      <td>ab cd</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  df['A'] = df['A'].str.replace('분석', '시각화')
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>데이터 시각화</td>
      <td>10</td>
      <td>ab cd</td>
    </tr>
    <tr>
      <th>1</th>
      <td>웹 프로그래밍</td>
      <td>20</td>
      <td>AB CD</td>
    </tr>
    <tr>
      <th>2</th>
      <td>앱 개발</td>
      <td>30</td>
      <td>ab cd</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  df['B'] = df['B'].replace(10, 100)
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>데이터 시각화</td>
      <td>100</td>
      <td>ab cd</td>
    </tr>
    <tr>
      <th>1</th>
      <td>웹 프로그래밍</td>
      <td>20</td>
      <td>AB CD</td>
    </tr>
    <tr>
      <th>2</th>
      <td>앱 개발</td>
      <td>30</td>
      <td>ab cd</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  df['B'] = df['B'].str.replace(20, 200)
  df
```

> 결과
```python
  AttributeError: Can only use .str accessor with string values!
```

<br>

### 02. 문자열 분리
- str.split() : 문자열 분리

  - 괄호 안에 값이 없을 때는 기본적으로 띄어쓰기를 기준으로 분리
 
  - 괄호 안에 구분자가 들어가면 해당 구분자를 기준으로 분리
 
  - 대괄호를 사용해 분리한 데이터의 특정 행만 선택 가능
 
- 분리 후 첫 번째 단어만 필요하다면 각 행별 첫 번째 값 선택

  - str.split() : 문자열을 리스트로 나눠 시리즈 자료형으로 반환

  - str[0] : 각 리스트의 첫 번째 값 선ㅌ택
  
```python
  df['A'].str.split()
```

> 결과
```python
  0    [데이터, 시각화]
  1    [웹, 프로그래밍]
  2       [앱, 개발]
  Name: A, dtype: object
```

<br>

```python
  df['A'].str.split()[0]
```

> 결과
```python
  ['데이터', '시각화']
```

<br>

```python
  df['D'] = df['A'].str.split().str[0]
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>데이터 시각화</td>
      <td>100</td>
      <td>ab cd</td>
      <td>데이터</td>
    </tr>
    <tr>
      <th>1</th>
      <td>웹 프로그래밍</td>
      <td>20</td>
      <td>AB CD</td>
      <td>웹</td>
    </tr>
    <tr>
      <th>2</th>
      <td>앱 개발</td>
      <td>30</td>
      <td>ab cd</td>
      <td>앱</td>
    </tr>
  </tbody>
</table>
</div>

<br>

#### 💡 str.split()[0] VS str.split().str[0]
- str 접근자로 인해 차이 발생

  - str.split()[0]
 
    - [0] : 첫 번째 행(0번째 인덱스)을 선택
   
  - str.split().str[0]
 
    - str[0] : 각 문자열 리스트 값에서 첫 번째 요소(0번째 인덱스)를 선택

<br>

### 03. 특정 문자열 검색
- str.contains() : 특정 단어가 포함되어 있는지 확인

```python
  df['A'].str.contains('웹')
```

> 결과
```python
  0    False
  1     True
  2    False
  Name: A, dtype: bool
```

<br>

```python
  df['웹 포함 유무'] = df['A'].str.contains('웹')
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>웹 포함 유무</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>데이터 시각화</td>
      <td>100</td>
      <td>ab cd</td>
      <td>데이터</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>웹 프로그래밍</td>
      <td>20</td>
      <td>AB CD</td>
      <td>웹</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>앱 개발</td>
      <td>30</td>
      <td>ab cd</td>
      <td>앱</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>

<br>

#### 💡 str.contains() VS isin()
- str.contains()

  - 값을 찾거나 값의 일부를 찾음
 
  - 데이터프레임 또는 시리즈에서 사용 가능
 
  - 문장 속에서 특정 문자열 찾기 가느
 
  - str을 통해 접근
 
  - 찾고자 하는 1개 값만 입력값으로 대입 가능
 
  - 리스트 형태가 아니므로 대괄호 필요 X

- isin()

  - 값을 찾음

  - 데이터프레임 또는 시리즈에서 사용 가능
 
  - 특정 값이 있는지 확인 및 괄호 안에는 리스트 형태로 데이터 입력
 
    - 여러 개의 값을 찾을 수 있음
   
    - 필터링에서 유용하게 사용
   
    - 1개 값만 찾더라도 대괄호 필요

```python
  menu = pd.Series(['치즈버거 세트', '더블 불고기버기', '상하이 스파이시버거'])
  menu.isin(['치즈버거 세트'])
```

> 결과
```python
  0     True
  1    False
  2    False
  dtype: bool
```

<br>

```python
  menu.str.contains('세트')
```

> 결과
```python
  0     True
  1    False
  2    False
  dtype: bool
```

<br>

### 04. 문자열 길이
```python
  df['문자길이'] = df['A'].str.len()
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>웹 포함 유무</th>
      <th>문자길이</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>데이터 시각화</td>
      <td>100</td>
      <td>ab cd</td>
      <td>데이터</td>
      <td>False</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>웹 프로그래밍</td>
      <td>20</td>
      <td>AB CD</td>
      <td>웹</td>
      <td>True</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>앱 개발</td>
      <td>30</td>
      <td>ab cd</td>
      <td>앱</td>
      <td>False</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 05. 문자열 대(소)문자 변경
- 파이썬에서는 대소문자 구분

- str.lower() : 영어로 된 문자열을 모두 소문자로 변경

- str.upper() : 영어로 된 문자열을 모두 대문자로 변경

- 문제에서 특정 영문 단어의 수를 물었을 때

  - 단어의 대소문자가 다른 경우
 
  - 공백이 포함된 경우
 
    - 소문자(또는 대문자)로 변경하고 공백도 제거하는 전처리 필요
  
```python
  'AB cd' == 'ab CD'
```

> 결과
```python
  False
```

<br>

```python
  df['C'] = df['C'].str.lower()
  df['C']
```

> 결과
```python
  0     ab cd
  1     ab cd
  2    ab cd 
  Name: C, dtype: object
```

<br>

```python
  df['C'] = df['C'].str.upper()
  df['C']
```

> 결과
```python
  0     AB CD
  1     AB CD
  2    AB CD 
  Name: C, dtype: object
```

<br>

```python
  df['C'] == 'AB CD'
```

> 결과
```python
  0     True
  1     True
  2    False
  Name: C, dtype: bool
```

<br>

```python
  df['C'] = df['C'].str.lower()
  df['C'] = df['C'].str.replace(' ', '')
  df['C']
```

> 결과
```python
  0    abcd
  1    abcd
  2    abcd
  Name: C, dtype: object
```

<br>

#### 💡 왼쪽, 오른쪽, 양쪽 공백 제거 방법
```python
  df['C'].str.strip()   # 양쪽 공백 제거
  df['C'].str.lstrip()  # 왼쪽 공백 제거
  df['C'].str.rstrip()  # 오른쪽 공백 제거
```

<br>

### 06. 문자열 슬라이싱
- str[시작 인덱스 번호:끝 인덱스 번호] : 데이터프레임에서 특정 구간만 슬라이싱

```python
  df['C'].str[1:3]
```

> 결과
```python
  0    bc
  1    bc
  2    bc
  Name: C, dtype: object
```

<br>

- str 없이 사용시 범위 내의 행 선택

```python
  df['C'][1:3]
```

> 결과
```python
  1    abcd
  2    abcd
  Name: C, dtype: object
```

<br>

---

<br>

SECTION15  내장 함수
---
> cafe4.csv 데이터프레임 불러오기

```python
  import pandas as pd
  
  df = pd.read_csv('./data/cafe4.csv')
  df.head(2)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
      <th>이벤트가</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>코스타리카</td>
      <td>1000.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 01. len()
- 리스트에서 데이터의 수 반환

- 데이터프레임에서 행(row)의 수 반환

- 파이썬 내장 함수지만, 데이터프레임의 행(레코드) 수를 구할 때 자주 사용

- df.shape로도 행과 열의 수 확인 가능

  - 행의 수 : df.shape[0]
 
  - 열의 수 : df.shape[1]
 
```python
  print(len(df))
  print(df.shape[0])
```

> 결과
```python
  8
  8
```

<br>

### 02. sum()
- 합계 함수

  - 이 함수를 잘 활용하면 조건에 맞는 데이터의 수 찾을 때 len() 보다 유용
 
    - len() 함수로는 조건에 맞는 데이터프레임을 구한 후 데이터프레임의 개수 구해야 함
 
- 조건문의 결과를 True/False로 반환받은 후 이를 모두 더하면 조건에 맞는 개수 확인 가능

  - True = 1, False = 0

- 기본적으로 컬럼별 합계 구함

- 행별 합계 구하기

  - 데이터프레임의 df의 행과 열 변경

    - T(대문자, transpose 약자) 사용
   
    - 변경한 형태로 저장하고 싶다면 df = df.T 로 저장
   
  - 축(axis) 변경
 
    - 기본적으로 axis = 0
   
    - axis = 1 로 변경하면 행별 합계 구하기 가능
   
    - drop에서 사용할 때와는 축설정을 반대라고 생각
   
      - sum(axis=0) : 컬럼별 합계
     
      - sum(axis=1) : 행별 합계

<br>

|-|axis = 0|axis = 1|
|:-:|:-:|:-:|
|drop()|행 삭제|컬럼 삭제|
|sum()|컬럼별 합계|행별 합계|

<br>

```python
  cond = df['가격'] > 5000
  
  # sum 으로 조건에 맞는 개수 구하기
  print(sum(cond))
  
  # len 으로 조건에 맞는 개수 구하기
  print(len(df[cond]))
```

> 결과
```python
  4
  4
```

<br>

```python
  df.sum(numeric_only = True)
```

> 결과
```python
  가격      40900.0
  칼로리       990.0
  이벤트가     2000.0
  dtype: float64
```

<br>

```python
  df.T
```

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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>메뉴</th>
      <td>아메리카노</td>
      <td>카페라떼</td>
      <td>카페모카</td>
      <td>카푸치노</td>
      <td>에스프레소</td>
      <td>밀크티</td>
      <td>녹차</td>
      <td>딸기라떼</td>
    </tr>
    <tr>
      <th>가격</th>
      <td>4500</td>
      <td>5000</td>
      <td>5500</td>
      <td>5000</td>
      <td>4000</td>
      <td>5900</td>
      <td>5300</td>
      <td>5700</td>
    </tr>
    <tr>
      <th>칼로리</th>
      <td>10</td>
      <td>110</td>
      <td>250</td>
      <td>110</td>
      <td>20</td>
      <td>210</td>
      <td>0</td>
      <td>280</td>
    </tr>
    <tr>
      <th>원산지</th>
      <td>콜롬비아</td>
      <td>코스타리카</td>
      <td>과테말라</td>
      <td>과테말라</td>
      <td>코스타리카</td>
      <td>코스타리카</td>
      <td>대한민국</td>
      <td>코스타리카</td>
    </tr>
    <tr>
      <th>이벤트가</th>
      <td>NaN</td>
      <td>1000.0</td>
      <td>1000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 💡 데이터프레임 속성
- df.T와 df.shape는 함수(메소드)가 아니라 데이터프레임 속성이므로 괄호 X

<br>

```python
  df.sum(axis = 1, numeric_only = True)
```

> 결과
```python
  0    4510.0
  1    6110.0
  2    6750.0
  3    5110.0
  4    4020.0
  5    6110.0
  6    5300.0
  7    5980.0
  dtype: float64
```

<br>

#### 💡 sum(df) VS df.sum()
- 계산 결과는 같으나 차이점 존재

  - sum(df)
 
    - 함수가 밖에서 데이터프레임을 감싸고 있으면 파이썬 내장함수
   
  - df.sum()
 
    - 데이터프레임 뒤에 점(.)과 함께 함수가 붙으면 판다스의 데이터프레임에서 제공하는 함수(메소드)

<br>

### 03. max(), min(), mean(), median(), sum(), std(), var()
- 기초 통계 함수

```python
  print('최대값: ', df['가격'].max())
  print('최소값: ', df['가격'].min())
  print('평균값: ', df['가격'].mean())
  print('중앙값: ', df['가격'].median())
  print('합계: ', df['가격'].sum())
  print('표준편차: ', df['가격'].std())
  print('분산: ', df['가격'].var())
```

> 결과
```python
  최대값:  5900
  최소값:  4000
  평균값:  5112.5
  중앙값:  5150.0
  합계:  40900
  표준편차:  631.1836952447815
  분산:  398392.85714285716
```

<br>

### 04. quantile()
- quantile(0 ~ 1 사이 값) : 분위수 확인 (소수점 앞의 0 생략 가능)

  - 0.1 : 데이터의 하위 10%

  - 0.25 : 1사분위수(데이터의 하위 25%)
 
  - 0.5 : 2사분위수(데이터의 중앙값)
 
  - 0.75 : 3사분위수(데이터의 하위 75%)
 
  - 0.9 : 데이터의 하위 90%
 
```python
  print('분위수 25% 값 : ', df['가격'].quantile(0.25))
  print('분위수 75% 값 : ', df['가격'].quantile(.75))
```

> 결과
```python
  분위수 25% 값 :  4875.0
  분위수 75% 값 :  5550.0
```

<br>

```python
  cond = df['가격'].quantile(.25) > df['가격']
  df[cond]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
      <th>이벤트가</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
      <td>코스타리카</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  cond = df['가격'].quantile(.75) < df['가격']
  df[cond]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
      <th>이벤트가</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>코스타리카</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>딸기라떼</td>
      <td>5700</td>
      <td>280</td>
      <td>코스타리카</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 05. mode()
- 최빈값을 찾아 시리즈 형태로 반환 (값만 반환하지 않음)

  - 반환 값이 1개가 아니라 여러 개일 수도 있기 때문

- 인덱스를 제외하고 최빈값만 얻고 싷다면 뒤에 인덱스 0 붙이기
 
```python
  df['원산지'].mode()[0]
```

> 결과
```python
  '코스타리카'
```

<br>

### 06. idxmax()와 idxmin()
- idxmax()

  - 데이터프레임 또는 시리즈의 열에서 최댓값을 갖는 인덱스를 반환
 
- idxmin()

  - 최소값을 갖는 인덱스를 반환

```python
  df['가격'].idxmax()
```

> 결과
```python
  5
```

<br>

```python
  max_ind = df['가격'].idxmax()
  df.loc[max_ind]
```

> 결과
```python
  메뉴        밀크티
  가격       5900
  칼로리       210
  원산지     코스타리카
  이벤트가      NaN
  Name: 5, dtype: object
```

<br>

```python
  print(df.loc[max_ind, '메뉴'])
  print(df.loc[max_ind]['메뉴'])
```

> 결과
```python
  밀크티
  밀크티
```

<br>

### 07. nlargest()와 nsmallest()
- nlargest(반환 개수, 컬럼명)

  - 데이터프레임의 특정 컬럼에서 가장 큰 값 반환

- nsmallest(반환 개수, 컬럼명)

  - 데이터프레임의 특정 컬럼에서 가장 작은 값 반환
 
  - 결과는 오름차순으로 정렬
 
  - 대체로 Sort_Values() 사용 가능

```python
  df.nlargest(3, '가격')
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
      <th>이벤트가</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>코스타리카</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>딸기라떼</td>
      <td>5700</td>
      <td>280</td>
      <td>코스타리카</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
      <td>과테말라</td>
      <td>1000.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  df.nsmallest(2, '가격')
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
      <th>이벤트가</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
      <td>코스타리카</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 08. apply()
- apply(적용할 함수명) : 데이터를 변경하거나 파생변수를 생성할 때 유용하게 활용

```python
  # 입력값이 100보다 크거나 같으면 No, 작으면 Yes 반환하는 함수
  def cal(x) :
      if x >= 100 :
          return 'No'
      else :
          return 'Yes'
  
  # apply(적용할 함수명)으로 '칼로리' 컬럼의 각 데이터를 cal()의 입력값으로 넣고
  # 각 결과값을 새로운 컬럼에 대입
  df['먹어도 될까요'] = df['칼로리'].apply(cal)
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
      <th>이벤트가</th>
      <th>먹말?</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
      <td>NaN</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>코스타리카</td>
      <td>1000.0</td>
      <td>No</td>
    </tr>
    <tr>
      <th>2</th>
      <td>카페모카</td>
      <td>5500</td>
      <td>250</td>
      <td>과테말라</td>
      <td>1000.0</td>
      <td>No</td>
    </tr>
    <tr>
      <th>3</th>
      <td>카푸치노</td>
      <td>5000</td>
      <td>110</td>
      <td>과테말라</td>
      <td>NaN</td>
      <td>No</td>
    </tr>
    <tr>
      <th>4</th>
      <td>에스프레소</td>
      <td>4000</td>
      <td>20</td>
      <td>코스타리카</td>
      <td>NaN</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>5</th>
      <td>밀크티</td>
      <td>5900</td>
      <td>210</td>
      <td>코스타리카</td>
      <td>NaN</td>
      <td>No</td>
    </tr>
    <tr>
      <th>6</th>
      <td>녹차</td>
      <td>5300</td>
      <td>0</td>
      <td>대한민국</td>
      <td>NaN</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>7</th>
      <td>딸기라떼</td>
      <td>5700</td>
      <td>280</td>
      <td>코스타리카</td>
      <td>NaN</td>
      <td>No</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 09. melt()
- 데이터프레임을 재구조화하는 데 사용

- '넓은 형태(wide format)'의 데이터를 '긴 형태(long format)'의 데이터로 변환하는데 유용

  - 넓은 형태
 
    - 각 행이 한 사람의 모든 정보를 담고 있고, 열이 다양한 변수를 나타내는 형태
   
  - 긴 형태
 
    - 각 행이 단 하나의 관측값만을 갖고, 다양한 변수들이 행으로 길게 나열되는 형태
   
- melt() 함수에서 인자 사용

  - id_vars(필수)
 
    - 데이터를 재구조화할 때 유지하고 싶은 열들 지정
   
  - value_vars(선택)
 
    - 재구조화할 열들 지정
   
    - 컬럼을 지정하면 해당 컬럼만 긴 형태로 변형됨
   
    - 지정하지 않으면 id_vars를 제외한 모든 열이 사용됨

> 예제 데이터 생성
```python
  df = pd.DataFrame({
      'Name' : {0:'최승철', 1:'윤정한', 2:'홍지수'},
      '수학' : {0:90, 1:92, 2:85},
      '영어' : {0:92, 1:84, 2:86},
      '국어' : {0:91, 1:94, 2:83}
  })
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>수학</th>
      <th>영어</th>
      <th>국어</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>최승철</td>
      <td>90</td>
      <td>92</td>
      <td>91</td>
    </tr>
    <tr>
      <th>1</th>
      <td>윤정한</td>
      <td>92</td>
      <td>84</td>
      <td>94</td>
    </tr>
    <tr>
      <th>2</th>
      <td>홍지수</td>
      <td>85</td>
      <td>86</td>
      <td>83</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  pd.melt(df, id_vars=['Name'])
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>variable</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>최승철</td>
      <td>수학</td>
      <td>90</td>
    </tr>
    <tr>
      <th>1</th>
      <td>윤정한</td>
      <td>수학</td>
      <td>92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>홍지수</td>
      <td>수학</td>
      <td>85</td>
    </tr>
    <tr>
      <th>3</th>
      <td>최승철</td>
      <td>영어</td>
      <td>92</td>
    </tr>
    <tr>
      <th>4</th>
      <td>윤정한</td>
      <td>영어</td>
      <td>84</td>
    </tr>
    <tr>
      <th>5</th>
      <td>홍지수</td>
      <td>영어</td>
      <td>86</td>
    </tr>
    <tr>
      <th>6</th>
      <td>최승철</td>
      <td>국어</td>
      <td>91</td>
    </tr>
    <tr>
      <th>7</th>
      <td>윤정한</td>
      <td>국어</td>
      <td>94</td>
    </tr>
    <tr>
      <th>8</th>
      <td>홍지수</td>
      <td>국어</td>
      <td>83</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  pd.melt(df, id_vars=['Name'], value_vars=['수학', '영어'])
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>variable</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>최승철</td>
      <td>수학</td>
      <td>90</td>
    </tr>
    <tr>
      <th>1</th>
      <td>윤정한</td>
      <td>수학</td>
      <td>92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>홍지수</td>
      <td>수학</td>
      <td>85</td>
    </tr>
    <tr>
      <th>3</th>
      <td>최승철</td>
      <td>영어</td>
      <td>92</td>
    </tr>
    <tr>
      <th>4</th>
      <td>윤정한</td>
      <td>영어</td>
      <td>84</td>
    </tr>
    <tr>
      <th>5</th>
      <td>홍지수</td>
      <td>영어</td>
      <td>86</td>
    </tr>
  </tbody>
</table>
</div>

<br>

---

<br>

SECTION16 그룹핑
---
- groupby(컬럼명) : 데이터를 다양한 방식으로 집계하고 분석할 때 사용

  - 특정 컬럼을 기준으로 여러 그룹으로 나눔
 
  - 각 그룹에 대해 합계, 평균, 최대, 최소, 빈도 등 구할 수 있음
 
  - 괄호 안에 대괄호 사용여부 (리스트 형식이므로)
 
    - 일반적으로 하나일 때 사용 X
   
    - 2개 이상일 때는 사용 O

<br>

> cafe4.csv 데이터프레임 불러오기

```python
  import pandas as pd
  
  df = pd.read_csv('./data/cafe4.csv')
  df.head(2)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>원산지</th>
      <th>이벤트가</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>아메리카노</td>
      <td>4500</td>
      <td>10</td>
      <td>콜롬비아</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>카페라떼</td>
      <td>5000</td>
      <td>110</td>
      <td>코스타리카</td>
      <td>1000.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 01. 그룹 기준 1개
```python
  df.groupby(['원산지']).mean(numeric_only = True)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>가격</th>
      <th>칼로리</th>
      <th>이벤트가</th>
    </tr>
    <tr>
      <th>원산지</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>과테말라</th>
      <td>5250.0</td>
      <td>180.0</td>
      <td>1000.0</td>
    </tr>
    <tr>
      <th>대한민국</th>
      <td>5300.0</td>
      <td>0.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>코스타리카</th>
      <td>5150.0</td>
      <td>155.0</td>
      <td>1000.0</td>
    </tr>
    <tr>
      <th>콜롬비아</th>
      <td>4500.0</td>
      <td>10.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br> 

#### 💡 코랩에서 발생하는 에러
- 최근 코랩의 판다스 라이브러리가 업데이트되면서 df.groupby(['원산지']).mean() 입력시 에러 발생

```
  TypeError: Could not convert 카페모카카푸치노 to numeric
```

- 해결 방법

  - 코랩 환경 : df.groupby(['원산지']).mean(numeric_only=True)
 
  - 시험 환경 : df.groupby(['원산지']).mean()

<br>

### 02. 집계 연산
- 그룹화된 결과에 다양한 연산 적용 가능

  - mean() : 평균
 
  - sum() : 합계
 
  - max(), min() : 최대, 최소
 
  - count() : 개수(단, 결측치 NaN 제외)
 
  - size() : 개수(모든 값 빈도, 결측치 포함)
 
  - agg() : 여러 연산을 한번에 적용
 
<br>

### 03. 그룹 기준 2개 이상
- 대괋호 필수

- 리스트 형태로 컬럼 입력

```python
  df.groupby(['원산지', '칼로리']).mean(numeric_only=True)
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>가격</th>
      <th>이벤트가</th>
    </tr>
    <tr>
      <th>원산지</th>
      <th>칼로리</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">과테말라</th>
      <th>110</th>
      <td>5000.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>250</th>
      <td>5500.0</td>
      <td>1000.0</td>
    </tr>
    <tr>
      <th>대한민국</th>
      <th>0</th>
      <td>5300.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">코스타리카</th>
      <th>20</th>
      <td>4000.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>110</th>
      <td>5000.0</td>
      <td>1000.0</td>
    </tr>
    <tr>
      <th>210</th>
      <td>5900.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>280</th>
      <td>5700.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>콜롬비아</th>
      <th>10</th>
      <td>4500.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 04. agg()
- 여러 개의 컬럼(열)에 대해 다양한 집계 연산을 동시에 수행 가능

```python
  df.groupby(['원산지', '메뉴']).agg(['mean', 'sum'])
```

> 결과

<div>

<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th colspan="2" halign="left">가격</th>
      <th colspan="2" halign="left">칼로리</th>
      <th colspan="2" halign="left">이벤트가</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>mean</th>
      <th>sum</th>
      <th>mean</th>
      <th>sum</th>
      <th>mean</th>
      <th>sum</th>
    </tr>
    <tr>
      <th>원산지</th>
      <th>메뉴</th>
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
      <th rowspan="2" valign="top">과테말라</th>
      <th>카페모카</th>
      <td>5500.0</td>
      <td>5500</td>
      <td>250.0</td>
      <td>250</td>
      <td>1000.0</td>
      <td>1000.0</td>
    </tr>
    <tr>
      <th>카푸치노</th>
      <td>5000.0</td>
      <td>5000</td>
      <td>110.0</td>
      <td>110</td>
      <td>NaN</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>대한민국</th>
      <th>녹차</th>
      <td>5300.0</td>
      <td>5300</td>
      <td>0.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">코스타리카</th>
      <th>딸기라떼</th>
      <td>5700.0</td>
      <td>5700</td>
      <td>280.0</td>
      <td>280</td>
      <td>NaN</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>밀크티</th>
      <td>5900.0</td>
      <td>5900</td>
      <td>210.0</td>
      <td>210</td>
      <td>NaN</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>에스프레소</th>
      <td>4000.0</td>
      <td>4000</td>
      <td>20.0</td>
      <td>20</td>
      <td>NaN</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>카페라떼</th>
      <td>5000.0</td>
      <td>5000</td>
      <td>110.0</td>
      <td>110</td>
      <td>1000.0</td>
      <td>1000.0</td>
    </tr>
    <tr>
      <th>콜롬비아</th>
      <th>아메리카노</th>
      <td>4500.0</td>
      <td>4500</td>
      <td>10.0</td>
      <td>10</td>
      <td>NaN</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 05. reset_index()
- 그룹핑된 데이터프레임의 인덱스는 기존과 모양이 다른 묶음

  - 그룹핑된 상태에서 추가적인 데이터 처리 또는 특정 값을 선택해 출력해야 할 경우
 
    - 그룹핑된 데이터프레임 뒤에 reset_index()

```python
  df.groupby(['원산지', '메뉴']).mean(numeric_only = True).reset_index()
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>원산지</th>
      <th>메뉴</th>
      <th>가격</th>
      <th>칼로리</th>
      <th>이벤트가</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>과테말라</td>
      <td>카페모카</td>
      <td>5500.0</td>
      <td>250.0</td>
      <td>1000.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>과테말라</td>
      <td>카푸치노</td>
      <td>5000.0</td>
      <td>110.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>대한민국</td>
      <td>녹차</td>
      <td>5300.0</td>
      <td>0.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>코스타리카</td>
      <td>딸기라떼</td>
      <td>5700.0</td>
      <td>280.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>코스타리카</td>
      <td>밀크티</td>
      <td>5900.0</td>
      <td>210.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>코스타리카</td>
      <td>에스프레소</td>
      <td>4000.0</td>
      <td>20.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>코스타리카</td>
      <td>카페라떼</td>
      <td>5000.0</td>
      <td>110.0</td>
      <td>1000.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>콜롬비아</td>
      <td>아메리카노</td>
      <td>4500.0</td>
      <td>10.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<br>

---

<br>

SECTION17 시계열 데이터(datetime)
---
- 날짜, 시간 관련 데이터

  - 시간의 순서에 따른 측정값, 기간 설정 등 다양한 분석과 작업에 사용
 
<br>

### 01. 날짜와 시간 데이터
- 일반적으로 날짜는 하이픈(-)

  - 연도-월-일(2024-09-26) 형태
 
- 일반적으로 시간은 콜론(:)

  - 시간:분:초(13:50:30) 형태
 
- 주어진 데이터

  - 하이픈(-), 콜론(:), 슬러시(/), 띄어쓰기 등 다양한 형태로 구분

<br>

> 예제 데이터 생성
```python
  import pandas as pd
  
  data = {
      'Date1' : ['2024-02-17', '2024-02-18', '2024-02-19', '2024-02-20'],
      'Date2' : ['2024:02:17', '2024:02:18', '2024:02:19', '2024:02:20'],
      'Date3' : ['24/02/17', '24/02/18', '24/02/19', '24/02/20'],
      'Date4' : ['02/17/2024', '02/18/2024', '02/19/2024', '02/20/2024'],
      'Date5' : ['17-Feb-2024', '18-Feb-2024', '19-Feb-2024', '20-Feb-2024'],
      'DateTime1' : ['24-02-17 13:50:30', '24-02-18 14:55:45', '24-02-19 15:30:15', '24-02-20 16:10:50'],
      'DateTime2' : ['2024-02-17 13-50-30', '2024-02-18 14-55-45', '2024-02-19 15-30-15', '2024-02-20 16-10-50'],
      'DateTime3' : ['02/17/2024 01:50:30 PM', '02/18/2024 02:55:45 PM', '02/19/2024 03:30:15 AM', '02/20/2024 04:10:50 AM'],
      'DateTime4' : ['17 Feb 2024 13:50:30', '18 Feb 2024 14:55:45', '19 Feb 2024 15:30:15', '20 Feb 2024 16:10:50']    
  }
  
  df = pd.DataFrame(data)
  df.to_csv('./data/date_data.csv', index = False)
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date1</th>
      <th>Date2</th>
      <th>Date3</th>
      <th>Date4</th>
      <th>Date5</th>
      <th>DateTime1</th>
      <th>DateTime2</th>
      <th>DateTime3</th>
      <th>DateTime4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2024-02-17</td>
      <td>2024:02:17</td>
      <td>24/02/17</td>
      <td>02/17/2024</td>
      <td>17-Feb-2024</td>
      <td>24-02-17 13:50:30</td>
      <td>2024-02-17 13-50-30</td>
      <td>02/17/2024 01:50:30 PM</td>
      <td>17 Feb 2024 13:50:30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2024-02-18</td>
      <td>2024:02:18</td>
      <td>24/02/18</td>
      <td>02/18/2024</td>
      <td>18-Feb-2024</td>
      <td>24-02-18 14:55:45</td>
      <td>2024-02-18 14-55-45</td>
      <td>02/18/2024 02:55:45 PM</td>
      <td>18 Feb 2024 14:55:45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2024-02-19</td>
      <td>2024:02:19</td>
      <td>24/02/19</td>
      <td>02/19/2024</td>
      <td>19-Feb-2024</td>
      <td>24-02-19 15:30:15</td>
      <td>2024-02-19 15-30-15</td>
      <td>02/19/2024 03:30:15 AM</td>
      <td>19 Feb 2024 15:30:15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2024-02-20</td>
      <td>2024:02:20</td>
      <td>24/02/20</td>
      <td>02/20/2024</td>
      <td>20-Feb-2024</td>
      <td>24-02-20 16:10:50</td>
      <td>2024-02-20 16-10-50</td>
      <td>02/20/2024 04:10:50 AM</td>
      <td>20 Feb 2024 16:10:50</td>
    </tr>
  </tbody>
</table>
</div>

<br>

<br>

- 파이썬은 데이터를 불러올 때 날짜와 시간 자동 인식 불가

  - 문자열 데이터로 인식해 자료형은 object

```python
  df.info()
```

> 결과
```python
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 4 entries, 0 to 3
  Data columns (total 9 columns):
   #   Column     Non-Null Count  Dtype 
  ---  ------     --------------  ----- 
   0   Date1      4 non-null      object
   1   Date2      4 non-null      object
   2   Date3      4 non-null      object
   3   Date4      4 non-null      object
   4   Date5      4 non-null      object
   5   DateTime1  4 non-null      object
   6   DateTime2  4 non-null      object
   7   DateTime3  4 non-null      object
   8   DateTime4  4 non-null      object
  dtypes: object(9)
  memory usage: 420.0+ bytes
```

<br>

### 02. datetime 자료형
- 날짜와 시간 데이터를 다루기 위해 object에서 datetime으로 자료형 변경(파싱)

  - 문자열을 의미 있는 단위로 분해하고 구조를 식별하는 과정
 
  - 판다스의 to_datetime(df['컬럼명]) 사용해 자료형 변경
 
- 대부분의 날짜와 시간 형태는 판다스가 자동으로 인식해 변경

  - 제대로 인식 못했을 때는 format 설정 필요

```python
  df = pd.read_csv('./data/date_data.csv')
  
  df['Date1'] = pd.to_datetime(df['Date1'])
  df['Date2'] = pd.to_datetime(df['Date2'], format = '%Y:%m:%d')
  df['Date3'] = pd.to_datetime(df['Date3'])
  df['Date4'] = pd.to_datetime(df['Date4'])
  df['Date5'] = pd.to_datetime(df['Date5'])
  df['DateTime1'] = pd.to_datetime(df['DateTime1'])
  df['DateTime2'] = pd.to_datetime(df['DateTime2'], format = '%Y-%m-%d %H-%M-%S')
  df['DateTime3'] = pd.to_datetime(df['DateTime3'])
  df['DateTime4'] = pd.to_datetime(df['DateTime4'])
  
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date1</th>
      <th>Date2</th>
      <th>Date3</th>
      <th>Date4</th>
      <th>Date5</th>
      <th>DateTime1</th>
      <th>DateTime2</th>
      <th>DateTime3</th>
      <th>DateTime4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2024-02-17</td>
      <td>2024-02-17</td>
      <td>2017-02-24</td>
      <td>2024-02-17</td>
      <td>2024-02-17</td>
      <td>2017-02-24 13:50:30</td>
      <td>2024-02-17 13:50:30</td>
      <td>2024-02-17 13:50:30</td>
      <td>2024-02-17 13:50:30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2024-02-18</td>
      <td>2024-02-18</td>
      <td>2018-02-24</td>
      <td>2024-02-18</td>
      <td>2024-02-18</td>
      <td>2018-02-24 14:55:45</td>
      <td>2024-02-18 14:55:45</td>
      <td>2024-02-18 14:55:45</td>
      <td>2024-02-18 14:55:45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2024-02-19</td>
      <td>2024-02-19</td>
      <td>2019-02-24</td>
      <td>2024-02-19</td>
      <td>2024-02-19</td>
      <td>2019-02-24 15:30:15</td>
      <td>2024-02-19 15:30:15</td>
      <td>2024-02-19 03:30:15</td>
      <td>2024-02-19 15:30:15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2024-02-20</td>
      <td>2024-02-20</td>
      <td>2020-02-24</td>
      <td>2024-02-20</td>
      <td>2024-02-20</td>
      <td>2020-02-24 16:10:50</td>
      <td>2024-02-20 16:10:50</td>
      <td>2024-02-20 04:10:50</td>
      <td>2024-02-20 16:10:50</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 03. 날짜와 시간 format
- pd.to_datetime()에서 날짜와 시간 표현 방식에 따라 문제 발생 가능성 있음

  - 가능하면 format 기본적으로 함께 작성

<br>

#### 에러가 발생한 케이스 : Date2 컬럼 (연도 4자리:월:일)
- 일반적으로 콜론은 시간을 나타낼 때 사용하므로 자동 인식 불가

- 자료 형태와 같은 형태로 포맷 작성 (대소문자 구분)

  - format = '%Y:%m:%d'
 
    - %Y : 연도 4자리 (에: 2024)
   
    - %m : 월 (에: 01 ~ 12)
   
    - %d : 일 (에: 01 ~ 31)
   
<br>

#### 잘못 인식한 케이스 : Date3 컬럼 (연도 2자리/월/일)
- 연도가 2자리라서 '연도/월/일'이 아니라 '일/월/연도'로 인식

  - 에러 발생하지 않는 경우이므로 주의
 
  - format = '%y/%m/%d'
 
    - %y : 연도 2자리 (예: 24)

<br>

#### 잘못 인식한 케이스 : DateTime1 컬럼 (연도 2자리-월-일 시간:분:초)
- 연도가 2자리라서 잘못 인식

  - format = '%y-%m-%d %H:%M:%S'
 
    - %H : 시간 (예: 00 ~ 23)
   
    - %M : 분 (예: 00 ~ 59)
   
    - %S : 초 (예: 00 ~ 59)

<br>

#### 에러가 발생한 케이스 : DateTime2 컬럼(연도 4자리-월-일 시간-분-초)
- 일반적으로 시간을 나타낼 때 콜론(:)을 사용하지 않으면 자동 인식 불가

  - format = '%Y-%m-%d %H-%M-%S'

 <br>

 ```python
  df = pd.read_csv('./data/date_data.csv')
  
  df['Date2'] = pd.to_datetime(df['Date2'], format = '%Y:%m:%d')
  df['Date3'] = pd.to_datetime(df['Date3'], format = '%y/%m/%d')
  df['DateTime1'] = pd.to_datetime(df['DateTime1'], format = '%y-%m-%d %H:%M:%S')
  df['DateTime2'] = pd.to_datetime(df['DateTime2'], format = '%Y-%m-%d %H-%M-%S')
  
  df[['Date2', 'Date3', 'DateTime1', 'DateTime2']]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date2</th>
      <th>Date3</th>
      <th>DateTime1</th>
      <th>DateTime2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2024-02-17</td>
      <td>2024-02-17</td>
      <td>2024-02-17 13:50:30</td>
      <td>2024-02-17 13:50:30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2024-02-18</td>
      <td>2024-02-18</td>
      <td>2024-02-18 14:55:45</td>
      <td>2024-02-18 14:55:45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2024-02-19</td>
      <td>2024-02-19</td>
      <td>2024-02-19 15:30:15</td>
      <td>2024-02-19 15:30:15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2024-02-20</td>
      <td>2024-02-20</td>
      <td>2024-02-20 16:10:50</td>
      <td>2024-02-20 16:10:50</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  df.info()
```

> 결과
```python
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 4 entries, 0 to 3
  Data columns (total 9 columns):
   #   Column     Non-Null Count  Dtype         
  ---  ------     --------------  -----         
   0   Date1      4 non-null      object        
   1   Date2      4 non-null      datetime64[ns]
   2   Date3      4 non-null      datetime64[ns]
   3   Date4      4 non-null      object        
   4   Date5      4 non-null      object        
   5   DateTime1  4 non-null      datetime64[ns]
   6   DateTime2  4 non-null      datetime64[ns]
   7   DateTime3  4 non-null      object        
   8   DateTime4  4 non-null      object        
  dtypes: datetime64[ns](4), object(5)
  memory usage: 420.0+ bytes
```

<br>

#### 💡 DataFrame에 대괄호를 2개 사용하는 이유
- df[[]]

  - 2개 이상의 컬럼을 출력하기 위해 사용
  
  - 1개 컬럼이지만 시리즈가 아닌 데이터프레임 형태로 출력하기 위해 사용

- 대괄호 2개 대신 컬럼명을 리스트 변수에 담아 출력 가능

```python
  cols = ['Date2', 'Date3', 'DateTime1', 'DateTime2']
  df[cols]
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date2</th>
      <th>Date3</th>
      <th>DateTime1</th>
      <th>DateTime2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2024-02-17</td>
      <td>2024-02-17</td>
      <td>2024-02-17 13:50:30</td>
      <td>2024-02-17 13:50:30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2024-02-18</td>
      <td>2024-02-18</td>
      <td>2024-02-18 14:55:45</td>
      <td>2024-02-18 14:55:45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2024-02-19</td>
      <td>2024-02-19</td>
      <td>2024-02-19 15:30:15</td>
      <td>2024-02-19 15:30:15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2024-02-20</td>
      <td>2024-02-20</td>
      <td>2024-02-20 16:10:50</td>
      <td>2024-02-20 16:10:50</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 04. 날짜와 시간 데이터 분할(datetime dt 속성)
- 판다스의 dt를 활용해 연도, 월, 일, 시간, 분, 초를 별도의 변수로 분리 생성

  - datetime 자료형만 dt 사용 가능

- 문제에서 특정 연도, 월 등을 묻는 경우 필터링으로 유용하게 사용 가능

```python
  df['year'] = df['DateTime1'].dt.year
  df['month'] = df['DateTime1'].dt.month
  df['day'] = df['DateTime1'].dt.day
  df['hour'] = df['DateTime1'].dt.hour
  df['minute'] = df['DateTime1'].dt.minute
  df['second'] = df['DateTime1'].dt.second
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date1</th>
      <th>Date2</th>
      <th>Date3</th>
      <th>Date4</th>
      <th>Date5</th>
      <th>DateTime1</th>
      <th>DateTime2</th>
      <th>DateTime3</th>
      <th>DateTime4</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
      <th>hour</th>
      <th>minute</th>
      <th>second</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2024-02-17</td>
      <td>2024-02-17</td>
      <td>2024-02-17</td>
      <td>02/17/2024</td>
      <td>17-Feb-2024</td>
      <td>2024-02-17 13:50:30</td>
      <td>2024-02-17 13:50:30</td>
      <td>02/17/2024 01:50:30 PM</td>
      <td>17 Feb 2024 13:50:30</td>
      <td>2024</td>
      <td>2</td>
      <td>17</td>
      <td>13</td>
      <td>50</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2024-02-18</td>
      <td>2024-02-18</td>
      <td>2024-02-18</td>
      <td>02/18/2024</td>
      <td>18-Feb-2024</td>
      <td>2024-02-18 14:55:45</td>
      <td>2024-02-18 14:55:45</td>
      <td>02/18/2024 02:55:45 PM</td>
      <td>18 Feb 2024 14:55:45</td>
      <td>2024</td>
      <td>2</td>
      <td>18</td>
      <td>14</td>
      <td>55</td>
      <td>45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2024-02-19</td>
      <td>2024-02-19</td>
      <td>2024-02-19</td>
      <td>02/19/2024</td>
      <td>19-Feb-2024</td>
      <td>2024-02-19 15:30:15</td>
      <td>2024-02-19 15:30:15</td>
      <td>02/19/2024 03:30:15 AM</td>
      <td>19 Feb 2024 15:30:15</td>
      <td>2024</td>
      <td>2</td>
      <td>19</td>
      <td>15</td>
      <td>30</td>
      <td>15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2024-02-20</td>
      <td>2024-02-20</td>
      <td>2024-02-20</td>
      <td>02/20/2024</td>
      <td>20-Feb-2024</td>
      <td>2024-02-20 16:10:50</td>
      <td>2024-02-20 16:10:50</td>
      <td>02/20/2024 04:10:50 AM</td>
      <td>20 Feb 2024 16:10:50</td>
      <td>2024</td>
      <td>2</td>
      <td>20</td>
      <td>16</td>
      <td>10</td>
      <td>50</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 05. 요일 찾기
- df['DataTime1'].dt.dayofweek

  - 해당 날짜의 요일을 숫자로 변경한 값 반환
 
  - 0 = 월요일, 1 = 화요일, 2 = 수요일, 3 = 목요일, 4 = 금요일, 5 = 토요일, 6 = 일요일

```python
  df['DateTime1'].dt.dayofweek
```

> 결과
```python
  0    5
  1    6
  2    0
  3    1
  Name: DateTime1, dtype: int32
```

<br>

### 06. 특정 시점과 특정 구간
- 특정 시점

  - datetime : 특정 날짜와 시간
 
  - ex) 2024-02-17 11:11:11
 
- 특정 구간

  - period : 특정 시간의 범위나 구간
 
  - ex) 2024-02 (2024년 2월 전체)

<br>

|구분|코드|예시|
|:-:|:-:|:-:|
|Y(연도)|dt.to_period('Y')|'2024-02-17' → '2024'|
|Q(분기)|dt.to_period('Q')|'2024-02-17' → '2024Q1'|
|M(월)|dt.to_period('M')|'2024-02-17' → '2023-02'|
|D(일)|dt.to_period('D')|'2024-02-17 15:30:24' → '2024-02-17'|
|H(시간)|dt.to_period('H')|'2024-02-17 15:30:24' → '2024-02-17 15:30'|

<br>

```python
  print(df['DateTime1'].dt.to_period('Y'))
  print(df['DateTime1'].dt.to_period('Q'))
  print(df['DateTime1'].dt.to_period('M'))
  print(df['DateTime1'].dt.to_period('D'))
  print(df['DateTime1'].dt.to_period('H'))
```

> 결과
```python
  0    2024
  1    2024
  2    2024
  3    2024
  Name: DateTime1, dtype: period[Y-DEC]
  0    2024Q1
  1    2024Q1
  2    2024Q1
  3    2024Q1
  Name: DateTime1, dtype: period[Q-DEC]
  0    2024-02
  1    2024-02
  2    2024-02
  3    2024-02
  Name: DateTime1, dtype: period[M]
  0    2024-02-17
  1    2024-02-18
  2    2024-02-19
  3    2024-02-20
  Name: DateTime1, dtype: period[D]
  0    2024-02-17 13:00
  1    2024-02-18 14:00
  2    2024-02-19 15:00
  3    2024-02-20 16:00
  Name: DateTime1, dtype: period[H]
```

<br>

#### 💡 시계열 데이터를 다룰 때 주의점
- 오타 조심

  - date, datetime, to_datetime 등을 입력할 때 data로 입력하는 경우 많음

<br>

---

<br>

SECTION18 시계열 데이터(Timedelta)
---
- 날짜와 시간을 더하거나 빼서 새로운 시점 계산 가능
  
  - datetime : 특정 시점의 날짜와 시간
 
    - datetime 자료형을 빼거나 더하면 결과값은 Timedelta 자료형
  
  - Timedelta : 두 시점 사이의 차이

<br>

> 날짜 컬럼 불러오기
```python
  import pandas as pd
  
  df = pd.read_csv('./data/date_data.csv', 
                   usecols = ['DateTime4'], # usecols로 DateTime4 컬럼 선택
                   parse_dates = ['DateTime4'])   # parse_dates로 datetime 자료형으로 변환
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>DateTime4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2024-02-17 13:50:30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2024-02-18 14:55:45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2024-02-19 15:30:15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2024-02-20 16:10:50</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 01. 특정 시간과의 차이
- pd.Timedelta() : 특정 일로부터 날짜 계산

  - pd.Timedelta(days=더하려는 일자) : 일(day) 더하기
 
  - pd.Timedelta(hours=시간) : ~ 시간 뒤 계산
 
  - 특점 시점에서 ~주, ~일, ~시간, ~분, ~초 이전 계산
 
    - pd.Timedelta()로 데이터 만들고 날짜와 시간에서 빼기
   
    - weeks : 주(7일), days : 일, hours : 시간, minutes : 분, seconds : 초

```python
  day = pd.Timedelta(days = 99)
  df['After-100day'] = df['DateTime4'] + day
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>DateTime4</th>
      <th>After-100day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2024-02-17 13:50:30</td>
      <td>2024-05-26 13:50:30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2024-02-18 14:55:45</td>
      <td>2024-05-27 14:55:45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2024-02-19 15:30:15</td>
      <td>2024-05-28 15:30:15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2024-02-20 16:10:50</td>
      <td>2024-05-29 16:10:50</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  hour = pd.Timedelta(hours = 100)
  df['After-100hour'] = df['DateTime4'] + hour
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>DateTime4</th>
      <th>After-100day</th>
      <th>After-100hour</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2024-02-17 13:50:30</td>
      <td>2024-05-26 13:50:30</td>
      <td>2024-02-21 17:50:30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2024-02-18 14:55:45</td>
      <td>2024-05-27 14:55:45</td>
      <td>2024-02-22 18:55:45</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2024-02-19 15:30:15</td>
      <td>2024-05-28 15:30:15</td>
      <td>2024-02-23 19:30:15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2024-02-20 16:10:50</td>
      <td>2024-05-29 16:10:50</td>
      <td>2024-02-24 20:10:50</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  difference = pd.Timedelta(weeks=7, days=7, hours=7, minutes=7, seconds=7)
  df['difference'] = df['DateTime4'] - difference
  df
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>DateTime4</th>
      <th>After-100day</th>
      <th>After-100hour</th>
      <th>difference</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2024-02-17 13:50:30</td>
      <td>2024-05-26 13:50:30</td>
      <td>2024-02-21 17:50:30</td>
      <td>2023-12-23 06:43:23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2024-02-18 14:55:45</td>
      <td>2024-05-27 14:55:45</td>
      <td>2024-02-22 18:55:45</td>
      <td>2023-12-24 07:48:38</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2024-02-19 15:30:15</td>
      <td>2024-05-28 15:30:15</td>
      <td>2024-02-23 19:30:15</td>
      <td>2023-12-25 08:23:08</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2024-02-20 16:10:50</td>
      <td>2024-05-29 16:10:50</td>
      <td>2024-02-24 20:10:50</td>
      <td>2023-12-26 09:03:43</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 02. 두 시간 사이의 차이
- 두 자료형 간에 차이를 계산하면 Timedelta 자료형

- dt.total_seconds()

  - 데이터프레임(시리즈)에 있는 두 날짜와의 일, 시간, 분, 초 계산
 
  - Timedelta 자료형에 사용시 전체 시간을 초 단위로 변경 가능

    - 60을 나누면 분이 되고, 또 60을 나누면 시간, 24를 나누면 일

```python
  diff = df['After-100hour'] - df['difference']
  diff
```

> 결과
```python
  0   60 days 11:07:07
  1   60 days 11:07:07
  2   60 days 11:07:07
  3   60 days 11:07:07
  dtype: timedelta64[ns]
```

<br>

```python
  print(diff.dt.total_seconds())          # 초
  print(diff.dt.total_seconds()/60)       #분
  print(diff.dt.total_seconds()/60/60)    # 시간
  print(diff.dt.total_seconds()/60/60/24) # 일
```

> 결과
```python
  0    5224027.0
  1    5224027.0
  2    5224027.0
  3    5224027.0
  dtype: float64
  0    87067.116667
  1    87067.116667
  2    87067.116667
  3    87067.116667
  dtype: float64
  0    1451.118611
  1    1451.118611
  2    1451.118611
  3    1451.118611
  dtype: float64
  0    60.463275
  1    60.463275
  2    60.463275
  3    60.463275
  dtype: float64
```

<br>

### 03. Timedelta의 dt 속성
- Timedelta에도 dt 속성 있음

  - days : 일 수 반환
 
  - seconds : 총 시간에서 일(day)를 제외한 초 반환
 
    - total_seconds()는 ~일을 포함한 전체 시간을 초 단위로 반환

```python
  print(diff.dt.days)
  print(diff.dt.seconds)
```

> 결과
```python
  0    60
  1    60
  2    60
  3    60
  dtype: int64
  0    40027
  1    40027
  2    40027
  3    40027
  dtype: int32
```

<br>

#### 💡 datetime의 dt VS Timedelta의 dt
- datetime의 dt

  - year, month, day, hour, minute 등 각 날짜와 시간에 대해 접근

- Timedelta의 dt

  - 시간의 차이 값을 days, seconds, microseconds 같은 속성과 total_seconds() 같은 메소드로 접근

<br>

### 04. 시간 반올림
- round() : 시간을 반올림 할 때 사용

  - ex) 5.41분
 
    - 5분 41초 (X)
   
    - 5분 + 0.41분 = 5분  24.6초 (O)
   
      - 0.41분 = 0.41 * 60 = 24.6초

```python
  min = 5.41
  print(int(min), '분')
  print(0.41*60, '초')
```

> 결과
```python
  5 분
  24.599999999999998 초
```

<br>

```python
  print(round(diff.dt.total_seconds()/60))
```

> 결과
```python
  0    87067.0
  1    87067.0
  2    87067.0
  3    87067.0
  dtype: float64
```

<br>

---

<br>

SECTION19 데이터프레임 합치기
---
- 여러 개의 데이터가 주어졌을 때 데이터를 합쳐야 하는 경우

  - concat() or merge() 활용

<br>

### 01. 단순 병합
- concat() : 데이터프레임을 위-아래 또는 왼쪽-오른쪽으로 단순히 연결할 때

  - 기본적(axis=0)으로 위-아래로 합침
 
    - axis=1 변경시 왼쪽-오른쪽 합침
 
  - 합쳤을 때 기존 데이터에서 갖고 있던 인덱스 번호 유지
 
    - ignore_index = Ture : 인덱스 새로 설정

<br>

> 예제 데이터 생성
```python
  import pandas as pd 
  
  # 에피타이저 메뉴
  appetizer = pd.DataFrame({
      'Menu' : ['Salad', 'Soup', 'Bread'],
      'Price' : [12000, 9000, 7000]
  })
  
  # 메인 메뉴
  main = pd.DataFrame({
      'Menu' : ['Steak', 'Pasta', 'Chicken'],
      'Price' : [33000, 19000, 21000]
  })
  
  print(appetizer)
  print(main)
```

> 결과
```python
      Menu  Price
  0  Salad  12000
  1   Soup   9000
  2  Bread   7000
        Menu  Price
  0    Steak  33000
  1    Pasta  19000
  2  Chicken  21000
```

<br>

```python
  full_menu = pd.concat([appetizer, main], ignore_index = True)
  full_menu
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Menu</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Salad</td>
      <td>12000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Soup</td>
      <td>9000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bread</td>
      <td>7000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Steak</td>
      <td>33000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pasta</td>
      <td>19000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Chicken</td>
      <td>21000</td>
    </tr>
  </tbody>
</table>
</div>

<br>

```python
  full_menu = pd.concat([appetizer, main], axis=1)
  full_menu
```

> 결과
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Menu</th>
      <th>Price</th>
      <th>Menu</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Salad</td>
      <td>12000</td>
      <td>Steak</td>
      <td>33000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Soup</td>
      <td>9000</td>
      <td>Pasta</td>
      <td>19000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bread</td>
      <td>7000</td>
      <td>Chicken</td>
      <td>21000</td>
    </tr>
  </tbody>
</table>
</div>

<br>

### 02. 키(key) 기준 병합
- merge() : 주어진 2개의 데이터에서 특정 키(key)를 기준으로 합칠 때

```python
  # 메뉴와 가격
  price = pd.DataFrame({
      'Menu' : ['Salad', 'Soup', 'Steak', 'Pasta'],
      'Price' : [12000, 9000, 33000, 19000]
  })
  
  # 메뉴와 칼로리
  cal = pd.DataFrame({
      'Menu' : ['Soup', 'Steak', 'Pasta', 'Salad'],
      'Calories' : [100, 500, 400, 150]
  })
  
  # 두 데이터프레임을 'Menu'를 기준으로 병합
  menu_info = pd.merge(price, cal, on='Menu')
  print(menu_info)
```

> 결과
```python
      Menu  Price  Calories
  0  Salad  12000       150
  1   Soup   9000       100
  2  Steak  33000       500
  3  Pasta  19000       400
```

<br>

---
