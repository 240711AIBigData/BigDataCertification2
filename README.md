﻿# 241130 빅분기 실기 대비 (75점 이상 목표!)
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

대괄호[], 중괄호{}, 소괄호() 사용법 
---
- 대괄호[] : 리스트와 데이터프레임에 사용

  - ex) 리스트 생성 : [1, 2, 3], 데이터프레임 인덱싱 및 슬라이싱 : df[0], df[1:2]
 
- 중괄호{} : 딕셔너리에 사용

  - ex) 딕셔너리 생성 : {'사과':1000, '딸기':2000}
 
- 소괄호() : 함수 호출에 사용

  - ex) 함수 호출 : print()

<br>

