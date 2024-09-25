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
```python
    menu	price
  0	아메리카노 4500
  1	카페라떼	5000
  2	카페모카	5500
```

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
```python
  	메뉴	가격	원두
  0	아메리카노 4500	케냐
  1	카페라떼	5000	콜롬비아
  2	카페모카	5500	케냐
```

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
```python
  	     메뉴	가격	칼로리
  0	아메리카노	4500	   10
  1	  카페라떼	5000	  110
  2	  카페모카	5500	  250
  3	  카푸치노	5000	  110
  4	에스프레소	4000	   20
  5	    밀크티	5900	  210
  6	      녹차	5300	    0
```

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
```python
  	Unnamed: 0	     메뉴 	가격	칼로리
  0	         0	아메리카노 	4500	   10
  1	         1	  카페라떼 	5000	  110
  2              2	  카페모카 	5500	  250
  3	         3	  카푸치노 	5000	  110
  4	         4	에스프레소 	4000	   20
  5	         5	   밀크티  	5900	  210
  6	         6	     녹차 	5300	    0
```

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
```python
  	메뉴	가격	칼로리
  0	아메리카노 4500	10
  1	카페라떼	  5000	110
  2	카페모카	  5500	250
  3	카푸치노	  5000	110
  4	에스프레소 4000	20
```

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
```python
  	메뉴	가격	칼로리
  0	아메리카노 4500	10
  1	카페라떼	5000	110
```

<br>

```python
  df.tail(3)
```

> 결과
```python
  	메뉴	가격	칼로리
  4	에스프레소 4000	20
  5	밀크티	5900	210
  6	녹차	5300	0
```

<br>

```python
  df.sample(3)
```

> 결과
```python
  	메뉴	가격	칼로리
  6	녹차 5300	0
  4	에스프레소 4000	20
  2	카페모카	5500	250
```

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
```python
  	가격	칼로리
  가격	1.000000	0.713227
  칼로리	0.713227	1.000000
```

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
```python
      car	size
  0	Sedan	S
  1	SUV	M
  2	Sedan	S
```

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
```python
          가격	    칼로리
  count	7.000000	7.000000
  mean	5028.571429	101.428571
  std	631.702160	99.402980
  min	4000.000000	0.000000
  25%	4750.000000	15.000000
  50%	5000.000000	110.000000
  75%	5400.000000	160.000000
  max	5900.000000	250.000000
```

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
```python
    car	size
  count	11	11
  unique 2	3
  top	Sedan	S
  freq	7	6
```

<br>

```python
  df.describe(include = 'object')
```

> 결과
```python
      메뉴
  count	7
  unique 7
  top	아메리카노
  freq	1
```
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
```python
  	메뉴	가격	칼로리
  0	아메리카노 4500	10
  1	카페라떼	5000	110
```

<br>

### 01. 새로운 컬럼 추가
-  df['새 컬럼명']
```python
  df['new'] = 0
  df.head(2)
```

> 결과
```python
      메뉴	가격	칼로리	new
  0	아메리카노 4500	10	0
  1	카페라떼	5000	110	0
```

<br>

### 02. 기존 컬럼을 사용한 계산
```python
  # 새로운 컬럼에 메뉴별 정상가에서 20% 할인한 금액 대입
  discount = 0.2
  df['할인가'] = df['가격'] * (1 - discount)
  df.head(2)
```

> 결과
```python
  	메뉴	가격	칼로리	new	할인가
  0	아메리카노 4500	10	0	3600.0
  1	카페라떼	5000	110	0	4000.0
```

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
```python
  	메뉴	가격	칼로리
  0	아메리카노 4500	10
  1	카페라떼	5000	110
  2	카페모카	5500	250
```

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
```python
      메뉴	가격	칼로리
  0	아메리카노 4500	10
  2	카페모카	5500	250
  3	카푸치노	5000	110
```

<br>

### 02. 컬럼(열) 삭제
- DataFrame.drop('컬럼명', axis = 1)

  - inplace 대신 대입(=) 연산자로 결과 저장 가능

```python
  df = df.drop('칼로리', axis = 1)
  df.head(3)
```

> 결과
```python
      메뉴	가격
  0 아메리카노	4500
  2	카페모카	5500
  3	카푸치노	5000
```

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
```python
      메뉴	가격	칼로리
  0	아메리카노 4500	10
  1	카페라떼	5000	110
```

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
```python
    	메뉴	가격
  1	카페라떼 5000
  2	카페모카	5500
  3	카푸치노	5000
```

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
```python
  	  메뉴	가격	칼로리
  1	카페라떼 5000	110
  2	카페모카	5500	250
```

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
```python
      메뉴	가격	칼로리
  2	카페모카	5500	250
  3	카푸치노	5000	110
```

<br>

> loc로 위와 같은 결과 출력해보기
```python
  df.loc[2:3, '메뉴':'칼로리']    # 컬럼 범위는 전체이므로 생략 가능
```

> 결과
```python
  	  메뉴	가격	칼로리
  2	카페모카	5500	250
  3	카푸치노	5000	110
```

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
```python
      메뉴	가격	칼로리
  0	아메리카노 4500	10
  1	카페라떼	5000	110
```

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
```python
      메뉴	가격	칼로리	원산지
  0	아메리카노 4500	10	NaN
  1	카페라떼	5000	110	NaN
  2	카페모카	5500	250	NaN
  3	카푸치노	5000	110	NaN
  4	에스프레소	4000	20	NaN
  5	밀크티	5900	210	NaN
  6	녹차	5300	0	NaN
```

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
```python
  	메뉴	가격	칼로리	원산지
  0	아메리카노 4500	10	콜롬비아
  1	카페라떼	5000	110	NaN
  2	카페모카	5500	250	과테말라
  3	카푸치노	5000	110	과테말라
```

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
```python
  	메뉴	가격	칼로리	원산지
  5	밀크티 5900	210	NaN
  6	녹차	5300	0	NaN
  시즌	크리스마스라떼	6000	300	한국
```

<br>

### 04. loc와 딕셔너리를 활용한 값 추가
- 리스트가 아닌 딕셔너리 형태로도 새로운 데이터 행(row) 추가 가능

  - 리스트 : 반드시 행의 컬럼 수와 리스트의 데이터 수 일치
 
  - 딕셔너리 : 특정 컬럼이 없다면 결측치(NaN)로 입력됨

```python
  
```

> 결과
```python
  
```

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
```python
      메뉴	가격	칼로리	원산지
  0	아메리카노 4500	10	콜롬비아
  1	카페라떼	5000	110	NaN
```

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
```python
    	메뉴	가격	칼로리	원산지
  7	딸기라떼 5700	280	NaN
  6	녹차	5300	0	NaN
  5	밀크티	5900	210	NaN
  4	에스프레소 4000	20	NaN
  3	카푸치노	5000	110	과테말라
  2	카페모카	5500	250	과테말라
  1	카페라떼	5000	110	NaN
  0	아메리카노 4500	10	콜롬비아
```

<br>

### 03. 데이터 값 기준 정렬
- by = '컬럼명' : 반드시 들어가야 할 파라미터

  - 'by =' 는 생략하고 컬럼명만 작성해도 OK
 
```python
  df.sort_values(by='메뉴', ascending = False)
```

> 결과
```python
  	메뉴	가격	칼로리	원산지
  3	카푸치노 5000	110	과테말라
  2	카페모카	5500	250	과테말라
  1	카페라떼	5000	110	NaN
  4	에스프레소 4000	20	NaN
  0	아메리카노 4500	10	콜롬비아
  5	밀크티	5900	210	NaN
  7	딸기라떼	5700	280	NaN
  6	녹차	5300	0	NaN
```

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
```python
  	메뉴	가격	칼로리	원산지
  5	밀크티 5900	210	NaN
  7	딸기라떼	5700	280	NaN
  2	카페모카	5500	250	과테말라
  6	녹차	5300	0	NaN
  1	카페라떼	5000	110	NaN
  3	카푸치노	5000	110	과테말라
  0	아메리카노 4500	10	콜롬비아
  4	에스프레소 4000	20	NaN
```

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
```python
  	메뉴	가격	칼로리	원산지
  0	밀크티 5900	210	NaN
  1	딸기라떼	5700	280	NaN
  2	카페모카	5500	250	과테말라
  3	녹차	5300	0	NaN
  4	카페라떼	5000	110	NaN
  5	카푸치노	5000	110	과테말라
  6	아메리카노 4500	10	콜롬비아
  7	에스프레소 4000	20	NaN
```

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
```python
      메뉴	가격	칼로리	원산지
  0	아메리카노 4500	10	콜롬비아
  1	카페라떼	5000	110	NaN
```

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
```python
  	메뉴	가격	칼로리	원산지
  0	아메리카노 4500	10	콜롬비아
  4	에스프레소 4000	20	NaN
  6	녹차	5300	0	NaN
```

<br>

> 방법2
```python
  cond = df['칼로리'] < 50
  df[cond]
```

> 결과
```python
  	메뉴	가격	칼로리	원산지
  0	아메리카노 4500	10	콜롬비아
  4	에스프레소 4000	20	NaN
  6	녹차	5300	0	NaN
```
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
```python
  	  메뉴	가격	칼로리	원산지
  1	카페라떼	5000	110	NaN
  2	카페모카	5500	250	과테말라
  3	카푸치노	5000	110	과테말라
  5	밀크티	5900	210	NaN
  7	딸기라떼	5700	280	NaN
```

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
```python
  	메뉴	가격	칼로리	원산지
  1	카페라떼	5000	110	NaN
  3	카푸치노	5000	110	과테말라
```

<br>

```python
  # 가격이 5,000원 이하거나 칼로리가 100보다 큰 데이터
  cond1 = df['가격'] <= 5000
  cond2 = df['칼로리'] > 100
  df[cond1 | cond2]
```

> 결과
```python
  	메뉴	가격	칼로리	원산지
  0	아메리카노	4500	10	콜롬비아
  1	카페라떼	5000	110	NaN
  2	카페모카	5500	250	과테말라
  3	카푸치노	5000	110	과테말라
  4	에스프레소	4000	20	NaN
  5	밀크티	5900	210	NaN
  7	딸기라떼	5700	280	NaN
```

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
```python
  	메뉴	가격	칼로리	원산지
  6	녹차	5300	0	NaN
```

<br>

```python
  box = ['녹차', '카푸치노', '카페라떼']
  cond = df['메뉴'].isin(box)
  df[cond]
```

> 결과
```python
  	메뉴	가격	칼로리	원산지
  1	카페라떼	5000	110	NaN
  3	카푸치노	5000	110	과테말라
  6	녹차	5300	0	NaN
```

<br>




