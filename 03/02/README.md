# CHAPTER02 분산 분석
- 분산 분석(ANOVA, 아노바) : 여러 집단의 평균 차이를 통계적으로 유의미한지 검정하는 방법

  - 주로 3개 이상의 집단을 비교할 때 사용
 
    - 일원 분산 분석 : 단일 요인의 수준 간 평균의 차이 검정
   
    - 이원 분산 분석 : 두 요인의 수준 간 및 그들의 상호작용이 평균에 미치는 영향 검정
   
- 요인(factor) : 독립변수

  - 머신러닝에서는 '피처' 또는 '변수'
 
  - 통계학에서는 '요인' 또는 '독립변수'

<br>

SECTION01 일원 분산 분석(One-way ANOVA)
---
- 3개 이상의 집단 간의 평균 차이가 통계적으로 유의한지 검정하는 방법

  - 집단을 나누는 요인이 하나고 집단의 수가 3개 이상일 때 사용
 
    - 집단을 나누는 요인이 하나고 집단의 수가 2개일 때는 t-검정 실시

<br>

### 01. 기본 가정
- 분산 분석의 기존 가정은 독립 표본 t-검정과 유사

  - 독립성, 정규성, 등분산성을 기본 가정으로 함
 
    - **독립성** : 각 집단의 관측치들은 모두 다르 집단의 관측치들과 독립적(기본 가정)
   
    - **정규성** : 각 집단에서의 관측치는 정규 분포를 따름(Shapiro-Wilk test)
   
    - **등분산성** : 모든 집단에서의 관측치는 동일한 분산을 가짐(Levene test)

<br>

### 02. 귀무가설과 대립가설
- 귀무가설(H₀) : 모든 집단의 평균은 동일하다

- 대립가설(H₁) : 집단의 평균에는 차이가 있다

  - 모두 같다고 할 수 없지만 적어도 두 그룹 간의 평균에는 차이가 있다

<br>

### 03. 일원 분산 분석
- 사이파이의 f_oneway 사용

> 코드
```python
  scipy.stats.f_oneway(sample1, sample2, sample3, ...)
```
- sample1 : 첫 번째 집단 데이터
  
- sample2 : 두 번째 집단 데이터

- sample3 : 세 번째 집단 데이터

<br>

#### ✏️ 문제
> 주어진 데이터는 4종류의 비료를 사용한 식물의 성장에 대한 실험 결과이다.<br>
> 이 실험에서는 비슷한 조건의 식물 40개를 무작위로 10개씩 나누고 화학비료 A, B, C, D 를 일정 기간 사용 후 <br>
> 성장량을 측정했다. 성장의 차이가 있는지 유의수준 0.05 하에서 검정하시오.<br>

- 귀무가설(H₀) : 네 가지 비료의 효과는 동일하다

- 대립가설(H₁) : 비료의 효과에는 차이가 있다(적어도 두 가지 비료의 효과에는 차이가 있다)

> 코드
```python
  import pandas as pd
  df = pd.DataFrame({
      'A' : [10.5, 11.3, 10.8, 9.6, 11.1, 10.2, 10.9, 11.4, 10.5, 10.3],
      'B' : [11.9, 12.4, 12.1, 13.2, 12.5, 11.8, 12.2, 12.9, 12.4, 12.3],
      'C' : [11.2, 11.7, 11.6, 10.9, 11.3, 11.1, 10.8, 11.5, 11.4, 11.0],
      'D' : [9.8, 9.4, 9.1, 9.5, 9.6, 9.9, 9.2, 9.7, 9.3, 9.4]
  })
  print(df.head(2))
```

> 결과
```python
        A     B     C    D
  0  10.5  11.9  11.2  9.8
  1  11.3  12.4  11.7  9.4
```

<br>

> 코드
```python
  from scipy import stats
  
  print('==== 정규성 검정 ====')
  print(stats.shapiro(df['A']))
  print(stats.shapiro(df['B']))
  print(stats.shapiro(df['C']))
  print(stats.shapiro(df['D']))
  
  print('\n==== 등분산성 검정 ====')
  print(stats.levene(df['A'], df['B'], df['C'], df['D']))
  
  print('\n==== 일원 분산 분석 ====')
  print(stats.f_oneway(df['A'], df['B'], df['C'], df['D']))
```

> 결과
```python
  ==== 정규성 검정 ====
  ShapiroResult(statistic=0.9649054066073813, pvalue=0.8400161543468654)
  ShapiroResult(statistic=0.9468040874196029, pvalue=0.6308700692815115)
  ShapiroResult(statistic=0.9701646110856055, pvalue=0.892367306190296)
  ShapiroResult(statistic=0.9752339025839644, pvalue=0.9346854448707653)
  
  ==== 등분산성 검정 ====
  LeveneResult(statistic=1.9355354288758708, pvalue=0.14127835331346628)
  
  ==== 일원 분산 분석 ====
  F_onewayResult(statistic=89.12613851177174, pvalue=1.001838152252373e-16)
```
- 정규성 검정(Shapiro-Wilk test)

  - A, B, C, D 의 모든 그룹에 대한 p-value > 0.05
 
    - 모든 그룹의 데이터가 정규 분포를 따름
   
- 등분산성 검정(Levene test)

  - p-value > 0.05
 
    - 모든 그룹의 분산이 동일
   
  - 레빈 검정은 center=mean 과 center=median 존재
 
    - mean : Levene(레빈) 검정
   
    - median : Brown-Forsythe(브라운 포사이드) 검정
   
- 일원 분산 분석(One-way ANOVA)

  - p-value < 0.05
 
    - 적어도 두 그룹 간의 평균 성장량에는 차이가 있다고 볼 수 있음

    - 모든 비료의 효과가 동일하다는 귀무가설 기각, 대립가설 채택
      
<br>

### 04. 일원 분산 분석(ols 활용)
- 일원 분산 분석 방법

  - 사이파이(scipy)의 f_oneway
 
  - 스태츠모델즈(statsmodels)의 ols.anova_lm
 
    - 제공된 데이터가 ols 입력 데이터로 적합하지 않은 경우 변경
   
      - 데이터 전처리는 주어진 데이터에 따라 작업할 뿐 분산분석의 필수 내용은 아님

> 코드
```pyrhon
  import pandas as pd
  df = pd.read_csv('./data/fertilizer.csv')
  df.head()
```

> 결과

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>비료</th>
      <th>성장</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>10.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A</td>
      <td>11.3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A</td>
      <td>10.8</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A</td>
      <td>9.6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A</td>
      <td>11.1</td>
    </tr>
  </tbody>
</table>
</div>

<br>

- ols 와 anova_lm 사용해 선형 모델 학습 및 결과 출력

  - ols() 함수는 R 스타일의 표현식(formula) 사용
 
|구분|설명|
|:-:|-|
|물결(~)|종속변수와 독립변수를 구분하는 기호<br>ex) target ~ a 에서 target 은 종속변수, a 는 독립변수|
|더하기(+)|여러 독립변수들을 모델에 포함하기 위한 기호<br>ex) target ~ a + b + c + d 는 a, b, c, d 독립변수를 모두 포함하겠다는 의미|

<br>

> 코드
```python
  from statsmodels.formula.api import ols
  from statsmodels.stats.anova import anova_lm
  model = ols('성장 ~ C(비료)', df).fit()
  print(anova_lm(model))
```

> 결과
```python
              df    sum_sq    mean_sq          F        PR(>F)
  C(비료)      3.0  43.21875  14.406250  89.126139  1.001838e-16
  Residual  36.0   5.81900   0.161639        NaN           NaN
```
- 사이파이(scipy)의 f_oneway 의 F-통계량과 p-value 동일

- C() 사용하면 이 변수가 범주형 변수임을 명시

  - variable 변수는 문자이기에 자동 원핫인코딩 처리하므로 C() 가 없더라도 결과는 같음

<br>

|구분|설명|
|:-:|-|
|df<br>(자유도, degree of freedom)|전체 데이터(관찰) 수 : 4 * 10 = 40<br>전체 데이터(관찰) 수의 자유도 : 40 - 1 = 39<br>그룹(처리 조건)의 자유도 : 4 - 1 = 3<br>잔차의 자유도 : 39 - 3 = 36|
|sum_sq<br>(제곱합, SS)|그룹(처리 조건)별 또는 잔차별 제곱합(sum of squares)|
|mean_sq<br>(평균 제곱, MS)|평균 제곱합(mean of sum of squares)으로 sum_sq 를 df 로 나눈 값|
|F(F-통계량)|F-통계량|
|PR(>F)(p-값)|F-통계량에 대한 p-value|

<br>

---

<br>

SECTION02 이원 분산 분석
---



<br>



























