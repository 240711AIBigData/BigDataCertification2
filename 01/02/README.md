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
























