# CHAPTER08 회귀 연습문제
- 회귀 문제를 풀 때 분류 문제와 가장 큰 차이점은 모델과 평가지표가 다르다는 것

  - 분류 : 랜덤포레스트 분류 모델인 RandomForestClassifier 사용
 
  - 회귀 : 랜덤포레스트 회귀 모델인 RandomForestRegressor 사용
 
  - 회귀 문제에서 분류 모델을 사용해 예측값 성능이 현저히 떨어져 0점 처리되는 경우 주의
 
- 사이킷런은 다양한 평가지표를 제공하지만, 모든 지표를 지원하진 않음

  - 필요한 지표가 사이킷런에 포함되어 있지 않다면 직접 구현해야 함
 
  - 문제에서 제시된 평가지표를 모를 경우 알고 있는 회귀 평가지표를 사용해 문제 해결
 
<br>

SECTION01 항공권 가격 예측
---
- 항공권 티켓 가격 예측

  - 제공된 데이터 목록 : flight_train.csv, flight_test.csv
 
  - 예측할 컬럼 : price
 
- 학습용 데이터(train)을 이용해 티켓 가격을 예측하는 모델 생성

- 평가용 데이터(test)에 적용해 얻은 예측값을 아래 형식의 csv 파일로 생성

  - 제출 파일은 아래 1개의 컬럼 포함
 
    - pred : 예측값(가격)
   
    - 제출 파일명 : 'result1.csv'
   
  - 제출한 모델의 성능은 RMSE 평가지표에 따라 채점
 
<br>

### 01. 베이스라인
- 데이터를 불러오고 간단한 탐색적 데이터 분석 진행

<br>

#### (1) EDA
> 코드
```python
  # 1. 문제 정의
  # 평가 : RMSE
  # target : price
  # 최종 파일 : result1.cst (컬럼 1개 pred)
  
  # 2. 라이브러리 및 데이터 불러오기
  import pandas as pd
  
  train = pd.read_csv('./data/flight_train.csv')
  test = pd.read_csv('./data/flight_test.csv')
  
  # 3. 탐색적 데이터 분석(EDA)
  print('==== 데이터 크기 ====')
  print('Train Shape :', train.shape)
  print('Test Shape :', test.shape)
  
  print('\n==== 데이터 정보(자료형) ====')
  print(train.info())
  
  print('\n==== train 결측치 수 ====')
  print(train.isnull().sum())
  
  print('\n==== test 결측치 수 ====')
  print(test.isnull().sum())
  
  print('\n==== 카테고리 비교 ====')
  cols = train.select_dtypes(include='object').columns
  for col in cols:
      set_train = set(train[col])
      set_test = set(test[col])
      same = (set_train == set_test)
      if same:
          print(col, '\t카테고리 동일함')
      else:
          print(col, '\t카테고리 동일하지 않음')
  
  print('\n==== target 기술 통계 ====')
  print(train['price'].describe())
```
- train 과 test 의 object 형 카테고리 비교

- 반복문 사용이 어렵다면 value_counts() 활용해 비교하거나 컬럼별로 비교

```python
  set_train = set(train['컬럼명'])
  set_test = set(test['컬럼명'])
  print(set_train == set_test)
```
- True : 같은 카테고리 / False : 다른 카테고리

> 결과
```python
  ==== 데이터 크기 ====
  Train Shape : (10505, 11)
  Test Shape : (4502, 10)
  
  ==== 데이터 정보(자료형) ====
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 10505 entries, 0 to 10504
  Data columns (total 11 columns):
   #   Column            Non-Null Count  Dtype  
  ---  ------            --------------  -----  
   0   airline           10505 non-null  object 
   1   flight            10505 non-null  object 
   2   source_city       10505 non-null  object 
   3   departure_time    10505 non-null  object 
   4   stops             10505 non-null  object 
   5   arrival_time      10505 non-null  object 
   6   destination_city  10505 non-null  object 
   7   class             10505 non-null  object 
   8   duration          10505 non-null  float64
   9   days_left         10505 non-null  int64  
   10  price             10505 non-null  int64  
  dtypes: float64(1), int64(2), object(8)
  memory usage: 902.9+ KB
  None
  
  ==== train 결측치 수 ====
  airline             0
  flight              0
  source_city         0
  departure_time      0
  stops               0
  arrival_time        0
  destination_city    0
  class               0
  duration            0
  days_left           0
  price               0
  dtype: int64
  
  ==== test 결측치 수 ====
  airline             0
  flight              0
  source_city         0
  departure_time      0
  stops               0
  arrival_time        0
  destination_city    0
  class               0
  duration            0
  days_left           0
  dtype: int64
  
  ==== 카테고리 비교 ====
  airline 	카테고리 동일함
  flight 	카테고리 동일하지 않음
  source_city 	카테고리 동일함
  departure_time 	카테고리 동일함
  stops 	카테고리 동일함
  arrival_time 	카테고리 동일함
  destination_city 	카테고리 동일함
  class 	카테고리 동일함
  
  ==== target 기술 통계 ====
  count     10505.000000
  mean      20650.139838
  std       22570.924117
  min        1105.000000
  25%        4755.000000
  50%        7455.000000
  75%       42457.000000
  max      110936.000000
  Name: price, dtype: float64
```
- 분류에서는 target 카테고리 확인을 위해 value_counts() 사용

- 회귀에서는 target 데이터 분포를 히스토그램 등으로 시각화해 확인하지만, 빅분기 시험 환경에서는 지원 X

  - describe() 로 출력
 
    - 평균값 > 중앙값(50%) : 오른쪽 왜곡
   
    - 대부분의 값들이 왼쪽에 몰려있고, 오른쪽으로 갈수록 희박해짐

<br>

<details>
  <summary>시각화(히스토그램) : 시험 환경 지원 X</summary>

<br>

> 코드
```python
train['price'].hist()
```

> 결과

![image](https://github.com/user-attachments/assets/5f65b63d-2ab3-4eb2-a06a-f06440a5e3c4)


</details>

<br>

#### (2) 전처리 및 예측

> 코드
```python
  # 4. 데이터 전처리
  target = train.pop('price')
  
  # 컬럼 삭제
  train = train.drop('flight', axis=1)
  test = test.drop('flight', axis=1)
  
  # 원-핫 인코딩
  train = pd.get_dummies(train)
  test =pd.get_dummies(test)
  
  # 5. 검증 데이터 나누기
  from sklearn.model_selection import train_test_split
  X_train, X_val, y_train, y_val = train_test_split(train, target, test_size=0.2, random_state=0)
  
  print('\n==== 분할된 데이터 크기 ====')
  print(X_train.shape, X_val.shape, y_train.shape, y_val.shape)
  
  # 6. 머신러닝 학습 및 평가
  from sklearn.ensemble import RandomForestRegressor
  rf = RandomForestRegressor(random_state=0)
  rf.fit(X_train, y_train)
  pred = rf.predict(X_val)
  
  # RMSE(Root Mean Squared Error)
  # from sklearn.metrics import mean_squared_error
  # result = mean_squared_error(y_val, pred, squared=False)
  from sklearn.metrics import root_mean_squared_error
  result = root_mean_squared_error(y_val, pred)
  print('\nRMSE :', result)
  
  # 7. 예측 및 결과 파일 생성
  pred = rf.predict(test)
  submit = pd.DataFrame({'pred':pred})
  submit.to_csv('result1.csv', index=False)
  
  # 제출 파일 확인
  print('\n==== 제출 파일 (샘플 5개) ====')
  print(pd.read_csv('result1.csv').head())
```
- flight 컬럼은 train 과 test 데이터의 카테고리가 달라 삭제

- 사이킷런에서 MSE 함수로 제공

  - RMSE 사용하기 위해 MSE 함수에 squared=False 설정 or MSE 제곱근으로 만들기
   
    - RMSE = √MSE
   
    - 파이썬에서 MSE 제곱근 계산 : mse ** 0.5
   
  - sklean 최신 버전이라면 root_mean_squared_error 사용 가능

<br>

<details>
  <summary>최신 버전의 scikit-learn에서 RMSE(평균 제곱근 오차) 계산</summary>

<br>

> scikit-learn 최신 버전 업데이트
```python
  pip install -U scikit-learn
```

<br>

> mean_squared_error와 squared=False 사용
```python
  from sklearn.metrics import mean_squared_error
  
  # y_true: 실제 값, y_pred: 예측 값
  rmse = mean_squared_error(y_true, y_pred, squared=False)
  print("RMSE:", rmse)
```

<br>

> root_mean_squared_error 사용
```python
  from sklearn.metrics import root_mean_squared_error
  
  # y_true: 실제 값, y_pred: 예측 값
  rmse = root_mean_squared_error(y_true, y_pred)
  print("RMSE:", rmse)
```

</details>

<br>

> 결과
```python
  ==== 분할된 데이터 크기 ====
  (8404, 37) (2101, 37) (8404,) (2101,)
  
  RMSE : 4376.841613585934
  
  ==== 제출 파일 (샘플 5개) ====
         pred
  0  57356.34
  1   5334.44
  2  13244.83
  3   5951.10
  4   5102.89
```

<br>

#### 💡 회귀 문제 예측값을 정수로 만들어야 할까?
- 문제에서 예시 예측값이 정수로 되어있다고 정수로 변환할 필요 X

  - 일반적으로 예측값은 소수점 형태로 그대로 사용
 
  - 예측값을 정수로 만들어야 할지 여부는 문제의 목적에 따라 달라짐
 
    - 사람 수 예측 등

- 회귀 문제의 예측값은 주로 소수점으로 나옴

  - 회귀 모델이 연속적인 값을 예측하기 때문

<Br>

### 02. 성능 개선
- flight 컬럼은 포함하되, 중복 제외하고 일부만 포함

  - train 과 test 카테고리가 다르므로 합쳐서 원-핫 or 레이블 인코딩할 경우 메모리 초과
 
    - 문자열을 나누는 split() 함수로 하이븐(-) 앞뒤로 나눠서 활용
   
- 데이터 전처리

  - 레이블 인코딩 : 효과 X
 
  - 스케일링 : Standard Scaler
 
  - flight 컬럼 : 앞의 영문은 airline 약자이므로 제외 후 뒤의 숫자만 활용
 
- 하이퍼파라미터 튜닝

  - max_depth : 일반적으로 회귀는 분류보다 더 깊은 10~20 정도에서 튜닝
 
  - n_estimators : 200, 500

<br>

|데이터 전처리/하이퍼파라미터 튜닝|RMSE|제출|
|-|-|-|
|베이스라인|4376.841613585934|선택 / 1차 선택|
|레이블 인코딩|4435.734155906736||
|스케일링(Standard Scaler)|4371.046950948944|선택 / 2차 제출|
|스케일링(Min-Max Scaler)|4372.00793145506||
|스케일링(Robust Scaler)|4377.079777085384||
|flight 컬럼 일부 활용|3715.0644662768786|선택 / 3차 제출|
|max_depth = 10|4278.021416520653||
|max_depth = 15|3791.338887502452||
|max_depth = 20|3704.892644266319|선택|
|max_depth = 20, n_estimators = 200|3675.155093297134|선택 / 4차 제출|
|max_depth = 20, n_estimators = 500|3689.7471606075715||

<br>

> 코드
```python
  # 2. 라이브러리 및 데이터 불러오기
  import pandas as pd
  
  train = pd.read_csv('./data/flight_train.csv')
  test = pd.read_csv('./data/flight_test.csv')
  
  # 4. 데이터 전처리
  target = train.pop('price')
  
  # flight 컬럼 일부 사용
  print('\n==== train 의 flight 컬럼 ====')
  print(train['flight'].head())
  
  print('\n==== test 의 flight 컬럼 ====')
  print(test['flight'].head())
  
  train['f2'] = train['flight'].str.split('-').str[1].astype(int)
  test['f2'] = test['flight'].str.split('-').str[1].astype(int)
  
  # 컬럼 삭제
  train = train.drop('flight', axis=1)
  test = test.drop('flight', axis=1)
  
  # 스케일링
  from sklearn.preprocessing import StandardScaler
  scaler = StandardScaler()
  cols = ['duration', 'days_left']
  train[cols] = scaler.fit_transform(train[cols])
  test[cols] = scaler.transform(test[cols])
  
  # 원-핫 인코딩
  train = pd.get_dummies(train)
  test = pd.get_dummies(test)
  
  # 레이블 인코딩
  # from sklearn.preprocessing import LabelEncoder
  # cols = train.select_dtypes(include='object').columns
  # for col in cols:
  #     le = LabelEncoder()
  #     train[col] = le.fit_transform(train[col])
  #     test[col] = le.transform(test[col])
  
  # 5. 검증 데이터 나누기
  from sklearn.model_selection import train_test_split
  X_train, X_val, y_train, y_val = train_test_split(train, target, test_size=0.2, random_state=0)
  
  # 6. 머신러닝 학습 및 평가
  from sklearn.ensemble import RandomForestRegressor
  rf = RandomForestRegressor(max_depth=20, n_estimators=200, random_state=0)
  rf.fit(X_train, y_train)
  pred = rf.predict(X_val)
  
  # RMSE(Root Mean Squared Error)
  from sklearn.metrics import root_mean_squared_error
  result = root_mean_squared_error(y_val, pred)
  print('\nRMSE :', result)
  
  # 7. 예측 및 결과 파일 생성
  pred = rf.predict(test)
  submit = pd.DataFrame({'pred':pred})
  submit.to_csv('result1.csv', index=False)
  
  print('\n==== 제출 파일 (샘플 5개) ====')
  print(pd.read_csv('result1.csv').head())
```

> 결과
```python
  ==== train 의 flight 컬럼 ====
  0     UK-776
  1     UK-852
  2    6E-2348
  3     AI-763
  4     6E-752
  Name: flight, dtype: object
  
  ==== test 의 flight 컬럼 ====
  0    UK-778
  1    AI-764
  2    AI-569
  3    UK-960
  4    G8-302
  Name: flight, dtype: object
  
  RMSE : 3675.155093297134
  
  ==== 제출 파일 (샘플 5개) ====
             pred
  0  56553.046886
  1   5286.811810
  2  12639.171249
  3   5958.368481
  4   4911.903971
```

<br>

---

<br>

SECTION02 노트북 가격 예측
---
- 노트북 정보로 가격 예측

  - 제공된 데이터 목록 : laptop_train.csv, laptop_test.csv
 
  - 예측할 컬럼 : price
 
- 학습용 데이터(train)을 이용해 노트북 가격을 예측하는 모델 생성

- 평가용 데이터(test)에 적용해 얻은 예측값을 아래 형식의 csv 파일로 생성

  - 제출 파일은 다음 1개의 컬럼 포함
 
    - pred : 예측값(가격)
   
    - 제출 파일명 : 'result2.csv'
   
  - 제출한 모델의 성능은 R²(결정 계수) 평가지표에 따라 채점

<br>

### 01. 베이스라인
- 데이터를 불러오고, 간단한 탐색적 데이터 분석 진행

<br>

#### (1) EDA

> 코드
```python
  # 1. 문제 정의
  # 평가 : R²
  # target : Price
  # 최종 파일 : result2.csv (컬럼 1개 pred, 1 확률값)
  
  # 2. 라이브러리 및 데이터 불러오기
  import pandas as pd
  
  train = pd.read_csv('./data/laptop_train.csv')
  test = pd.read_csv('./data/laptop_test.csv')
  
  # 3. 탐색적 데이터 분석(EDA)
  print('==== 데이터 크기 ====')
  print('Train Shape :', train.shape)
  print('Test Shape :', test.shape)
  
  print('\n==== 데이터 정보(자료형) ====')
  print(train.info())
  
  print('\n==== train 결측치 수 ====')
  print(train.isnull().sum())
  
  print('\n==== test 결측치 수 ====')
  print(test.isnull().sum())
  
  print('\n==== 카테고리 비교 ====')
  cols = train.select_dtypes(include='object').columns
  for col in cols:
      set_train = set(train[col])
      set_test = set(test[col])
      same = (set_train == set_test)
      if same:
          print(col, '\t카테고리 동일함')
      else:
          print(col, '\t카테고리 동일하지 않음')
          
  print('\n==== target 기술 통계 ====')
  print(train['Price'].describe())
```

> 결과
```python
  ==== 데이터 크기 ====
  Train Shape : (91, 10)
  Test Shape : (39, 9)
  
  ==== 데이터 정보(자료형) ====
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 91 entries, 0 to 90
  Data columns (total 10 columns):
   #   Column              Non-Null Count  Dtype  
  ---  ------              --------------  -----  
   0   Brand               91 non-null     object 
   1   Model               82 non-null     object 
   2   Series              55 non-null     object 
   3   Processor           86 non-null     object 
   4   Processor_Gen       86 non-null     object 
   5   RAM                 85 non-null     float64
   6   Hard_Disk_Capacity  85 non-null     object 
   7   OS                  85 non-null     object 
   8   Rating              91 non-null     float64
   9   Price               91 non-null     int64  
  dtypes: float64(2), int64(1), object(7)
  memory usage: 7.2+ KB
  None
  
  ==== train 결측치 수 ====
  Brand                  0
  Model                  9
  Series                36
  Processor              5
  Processor_Gen          5
  RAM                    6
  Hard_Disk_Capacity     6
  OS                     6
  Rating                 0
  Price                  0
  dtype: int64
  
  ==== test 결측치 수 ====
  Brand                  0
  Model                  5
  Series                14
  Processor              2
  Processor_Gen          2
  RAM                    2
  Hard_Disk_Capacity     2
  OS                     2
  Rating                 0
  dtype: int64
  
  ==== 카테고리 비교 ====
  Brand 	카테고리 동일하지 않음
  Model 	카테고리 동일하지 않음
  Series 	카테고리 동일하지 않음
  Processor 	카테고리 동일하지 않음
  Processor_Gen 	카테고리 동일하지 않음
  Hard_Disk_Capacity 	카테고리 동일하지 않음
  OS 	카테고리 동일하지 않음
  
  ==== target 기술 통계 ====
  count        91.000000
  mean      53540.813187
  std       21371.760428
  min       17640.000000
  25%       39490.000000
  50%       46840.000000
  75%       60194.500000
  max      129990.000000
  Name: Price, dtype: float64
```
- 학습용 데이터가 91개인 매우 작은 데이터 크기

- train, test 데이터에 결측치 有, object 컬럼의 경우 카테고리가 모두 동일하지 않음

<br>

#### (2) 전처리 및 예측

> 코드
```python
  # 4. 데이터 전처리
  target = train.pop('Price')
  
  # 결측치 처리(범주형)
  c_cols = ['Model', 'Series', 'Processor', 'Processor_Gen', 'Hard_Disk_Capacity', 'OS']
  train[c_cols] = train[c_cols].fillna('X')
  test[c_cols] = test[c_cols].fillna('X')
  
  # 결측치 처리(수치형)
  n_cols = ['RAM']
  train[c_cols] = train[c_cols].fillna(-1)
  test[c_cols] = test[c_cols].fillna(-1)
  
  # 원-핫 인코딩
  combined = pd.concat([train, test])
  combined_dummies = pd.get_dummies(combined)
  n_train = len(train)
  train = combined_dummies[:n_train]
  test = combined_dummies[n_train:]
  
  # 5. 검증 데이터 나누기
  from sklearn.model_selection import train_test_split
  X_train, X_val, y_train, y_val = train_test_split(train, target, test_size=0.2, random_state=0)
  print(X_train.shape, X_val.shape, y_train.shape, y_val.shape)
  
  # 6. 머신러닝 학습 및 평가
  from sklearn.ensemble import RandomForestRegressor
  rf = RandomForestRegressor(random_state=0)
  rf.fit(X_train, y_train)
  pred = rf.predict(X_val)
  
  from sklearn.metrics import r2_score
  result = r2_score(y_val, pred)
  print('\nR2 :', result)
  
  # 7. 예측 및 결과 파일 생성
  pred = rf.predict(test)
  submit = pd.DataFrame({'pred':pred})
  submit.to_csv('result2.csv', index=False)
  
  print('\n==== 제출 파일 (샘플 5개) ====')
  print(pd.read_csv('result2.csv').head())
```
- 결측치 처리를 위해 범주형 컬럼에는 X 값 대입, 수치형 데이터에는 -1 값 대입

  - 결측치를 표시하기 위한 임의값
 
- train 과 test 합쳐서 인코딩 후 다시 train 과 test 로 나누기

- r2 는 사이킷런에서 평가지표 함수 제공

> 결과
```python
  (72, 119) (19, 119) (72,) (19,)

  R2 : 0.7637860886010525
  
  ==== 제출 파일 (샘플 5개) ====
         pred
  0  40720.15
  1  39409.13
  2  59492.65
  3  39960.00
  4  43535.17
```

<br>

### 02. 성능 개선
- 데이터 전처리

  - Series 컬럼 삭제 : 40% 정도의 결측치를 갖고 있는 Series 컬럼 삭제
  
    - 40% 결측치를 대체하는 대신 이 컬럼을 삭제해 모델의 성능 높이기
 
  - Model 컬럼 삭제 : 여러 희소한 카테고리 값 有
 
    - Brand 컬럼이 Model 정보를 부분적으로 포함
   
      - Model 컬럼 삭제하니 모델 성능 향상
     
- 하이퍼파라미터 튜닝

  - 간단한 튜닝 시도했으나 뚜렷한 개선 X
 
<br>

|데이터 전처리/하이퍼파라미터 튜닝|R²|제출|
|-|-|-|
|베이스라인|0.7637860886010525|선택 / 1차 제출|
|Series 컬럼 삭제|0.779055103270554|선택|
|Model 컬럼 삭제|0.8109566453793982|선택 / 2차 제출|
|max_depth = 10|0.8071431979459575||
|max_depth = 15|0.8109566453793982||
|max_depth = 20|0.8109566453793982||
|n_estimators = 200|0.796874056256514||
|n_estimators = 500|0.7874514926096796||

<br>

> 코드
```python
  # 2. 라이브러리 및 데이터 불러오기
  import pandas as pd
  
  train = pd.read_csv('./data/laptop_train.csv')
  test = pd.read_csv('./data/laptop_test.csv')
  
  # 4. 데이터 전처리
  target = train.pop('Price')
  
  # Series 결측치 삭제
  train = train.drop('Series', axis=1)
  test = test.drop('Series', axis=1)
  
  # Brand 컬럼이 Model 컬럼에 포함되는지 확인하는 함수
  def check_brand_in_model(row):
      brand = str(row['Brand']).lower()
      model = str(row['Model']).lower()
      return brand in model
  
  # 각 행에 대해 브랜드가 모델 이름에 포함되는지를 확인
  brand_in_model = train.apply(check_brand_in_model, axis=1)
  
  # 포함된 비율 확인
  print('브랜드가 모델 정보에 포함될 비율 :', brand_in_model.mean())
  
  # 샘플 출력
  print('\n', train[brand_in_model][['Brand', 'Model']].head())
  
  # Model 결측치 삭제
  train = train.drop('Model', axis=1)
  test = test.drop('Model', axis=1)
  
  # 결측치 처리(범주형)
  c_cols = ['Processor', 'Processor_Gen', 'Hard_Disk_Capacity', 'OS']
  train[c_cols] = train[c_cols].fillna('X')
  test[c_cols] = test[c_cols].fillna('X')
  
  # 결측치 처리(수치형)
  n_cols = ['RAM']
  train[c_cols] = train[c_cols].fillna(-1)
  test[c_cols] = test[c_cols].fillna(-1)
  
  # 원-핫 인코딩
  combined = pd.concat([train, test])
  combined_dummies = pd.get_dummies(combined)
  n_train = len(train)
  train = combined_dummies[:n_train]
  test = combined_dummies[n_train:]
  
  # 5. 검증 데이터 나누기
  from sklearn.model_selection import train_test_split
  X_train, X_val, y_train, y_val = train_test_split(train, target, test_size=0.2, random_state=0)
  
  # 6. 머신러닝 학습 및 평가
  from sklearn.ensemble import RandomForestRegressor
  rf = RandomForestRegressor(random_state=0)
  rf.fit(X_train, y_train)
  pred = rf.predict(X_val)
  
  from sklearn.metrics import r2_score
  result = r2_score(y_val, pred)
  print('\nr2 :', result)
  
  # 7. 예측 및 결과 파일 생성
  pred = rf.predict(test)
  submit = pd.DataFrame({'pred':pred})
  submit.to_csv('result2.csv', index=False)
  
  print('\n==== 제출 파일 (샘플 5개) ====')
  print(pd.read_csv('result2.csv').head())
```

> 결과
```python
  브랜드가 모델 정보에 포함될 비율 : 0.02197802197802198
  
      Brand Model
  19    HP    HP
  22  ASUS  ASUS
  
  r2 : 0.8109566453793982
  
  ==== 제출 파일 (샘플 5개) ====
         pred
  0  40008.05
  1  40648.49
  2  59986.05
  3  39960.00
  4  45183.02
```

<br>

---

<br>

SECTION03 중고차 가격 예측
---




<br>





















