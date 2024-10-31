# 241130 빅분기 실기 대비 (75점 이상 목표!)
INDEX
---
|No|Title|Link|
|-|-|-|
|00|기본 정보|-|
|01|Part1.작업형1|[바로가기](./01)|
|02|Part2.작업형2|[바로가기](./02)|
|03|Part3.작업형3|[바로가기](./03)|
|04|Part4.기출정리|[바로가기](./04)|

<br>

# 기본 정보

빅데이터분석기사 실기 개요
---
- 일시 : 2024년 11월 30일 토요일 10시

- 시험 시간 : 180분 (3시간)

- 총 6문항, 100점 만점으로 60점 이상(과목별 과락 x)

  - 작업형 1 : 3문항, 문항당 10점으로 총 30점
 
    - 코딩 화면에서 문제 풀이 후, 답안은 답안 제출 화면으로 이동해 제출
   
    - 지시된 제출 형식(소수점) 준수
   
    - 정답 여부에 따라 만점 or 0점
 
  - 작업형 2 : 1문항, 총 40점
 
    - 예측 결과를 CSV 파일로 제출
   
      - 지시된 컬럼명 사용
     
      - 자동 생성되는 index 컬럼 제거
     
      - 예측 결과 컬럼 1개만 생성
     
      - 지시된 파일명으로 생성
     
      - 별도 디렉토리 지정 금지
 
  - 작업형 3 : 2문항, 문항당 15점으로 총 30점
 
    - 코딩 화면에서 문제 풀이 후, 답안은 답안 제출 화면으로 이동해 제출
   
    - 각 문항별 소문항의 순서대로 답안 제출

<br>

해결 과정 주석 정리
---
- 데이터 불러오기

- 데이터 전처리

- 검증 데이터 나누기

- 모델 학습 및 평가

- *test 데이터로 예측 및 제출*

- *1) 예측 행의 수 및 2) 생성한 csv 확인*

<br>

판다스 출력 옵션 설정
---
- 데이터프레임 출력 결과 일부 생략시 설정 변경

```python
  import pandas as pd

  pd.set_option('dispaly.max_columns', None)  # 컬럼(열)
  pd.set_option('display.max_rows', None)     # 행
  pd.set_option('display.float_format', '{:.10f}'.format)  # 소수 10번째 자리까지 출력
```

<br>

[작업형1] dir()과 help() 사용하기
---
- dir(pd) : 판다스 함수(메소드)명
```python
  import pandas as pd

  print(dir(pd))  # 판다스 함수의 풀네임 확인 가능
```

> 결과
```
  ['ArrowDtype', 'BooleanDtype', 'Categorical', 'CategoricalDtype', ..., 'wide_to_long']
```

<br>

- help(pd.함수명) : 함수 사용 방법 및 예시 코드
```python
  import pandas as pd

  # 함수명에서는 dir(함수명)이 아닌 help(함수명) 사용
  print(help(pd.to_datetime))  # pd.to_datetime 함수에 대한 설명과 예시 코드 확인 가능
```

> 결과
```
  Help on function to_datetime in module pandas.core.tools.datetimes:
  
  to_datetime(arg: 'DatetimeScalarOrArrayConvertible | DictConvertible', errors: 'DateTimeErrorChoices' = 'raise', dayfirst: 'bool' = False, ...
```

<br>

[작업형2] 사이킷런에서 __all__, help(), dir() 활용하기
---
- sklearn.__all__ (all 앞뒤로 언더바(_) 2개씩) : 판다스 함수(메소드)명
```python
  import sklearn

  print(sklearn.__all__)  # 사이킷런에서 사용할 수 있는 모듈 목록 확인 가능
```

> 결과
```
  ['calibration', 'cluster', 'covariance', 'cross_decomposition', ..., 'show_versions']
```

<br>

- dir(preprocessing) : 전처리의 함수명
```python
  from sklearn import preprocessing  # from sklearn import 모듈이름 형식으로 불러오고 나서 dir(모듈 이름) 가능

  print(dir(preprocessing))  # 전처리 모듈을 불러온 후 dir를 통해 전처리 함수 리스트 확인 가능
```

> 결과
```
  ['Binarizer', 'FunctionTransformer', 'KBinsDiscretizer', 'KernelCenterer', 'LabelBinarizer', ..., 'scale']
```

<br>

- help(preprocessing.함수명) : 함수 사용 방법 및 예시 코드
```python
  from sklearn import preprocessing

  print(help(preprocessing.LabelEncoder))  # 레이블 인코더 함수에 대한 설명과 예시 코드 확인 가능
```

> 결과
```
  Help on class LabelEncoder in module sklearn.preprocessing._label:

  class LabelEncoder(sklearn.base.TransformerMixin, sklearn.base.BaseEstimator)
   |  Encode target labels with value between 0 and n_classes-1. ...
```

<br>

[작업형3] 사이파이에서 dir(), help(), 메모장 사용하기
---
- dir(stats) : 전처리의 함수명
```python
  from scipy import stats  # from scipy import stats로 불러온 후 

  print(dir(stats))  # dir(stats) 실행하면 사용 가능한 함수 확인 가능
```

> 결과
```
  ['BootstrapMethod', 'CensoredData', 'ConstantInputWarning', 'Covariance', ..., 'zscore']
```

<br>

- 메모장 활용(단, 시험 환경 자체 메모장만 사용 가능)

  - 많은 함수가 출력되어 스크롤이 생길 경우 실행결과를 전체 선택 후 마우스 우클릭해 복사 후 메모장에 붙여넣기
 
  - 검색(Ctrl + F) 기능을 활용해 찾고자 하는 함수명 검색

<br>

- help(stats.함수명) : 함수 사용 방법 및 예시 코드
```python
  from scipy import stats

  # help() 함수를 활용해 사용 방법 확인
  print(help(stats.ttest_rel))  # 대응 표본 t-test 설명과 예시 코드 확인 가능
```

> 결과
```
  Help on function ttest_rel in module scipy.stats._stats_py:

  ttest_rel(a, b, axis=0, nan_policy='propagate', alternative='two-sided', *, keepdims=False)
    Calculate the t-test on TWO RELATED samples of scores, a and b.

    This is a test for the null hypothesis that two related or
    repeated samples have identical average (expected) values.

    Parameters
    ----------
    a, b : array_like
        The arrays must have the same shape.
    axis : int or None, default: 0  ...
```

<br>

[작업형3] 스태츠모델즈(statsmodels)에서 dir()과 help() 활용하기
---
- ols() 함수 찾는 방법
```python
  import statsmodels.api as sm  # import statsmodels.api as sm 불러온 후

  print(dir(sm))
  print(dir(sm.formula))
  print(help(sm.formula.ols))
  # 위 순으로 ols() 함수 설명 글 확인
```

> 결과
```
  ['BayesGaussMI', 'BinomialBayesMixedGLM', 'ConditionalLogit', 'ConditionalMNLogit', ..., 'rlm', 'wls']
  Help on method from_formula in module statsmodels.base.model:
  
  from_formula( ...
```

<br>

```python
  import statsmodels.api as sm
  import statsmodels
  # 위 두 개 모두 필요한 이유는 statsmodels.api는 자주 사용되는 모듈과 함수만 불러오기 때문

  print(dir(statsmodels))
  print(dir(statsmodels.stats))
  print(dir(statsmodels.stats.anova))
  print(help(statsmodels.stats.anova.anova_lm))
```

> 결과
```
  ['__all__', '__builtins__', '__cached__', '__doc__', '__file__', ..., 'tsa']
  ['PytestTester', '__builtins__', '__cached__', '__doc__', '__file__', ..., 'weightstats']
  ['AnovaRM', 'AnovaResults', 'DataFrame', 'Index', 'OLS', '__builtins__', ..., 'summary2']
  Help on function anova_lm in module statsmodels.stats.anova:
  
  anova_lm(*args, **kwargs)
      Anova table ...
```

<br>

---

<br>

대괄호[], 중괄호{}, 소괄호() 사용법 
---
- 대괄호[] : 리스트와 데이터프레임에 사용

  - ex) 리스트 생성 : [1, 2, 3], 데이터프레임 인덱싱 및 슬라이싱 : df[0], df[1:2]
 
- 중괄호{} : 딕셔너리에 사용

  - ex) 딕셔너리 생성 : {'사과':1000, '딸기':2000}
 
- 소괄호() : 함수 호출에 사용

  - ex) 함수 호출 : print()

<br>

---

<br>

자주 사용하는 Python 패키지
---
- pandas, sklearn(Scikit-Learn), numpy

  - 데이터 처리와 분석을 위해 널리 사용되는 Python 패키지

<br>

> 차이점 요약

|패키지|주요 역할|주요 자료 구조|주요 기능 및 용도|
|-|-|-|-|
|pandas|데이터 조작 및 분석|DataFrame, Series	테이블형|데이터 처리, 결측치 처리, 그룹화, 필터링 등|
|sklearn|머신러닝|numpy 배열 사용|모델 학습, 평가, 하이퍼파라미터 튜닝, 전처리|
|numpy|고성능 수치 연산|ndarray|다차원 배열 및 행렬 연산, 선형대수, 난수 생성|


<br>

### 01. pandas
- 테이블 형태의 데이터를 다루기 위한 데이터 조작 및 분석 라이브러리

- 자료 구조

  - DataFrame(2D 구조)과 Series(1D 구조)를 사용하여 표 형태로 데이터를 조작
 
- 주요 기능

  - 데이터 로드/저장(CSV, Excel, SQL, JSON 등)
 
    - 다양한 형식의 파일(CSV, Excel, SQL, JSON 등)에서 데이터를 불러오고, 처리 후 다시 저장 가능
 
      - pd.read_csv()와 같은 함수로 데이터를 불러오고, df.to_csv() 등의 메서드로 저장
 
  - 데이터 필터링, 인덱싱, 슬라이싱
 
    - 특정 조건에 맞는 행 또는 열 선택 및 인덱싱과 슬라이싱을 통해 세밀한 데이터 조작 가능
   
      - [.loc[]와 .iloc[] 메서드를 사용해 레이블 및 정수 인덱스를 통해 데이터 접근 가능](./01/02)
 
  - 결측치 처리, 데이터 정렬, 데이터 집계 및 그룹화
 
    - 데이터에 포함된 결측값을 쉽게 탐색하고 처리 가능
    
      - 결측값을 삭제하거나, 특정 값으로 대체
     
      - df.isnull()로 결측치 확인, .fillna()로 대체 또는 .dropna()로 제거
   
    - 데이터프레임을 특정 열을 기준으로 오름차순 또는 내림차순으로 정렬 가능
   
      - .sort_values() 메서드를 사용하여 열 기준으로 정렬
     
    - 데이터를 특정 기준으로 그룹화하여 집계 가능
   
      - .groupby()와 .agg() 메서드를 사용하여, 평균, 합계, 카운트 등 다양한 집계 가능
 
  - 피벗 테이블과 시계열 데이터 처리
 
    - 피벗 테이블 : 데이터를 특정 열을 기준으로 요약하여 집계된 새로운 표를 생성(엑셀의 피벗 테이블과 유사
   
      - .pivot_table() 메서드를 사용해 복잡한 데이터를 요약 및 집계하여 새로운 표 생성
     
    - 시계열 데이터 처리 : 날짜와 시간을 다루며, 날짜 인덱스 설정과 시간별 집계 등 다양한 기능을 지원
   
      - .resample()을 통해 시계열 데이터의 주기별 집계 가능

> ex
```python
  import pandas as pd
  
  df = pd.read_csv('data.csv')  # CSV 파일 불러오기
  df.to_excel('output.xlsx')        # Excel 파일로 저장

  # 조건에 맞는 행 필터링
  filtered_df = df[df['column_name'] > 50]  
  # 특정 행과 열 선택
  selection = df.loc[10:20, ['col1', 'col2']]

  df.fillna(df.mean(), inplace=True)   # 결측치를 열의 평균값으로 대체
  df.dropna(inplace=True)              # 결측치가 포함된 행 삭제

  df_sorted = df.sort_values(by='column_name', ascending=False)  # df 를 특정 열(column_name)을 기준으로 내림차순 정렬

  df.describe()  # 기본 통계 정보 확인
  df.groupby('column_name').mean()  # 특정 컬럼으로 그룹화하고 평균 계산

  # 피벗 테이블 생성
  pivot_table = df.pivot_table(values='sales', index='region', columns='product', aggfunc='sum')
  
  # 시계열 데이터 처리
  df['date'] = pd.to_datetime(df['date'])
  df.set_index('date', inplace=True)
  monthly_sales = df['sales'].resample('M').sum()  # 월별 합계 계산
```

<br>

### 02. sklearn (Scikit-Learn)
- 머신러닝 모델 구축과 평가를 위한 종합 라이브러리

  - 다양한 머신러닝 알고리즘 포함
 
- 자료 구조

  - numpy 배열을 입력으로 받아 모델을 학습하고 예측 수행

- 주요 기능

  - 데이터 전처리 (스케일링, 인코딩, 결측치 처리 등)
 
    - 스케일링 : 데이터의 스케일(크기)을 조정하여 모델이 다양한 범위의 데이터를 효과적으로 학습할 수 있도록 도움
    
      - StandardScaler, MinMaxScaler 등을 사용해 각 열의 범위를 일정하게 맞춤
     
    - 인코딩 : 범주형 데이터를 수치형으로 변환하여 모델에 사용할 수 있도록 함
    
      - LabelEncoder : 레이블을 숫자로 변환
      
      - OneHotEncoder : 각 범주를 개별 열로 변환해 다중 카테고리를 다룰 수 있게 함
     
    - 결측치 처리 : 결측값을 특정 값(평균, 중위수 등)으로 대체하거나 삭제하여 모델에 적합하게 정제
    
      - SimpleImputer 사용하여 결측치 자동 처리 가능
 
  - 지도 학습/비지도 학습 모델 (회귀, 분류, 군집 등)
 
    - 지도 학습 : 레이블이 있는 데이터를 학습하여 예측을 수행하는 방식
   
      - 회귀 : 연속적인 값을 예측하는 모델
      
        - LinearRegression, Ridge, Lasso 등
       
      - 분류: 이산적 범주를 예측하는 모델
     
        - LogisticRegression, SVC(Support Vector Classifier), KNeighborsClassifier 등
   
    - 비지도 학습 : 레이블이 없는 데이터를 학습하여 패턴을 찾거나 군집화
   
      - 군집화 : 유사한 데이터끼리 묶는 작업
     
        - KMeans, DBSCAN 등
       
      - 차원 축소 : 데이터의 주요 특성을 추출해 차원을 줄이는 작업
     
        - PCA(Principal Component Analysis), t-SNE 등
 
  - 모델 평가(정확도, F1 점수 등) 및 메트릭 제공
 
    - 정확도 : 분류 문제에서 전체 예측 중 맞춘 비율
   
      - accuracy_score 메서드를 사용하여 계산
     
    - F1 점수 : 정밀도와 재현율의 조화 평균
   
      - 불균형 데이터에서 성능을 평가할 때 유용
     
      - f1_score 메서드로 계산
     
    - 기타 메트릭 : mean_squared_error(MSE), mean_absolute_error(MAE) 등 다양한 회귀 및 분류 성능 평가 지표 有
 
  - 교차 검증과 하이퍼파라미터 튜닝 지원
 
    - 교차 검증 : 데이터셋을 여러 부분으로 나누어 모델의 일반화 성능을 평가
   
      - cross_val_score 함수를 사용해 평균 성능을 계산

      - 과적합을 방지 가능
     
    - 하이퍼파라미터 튜닝 : 모델의 성능을 최적화하기 위해 파라미터 값을 조정
   
      - GridSearchCV나 RandomizedSearchCV와 같은 메서드를 사용해 다양한 파라미터 조합을 자동으로 테스트하여 최적의 조합 확인

> ex
```python
  from sklearn.model_selection import train_test_split
  from sklearn.linear_model import LinearRegression
  from sklearn.metrics import accuracy_score, f1_score, mean_squared_error
  from sklearn.preprocessing import StandardScaler, OneHotEncoder
  from sklearn.impute import SimpleImputer
  from sklearn.cluster import KMeans

  scaler = StandardScaler()
  data_scaled = scaler.fit_transform(data)  # 데이터 스케일링
  imputer = SimpleImputer(strategy='mean')  # 결측치를 평균으로 대체
  data_imputed = imputer.fit_transform(data)

  # 지도 학습 예시
  model = LinearRegression().fit(X_train, y_train)  # 회귀 모델 학습
  
  # 비지도 학습 예시
  kmeans = KMeans(n_clusters=3).fit(X)  # K-means 군집화

  y_pred = model.predict(X_test)
  accuracy = accuracy_score(y_test, y_pred)
  f1 = f1_score(y_test, y_pred, average='weighted')
  mse = mean_squared_error(y_test, y_pred)
```

<br>

### 03. numpy
- 고성능 수치 연산을 위해 사용되는 라이브러리

  - 다차원 배열과 행렬 연산 지원

- 자료 구조

  - ndarray는 다차원 배열 형태로 데이터 저장을 최적화하여 빠르게 연산할 수 있도록 함
 
- 주요 기능

  - 기본 수치 연산 (덧셈, 뺄셈, 곱셈 등)
 
    - numpy는 기본적으로 배열의 요소들에 대한 빠른 연산을 지원
   
      - \+, \-, \*, \/ 와 같은 산술 연산자를 사용하여 배열 내 요소 간 연산 가능
     
    - 브로드캐스팅 : numpy의 특별한 기능, 배열 간 크기가 다를 때 작은 배열이 자동으로 확장되어 연산 가능
 
  - 선형 대수, 푸리에 변환, 난수 생성
 
    - 선형 대수((Linear Algebra) : 벡터, 행렬, 그리고 그들 사이의 연산을 다루는 수학 분야
   
      - 벡터와 행렬의 곱셈, 역행렬, 행렬식 계산 등 다양한 선형 대수 연산을 지원
     
      - np.dot() 함수는 벡터와 벡터, 벡터와 행렬, 행렬과 행렬 간의 내적 연산을 수행
     
        - np.linalg 모듈을 사용하여 선형 대수 연산을 수행 가능
       
      - 선형 대수는 머신러닝, 물리학, 컴퓨터 그래픽스 등 수많은 분야에서 널리 활용됨
     
    - np.fft 모듈을 사용하여 푸리에 변환(Fourier Transform) 쉽게 수행 가능
   
      - 신호 분석, 이미지 처리, 음성 인식 등에서 주파수 성분을 추출하는 데 사용
     
      - np.fft.fft() 함수는 주어진 데이터의 푸리에 변환을 계산하여 주파수 성분을 분석
     
    - 난수 생성을 위한 np.random 모듈 제공
   
      - 정규분포, 균등분포, 이항분포 등 다양한 확률 분포를 따르는 난수를 생성 가능
 
  - 빠른 벡터 및 행렬 연산을 지원하여 pandas와 sklearn에서 기본 자료형으로 활용
 
    - 다차원 배열(ndarray)을 사용하여 고속으로 벡터 및 행렬 연산을 수행 가능
   
      - 반복문을 사용할 필요 없이 배열 연산을 벡터화해 한 번에 수행
     
        - 처리 속도가 빠름
        
    - pandas와 sklearn 등 여러 라이브러리에서 기본 자료형으로 사용
     
    - 다차원 배열을 통해 대규모 데이터 연산을 효율적으로 처리할 수 있어 데이터 분석, 머신러닝, 과학 계산 등에 적합
 
> ex
```python
  import numpy as np
  
  arr = np.array([1, 2, 3])  # 배열 생성
  arr2 = arr * 2       # 각 요소에 2를 곱함 -> [2, 4, 6]
  arr3 = arr * arr     # 각 요소의 제곱 -> [1, 4, 9]
  matrix = np.dot(arr, arr.T)  # 행렬 곱 계산

  matrix = np.array([[1, 2], [3, 4]])
  vector = np.array([2, 3])
  dot_product = np.dot(matrix, vector)   # 행렬과 벡터 곱
  inverse_matrix = np.linalg.inv(matrix)  # 역행렬

  # 예제: 신호 데이터의 푸리에 변환
  time = np.linspace(0, 1, 500)
  signal = np.sin(2 * np.pi * 50 * time)  # 50Hz의 사인파 생성
  frequency_data = np.fft.fft(signal)     # 푸리에 변환 수행

  random_numbers = np.random.rand(3, 3)    # 3x3 크기의 균등 분포 난수 배열 생성
  normal_numbers = np.random.randn(5)      # 평균 0, 표준편차 1의 정규 분포 난수 생성

  # 벡터화된 연산을 통한 고속 처리
  array1 = np.array([1, 2, 3])
  array2 = np.array([4, 5, 6])
  result = array1 + array2  # 요소별 덧셈 -> [5, 7, 9]
```

<br>
