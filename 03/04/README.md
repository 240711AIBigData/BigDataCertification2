# CHAPTER04 회귀분석
- 수치형 변수 간의 관계 또는 Input(원인)과 Output(결과) 간의 관계를 추정하거나 예측하는 데 사용

  - 통계에서의 Input(원인) : 독립(independent) 변수
 
  - 통계에서의 Output(결과) : 종속(dependent) 변수

> ex
```
  회귀 모델은 빅분기 실기 학습 시간을 독립변수, 성적을 종속변수로 두고 학습 시간에 따라 시험 성적을 예측하는 것이 목적

  독립변수는 학습 시간 1개가 아니라 수험생 나이 등 2개 이상일 수도 있음
```

- 상관계수 : 변수 간의 강도와 방향을 측정하는 방법 (변수 간의 관계 파악)

  - 두 변수 간의 양의 상관관계, 음의 상관관계, 상관관계 없음을 확인
 
- 회귀모델(Regression Model) : Input(원인)과 Output(결과)의 관계를 설명하는 것

  - 선형 회귀모델 : 수치 변수 간의 인과 관계를 설명하는 대표적인 모델
 
    - 단순 선형 회귀 : 독립변수가 1개
   
      - 하나의 독립변수와 하나의 종속변수의 관계를 고려해 직선의 1차 방정식 찾아냄
     
      - y = ax + b (a : 기울기(회귀계수), b : y절편(상수항))
   
    - 다중 선형 회귀 : 독립변수가 2개 이상
   
      - 2개 이상의 독립변수 고려

<br>

SECTION01 상관계수(Correlation Coefficient)
---
- 두 변수 간의 선형적인 관계가 어느 정도 강한지를 나타냄

  - -1 ≤ r ≤ 1
 
  - r 이 1 에 가까울수록 강한 양의 선형관계 의미
 
  - r 이 0 에 가까울수록 약한 선형관계 의미
 
  - r 이 -1 에 가까울수록 강한 음의 선형관계 의미
 
- 연속형이 두 변수 간의 관계는 산점도를 통해 그래프로 그릴 수 있음 

|양(positive)의 상관관계)|음(negative)의 상관관계|
|:-:|:-:|
|![이미지](./img/01.png)|![이미지](./img/02.png)|
|x 값이 증가함에 따라 y 값 증가|x 값이 증가함에 따라 y 값 감소|

<br>

### 01. 상관 계수
> 상관 계수를 구할 때는 판다스의 corr() 함수 사용
```python
  pandas.DataFrame.corr(method='pearson', numeric_only=False)
```
- method : 상관 관계 방법

  - pearson : 피어슨(기본값)
 
  - kendall : 켄달의 타우(Kendall's tau)
 
  - spearman : 스피어만
 
- numeric_only : 숫자 자료형만 포함 여부(기본값 False)

<br>

#### ✏️ 문제
> 다음은 학생들의 키와 몸무게 데이터다. 이를 바탕으로 상관 계수를 구하라.

|학생|키(cm)|몸무게(kg)|
|:-:|:-:|:-:|
|A|150|42|
|B|160|50|
|C|170|70|
|D|175|64|
|E|165|56|

<br>

> 코드
```python
  import pandas as pd
  
  # 주어진 데이터
  data = {
      '키' : [150, 160, 170, 175, 165],
      '몸무게' : [42, 50, 70, 64, 56]
  }
  
  df = pd.DataFrame(data)
  
  # 상관계수 계산
  correlation = df.corr()
  print(correlation)
```
- 판다스 데이터프레임에서 제공하는 corr() 함수를 활용하면 상관 계수 구할 수 있음

  - corr : correlation 약자

> 결과
```python
            키       몸무게
  키      1.000000  0.919509
  몸무게  0.919509  1.000000
```
- 같은 변수인 키의 상관계수, 몸무게와 몸무게의 상관 계수는 1

  - 키와 몸무게의 상관계수 : 0.919509

<br>

> 키와 몸무게의 상관관계 값만 출력하고자 한다면 iloc 활용
```python
  print(correlation.iloc[0,1])
```
- 키와 몸무게의 상관관계가 두 군데 있으므로 하나 선택

> 결과
```python
  0.9195090879163764
```

<br>

> 두 변수에 대한 상관관계만 구하기
```python
  print(df['키'].corr(df['몸무게']))
  print(df['몸무게'].corr(df['키']))
```
- df['컬럼'].corr(df['컬럼']) 방법 사용

  - 컬럼 순서 개의치 않음

> 결과
```python
  0.9195090879163765
  0.9195090879163765
```
- 결과 값이 소수 끝자리에서 다를 수도 있으나 일반적으로 문제에서는 소수 둘째~넷째 자리에서 반올림 처리하므로 영향 X

<br>

> method 파라미터
```python
  # 피어슨 상관계수(기본값)
  print(df.corr())
  
  # 스피어만 상관계수
  print(df.corr(method='spearman'))
  
  # 켄달의 타우 상관계수
  print(df.corr(method='kendall'))
```
- 판다스에서 기본적으로 피어슨(Pearson) 상관계수 계산

  - method 파라미터 활용해 다른 종류의 상관계수 계산 가능

> 결과
```python
              키       몸무게
  키      1.000000  0.919509
  몸무게  0.919509  1.000000
         키  몸무게
  키      1.0  0.9
  몸무게  0.9  1.0
         키  몸무게
  키      1.0  0.8
  몸무게  0.8  1.0
```

<br>

### 02. 두 변수의 상관계수와 t-검정
- 두 변수의 상관계수와 t-검정 결과 확인 가능

  - 일반적으로 t-검정을 묻는다면 피어슨 상관계수 값이 표준

> 코드
```python
  from scipy import stats
  
  # 피어슨 상관계수와 p-value 계산
  print(stats.pearsonr(df['몸무게'], df['키']))
  
  # 스피어만 상관계수와 p-value 계산
  print(stats.spearmanr(df['몸무게'], df['키']))
  
  # 켄달의 타우 상관계수와 p-value 계산
  print(stats.kendalltau(df['몸무게'], df['키']))
```

> 결과
```python
  PearsonRResult(statistic=0.9195090879163765, pvalue=0.027079456895589476)
  SignificanceResult(statistic=0.8999999999999998, pvalue=0.03738607346849874)
  SignificanceResult(statistic=0.7999999999999999, pvalue=0.08333333333333333)
```

<br>

---

<br>

SECTION02 단순 선형 회귀 분석
---
- 회귀 분석(Regression Analysis)

  - 2개 이상의 변수 간의 관계를 파악하려는 통계적 분석 방법
 
  - 원인과 결과 간의 관계를 수학적으로 모델링해 예측할 수 있도록 도와줌

- 단순 선형 회귀(Simple Linear Regression) 분석

  - 하나의 독립변수로부터 하나의 종속변수와의 관계를 분석하거나 예측하는 방법
 
- ex) 키워드 광고를 많이 하면 판매량이 어떻게 변할까?

  -  **독립변수(X)** : 원인을 나타내는 데이터 (키워드 광고)
 
  - **종속변수(y)** : 결과를 나타내는 데이터 (판매량)

<br>

### 01. 단순 회귀 분석과 다중 회귀 분석
- 회귀 분석의 유형 : 독립변수의 개수에 따라 달라짐

  - **단순 회귀 분석** : 독립변수(원인)가 하나일 때 (키워드 광고만으로 판매량 예측)
 
  - **다중 회귀 분석** : 독립변수(원인)가 여러 개일 때 (키워드 광고, 직원 수, 서비스로 판매량 예측)

<br>

<details>
  <summary>💡 머신러닝과 통계학 용어</summary>

<br>

- 머신러닝과 통계학에서 같은 개념을 다르게 표현하는 경우 有

|머신러닝|통계학|예시|
|:-:|:-:|:-:|
|X 데이터,<br>features(특징, 피처)|톡립변수,<br>설명변수|온도, 강수량, 습도, 시간, 평일/주말 등|
|y 데이터,<br>label,<br>target|종속변수,<br>반응변수,<br>결과변수|매출액, 주문량 등|

<br>

</details>

#### (1) 단순 선형 회귀식
```
  y = α + βX + ε
```
- X : 독립변수

- y : 종속변수

- α(알파) : 절편(상수항)

- β(베타) : 기울기(X를 1 증가시켰을 때 y의 증가량)

- ε(엡실론) : 오차항(모델이 설명하지 못하는 부분)

- X 와 y 를 가장 잘 나타내는 직선을 찾기 위해 β₀(y절편)와 β₁(기울기) 값 추정

<br>

#### (2) 단순 선형 회귀선
|키와 몸무게 데이터를 바탕으로 만든 회귀 모델을 시각화한 회귀선|
|-|
|![이미지](./img/03.png)|
|- 이 회귀선은 데이터를 모두 설명하는 완벽한 직선을 만들 수는 없지만, 각 데이터를 잘 설명하는 가장 좋은 직선을 찾을 수 있음<br><br>- 예측된 회귀선과 실제 data 는 일치하지 않는 경우가 많은데, 이 실제 값과 예측값의 차이가 잔차(residual)<br><br>- 잔차가 0에 가깡루수록 회귀선ㅇ니 실제 값을 잘 설명한다고 할 수 있음|

<br>

- **최소제곱법(Ordinary Least Squares)**

  - 관측된 값과 회귀 모델의 예측값 간의 차이(잔차)의 제곱합을 최소화하는 것
 
  - 회귀 분석 모델을 만들 때 기본적으로 최소제곱법(OLS) 활용
 
  - 회귀 분석 실습에서는 statsmodels 의 ols() 함수 활용
 
    - ols 방법을 사용해 선형 회귀 모델 구축

- **ols 모델**

  - 최소제곱 선형 모델을 구축하는 데는 statsmodels 의 ols() 함수 사용
 
    - 종속변수와 하나 이상의 독립변수 간의 선형 관계를 모델링하는 데 사용됨
   
  - statsmodels 의 ols() 함수 중 R 스타일(formula, 공식)로 사용 가능한 ols() 함수 사용

```python
  ols('종속변수~독립변수', data=df).fit()
```
- 종속변수와 독립변수 사이에는 물결(~) 표시 사용

  - 주의 : df['컬럼명'] 이 아니라 컬럼명만 작성
 
- 종속변수 : 모델에서 예측하려는 변수 (ex. 작업형2 에서 target 데이터)

- 독립변수 : 종속변수에 영향을 미치는 독립적인 변수 (ex. 작업형2 에서 target 을 제외한 train 데이터)

- data=df : df 에서 변수를 찾아 사용하도록 데이터 연결

- \.fit() : ols 모델을 주어진 데이터에 학습(적합)시킴

<br>

<details>
  <summary>💡 R 스타일 사용 이유</summary>

<br>

- 작업형2에서 사용하는 학습(fit) 방식과 유사한 statsmodels.api 의 OLS 有

  - 상수항(절편)을 수동으로 직접 처리(코딩)해야 하는 번거로움 존재
 
- 상수항을 자동으로 처리해주는 statsmodels.formula.api 의 ols 사용, formula 는 R 스타일 사용

|구분|주의|특징|
|:-:|:-:|:-:|
|statsmodels.formula.api 의 ols<br>(함수)|소문자로 사용<br>ols()|R 스타일의 공식을 사용해 모델을 생성하고, 결과를 분석<br>ols(종송변수 ~ 독립변수1 + 독립변수2, data=df)|
|statsmodles.api 의 OLS<br>(클래스)|대문자로 사용<br>OLS()|작업형2에서 사용했던 model.fit(X, y) 방식과 유사<br>단, OLS(y, X).fit() 로 순서가 다름<br>OLS(종속변수, 독립변수 데이터프레임)|

<br>

</details>

- **제곱합**

  - 선형 회귀에서 제곱합(Sum of Squares)은 모델이 데이터를 잘 설명하는가(적합도)를 평가하는 데 사용
 
  - 선형 회귀는 최소제곱법 적용
 
    - 최소제곱법 : SSE 를 최소화하는 회귀 계수를 찾는 것

|용어(영문)|용어(해석)|의미|
|:-:|:-:|:-:|
|SST<br>(Sum of Squares Total)|총 제곱합|각 관측치가 평균으로부터 얼마나 떨어져 있는지를 나타냄<br>SST = SSR + SSE|
|SSR<br>(Sum of Squares for Regression)|회귀 제곱합|회귀선이 평균으로부터 얼마나 떨어져 있는지를 나타냄|
|SSE<br>(Sum of Squares for Error)|오차 제곱합<br>(잔차 제곱합)|관측치가 회귀선으로부터 얼마나 떨어져 있는지를 나타냄|

|-|
|-|
|![이미지](./img/04.png)|

<br>

- **결정계수(R-squared)**

  - 모델이 그 데이터를 얼마나 잘 설명하느냐를 나타내는 통계값
 
  - 머신러닝(작업형2) 회귀 평가지표 중에 결정 계수(R²) 구하는 방법
 
    - R² = SSR / SST
   
      - 1 에 가까울수록 데이터를 잘 설명한다는 뜻
     
      - 0 에 가깝거나 음수가 나오는 경우 모델이 데이터를 잘 설명하지 못한다는 뜻

<br>

#### ✏️ 문제
> 다음은 20명의 키와 몸무게에 관한 정보다. 이 데이터를 바탕으로 회귀 모델을 구축하고 각 소문제의 값을 구하시오.

> 코드
```python
  import pandas as pd
  
  data = {
      '키' : [150, 160, 170, 175, 165, 155, 172, 168, 174, 158, 162, 173, 156, 159, 167, 163, 171, 169, 176, 161],
      '몸무게' : [42, 50, 70, 64, 56, 48, 68, 60, 65, 52, 54, 67, 49, 51, 58, 55, 69, 61, 66, 53]
  }
  
  df = pd.DataFrame(data)
```

<br>

**1. 주어진 데이터로 최소제곱법을 이용한 단순 선형 회귀 모델을 구축하고 통계적 요약 출력**
> 코드
```python
  from statsmodels.formula.api import ols
  model = ols('키 ~ 몸무게', data=df).fit()
  print(model.summary())
```
- statsmodels.formula.api 에서 ols() 함수 불러오기

- 키는 종속변수, 몸무게는 독립변수로 설정하고 선형 회귀 모델 생성

- R 스타일은 종속변수가 먼저 온다는 점에 유의

- model.summary() 함수 : 통계적 요약 결과 확인 가능

> 결과
```python
                              OLS Regression Results                            
  ==============================================================================
  Dep. Variable:                      키   R-squared:                       0.892
  Model:                            OLS   Adj. R-squared:                  0.886
  Method:                 Least Squares   F-statistic:                     148.0
  Date:                Mon, 18 Nov 2024   Prob (F-statistic):           4.04e-10
  Time:                        09:44:49   Log-Likelihood:                -45.761
  No. Observations:                  20   AIC:                             95.52
  Df Residuals:                      18   BIC:                             97.51
  Df Model:                           1                                         
  Covariance Type:            nonrobust                                         
  ==============================================================================
                   coef    std err          t      P>|t|      [0.025      0.975]
  ------------------------------------------------------------------------------
  Intercept    115.0676      4.158     27.671      0.000     106.331     123.804
  몸무게         0.8658      0.071     12.167      0.000       0.716       1.015
  ==============================================================================
  Omnibus:                        0.985   Durbin-Watson:                   2.609
  Prob(Omnibus):                  0.611   Jarque-Bera (JB):                0.336
  Skew:                          -0.315   Prob(JB):                        0.845
  Kurtosis:                       3.082   Cond. No.                         432.
  ==============================================================================
  
  Notes:
  [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
```
- 몸무게의 기울기 : coef 0.8658

- 절편(Intercept)의 기울기 : coef 115.0676

- 결정 계수 : R-squared 0.892

- 몸무게의 p-value : 0.000 (0에 가까운 값으로 정확한 값은 별도 출력 필요)

<br>

<details>
  <summary>💡 모델의 요약 결과 설명</summary>

<br>

|용어|의미|
|:-:|-|
|Dep. Variable|종속변수|
|R-squared|결정 계수|
|Adj. R-squared|조정된 결정 계수|
|Method|사용된 방법 ⇒ 'Least Sqaures(최소제곱법)'|
|F-statistic|F-통계량|
|Prob (F-statistic)|F-통계량의 유의확률, 일반적으로 0.05 이하의 회귀 모델이 유의미함|
|Log-Likelihood|로그 우도(모델의 적합도, 최대화하는 것이 좋음)|
|AIC & BIC|모델의 적합도와 복잡성 사이의 균형을 평가하는 척도, 작은 값이 더 좋은 모델을 의미함|
|No. Observations|관측치 수(데이터 수)|
|Df Residuals|잔차의 자유도|
|Df Model|모델의 자유도|
|Covariance Type|공분산 유형|
|coef|각 변수의 계수 ⇒ 'Intercept' 는 상수항(절편), '몸무게'는 몸무게의 계수(기울기)를 나타냄|
|std err|계수의 표준 오차|
|t|t 통계량(검정 통계량|
|P>\|t\||각 계수의 t 통계량에 대한 p-value|
|[0.025 0.975]|95% 신뢰 구간, 각 계수에 대한 95% 신뢰 구간|

<br>

</details>

**2. 회귀 모델의 결정 계수 구하기**
- model.summary() 함수 값을 확인하는 방법 or 별도 값만 출력

> 별도 값만 출력
```python
  print('결정계수 :', model.rsquared)
```

> 결과
```python
  결정계수 : 0.8915914350087262
```

<br>

**3. 회귀 모델에서 회귀 계수(기울기와 절편) 구하기**
- model.params 활용해 model.summary() 함수에 있는 coef 값 출력 가능

> 코드
```python
  print('기울기 :', model.params['몸무게'])
  print('절편 :', model.params['Intercept'])
```

> 결과
```python
  기울기 : 0.8658438852380215
  절편 : 115.0676390447185
```

<br>

**4. 회귀 모델에서 몸무게의 회귀 계수가 통계적으로 유의한지 검정했을 때의 p-value 구하기**
- 결과가 지수 표기법으로 출력되어 일반 표기법으로 변경

  - 방법1 : print(format(변경할 값 또는 변수명, '.10f'))
 
  - 방법2 : print('{:.10f}'.format(변경할 값 또는 병수명))
 
> 코드
```python
  print('p-value :', model.pvalues['몸무게'])
  print('p-value :', '{:.10f}'.format(model.pvalues['몸무게']))
```

> 결과
```python
  p-value : 4.0379325599303475e-10
  p-value : 0.0000000004
```

<br>

**5. 회귀 모델을 사용해 몸무게가 67일 때의 예측 키 구하기**
- 새로운 데이터를 학습할 때 사용했던 데이터와 동일한 컬럼명으로 데이터프레임 형태 만들고 model.predict() 함수 사용

- 예측한 결과는 시리즈 형태로 값만 출력하기 위해 [0] 추가

> 코드
```python
  new_data = pd.DataFrame({'몸무게' : [67]})
  result = model.predict(new_data)
  print('몸무게가 67일 때의 예측 키 :', result[0])
```

> 결과
```python
  몸무게가 67일 때의 예측 키 : 173.07917935566593
```

<br>

**6. 회귀 모델의 잔차 제곱합 구하기**
- 잔차 : '실제(관측) 값 - 모델' 로 예측된 값

- 잔차 먼저 구하기

  - 모델로 예측된 값을 구할 때 predict(df['몸무게']) 대신 predict(df) 그대로 넣더라도 모델이 자동으로 독립변수 구분
 
- 잔차를 제곱한 값 모두 더가히

  - sum() 함수는 (df['잔차'] ** 2).sum() 형태로 사용해도 결과는 같음

> 코드
```python
  df['잔차'] = df['키'] - model.predict(df)
  print('잔차 제곱합 :', sum(df['잔차']**2))
```

> 결과
```python
  잔차 제곱합 : 113.74226638884441
```

<br>

**7. 회귀 모델의 MSE 구하기**
- MSE : 평균 제곱 오차(Mean Squared Error), 잔차들의 평균

|-|
|-|
|![이미지](./img/05.png)|

> 코드
```python
  df['잔차'] = df['키'] - model.predict(df)
  MSE = (df['잔차']**2).mean()
  print('MSE :', MSE)
```

> 결과
```python
  MSE : 5.68711331944222
```

<br>

> 사이킷런에서 제공하는 MSE 평가지표 결과
```python
  from sklearn.metrics import mean_squared_error
  pred = model.predict(df['몸무게'])
  mse = mean_squared_error(df['키'], pred)
  print('MES :', mse)
```

> 결과
```python
  MSE : 5.68711331944222
```
- 직접 계산한 MSE 와 결과가 같음

<br>

<details>
  <summary>💡 부동 소수점 연산</summary>

<br>

- 직접 잔차를 계산한 MSE 와 사이킷런의 MSE 결과에 미세한 차이가 있을 수도 있음

  - 보통 소수점 끝자리에서 다름
 
- 차이는 매우 미미하며, 실제 시험에서 문제가 출제된다면 정답이 동일하게 소수 0~6 자리에서 반올림 처리

- 부동 소수점 연산의 미세한 불일치로 인해 발생

  - 부동 소수점 : 컴퓨터에서 소수점이 있는 숫자를 표현하고 연산하는 방식

<br>

</details>

#### ✏️ 심화
**1. 몸무게의 95% 신뢰 구간 구하기**
- model.summary() 함수로 확인 가능

- alpha 기본값은 0.05(95%)

  - 만약 문제에서 90% 신뢰 구간 구하라고 한다면 alpha 를 0.1 로 변경 가능
 
> 코드
```python
  print('신뢰구간 :\n', model.conf_int(alpha=0.05).loc['몸무게'])
```

> 결과
```python
  신뢰구간 :
  0    0.716337
  1    1.015351
  Name: 몸무게, dtype: float64
```

<br>

**2. 몸무게가 50일 때 예측 키의 신뢰 구간과 예측 구간 구하기**
- 몸무게가 50일 때 get_prediction() 함수를 사용해 예측값 및 예측 구간 구하기

- summary_frame() 함수를 사용해 예측 결과 요약

  - alpha=0.05(기본값) : 95% 신뢰수준 의미

> 코드
```python
  new_data = pd.DataFrame({'몸무게' : [50]})
  pred = model.get_prediction(new_data)
  result = pred.summary_frame(alpha=0.05)
  print('예측값의 신뢰구간과 예측구간 :\n', result)
```

> 결과
```python
  예측값의 신뢰구간과 예측구간 :
            mean   mean_se  mean_ci_lower  mean_ci_upper  obs_ci_lower  \
  0  158.359833  0.794986      156.68963     160.030037    152.820798   
  
     obs_ci_upper  
  0    163.898869  
```
- mean_ci_lower, mean_ci_upper : 예측 키의 95% 신뢰 구간의 하한과 상한 의미

- obs_ci_lower, obs_ci_upper : 예측 구간의 하한과 상한 의미

<br>

---

<br>

SECTION03 다중 선형 회귀 분석
---




<br>

---

<br>

SECTION04 범주형 변수
---




<br>

















