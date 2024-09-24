# CHAPTER01 파이썬
- 배우기 쉽고 인기 있는 프로그래밍 언어

- 데이터 분석 뿐만 아니라 업무 자동화, 웹 프로그래밍 등 다양한 환경에서 사용

<br>

SECTION01 출력
---
- print() 함수(or print문) 활용

  - print 단어 뒤의 괄호 안에 출력하고자 하는 값을 넣어주면 됨
 
  - 숫자는 그대로 사용, 문자는 큰따옴표("") 또는 작은따옴표('')로 묶어줌
 
<br>

### 01. 문자 출력
```python
  print('Hello World')
```

> 결과
```
  Hello World
```

<br>

### 02. 숫자 출력
```python
  print(2024)
```

> 결과
```
  2024
```

<br>

### 03. 자동 출력
- 주피터 노트북에서는 각 셀의 가장 마지막 문장 자동 출력

  - 마지막 코드 출력할 때 print 문 생략 가능
    
```python
  '빅데이터분석기사'
  '합격해봅시다'
```

> 결과
```
  '합격해봅시다'
```

<br>

#### 💡 시험에서는 반드시 print() 함수를 작성해야 출력됨
- 데이터 분석시 코딩 작업 환경은 스크립트 환경 or 주피터 노트북 환경

  - 스크립트 환경 (시험 환경)
 
    - 코드 전체를 처음부터 끝까지 순차적으로 실행
   
    - print() 함수가 있다면 출력 부분에서 모두 한번에 출력
   
  - 주피터 노트북 환경 (학습 환경)
 
    - 셀 단위로 나눠 실행
   
    - 중간 결과를 즉시 확인 가능 (대화형 환경 제공)

<br>

---

<br>

SECTION02 주석
---
- 코드에 설명을 달고 싶을 때

  - 코드에 메모를 추가하는데 사용

- 다른 방법으로 코드를 작성하면서 이전 코드는 실행되지 않고 잠시 컴퓨터가 인식하지 못하게 만들고 싶을 때

  - 주석 처리된 부분은 컴퓨터가 인식하지 못함
 
- 시험에서는 이전 코드는 남겨둔 채 풀이 방식을 다양하게 시도, 검증하기 위해 활용

<br>

### 01. 한 줄 주석 처리
- \# 기호로 시작

  - 해당 기호 뒤에 오는 모든 텍스트가 주석으로 처리됨
 
  - 단축기 : Ctrl + /
 
```python
  print('파이썬')
  # print('파이썬은 쉽다')
```

> 결과
```
  파이썬
```

<br>

### 02. 여러 줄 주석 처리
- 주석 처리하고 싶은 줄(행) 블록 처리 후 Ctrl + \

```python
  # print('Swerving')
  print("I'm speeding on serpent road")
  # print("Luxurious like I'm an S-Class")
```

> 결과
```
  I'm speeding on serpent road
```

<br>

---

<br>

## SECTION03 산술 연산자
### 01. 사칙연산
- 더하기(+), 빼기(-), 곱하기(*), 나누기(/) 등 산술 연산은 "1+2" 처럼 직관적으로 사용 가능

  - 자동으로 계산 결과값 출력
    
```python
  print(1+2, 4-1, 2*3, 16/3)
```

> 결과
```
 3 3 6 5.333333333333333
```

<br>

### 02. 나누기 결과
- 나머지가 0이더라도 소수점 형태(5.0) 반환

```python
  print(15/3)
```

> 결과
```
  5.0
```

<br>

### 03. 몫 연산자
- 16/3 = 5.333~

  - 이럴 때 몫 연산자인 //(슬러시 2개)는 소수점을 버리고 5만 반환

```python
  16//3
```

> 결과
```
  5
```

<br>

### 04. 나머지 연산자
- 나머지 연산자인 %(퍼센트) 사용하면 16을 3으로 나눈 나머지인 1 반환

```python
  16%3
```

> 결과
```
  1
```

<br>

### 05. 거듭제곱
- 거듭제곱(Exponentiation) : 어떤 수를 여러 번 곱하는 연산

- **(별 모양 2개) 사용

```python
  4**2
```

> 결과
```
  16
```

<br>

### 06. 제곱근
- 어떤 수의 제곱근(Square Root) : 그 수를 제곱했을 때 그 결과가 되는 수

- 제곱근 구하는 방법

  - 거듭제곱 연산자를 사용해 해당 수에 0.5를 거듭제곱
 
  - ex) 16**0.5 는 16의  제곱근을 계산하며 결과는 4.0 (루트16 = 4 와 동일)
 
    - 작업형2 회귀 모델 평가에서 사용

<br>

```python
  16**0.5
```

> 결과
```
  4.0
```

<br>

### 07. 산술 연산자 우선순위
- 연산자에는 우선순위가 있음

  - 거듭제곱(**) → 곱하기(*), 나누기(/), 나누기몫(//), 나머지(%) → 더하기(+), 빼기(-)
 
  - 더하기나 빼기 같이 우선순위가 같은 경우 왼쪽에서 오른쪽 순서대로 계산
 
  - 최상위 우선순위는 (괄호)
 
<br>

```python
  4+3*2
```

> 결과
```
  10
```

<br>

```python
  (4+3)*2
```

> 결과
```
  14
```

<br>

### 08. 문자끼리 더하기
- 숫자가 아니라 문자끼리 더하면 문자가 합쳐짐

```python
  "py" + "thon"
```

> 결과
```
  'python'
```

<br>

### 09. 문자와 숫자 더하기
- 문자와 숫자를 더하면 타입 에러(TypeError) 발생

  - 문자와 숫자는 더할 수 없음
 
- 숫자를 문자처럼 사용하는 경우 문자 형태로 합칠 수 있음
 
```python
  'py' + 3
```

> 결과
```
  TypeError: can only concatenate str (not "int") to str
```

<br>

```python
  'py' + '3'
```

> 결과
```
  'py3'
```

<br>

---

<br>

SECTION04 자료형
---
- type() 함수로 어떤 자료형인지 확인 가능

|자료형|문법|예시|
|:-:|:-:|:-:|
|숫자(정수)|int|1, 2, 3|
|숫자(실수)|float|1.0, 2.0, 3.0|
|문자열|str(string)|'hello', '3'|
|참과 거짓|bool(boolean)|True. False|

<br>

### 01. 정수형
```python
  type(1)
```

> 결과
```
  int
```

<br>

### 02. 실수형
- 소수점은 포함한 실수 값

```python
  type(1.1)
```

> 결과
```
  float
```

<br>

### 03. 문자열
- 문자열 : 문자들이 순서를 갖고 있는 자료형

  - 작은따옴표나 큰따옴표로 묶여 있음
 
  - str 은 string 의 약자
  
```python
  type('hello')
```

> 결과
```
  str
```

<br>

### 04. 숫자로 된 문자
- 숫자를 따옴표로 묶으면 문자
  
```python
  type('3')
```

> 결과
```
  str
```

<br>

### 05. 같지만 다른 문자
- 3과 3.0, '3'은 그냥 볼 때는 모두 같은 3 이지만, 프로그래밍에서는 각각 정수형, 실수형, 문자열

- 한 줄에 여러 값을 출력하기 위해 콤마 사용 가능

  - 콤마로 구분할 경우 소괄호로 묶여서 출력됨
    
```python
  type(3), type(3.0), type('3')
```

> 결과
```
  (int, float, str)
```

<br>

### 06. 참과 거짓
- 불리언(Boolean)은 참(True)와 거짓(False)을 나타내는 두 가지 값 보유

  - 문자를 쓸 때와 달리 따옴표 X
 
    - 예약어로 설정되어 있어 따옴표가 없어도 에러 발생 X
   
  - 첫 글자 대문자
     
```python
  type(True), type(False)
```

> 결과
```
  (bool, bool)
```

<br>

<details>
  <summary> 💡 예약어 </summary>
      
- 파이썬에서 미리 정의된 단어

  - 파이썬에서 특정 기능을 수행하도록 예약되어 있는 단어

- 일반적으로 색깔로 구분됨

  - 코랩에서는 파란색, 시험 환경에서는 붉은색
 
<br>

> 예약어 정리

|-|-|-|-|-|-|
|:-:|:-:|:-:|:-:|:-:|:-:|
|False|None|True|__peg_parser__|and|as|
|assert|async|await|break|class|continue|
|def|del|elif|else|except|finally|
for|from|global|if|import|in|
|is|lambda|nonlocal|not|or|pass|
|raise|return|try|while|with|yield|
  
</details>

<br>

### 07. 참은 1, 거짓은 0
- 불리언 값은 내부적으로 True는 1, False는 0 으로 사용됨

  - 불리언 값들 간의 산술 연산 가능
 
    - True 와 False 는 각각 1과 0으로 계산
      
```python
  True + True + True + False + False
```

> 결과
```
  3
```

<br>

---

<br>

SECTION05 변수
---
- 변수 : 파이썬에서 데이터를 저장하고 참조하는데 사용되는 식별자

  - 코딩에서는 숫자와 문자를 그대로 사용하지 않고 변수에 담아서 사용함
 
  - 변수명을 부르면 변수에 저장된 값을 알려줌
 
  - 변수를 사용하기 위한 명명 방식
 
    - 대소문자 혹은 문자와 숫자, 밑줄(_) 사용 가능
   
      - 숫자가 먼저 오면 X
     
      - 대소문자 구분 (Data 와 data 는 다른 변수)
     
    - True, False 같은 예약어 사용 불가

<br>

### 01. 변수에 값 대입
- 등호(=)는 "같다"가 아니라 "대입(할당)"

  - 오른쪽 결과가 왼쪽에 대입됨

```python
  americano = 4500
```

> 결과
```
  # 4500 값이 americano 변수에 저장됨
```

<br>

### 02. 변수 출력
- 변수명 출력시 변수에 담겨 있던 값 출력

  - 변수명은 따옴표 X, 문자는 따옴표 O
 
```python
  print(americano)    # 변수 출력
  print('americano')  # 문자 출력
```

> 결과
```
  4500
  americano
```

<br>

### 03. 변수 연산
- 변수명끼리 더하기 연산 진행시 숫자형일 경우, 그 변수 값끼리 더해짐

```python
  latte = 5000
  print(americano + latte)
```

> 결과
```
  9500
```

<br>

### 04. 결과값 변수에 대입
- 연산된 결과값을 바로 출력하는 것이 아니라 새로운 result 변수에 담아서 출력

  - 일반적으로 결과값을 변수에 담아두는 방식 많이 사용
 
```python
  result = americano + latte
  print(result)
```

> 결과
```
  9500
```

<br>

### 05. 변수 업데이트
- "=" 기준으로 양쪽에 같은 변수가 있을 경우, 오른쪽의 결과값을 왼쪽에 대입

```python
  americano = 4500
  americano = americano - 1000
  print(americano)
```

> 결과
```
  3500
```

<br>

### 06. 다중 변수 할당
- 여러 변수에 동시에 여러 값 할당 가능

```python
  a, b, c = 10, 20, 30
  print(a + b + c)
```

> 결과
```
  60
```

<br>

---

<br>

SECTION06 자료형 변환
---
- 형변환 = 자료형(데이터 타입)을 변경하는 것

  - 암시적 자료형 변환
 
    - 자료형이 자동으로 변경
   
  - 명시적 자료형 변환
 
    - 사용자가 원하는 자료형으로 변경
   
<br>

### 01. 암시적 자료형 변환
- 정수와 실수를 더하고 결과값을 정수에 대입하면 정수는 실수로 자동 변환

```python
  a = 2
  b = 0.17
  a = a + b
  type(a)
```

> 결과
```
  float
```

<br>

### 02. 명시적 자료형 변환

```python
  box = 2.17
  print('문자열 : ', str(box))
  print('정수형 : ', int(box))
```

> 결과
```
  문자열 :  2.17
  정수형 :  2
```

<br>

### 03. 자료형 변환
- 문자열 자료형을 실수형으로 변환하면 산술 연산 가능

  - 자료형 변환 없이 문자와 숫자를 산술 연산하면 타입 에러 발생

```python
  box = '3.14'
  box = float(box) + 10
  box
```

> 결과
```
  13.14
```

<br>

---

<br>

SECTION07 비교 연산자
---
- 2개의 값을 비교해 결과값으로 True(참) or False(거짓) 반환

  - 주로 조건문에서 활용

<br>

> 연산자 종류

|기호|의미<br>(왼쪽값이 오른쪽값보다)|기호|의미<br>(두 값은)|
|:-:|:-:|:-:|:-:|
|>|크다|==|같다|
|<|작다|!=|다르다|
|>=|크거나 같다|-|-|
|<=|작거나 같다|-|-|

<br>

### 01. 참 조건
```python
  10 > 5
```

> 결과
```
  True
```

<br>

### 02. 거짓 조건
```python
  10 < 5
```

> 결과
```
  False
```

<br>

### 03. 크거나(작거나) 같다
```python
  10 >= 5
```

> 결과
```
  True
```

<br>

### 04. 두 값이 같다
```python
  10 == 10
```

> 결과
```
  True
```

<br>

### 05. 두 값이 다르다
```python
  10 != 5
```

> 결과
```
  True
```

<br>

#### 💡 부등호 순서 : 항상 "=" 기호가 뒤에 와야 함

<br>

### 06. 변수 값 비교
- 변수에 숫자를 담아 비교 연산자 활용 가능
  
```python
  a = 10
  b = 10
  a == b
```

> 결과
```
  True
```

<br>

- 참 조건 : a가 b보다 같거나 크다는 조건이 성립하므로 True 반환
```python
  a >= b
```

> 결과
```
  True
```

<br>

- 거짓 조건 : a가 b보다 크다는 조건이 성립하지 않으므로 False 반환
```python
  a > b
```

> 결과
```
  False
```

<br>

### 07. 문자 비교
- 문자로도 비교 연산 가능
  
```python
  c = '빅데이터'
  d = '빅데이터'
  e = '데이터'
  
  print(c == d)
  print(d == e)
```

> 결과
```
  True
  False
```

<br>

---

<br>

SECTION08 조건문
---
- 프로그래밍에서 흐름을 제어하거나 결정을 내릴 때 사용

  - if, elif, else 키워드를 이용해 조건문 구성
 
    - if 키워드는 필수, elif와 else는 상황에 따라 사용하지 않아도 OK
 
- 주어진 조건이 참이면 특정 코드 실행, 거짓이면 다른 코드 실행 가능

  - 각 조건이 불리언(Boolean) 값인 True(참) 또는 False(거짓) qksghks

<br>

> 조건문 작성 구조
```
  1. if  키워드로 시작, 한 칸 띄어쓰기 후 조건 작성

  2. 조건 작성 후 콜론(:) 붙이고, 조건이 참일 때 실행될 코드를 다음 줄에 들여쓰기 후 작성

  3. elif(else if 줄임말) 사용해 추가 조건 사용 가능, elif도 조건 뒤에 콜론 사용

  4. if와 elif 조건이 모두 거짓일 때 실행될 코드는 else 블록에 작성
     else는 조건을 체크하지 않으므로 뒤에 조건을 작성하지 않으며, 콜론만 붙임

  5. 조건문 안에 들어가는 코드는 들여쓰기를 통해 구분
     파이썬은 들여쓰기가 매우 중요하며, 이를 통해 코드 식별
```

<br>

#### 💡 들여쓰기와 내어쓰기
- 들여쓰기와 내어쓰기도 문법의 일부

  - 코드의 블록을 구분하는 역할
 
  - 가독성과 코드의 실행 흐름을 제어하는 데 중요한 역할
 
- 들여쓰기 : Tab

- 내어쓰기 : Shift + Tab

<br>

### 01. 조건문
> 참
```python
  if True:
      print('실행')
```

> 결과
```
  실행
```

<br>

> 거짓
```python
  if False:
      print('무시')
```

> 결과
```
  실행되지 않음
```

<br>

#### 💡 흔히 하는 실수
- 콜론(:) 입력하지 않아 에러 발생하는 경우 많음

  - 자동 들여쓰기가 되지 않는다면 대부분 콜론(:)을 빠뜨린 경우

<br>

### 02. 비교 연산자
```python
  score = 10
  if score >= 10 :
      print('10보다 크거나 같다')
```

> 결과
```
  10보다 크거나 같다
```

<br>

```python
  if score > 9 :
      print('9 보다 크다')
```

> 결과
```
  9 보다 크다
```

<br>

```python
  if score <= 10 :
      print('10 보다 작거나 같다')
```

> 결과
```
  10 보다 작거나 같다
```

<br>

```python
  if score < 11 :
      print('11 보다 작다')
```

> 결과
```
  11 보다 작다
```

<br>

```python
  if score == 10 :
      print('score는 10이다')
```

> 결과
```
  score는 10이다
```

<br>

```python
  if score != 11 :
      print('score는 11과 같지 않다')
```

> 결과
```
  score는 11과 같지 않다
```

<br>

### 03. 논리 연산자
- and : 모든 조건이 참일 때 참 반환

- or : 하나 이상의 조건이 참일 때 참 반환

|기호|코드|설명|결과|
|:-:|:-:|:-:|:-:|
|and|True and False|참 and 거짓|거짓(False)|
|and|True and True|참 and 참|참(True)|
|or|True or False|참 or 거짓|참(True)|
|or|True or Ture|참 or 참|참(True)|

<br>

```python
  print('True and False : ', True and False)
  print('True and True : ', True and True)
  print('True or False : ', True or False)
  print('True or True : ', True or True)
```

> 결과
```
  True and False :  False
  True and True :  True
  True or False :  True
  True or True :  True
```

<br>

### 04. else
- if 조건이 거짓일 때 실행할 코드가 필요할 때 else 활용

  - 별도 조건 필요 X, if 조건 미성립시 else 아래 들여쓰기 된 코드 실행

```python
  if score < 10 and score >= 5 :
      print('score는 5 이상, 10 미만입니다')
  else :
      print('score는 5 미만, 10 이상입니다')
```

> 결과
```
  score는 5 미만, 10 이상입니다
```

<br>

### 05. elif
```python
  score = 7
  
  if score >= 10 :
      print('A')
  elif score < 10 and score >= 5 :
      print('B')
  else :
      print('C')
```

> 결과
```
  B
```

<br>

### 06. 조건문의 구성
- if와 else는 각각 한 번씩만 사용 가능

- elif는 필요에 따라 여러 번 사용 가능

```python
  score = 2
  
  if score >= 10 :
      print('score는 10 이상입니다')
  elif score < 10 and score >= 5 :
      print('score는 5 이상 10 미만입니다')
  elif score < 4 and score >= 3 :
      print('score는 3 이상 4 미만입니다')
  else :
      print('score는 2 이하입니다')
```

> 결과
```
  score는 2 이하입니다
```

<br>

---

<br>

SECTION09 리스트
---
- 여러 개의 값을 저장할 수 있는 자료형 중 하나

  - 여러 개의 값을 하나의 변수에 저장 가능
 
    - 데이터 관리 편리
   
  - 순서가 있는 자료형으로 데이터를 입력한 순서대로 저장
    
    - 인덱스를 통한 접근 가능
   
      - 인덱스는 0부터 시작
 
<br>

### 01. 리스트 생성
- 리스트에 데이터를 대입할 때는 [대괄호]로 묶어주고, 각 값은 콤마(,)로 구분

```python
  listbox = [4, 2, 10, 6, 8]
  print(listbox)
```

> 결과
```
  [4, 2, 10, 6, 8]
```

> listbox

|-|-|-|-|-|-|
|:-:|:-:|:-:|:-:|:-:|:-:|
|값|4|2|10|6|8|
|인덱스|[0]|[1]|[2]|[3]|[4]|

<br>

### 02. 리스트의 첫 번째 값
```python
  print(listbox[0])
```

> 결과
```
  4
```

<br>

### 03. 리스트 자료형 확인
```python
  print(type(listbox))
```

> 결과
```
  <class 'list'>
```

<br>

### 04. 리스트 생성(문자)
- 문자 대입 가능

  - 문자 입력시 따옴표 필수
    
```python
  listbox = ['빅데이터', '분석', '기사']
  print(listbox)
```

> 결과
```
  ['빅데이터', '분석', '기사']
```

<br>

### 05. 리스트 값 추가
- 리스트는 다양한 함수(메소드) 내장

  - append() 함수를 통해 이미 만들어진 리스트에 값 추가 가능
 
```python
  listbox.append('분석기사')
  listbox
```

> 결과
```
  ['빅데이터', '분석', '기사', '분석', '분석기사']
```

<br>

### 06. 리스트 정렬
- 순서 정렬시 sorted() 함수 사용

  - 기본적으로는 오름차순으로 정렬됨
 
  - 내림차순으로 정렬하고 싶으면 reverse = True 사용
 
  - 문자가 있는 리스트 자료형도 가나다 순으로 정렬 가능
 
    - 문자와 숫자가 섞여 있다면 정렬 불가

```python
  listbox = [4, 2, 10, 6, 8]
  listbox_sorted = sorted(listbox)
  listbox_sorted
```

> 결과
```
  [2, 4, 6, 8, 10]
```

<br>

```python
  sorted(listbox, reverse = True)
```

> 결과
```
  [10, 8, 6, 4, 2]
```

<br>

```python
  listbox = ['빅데이터', '분석', '기사']
  listbox_sorted = sorted(listbox)
  listbox_sorted
```

> 결과
```
  ['기사', '분석', '빅데이터']
```

<br>

---

<br>

SECTION10 딕셔너리
---
- 리스트와 같이 여러 개의 데이터를 한번에 담을 수 있는 자료형

  - key(키)와 value(값)의 쌍을 저장하는 연관 배열
 
  - 키를 통해 값 찾기 가능
 
<br>

### 01. 딕셔너리 생성
- 딕셔너리는 {중괄호}를 사용해 정의, 각 키와 값은 콜론(:)으로 구분

  - 키는 고유한 값으로 중복 불가
 
```python
  dictbox = {'name':'최승철', 'age':30}
  dictbox
```

> 결과
```
  {'name': '최승철', 'age': 30}
```

<br>

### 02. 딕셔너리 자료형
- 딕셔너리 자료형은 dict 이며, dictionary의 약자

```python
  type(dictbox)
```

> 결과
```
  dict
```

<br>

### 03. 딕셔너리 값 출력
- 딕셔너리 변수명[key]로 value(값) 확인 가능

```python
  print(dictbox['name'])
  print(dictbox['age'])
```

> 결과
```
  최승철
  30
```

<br>

### 04. 딕셔너리 값 변경
- 대괄호 안에 key 입력 후 새로운 값(value) 변경 가능

```python
  dictbox['name'] = '윤정한'
  dictbox['name']
```

> 결과
```
  '윤정한'
```

<br>

### 05. 딕셔너리 키
- 딕셔너리 변수에 ".keys()"를 사용해 전체 key만 확인 가능

```python
  dictbox.keys()
```

> 결과
```
  dict_keys(['name', 'age'])
```

<br>

### 06. 딕셔너리 값
- 딕셔너리 변수에 ".values()"를 사용해 전체 value만 확인 가능

```python
  dictbox.values()
```

> 결과
```
  dict_values(['윤정한', 30])
```

<br>

### 07. 딕셔너리 키와 값
- 딕셔너리 변수에 ".items()"를 사용해 전체 key와 value 확인 가능

```python
  dictbox.items()
```

> 결과
```
  dict_items([('name', '윤정한'), ('age', 30)])
```

<br>

### 08. 딕셔너리를 리스트로 변환
- value만 리스트 형태로 변경하고 싶을 경우 list()로 묶어주면 변환 가능

```python
  list(dictbox.values())
```

> 결과
```
  ['윤정한', 30]
```

<br>

### 09. 딕셔너리 생성(변수)
- 딕셔너리를 만들 때 key나 value에 변수 사용 가능

  - 변수에 담겨진 값이 전달되어 딕셔너리 생성
 
```python
  a = '합격기원'
  b = '수험번호'
  c = 123456789
  
  dictbox = {'닉네임':a, b:c}
  dictbox
```

> 결과
```
  {'닉네임': '합격기원', '수험번호': 123456789}
```

<br>

### 10. 딕셔너리 생성(리스트)
- 딕셔너리를 만들 때 리스트 활용 가능

  - 작업형2에서 이 방법 응용해 사용
    
```python
  listbox1 = ['파스타', '스테이크', '샐러드']
  listbox2 = [4.8, 4.9, 3.7]
  
  dictbox = {'메뉴':listbox1, '평점':listbox2}
  dictbox
```

> 결과
```
  {'메뉴': ['파스타', '스테이크', '샐러드'], '평점': [4.8, 4.9, 3.7]}
```

<br>

---

<br>

SECTION11 인덱싱과 슬라이싱
---
- 순서가 있는 리스트, 문자열과 같은 자료형에 사용 가능

  - 딕셔너리에는 순서가 없으므로 인덱스 사용 불가, 특정 키(key)에 대한 값을 가져옴
    
- 인덱싱(indexing)

  - 리스트에서 특정한 하나의 값에 접근하는 것
 
- 슬라이싱(slicing)

  - 리스트의 특정 구간을 추출(생성)하는 것

<br>

### 01. 인덱싱
- 인덱스는 0부터 시작

- 리스트에서 가장 마지막 값을 찾을 때는 마지막 인덱스 번호 입력

  - 데이터가 많은 경우, 마이너스 기호 활용 (마이너스는 끝에서부터 값 출력)
  
    - 마지막 값을 찾는다면 "-1"
 
    - 뒤에서 두 번째 값을 찾는다면 "-2"

```python
  listbox = [2, 4, 6, 8, 10]
  print(listbox[0])   # index 0, 첫 번째 값
  print(listbox[3])   # index 3, 네 번째 값
```

> 결과
```
  2
  8
```

<br>

```python
  print(listbox[-1])
```

> 결과
```
  10
```

<br>

### 02. 슬라이싱
- 순서가 있는 자료형에서 범위를 지정하여 특정 부분을 추출해 새로운 리스트로 생성

- list[시작 인덱스:끝 인덱스] 입력시 슬라이싱

  - 끝 지점 앞까지만 슬라이싱 된다는 점 주의

```python
  print(listbox[0:3])
```

> 결과
```
  [2, 4, 6]
```

<br>

```python
  print(listbox[1:3])
```

> 결과
```
  [4, 6]
```

<br>

- 끝 인덱스 값 생략시 마지막까지 슬라이싱
```python
  print(listbox[3:])
```

> 결과
```
  [8, 10]
```

<br>

- 시작 인덱스 값 생략시 처음부터 슬라이싱
```python
  print(listbox[:3])
```

> 결과
```
  [2, 4, 6]
```

<br>

- list[시작 인덱스:끝 인덱스:간격]

  - 간격은 시작부터 끝까지 N개씩 인덱스 건너뛸 수 있음
    
```python
  print(listbox[::2])
```

> 결과
```
  [2, 6, 10]
```

<br>

#### 💡 인덱스 번호 
- 시작 지점은 '이상', 끝 지점은 포함되지 않으므로 '미만'으로 이해

<br>

### 03. 값 변경(슬라이싱 활용)
- 새로운 값 대입으로 값 변경 가능

```python
  listbox[1:3] = [10, 20]
  listbox
```

> 결과
```
  [2, 10, 20, 8, 10]
```

<br>

---

<br>

SECTION12 내장함수
---
- 사전에 정의된 함수

  - print() : 지정된 값 출력하는 함수
 
  - type() : 데이터 타입을 반환하는 함수
 
<br>

### 01. 합계
- sum() : 리스트 안에 있는 모든 값을 더하는 데 사용

  - 리스트에 포함된 모든 숫자들을 순서대로 더한 후 그 합계 반환
 
  - 불리언(Boolean) 값에도 적용 가능
 
    - True = 1, False = 0 으로 계산
   
```python
  listbox = [4, 2, 10, 6, 8]
  sum(listbox)
```

> 결과
```
  30
```

<br>

```python
  boolbox = [True, False, True]
  sum(boolbox)
```

> 결과
```
  2
```

<br>

### 02. 최댓값
- max() : 최대값 찾는 데 사용

```python
  max(listbox)
```

> 결과
```
  10
```

<br>

### 03. 최솟값
- min() : 최솟값 찾는 데 사용

```python
  min(listbox)
```

> 결과
```
  2
```

<br>

### 04. 항목의 개수
- len() : 리스트에 포함된 항목의 수, 문자열에 포함된 문자의 개수 반환

```python
  len(listbox)
```

> 결과
```
  5
```

<br>

### 05. 반올림
- round(값, 반올림 후 소수점 개수) : 숫자를 반올림하는데 사용

  - 반올림할 자리가 5 미만이면 버리고, 5 이상이면 올림
 
```python
  round(1.2345, 2), round(1.2375, 2)
```

> 결과
```
  (1.23, 1.24)
```

<br>

---

<br>

SECTION13 문자열
---
- 문자의 순서가 있는 자료형

  - 따옴표로 둘러싸여 있음
 
<br>

### 01. 문자 변경
- replace(변경 전 단어, 변경 후 단어) : 문자열에서 특정 단어 변경

```python
  text = "빅데이터 분석기사 파이썬 공부"
  text = text.replace('공부', '스터디')
  text
```

> 결과
```
  '빅데이터 분석기사 파이썬 스터디'
```

<br>

```python
  text = "빅데이터 분석기사 파이썬 공부"
  text = text.replace("파이썬","머신러닝").replace("분석기사","분석을 위한")
  text
```

> 결과
```
  '빅데이터 분석을 위한 머신러닝 공부' 
```

<br>

### 02. 문자열 슬라이싱
- 문자열도 순서가 있는 자료형이므로 인덱싱과 슬라이싱 가능

  - 띄어쓰기도 포함
 
```python
  text = '안녕하세요! 함께 성장해요.'
  text[:2]
```

> 결과
```
  '안녕'
```

<br>

```python
  text[7:9]
```

> 결과
```
  '함께'
```

<br>

```python
  date = '2024-12-25'
  date[5:]
```

> 결과
```
  '12-25'
```

<br>

#### 💡 문자열 출력시 따옴표
- print() 함수 사용시 따옴표 없이 출력되나, 자동 출력시에는 작은따옴표가 붙음

  - 자동 출력시 나타나는 작은따옴포는 신경쓰지 않아도 OK
 
<br>

### 03. 문자열 분리
- split() : 데이터에서 띄어쓰기나 특정 문자를 기준으로 값을 구분할 때 사용

  - 값을 구분한 후 구분된 값을 리스트로 반환
 
  - 괄호 안에 특정 문자가 없다면 띄어쓰기를 기준으로 구분
 
- 문자열을 list()로 자료형 변환하면 한 글자씩을 순서대로 값으로 가진 리스트가 됨

```python
  print(date.split('-'))
  print(text.split())
```

> 결과
```
  ['2024', '12', '25']
  ['안녕하세요!', '함께', '성장해요.']
```

<br>

```python
  list(date)
```

> 결과
```
  ['2', '0', '2', '4', '-', '1', '2', '-', '2', '5']
```

<br>

---

<br>

SECTION14 반복문
---
- 데이터만 다르고 같은 작업을 여러 번 처리할 때 사용

  - 빅분기 실기시 리스트에 있는 값을 하나씩 불러와 동일한 작업 수행 필요

<br>

### 01. for 함수
- 리스트에 있는 모든 값 출력 가능

  - for 변수명 in 리스트 :
  
    - 리스트에 있는 모든 값을 반복해 불러옴
   
    - 리스트의 값을 순서대로 불러와 '변수명'에 넣고, for 아래의 들여쓰기 된 코드 실행
   
  - 리스트에 있는 문자도 반복문으로 출력 가능

<br>

```python
  listbox = [2, 4, 6, 8, 10]
  for item in listbox :
      print(item)
```

> 결과
```
  2
  4
  6
  8
  10
```

<br>

```python
  listbox = ['빅데이터', '분석', '기사']
  for i in listbox :
      print(i)
```

> 결과
```
  빅데이터
  분석
  기사
```

<br>

### 02. for문 코드 범위
- 반복문 안의 들여쓰기에 해당하는 코드가 모두 실행된 후 반복문 밖의 코드가 순서대로 실행

```python
  listbox = [2, 4, 6, 8, 10]
  for item in listbox :
      print(item)
  print('끝')
```

> 결과
```
  2
  4
  6
  8
  10
  끝
```

<br>

```python
  listbox = [2, 4, 6, 8, 10]
  for item in listbox :
      result = item + 1
      print(result)
```

> 결과
```
  3
  5
  7
  9
  11
```

<br>

### 03. range() 활용
- 반복문을 활용할 때 list() 외에도 range() 활용 가능

- range(N) : 0부터 N-1까지의 숫자를 나열

  - 반복문에서 활용시 N개만큼 반복 가능
 
- range(시작 숫자, 끝 숫자) : 시작 숫자부터 끝 숫자 앞까지의 숫자를 나열
 
```python
  for item in range(5) :
      print(item)
```

> 결과
```
  0
  1
  2
  3
  4
```

<br>

```python
  for item in range(5, 10) :
      print(item)
```

> 결과
```
  5
  6
  7
  8
  9
```

<br>

### 04. list.append()
- 리스트에 값을 추가하는 함수

```python
  listbox = []
  for i in range(1,6) :
      listbox.append(i)
      
  listbox
```

> 결과
```
  [1, 2, 3, 4, 5]
```

<br>

### 05. enumerate()
- 리스트에 있는 값을 출력할 때 인덱스 번호를 함께 알고 싶은 경우 사용

- 반복문에 사용되며, 인덱스와 값을 함께 반환

  - for문 안에 2개 변수 작성
 
    - 첫 번째 변수 : 인덱스
   
    - 두 번째 변수 : 리스트에 있는 값을 받을 변수

```python
  listbox = ['빅데이터', '분석', '기사', '합격']
  for index, item in enumerate(listbox) :
      print(index, item)
```

> 결과
```
  0 빅데이터
  1 분석
  2 기사
  3 합격
```

<br>

### 06. zip()
- 여러 개의 값을 묶어주는 역할

```python
  person_info = {
      'name' : '윤정한',
      'age' : 30,
      'city' : '서울',
      'hobbies' : ['돌키우기', '레고조립', '웨이크보드']
  }
  
  for k, v in zip(person_info.keys(), person_info.values()) :
      print(k, v)
```

> 결과
```
  name 윤정한
  age 30
  city 서울
  hobbies ['돌키우기', '레고조립', '웨이크보드']
```

<br>

---

<br>

SECTION15 함수
---
- 프로그램에서 재사용 가능한 코드 블록

- 필요한 함수가 있다면 def로 함수를 만들어 사용 가능 (def는 define 약자)

- 함수 정의를 먼저 하고 함수를 실행해야 함

<br>

### 01. 일반 함수
- def 함수명() 으로 함수 정의 후 여러 번 실행 가능

```python
  def hello() :   # 함수 정의
      print('안녕하세요!')
      
  hello()         # 함수 호출
  hello()         # 함수 호출
  hello()         # 함수 호출
```

> 결과
```
  안녕하세요!
  안녕하세요!
  안녕하세요!
```

<br>

### 02. 매개변수가 있는 함수
- 매개변수(parameters) : 함수를 사용할 때 과호 안에 넣는 변수

  - 함수에 전달되는 값을 받기 위해 사용되는 변수
 
  - 함수를 실행할 때 괄호 안에 값을 넘겨주고 함수에서 매개변수 name에 그 값을 대입
 
```python
  def hello(name) :
      print('hello ' + name)
      
  hello('빅분기')
```

> 결과
```
  hello 빅분기
```

<br>

#### 💡 매개변수의 범위
- 매개변수 name은 일반 변수와 달리, hello() 함수 안에서만 사용 가능

  - 함수 밖에서 print(name) 출력시 'name 변수를 알 수 없다'라는 에러 발생

```python
  def hello(name) :
      print(name)
  print(name)
  
  hello('빅분기')
```

> 결과
```
  NameError                                 Traceback (most recent call last)
  Cell In[5], line 3
        1 def hello(name) :
        2     print(name)
  ----> 3 print(name)
        5 hello('빅분기')
  
  NameError: name 'name' is not defined
```

<br>

```python
  def plus(x, y) :
      print(x + y)
      
  # 함수 호출
  a = 2
  b = 3
  plus(a, b)
```

> 결과
```
  5
```

<br>

### 03. 반환 값이 있는 함수
- 함수에서 가장 많이 활용하는 것은 반환(return)

  - 함수 안에서 작업이 진행되고 작업 결과를 반환받음
 
- ex) len() 함수는 개수를 return, max() 함수는 최댓값을 return

- 반환 값은 복수도 가능

```python
  def plus(x, y) :
      result = x + y
      return result
  
  a = plus(2, 3)
  print(a)
```

> 결과
```
  5
```

<br>

```python
  listbox = [15, 46, 78, 24, 56]
  def min_max(data) :
      mi = min(data)
      ma = max(data)
      return mi, ma
  
  a, b = min_max(listbox)
  print(a, b)
```

> 결과
```
  15 78
```

<br>

```python
  listbox = [15, 46, 78, 24, 56]
  def mean(data) :
      return sum(data) / len(data)
  
  mean(listbox)
```

> 결과
```
  43.8
```

<br>





































