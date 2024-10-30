# CHAPTER06 이진 분류 연습문제
- 첫 번째 베이스라인을 만들 때는 머신러닝 프로세스대로

- 랜덤포레스트 모델 사용

<br>

SECTION01 환자의 당뇨병 여부 예측
---
- 환자의 당뇨병 여부 예측

  - 제공된 데이터 목룍 : diabetes_train.csv, diabetes_test.csv
 
  - 예측할 컬럼 : Outcome(0: 정상, 1: 당뇨병)

- 학습용 데이터(train)를 이용해 환자의 당뇨병을 예측하는 모델 생성

- 평가용 데이터(test)에 적용해 얻은 예측값은 아래 형식의 csv 파일로 생성

  - 제출 파일은 다음 1개의 컬럼을 포함해야 함
 
    - pred : 예측값(당뇨병일 확률)
   
    - 제출 파일명 : 'result1.csv'
   
  - 제출한 모델의 성능은 ROC-AUC 평가지표에 따라 채점

<br>

### 01. 베이스라인
- 데이터를 불러오고, 간단한 탐색적 데이터 분석 진행

> 코드
```python
  # 1. 문제 정의
  # 평가 : roc-auc
  # target : Outcome
  # 최종 파일 : result.csv (컬럼 1개 pred, 1 확률값)
  
  # 2. 라이브러리 및 데이터 불러오기
  import pandas as pd
  
  train = pd.read_csv('./data/diabetes_train.csv')
  test = pd.read_csv('./data/diabetes_test.csv')
  
  # 3. 탐색적 데이터 분석(EDA)
  print('==== 데이터 크기 ====')
  print('Train Shape :', train.shape)
  print('Test Shape :', test.shape)
  print('\n')     # 줄바꿈
  
  print('==== train 데이터 샘플 ====')
  print(train.head(1))
  print('\n')
  
  print('==== test 데이터 샘플 ====')
  print(test.head(1))
  print('\n')
  
  print('==== 데이터 정보(자료형) ====')
  print(train.info())
  print('\n')
  
  print('==== train 결측치 수 ====')
  print(train.isnull().sum().sum())
  print('\n')
  
  print('==== test 결측치 수 ====')
  print(test.isnull().sum().sum())
  print('\n')
  
  print('==== target 빈도 ====')
  print(train['Outcome'].value_counts())
```

> 결과
```python
  ==== 데이터 크기 ====
  Train Shape : (614, 9)
  Test Shape : (154, 8)
  
  
  ==== train 데이터 샘플 ====
     Pregnancies  Glucose  BloodPressure  SkinThickness  Insulin   BMI  \
  0            1      118             58             36       94  33.3   
  
     DiabetesPedigreeFunction  Age  Outcome  
  0                     0.261   23        0  
  
  
  ==== test 데이터 샘플 ====
     Pregnancies  Glucose  BloodPressure  SkinThickness  Insulin   BMI  \
  0            3      102             74              0        0  29.5   
  
     DiabetesPedigreeFunction  Age  
  0                     0.121   32  
  
  
  ==== 데이터 정보(자료형) ====
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 614 entries, 0 to 613
  Data columns (total 9 columns):
   #   Column                    Non-Null Count  Dtype  
  ---  ------                    --------------  -----  
   0   Pregnancies               614 non-null    int64  
   1   Glucose                   614 non-null    int64  
   2   BloodPressure             614 non-null    int64  
   3   SkinThickness             614 non-null    int64  
   4   Insulin                   614 non-null    int64  
   5   BMI                       614 non-null    float64
   6   DiabetesPedigreeFunction  614 non-null    float64
   7   Age                       614 non-null    int64  
   8   Outcome                   614 non-null    int64  
  dtypes: float64(2), int64(7)
  memory usage: 43.3 KB
  None
  
  
  ==== train 결측치 수 ====
  0
  
  
  ==== test 결측치 수 ====
  0
  
  
  ==== target 빈도 ====
  Outcome
  0    403
  1    211
  Name: count, dtype: int64
```
- 주어진 데이터는 결측치가 없고 모두 수치형

  - 베이스라인에서는 전처리 생략

<br>

> 코드
```python
  # 4. 데이터 전처리
  target = train.pop('Outcome')    # 변수 분리
  
  # 5. 검증 데이터 나누기
  from sklearn.model_selection import train_test_split
  X_train, X_val, y_train, y_val = train_test_split(train, target, test_size=0.2, random_state=0)
  
  print('\n ==== 분할된 데이터 크기 ====')
  print(X_train.shape, X_val.shape, y_train.shape, y_val.shape)
  
  # 6. 머신러닝 학습 및 평가
  from sklearn.ensemble import RandomForestClassifier
  rf = RandomForestClassifier(random_state=0)
  rf.fit(X_train, y_train)
  pred = rf.predict_proba(X_val)
  
  print('\n ==== 예측 결과 확인 (샘플 5개) ====')
  print(pred[:5])
  
  from sklearn.metrics import roc_auc_score
  roc_auc = roc_auc_score(y_val, pred[:, 1])
  print('\n roc_auc :', roc_auc)
  
  # 7. 예측 및 결과 파일 생성
  pred = rf.predict_proba(test)
  submit = pd.DataFrame({'pred':pred[:, 1]})
  submit.to_csv('result1.csv', index=False)
  
  # 제출 파일 확인
  print('\n ==== 제출 파일(샘플 5개) ====')
  print(pd.read_csv('result1.csv').head())
```
- 검증 데이터를 학습용(train) 데이터에서 20% 정도 사용

- 데이터 분할 전 target 분리하지 않는다면
```python
  X_train, X_val, y_train, y_val = train_test_split(train.drop('target', axis=1), train['target'], test_size=0.2, random_state=0)
```

- 랜덤포레스트로 모델을 만들고 예측한 결과 ROC-AUC 가 0.80

- 시험에서는 pd.read_csv('result.csv') 로 생성된 csv 확인 후 베이스라인을 1차 제출

> 결과
```python
   ==== 분할된 데이터 크기 ====
  (491, 8) (123, 8) (491,) (123,)
  
   ==== 예측 결과 확인 (샘플 5개) ====
  [[0.88 0.12]
   [0.29 0.71]
   [0.41 0.59]
   [0.75 0.25]
   [0.89 0.11]]
  
   roc_auc : 0.8002739726027398
  
   ==== 제출 파일(샘플 5개) ====
     pred
  0  0.17
  1  0.33
  2  0.11
  3  0.04
  4  0.09
```

<br>

### 02. 성능 개선
- 베이스라인을 도움 없이 만들 수 있을 때부터 시작

- 성능 개선의 목적은 베이스라인보다 좋은 결과 얻기

- 성능 개선 기준

  - 성능이 베이스라인보다 올라가면 적용
 
  - 수정된 마지막 점수보다 내려가면 적용 X

- 성능 개선 방법 및 순서

  - 전처리 → 하이퍼파라미터 튜닝 : 데이터가 달라지면 하이퍼파라미터 튜닝도 다시 해야하기 때문
 
    - 데이터 전처리
   
      - 모두 수치형 데이터므로 스케일링 세 가지 적용
     
      - Min-Max-Scaler 적용값이 가장 높음
   
    - 하이퍼파라미터 튜닝
   
      - 랜덤포레스트 모델에서 하이퍼파라미터는 max_depth 와 n_estimators
     
        - max_depth : 트리의 최대 깊이
       
          - 트리의 깊이 제한 → 과적합 방지
         
          - 기본값 없음
         
        - n_estimators : 트리의 개수
       
          - 높을수록 안정적으로 예측 가능, 학습 시간 증가
         
          - 기본값 : 100
         
      - 랜덤포레스트 분류에서 max_depth 는 3\~7, n_estimators 는 200\~500 정도로 적용

<br>

|데이터 전처리/하이퍼파라미터 튜닝|ROC-AUC|제출|
|-|-|-|
|베이스라인|0.8002739726027398|선택 / 1차 제출|
|스케일링(Standard Scaler)|0.8005479452054794||
|스케일링(Min-Max Scaler)|0.8031506849315069|선택|
|스케일링(Robust Scaler)|0.7987671232876713||
|max_depth = 3|0.8123287671232877||
|max_depth = 5|0.8156164383561644|선택|
|max_depth = 7|0.8054794520547945||
|max_depth = 5, n_estimators = 200|0.8216438356164385||
|max_depth = 5, n_estimators = 400|0.821917808219178||
|max_depth = 5, n_estimators = 600|0.8241095890410959|선택 / 최종 제출|

<br>

> 코드
```python
  # 2. 라이브러리 및 데이터 불러오기
  import pandas as pd
  
  train = pd.read_csv('./data/diabetes_train.csv')
  test = pd.read_csv('./data/diabetes_test.csv')
  
  # 4. 데이터 전처리
  # 스케일링
  target = train.pop('Outcome')
  from sklearn.preprocessing import StandardScaler
  from sklearn.preprocessing import MinMaxScaler
  from sklearn.preprocessing import RobustScaler
  scaler = RobustScaler()
  train = scaler.fit_transform(train)
  test = scaler.transform(test)
  
  # 5. 검증 데이터 나누기
  from sklearn.model_selection import train_test_split
  X_train, X_val, y_train, y_val = train_test_split(train, target, test_size=0.2, random_state=0)
  
  # 6. 머신러닝 학습 및 평가
  from sklearn.ensemble import RandomForestClassifier
  rf = RandomForestClassifier(max_depth=5, n_estimators=600, random_state=0)
  rf.fit(X_train, y_train)
  pred = rf.predict_proba(X_val)
  
  from sklearn.metrics import roc_auc_score
  roc_auc = roc_auc_score(y_val, pred[:, 1])
  print('roc_auc :', roc_auc)

  # 7. 예측 및 결과 파일 생성
  pred = rf.predict_proba(test)
  submit = pd.DataFrame({'pred':pred[:, 1]})
  submit.to_csv('result1.csv', index=False)
```

> 결과
```python
  roc_auc : 0.8241095890410959
```

<br>

---

<br>

SECTION02 이직 여부 예측
---
- 새로운 일자리를 찾을지 예측

  - 제공된 데이터 목록 : hr_train.csv, hr_test.csv
 
  - 예측할 컬럼 : target(0: 새 일자리를 찾지 않음, 1: 새 일자리를 찾음)
 
- 학습용 데이터(train) 이용해 새 일자리를 찾을지 예측하는 모델 생성

- 평가용 데이터(test)에 적용해 얻은 예측값을 아래 형식의 csv 파일로 생성

  - 제출 파일은 다음 2개의 컬럼 포함
 
    - pred : 예측값(이직할 확률)
   
    - 제출 파일명 : 'result2.csv'
   
  - 제출한 모델의 성능은 ROC-AUC 평가지표에 따라 채점

<br>

### 01. 베이스라인
- 데이터를 불러오고, 간단한 탐색적 데이터 분석 진행

<br>

#### (1) EDA

> 코드
```python
  # 1. 문제 정의
  # 평가 : roc-auc
  # target : target
  # 최종 파일 : result.csv(컬럼 1개 pred, 1 확률값)
  
  # 2. 라이브러리 및 데이터 불러오기
  import pandas as pd
  
  train = pd.read_csv('./data/hr_train.csv')
  test = pd.read_csv('./data/hr_test.csv')
  
  # 3. 탐색적 데이터 분석(EDA)
  print('==== 데이터 정보(자료형) ====')
  print(train.info())
  
  print('\n ==== train 결측치 수 ====')
  print(train.isnull().sum())
  
  print('\n ==== test 결측치 수 ====')
  print(test.isnull().sum())
  
  print('\n ==== train 카테고리별 수 ====')
  print(train.nunique())
  
  print('\n ==== test 카테고리별 수 ====')
  print(test.nunique())
  
  print('\n ==== target 빈도 ====')
  print(train['target'].value_counts())
```

> 결과
```python
  ==== 데이터 정보(자료형) ====
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 15326 entries, 0 to 15325
  Data columns (total 14 columns):
   #   Column                  Non-Null Count  Dtype  
  ---  ------                  --------------  -----  
   0   enrollee_id             15326 non-null  int64  
   1   city                    15326 non-null  object 
   2   city_development_index  15326 non-null  float64
   3   gender                  11750 non-null  object 
   4   relevent_experience     15326 non-null  object 
   5   enrolled_university     15012 non-null  object 
   6   education_level         14961 non-null  object 
   7   major_discipline        13045 non-null  object 
   8   experience              15272 non-null  object 
   9   company_size            10539 non-null  object 
   10  company_type            10383 non-null  object 
   11  last_new_job            14984 non-null  object 
   12  training_hours          15326 non-null  int64  
   13  target                  15326 non-null  float64
  dtypes: float64(2), int64(2), object(10)

  memory usage: 1.6+ MB
  None
  
   ==== train 결측치 수 ====
  enrollee_id                  0
  city                         0
  city_development_index       0
  gender                    3576
  relevent_experience          0
  enrolled_university        314
  education_level            365
  major_discipline          2281
  experience                  54
  company_size              4787
  company_type              4943
  last_new_job               342
  training_hours               0
  target                       0
  dtype: int64
  
   ==== test 결측치 수 ====
  enrollee_id                  0
  city                         0
  city_development_index       0
  gender                     932
  relevent_experience          0
  enrolled_university         72
  education_level             95
  major_discipline           532
  experience                  11
  company_size              1151
  company_type              1197
  last_new_job                81
  training_hours               0
  dtype: int64
  
   ==== train 카테고리별 수 ====
  enrollee_id               15326
  city                        123
  city_development_index       93
  gender                        3
  relevent_experience           2
  enrolled_university           3
  education_level               5
  major_discipline              6
  experience                   22
  company_size                  8
  company_type                  6
  last_new_job                  6
  training_hours              241
  target                        2
  dtype: int64
  
   ==== test 카테고리별 수 ====
  enrollee_id               3832
  city                       113
  city_development_index      87
  gender                       3
  relevent_experience          2
  enrolled_university          3
  education_level              5
  major_discipline             6
  experience                  22
  company_size                 8
  company_type                 6
  last_new_job                 6
  training_hours             235
  dtype: int64
  
   ==== target 빈도 ====
  target
  0.0    11517
  1.0     3809
  Name: count, dtype: int64
```
- 수치형 컬럼(변수) : 4개, 범주형 컬럼(변수) : 10개

- 결측치도 train 과 test 모두 8개의 컬럼에 有

  - 모두 object 자료형

- nunique() 활용해 컬럼별 카테고리 수 확인

  - object 외의 자료형도 포함됨
 
  - object 형만 확인하고 싶으면?
 
    - train.select_dtypes(include=['object']).unique()
   
  - city 컬럼은 train 과 test 가 다름

<br>

#### 💡 train 과 test 범주형 데이터 비교
- object 가 컬럼과 카테고리가 많이 있을 때는 train 과 test 의 카테고리 차이를 눈으로 비교하기 어려움

- 카테고리 개수가 같더라도 값이 다를 수 있음

- 중복된 값을 허용하지 않는 set() 활용해 2개의 데이터 집합 간에 정확한 비교 가능

> 코드
```python
  import pandas as pd
  
  train = pd.read_csv('./data/hr_train.csv')
  test = pd.read_csv('./data/hr_test.csv')
  
  cols = train.select_dtypes(include='object').columns
  
  for col in cols:
      set_train = set(train[col])
      set_test = set(test[col])
      same = (set_train == set_test)
      if same:
          print(col, '\t 카테고리 동일함')
      else:
          print(col, '\t 카테고리 동일하지 않음')
```

> 결과
```python
  city 	 카테고리 동일하지 않음
  gender 	 카테고리 동일함
  relevent_experience 	 카테고리 동일함
  enrolled_university 	 카테고리 동일함
  education_level 	 카테고리 동일함
  major_discipline 	 카테고리 동일함
  experience 	 카테고리 동일함
  company_size 	 카테고리 동일함
  company_type 	 카테고리 동일함
  last_new_job 	 카테고리 동일함
```

<br>

#### (2) 전처리

> 코드
```python
  # 4. 데이터 전처리
  target = train.pop('target')
  
  # 결측치 처리
  train = train.fillna('X')
  test = test.fillna('X')
  
  # train 과 test 합쳐서 원-핫 인코딩
  combined = pd.concat([train, test])
  combined_dummies = pd.get_dummies(combined)
  n_train = len(train)
  train = combined_dummies[:n_train]
  test = combined_dummies[n_train:]
  
  # 5. 검증 데이터 나누기
  from sklearn.model_selection import train_test_split
  X_train, X_val, y_train, y_val = train_test_split(train, target, test_size=0.2, random_state=0)
  
  # 6. 머신러닝 학습 및 평가
  from sklearn.ensemble import RandomForestClassifier
  rf = RandomForestClassifier(random_state=0)
  rf.fit(X_train, y_train)
  pred = rf.predict_proba(X_val)
  
  from sklearn.metrics import roc_auc_score
  roc_auc = roc_auc_score(y_val, pred[:, 1])
  print('roc_auc :', roc_auc)
  
  # 7. 예측 및 결과 파일 생성
  pred = rf.predict_proba(test)
  submit = pd.DataFrame({'pred': pred[:, 1]})
  submit.to_csv('result2.csv', index=False)
```
- 빈 값은 별도로 X 로 표기

- 컬럼의 수가 다르므로 train 과 test 를 합쳐 원-핫 인코딩 진행 후 다시 train 과 test 로 나눔

- 랜덤포레스트로 모델을 만들고 예측

> 결과
```python
  roc_auc : 0.7730742036233207
```

<br>

### 02. 성능 개선
- **데이터 전처리**

  - **레이블 인코딩** : 베이스라인에 있는 원-핫 인코딩을 레이블 인코딩으로 변경
 
  - 스케일링(Standard Scaler, Min-Max Scaler, Robust Scaler)
 
  - id 제거
 
- **하이퍼파라미터 튜닝**

  - **max-depth** : 3 ~ 7
 
  - **n_estimators** : 200 ~ 500

- 위에서는 결측치가 object 자료형이라 일괄 X 로 처리

  - 각 컬럼별로 다른 결측 처리 할 수도 있음

<br>

|데이터 전처리/하이퍼파라미터 튜닝|ROC-AUC|제출|
|베이스라인|0.7730742036233207|선택 / 1차 제출|
|레이블 인코딩|0.7747496616891663|선택|
|id 제거|0.7649556215788462|성능 떨어짐 - 생략|
|스케일링(Standard Scaler)|0.7749234996090111||
|스케일링(Min-Max Scaler)|0.7749741291715249||
|스케일링(Robust Scaler)|0.7750549023464022|선택|
|max-depth = 3|0.775941358675039||
|max-depth = 5|0.7796899948960718||
|max-depth = 7|0.7816010413886431|선택|
|max-depth = 7, n_estimators = 200|0.7825363713412095|선택 / 2차 제출|
|max-depth = 7, n_estimators = 400|0.7825246650839807||
|max-depth = 7, n_estimators = 600|0.7823490712255514||

<br>

> 코드
```python
  # 2. 라이브러리 및 데이터 불러오기
  import pandas as pd
  train = pd.read_csv('./data/hr_train.csv')
  test = pd.read_csv('./data/hr_test.csv')
  
  # 4. 데이터 전처리
  target = train.pop('target')
  
  # 결측치 제거
  train = train.fillna('X')
  test = test.fillna('X')
  
  # 레이블 인코딩
  from sklearn.preprocessing import LabelEncoder
  combined = pd.concat([train, test])
  cols = train.select_dtypes(include = 'object').columns
  for col in cols:
      le = LabelEncoder()
      combined[col] = le.fit_transform(combined[col])
  n_train = len(train)
  train = combined[:n_train]
  test = combined[n_train:]
  
  # id 제거   (성능 떨어짐)
  # train = train.drop('enrollee_id', axis=1)
  # test = test.drop('enrollee_id', axis=1)
  
  # 스케일링
  from sklearn.preprocessing import RobustScaler
  scaler = RobustScaler()
  n_cols = train.select_dtypes(exclude='object').columns
  train = scaler.fit_transform(train)
  test = scaler.transform(test)
  
  # 5. 검증 데이터 분할
  from sklearn.model_selection import train_test_split
  X_train, X_val, y_train, y_val = train_test_split(train, target, test_size=0.2, random_state=0)
  
  # 6. 머신러닝 학습 및 평가
  from sklearn.ensemble import RandomForestClassifier
  rf = RandomForestClassifier(max_depth=7, n_estimators=200, random_state=0)
  rf.fit(X_train, y_train)
  pred = rf.predict_proba(X_val)
  
  from sklearn.metrics import roc_auc_score
  roc_auc = roc_auc_score(y_val, pred[:, 1])
  print('roc_auc :', roc_auc)

  # 7. 예측 및 결과 파일 생성
  pred = rf.predict_proba(test)
  submit = pd.DataFrame({'pred': pred[:, 1]})
  submit.to_csv('result2.csv', index=False)

  # 결과 샘플
  print('\n==== result2.csv 샘플 데이터 5개 ====')
  print(pd.read_csv('result2.csv').head())
```

> 결과
```python
  roc_auc : 0.7825363713412095
  
  ==== result2.csv 샘플 데이터 5개 ====
         pred
  0  0.188463
  1  0.529855
  2  0.600765
  3  0.080796
  4  0.109437
```

<br>

---

<br>

SECTION03 신용카드 신천자의 미래 신용 예측
---




<br>















