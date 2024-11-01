# CHAPTER07 다중 분류 연습문제
- 다중 분류는 여러 개의 클래스 중 하나를 예측

- 이진 분류와 크게 다르지 않으나, 평가지표 사용할 때 차이점 있음

<br>

SECTION01 신용 등급 예측
---
- 은행 정보로 신용 등급 예측

  - 제공된 데이터 목록 : score_train.csv, score_test.csv
 
  - 예측할 컬럼 : Credit_Score(Good, Standard, Poor)
 
- 학습용 데이터(train)를 이용해 신용 등급 예측하는 모델 생성

- 평가용 데이터(test)에 적용해 얻은 예측값을 아래 형식의 csv 파일로 생성

  - 제출 파일은 다음 1개의 컬럼을 포함
 
    - pred : 예측값
   
    - 제출 파일명 : 'result1.csv'
   
  - 제출한 모델의 성능은 f1-macro 평가지표에 따라 채점

<br>

### 01. 베이스라인
- 데이터를 불러오고, 간단한 탐색적 데이터 분석 진행

<br>

#### (1) EDA
> 코드
```python
  # 1. 문제정의
  # 평가 : f1-macro
  # target : Credit_Score
  # 최종 파일 : result1.csv(컬럼 1개 pred)
  
  # 라이브러리 및 데이터 불러오기
  import pandas as pd
  
  train = pd.read_csv('./data/score_train.csv')
  test = pd.read_csv('./data/score_test.csv')
  
  # 3. 탐색적 데이터 분석(EDA)
  print('==== 데이터 크기 ====')
  print('train shape :', train.shape)
  print('test shape :', test.shape)
  print('\n')     # 줄 바꿈
  
  print('==== 데이터 정보(자료형) ====')
  print(train.info())
  print('\n')
  
  print('==== train 결측치 수 ====')
  print(train.isnull().sum())
  print('\n')
  
  print('==== test 결측치 수 ====')
  print(test.isnull().sum())
  print('\n')
  
  print('==== target 빈도 ====')
  print(train['Credit_Score'].value_counts())
```

> 결과
```python
  ==== 데이터 크기 ====
  train shape : (4198, 21)
  test shape : (1499, 20)
  
  
  ==== 데이터 정보(자료형) ====
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 4198 entries, 0 to 4197
  Data columns (total 21 columns):
   #   Column                    Non-Null Count  Dtype  
  ---  ------                    --------------  -----  
   0   Delay_from_due_date       4198 non-null   float64
   1   Num_of_Delayed_Payment    4198 non-null   float64
   2   Num_Credit_Inquiries      4198 non-null   float64
   3   Credit_Utilization_Ratio  4198 non-null   float64
   4   Credit_History_Age        4198 non-null   float64
   5   Payment_of_Min_Amount     4198 non-null   object 
   6   Amount_invested_monthly   4198 non-null   float64
   7   Monthly_Balance           4198 non-null   float64
   8   Credit_Mix                4198 non-null   object 
   9   Payment_Behaviour         4198 non-null   object 
   10  Age                       4198 non-null   float64
   11  Annual_Income             4198 non-null   float64
   12  Num_Bank_Accounts         4198 non-null   float64
   13  Num_Credit_Card           4198 non-null   float64
   14  Interest_Rate             4198 non-null   float64
   15  Num_of_Loan               4198 non-null   float64
   16  Monthly_Inhand_Salary     4198 non-null   float64
   17  Changed_Credit_Limit      4198 non-null   float64
   18  Outstanding_Debt          4198 non-null   float64
   19  Total_EMI_per_month       4198 non-null   float64
   20  Credit_Score              4198 non-null   object 
  dtypes: float64(17), object(4)
  memory usage: 688.9+ KB
  None
  
  
  ==== train 결측치 수 ====
  Delay_from_due_date         0
  Num_of_Delayed_Payment      0
  Num_Credit_Inquiries        0
  Credit_Utilization_Ratio    0
  Credit_History_Age          0
  Payment_of_Min_Amount       0
  Amount_invested_monthly     0
  Monthly_Balance             0
  Credit_Mix                  0
  Payment_Behaviour           0
  Age                         0
  Annual_Income               0
  Num_Bank_Accounts           0
  Num_Credit_Card             0
  Interest_Rate               0
  Num_of_Loan                 0
  Monthly_Inhand_Salary       0
  Changed_Credit_Limit        0
  Outstanding_Debt            0
  Total_EMI_per_month         0
  Credit_Score                0
  dtype: int64
  
  
  ==== test 결측치 수 ====
  Delay_from_due_date         0
  Num_of_Delayed_Payment      0
  Num_Credit_Inquiries        0
  Credit_Utilization_Ratio    0
  Credit_History_Age          0
  Payment_of_Min_Amount       0
  Amount_invested_monthly     0
  Monthly_Balance             0
  Credit_Mix                  0
  Payment_Behaviour           0
  Age                         0
  Annual_Income               0
  Num_Bank_Accounts           0
  Num_Credit_Card             0
  Interest_Rate               0
  Num_of_Loan                 0
  Monthly_Inhand_Salary       0
  Changed_Credit_Limit        0
  Outstanding_Debt            0
  Total_EMI_per_month         0
  dtype: int64
  
  
  ==== target 빈도 ====
  Credit_Score
  Standard    2225
  Poor        1232
  Good         741
  Name: count, dtype: int64
```
- train 데이터의 자료형 : float64 17개, object 4개

- target : 세 가지 카테고리(클래스)가 있는 object 자료형

  - 인코딩할 경우 target 컬럼 제외
 
    - target 컬럼 원-핫 인코딩할 경우 target 컬럼이 1개가 아닌 여러개 만들어짐
   
    - 레이블 인코딩은 가능하지만, 0, 1, 2 로 변경한 후 마지막 csv 제출에서 다시 Good, Standard, Poor 로 복원해야 함
   
    - 랜덤포레스트 모델은 target 이 object 더라도 자동으로 인식해 수치형으로 인코딩 없이 사용 가능

- 결측치 없음

<br>

#### (2) 전처리 및 예측
- 평가지표 : f1-macro

  - 이진분류와 같이 F1 스코어 평가지표 사용하되, average='macro' 설정
 
> 코드
```python
  # 4. 데이터 전처리
  # 원-핫 인코딩(target 컬럼이 object 형이라 제외)
  target = train.pop('Credit_Score')
  
  train = pd.get_dummies(train)
  test = pd.get_dummies(test)
  
  # 5. 검증 데이터 나누기
  from sklearn.model_selection import train_test_split
  X_train, X_val, y_train, y_val = train_test_split(train, target, test_size=0.2, random_state=0)
  
  print('\n==== 분할된 데이터 크기 ====')
  print(X_train.shape, X_val.shape, y_train.shape, y_val.shape)
  
  # 6. 머신러닝 학습 및 평가
  from sklearn.ensemble import RandomForestClassifier
  rf = RandomForestClassifier(random_state=0)
  rf.fit(X_train, y_train)
  pred = rf.predict(X_val)
  
  from sklearn.metrics import f1_score
  f1 = f1_score(y_val, pred, average='macro')
  print('\nf1-macro :', f1)
  
  # 7. 예측 및 결과 파일 생성
  pred = rf.predict(test)
  submit = pd.DataFrame({'pred':pred})
  submit.to_csv('result1.csv', index=False)
  
  # 제출 파일 확인
  print('\n==== 제출 파일 (샘플 5개) ====')
  print(pd.read_csv('result1.csv').head())
```

> 결과
```python
  ==== 분할된 데이터 크기 ====
  (3358, 29) (840, 29) (3358,) (840,)
  
  f1-macro : 0.7004593488873695
  
  ==== 제출 파일 (샘플 5개) ====
         pred
  0      Poor
  1      Good
  2  Standard
  3      Good
  4  Standard
```

<br>

### 02. 성능 개선
- 간단한 하이퍼파라미터 튜닝으로는 성능 향상 실패

  - 성능이 향상되지 않는 케이스에선 튜닝을 더 하기보단 작업한 내용 중 최고 점수 제출
 
- 데이터 전처리

  - 레이블 인코딩 : 성능이 오히려 떨어짐
 
  - 스케일링(Standard Scaler) : 약간의 변화 확인됨
 
- 하이퍼파라미터 튜닝

  - max_depth : 5 ~ 10, 이진 분류보다는 좀 더 깊이를 깊게 설정
 
  - n_setimators : 200 ~ 500

<BR>

|데이터 전처리/하이퍼파라미터 튜닝|F1|제출|
|-|-|-|
|베이스라인|0.7004593488873695|선택 / 1차 제출|
|레이블 인코딩|0.6853171856067161||
|스케일링(Standard Scaler)|0.7020460066061172|선택 / 2차 제출|
|스케일링(Min-Max Scaler)|0.7006138262986147||
|스케일링(Robust Scaler)|0.6988656925588274||
|max_depth = 5|0.6766506819894232||
|max_depth = 7|0.6870057878861987||
|max_depth = 10|0.6916940184736795||
|n_estimators = 200|0.6962063487956804||
|n_estimators = 400|0.6940222897669707||
|n_estimators = 500|0.6928450293038421||

<br>

> 코드
```python
  # 2. 라이브러리 및 데이터 불러오기
  import pandas as pd
  
  train = pd.read_csv('./data/score_train.csv')
  test = pd.read_csv('./data/score_test.csv')
  
  # 4. 데이터 전처리
  target = train.pop('Credit_Score')
  
  # 스케일링
  from sklearn.preprocessing import StandardScaler
  scaler = StandardScaler()
  cols = train.select_dtypes(exclude='object').columns
  train[cols] = scaler.fit_transform(train[cols])
  test[cols] = scaler.transform(test[cols])
  
  # 원-핫 인코딩
  train = pd.get_dummies(train)
  test = pd.get_dummies(test)
  
  # 레이블 인코딩 : 성능 떨어짐 주석처리
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
  from sklearn.ensemble import RandomForestClassifier
  rf = RandomForestClassifier(random_state=0)
  rf.fit(X_train, y_train)
  pred = rf.predict(X_val)
  
  from sklearn.metrics import f1_score
  f1 = f1_score(y_val, pred, average='macro')
  print('f1-macro :', f1)
  
  # 7. 예측 및 결과 파일 생성
  pred = rf.predict(test)
  submit = pd.DataFrame({'pred':pred})
  submit.to_csv('result1.csv', index=False)
  
  # 제출 파일 확인
  print('\n==== 제출 파일 (샘플 5개) ====')
  print(pd.read_csv('result1.csv').head())
```

> 결과
```python
  f1-macro : 0.7020460066061172
  
  ==== 제출 파일 (샘플 5개) ====
         pred
  0      Poor
  1      Good
  2  Standard
  3      Good
  4  Standard
```

<br>

---

<BR>

SECTION02 약물 종류 예측
---
- 주어진 데이터에서 약물의 종류 예측

  - 제공된 데이터 목록 : drug_train.csv, drug_test.csv
 
  - 예측할 컬럼 : Drug(DrugY, drugX, drugA, drugC, drugB)
 
- 학습용 데이터(train.csv)을 이용해 약물의 종류 예측하는 모델 생성

- 평가용 데이터(test.csv)에 적용해 얻은 예측값을 아래 형식의 csv 파일로 생성

  - 제출 파일은 다음 1 개의 컬럼 포함
 
    - pred : 예측값
   
    - 제출 파일명 : 'result2.csv'
   
  - 제출한 모델의 성능은 f1-macro 평가지표에 따라 채점

<BR>

### 01. 베이스 라인
- 베이스라인에서 f1 평가 점수의 결과가 높게(1에 가깝게) 나올 경우

<br>

#### (1) EDA

> 코드
```python
  # 1. 문제 정의
  # 평가 : f1-macro
  # target : Drug
  # 최종 파일 : result2.csv(컬럼 1개 pred, 1 확률값)
  
  # 2. 라이브러리 및 데이터 불러오기
  import pandas as pd
  
  train = pd.read_csv('./data/drug_train.csv')
  test = pd.read_csv('./data/drug_test.csv')
  
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
  
  print('\n==== train 카테고리별 수 ===')
  print(train[['Sex', 'BP', 'Cholesterol']].nunique())
  
  print('\n==== test 카테고리별 수 ====')
  print(test[['Sex', 'BP', 'Cholesterol']].nunique())
  
  print('\n==== target 빈도 ====')
  print(train['Drug'].value_counts())
```

> 결과
```python
  ==== 데이터 크기 ====
  Train Shape : (100, 6)
  Test Shape : (100, 5)
  
  ==== 데이터 정보(자료형) ====
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 100 entries, 0 to 99
  Data columns (total 6 columns):
   #   Column       Non-Null Count  Dtype  
  ---  ------       --------------  -----  
   0   Age          100 non-null    int64  
   1   Sex          100 non-null    object 
   2   BP           100 non-null    object 
   3   Cholesterol  100 non-null    object 
   4   Na_to_K      100 non-null    float64
   5   Drug         100 non-null    object 
  dtypes: float64(1), int64(1), object(4)
  memory usage: 4.8+ KB
  None
  
  ==== train 결측치 수 ====
  Age            0
  Sex            0
  BP             0
  Cholesterol    0
  Na_to_K        0
  Drug           0
  dtype: int64
  
  ==== test 결측치 수 ====
  Age            0
  Sex            0
  BP             0
  Cholesterol    0
  Na_to_K        0
  dtype: int64
  
  ==== train 카테고리별 수 ===
  Sex            2
  BP             3
  Cholesterol    2
  dtype: int64
  
  ==== test 카테고리별 수 ====
  Sex            2
  BP             3
  Cholesterol    2
  dtype: int64
  
  ==== target 빈도 ====
  Drug
  DrugY    41
  drugX    34
  drugA    13
  drugB     8
  drugC     4
  Name: count, dtype: int64
```

<br>

#### (2) 전처리 및 예측
- f1 평가 점수가 너무 높게 나올 경우(0~1 중에 1점) 원인

  - 데이터를 나눌 때 또는 전처리 때 잘못한 부분 有
 
    - model.fit(X, y) 에서 모델 학습시 사용하는 X 데이터를 head() 로 출력해 확인
   
    - 간혹 target 이 학습용 데이터 X 에 포함된 경우 이미 답을 알고 있기에 만점이 나옴
   
  - 검증 데이터가 너무 쉽게 나눠짐

    - 이번 문제의 경우 평소대로 20% 검증 데이터로 평가했을 때 1점 나옴
   
      - 검증 데이터를 평가하는 다른 방식 필요
     
        - 크로스 밸리데이션 활용 (필수 X)

> 코드
```python
  # 4. 데이터 전처리
  # 원-핫 인코딩
  target = train.pop('Drug')
  
  train = pd.get_dummies(train)
  test = pd.get_dummies(test)
  
  # 5. 검증 데이터 나누기
  from sklearn.model_selection import train_test_split
  X_train, X_val, y_train, y_val = train_test_split(train, target, test_size=0.2, random_state=0)
  
  # 6 머신러닝 학습 및 평가
  from sklearn.ensemble import RandomForestClassifier
  rf = RandomForestClassifier(random_state=0)
  rf.fit(X_train, y_train)
  pred = rf.predict(X_val)
  
  from sklearn.metrics import f1_score
  f1 = f1_score(y_val, pred, average='macro')
  print('f1-macro :', f1)
  
  # 7. 예측 및 결과 파일 생성
  pred = rf.predict(test)
  submit = pd.DataFrame({'pred':pred})
  submit.to_csv('result2.csv', index=False)
  
  # 제출 파일 확인
  print('\n==== 제출 파일 (샘플 5개) ====')
  print(pd.read_csv('result2.csv').head())
```

> 결과
```python
  f1-macro : 1.0
  
  ==== 제출 파일 (샘플 5개) ====
      pred
  0  DrugY
  1  DrugY
  2  DrugY
  3  DrugY
  4  drugB
```

<br>

#### 💡 크로스 밸리데이션(cross-validation)
- 주어진 데이터셋(train)을 K 개로 나눠 모든 데이터가 학습과 검증 데이터로 활용됨

  - K 번의 학습과 평가로 진행
 
> 코드
```python
  from sklearn.metrics import f1_score
  from sklearn.model_selection import cross_val_score
  
  f1_scores = cross_val_score(rf, train, target, cv=3, scoring='f1_macro')
  print(f1_scores)
  print(f1_scores.mean())
```
- scoring='f1_macro' : 평가 지표로 f1-macro 점수를 사용하겠다는 뜻

  - 각 클래스별 F1 점수를 계산한 후, 클래스 간의 불균형을 고려해 평균을 내며 클래스 비율이 불균형한 문제에서 효과적

> 결과
```python
  [1.         0.93777778 0.78461538]
  0.9074643874643874
```
- cv = 3 으로 설정 : 3번의 학습과 평가가 진행됨

  - 각각 [1. 0.93777778 0.78461538] 결과가 나옴
 
    - 0.78 있는 것으로 보아 베이스라인에서 데이터를 나눌 때 운 좋게 쉬운 데이터로만 검증데이터가 나눠졌을 가능성 有
   
    - 3개의 결과를 평균하면 0.9점

<br>

#### 💡 scoring 파라미터
- 평가 기준을 지정하며, 모델의 성능을 다양한 방식으로 측정할 수 있도록 여러 평가지표를 지원

  - 분류, 회귀 등 다양한 문제 유형에 맞는 성능 평가가 가능

<br>

(1) 분류 평가 지표
- accuracy: 정확도. 전체 샘플 중에서 정확히 예측한 비율

- f1: F1 점수. 정밀도와 재현율의 조화 평균, 불균형 데이터셋에서 유용

- f1_macro: 클래스별 F1 점수를 계산한 후, 이를 평균하여 계산. 클래스 불균형 문제에서 성능을 균형 있게 평가

- f1_micro: 클래스별 예측을 전부 합산하여 F1 점수를 계산. 클래스 빈도에 따른 가중 평균이 반영됨

- f1_weighted: 클래스별 F1 점수를 계산한 후 각 클래스의 샘플 수를 가중치로 반영해 평균

- precision: 정밀도. 양성으로 예측된 샘플 중 실제로 양성인 샘플의 비율

- recall: 재현율. 실제 양성 샘플 중에서 양성으로 정확히 예측한 비율

- roc_auc: ROC 곡선 아래의 면적. 이진 분류 문제에서 클래스 구분 능력을 측정

- log_loss: 로그 손실. 예측 확률과 실제 클래스 간의 손실을 측정

<br>

(2) 회귀 평가 지표
- r2: 결정 계수. 예측 값이 실제 값을 얼마나 잘 설명하는지를 나타내는 지표

- neg_mean_absolute_error: 평균 절대 오차. 예측값과 실제값의 차이를 절대값으로 계산하여 평균

- neg_mean_squared_error: 평균 제곱 오차. 오차를 제곱하여 평균한 값, 큰 오차에 큰 패널티를 부과

- neg_root_mean_squared_error: 평균 제곱근 오차. 평균 제곱 오차의 제곱근, 예측값의 표준 편차와 유사한 해석

- explained_variance: 예측값이 실제 데이터의 분산을 설명하는 비율

<br>

(3) 다중 분류 평가 지표
- balanced_accuracy: 각 클래스별로 정확도를 계산하여 평균

- top_k_accuracy: k개의 상위 예측 중 정답이 포함된 비율(다중 클래스 분류)

- jaccard: 예측 값과 실제 값 사이의 유사성을 측정하는 Jaccard 계수

<br>

### 02. 성능 개선
- 베이스라인 모델 점수와 성능 개선 모델 점수 비교

- 데이터 전처리

  - 레이블 인코딩
 
  - 스케일 : Standard Encoder, Min-Max Encoder, Robust Encoder
 
- 하이퍼파라미터 튜닝

  - max_depth : 3 ~ 7
 
  - n_estimators : 200 ~ 500

<br>

|데이터 전처리/하이퍼파라미터 튜닝|f1|제출|
|-|-|-|
|베이스라인|0.9074643874643874|선택 / 1차 제출, 2차 제출|
|레이블 인코딩|0.8815384615384616||
|스케일링(Standard, Min-Max, Robust Encoder)|0.9074643874643874||
|max_depth = 3|0.7230140873619134||
|max_depth = 5, 7|0.9074643874643874||
|n_estimators = 200, 400, 500|0.9074643874643874||

<br>

> 코드
```python
  # 2. 라이브러리 및 데이터 불러오기
  import pandas as pd
  
  train = pd.read_csv('./data/drug_train.csv')
  test = pd.read_csv('./data/drug_test.csv')
  
  # 4. 데이터 전처리
  target = train.pop('Drug')
  
  # 스케일링 (영향 X, 생략)
  # from sklearn.preprocessing import RobustScaler
  # scaler = RobustScaler()
  # train['Age'] = scaler.fit_transform(train[['Age']])
  # test['Age'] = scaler.transform(test[['Age']])
  
  # 원-핫 인코딩(Drug 컬럼 제외)
  train = pd.get_dummies(train)
  test = pd.get_dummies(test)
  
  # 레이블 인코딩(Drug 컬럼 제외)
  # from sklearn.preprocessing import LabelEncoder
  # cols = train.select_dtypes(include='object').columns
  # for col in cols:
  #     le = LabelEncoder()
  #     train[col] = le.fit_transform(train[col])
  #     test[col] = le.transform(test[col])
  
  # 5. 크로스 밸리데이션(cross-validation)
  from sklearn.metrics import f1_score
  from sklearn.model_selection import cross_val_score
  from sklearn.ensemble import RandomForestClassifier
  
  rf = RandomForestClassifier(random_state=0)
  f1_scores = cross_val_score(rf, train, target, cv=3, scoring='f1_macro')
  print(f1_scores.mean())
  
  # 6. 머신러닝 학습
  rf.fit(train, target)
  
  # 7. 예측 및 결과 파일 생성
  pred = rf.predict(test)
  submit = pd.DataFrame({'pred':pred})
  submit.to_csv('result2.csv', index=False)
```
- 크로스밸리데이션 사용시 train_test_split() 필요 X

  - 크로스밸리데이션으로 점수 확인 후 train 전체 데이터 사용해 모델 학습

> 결과
```python
  0.9074643874643874
```

<br>

#### 💡 데이터프레임에서 대괄호 수
- 데이터프레임에서 컬럼 선택 시 대괄호 사용하는 방법

  - 대괄호가 1개인 경우 : train['Age']
 
    - 선택한 컬럼을 시리즈(Series) 형태로 반환
   
  - 대괄호가 2개인 경우 : train[['Age']]
 
    - 선택한 컬럼을 데이터프레임(DataFrame) 형태로 반환
   
- 스케일링 등 전처리 함수들은 일반적으로 데이터프레임 자료형 입력

  - 대괄호 2개 사용해 데이터프레임 형태로 데이터 넘겨주기
 
- 여러 컬럼 선택 할 때 대괄호 2개 사용

  -  train[['컬럼명1', '컬럼명2']]
 
  - 일반적으로 여러 컬럼인 경우 cols = ['컬럼명1', '컬럼명2'] 처럼 리스트로 만든 후 train[cols] 에 적용
  
    - 대괄호가 1개처럼 보였을 뿐

<br>

---

<BR>

SECTION03 유리 종류 예측
---
- 유리 식별데이터에서 유리의 종류 예측

  - 제공된 데이터 목록 : glass_train.csv, glass_test.csv
 
  - 예측할 컬럼 : Type(1, 2, 3, 5, 6, 7)
 
- 학습용 데이터(train.csv)를 이용해 약물 종류를 예측하는 모델 생성

- 평가용 데이터(test.csv)에 적용해 얻은 예측값을 아래와 같은 형식의 csv 파일로 생성

  - 제출 파일은 다음 1개의 컬럼 포함
 
    - pred : 예측값
   
    - 제출 파일명 : 'result3.csv'
   
  - 제출한 모델의 성능은 f1-weighted 평가지표에 따라 채점
 
<br>

### 01. 베이스라인
- 데이터를 불러오고, 간단한 탐색적 데이터 분석 진행

<br>

#### (1) EDA
> 코드
```python
  # 1. 문제 정의
  # 평가 : f1-weighted
  # target : Type
  # 최종 파일 : result3.csv
  
  # 2. 라이브러리 및 데이터 불러오기
  import pandas as pd
  
  train = pd.read_csv('./data/glass_train.csv')
  test = pd.read_csv('./data/glass_test.csv')
  
  # 3. 탐색적 데이터 분석 (EDA)
  print('==== 데이터 크기 ====')
  print('Train Shape :', train.shape )
  print('Test Shape :', test.shape)
  
  print('\n==== train 데이터 샘플 ====')
  print(train.head())
  
  print('\n==== test 데이터 샘플 ====')
  print(test.head())
  
  print('\n==== 데이터 정보(자료형) ====')
  print(train.info())
  
  print('\n==== train 결측치 수 ====')
  print(train.isnull().sum())
  
  print('\n==== test 결측치 수 ====')
  print(train.isnull().sum())
  
  print('\n==== target 빈도 ====')
  print(train['Type'].value_counts())
```

> 결과
```python
  ==== 데이터 크기 ====
  Train Shape : (149, 10)
  Test Shape : (65, 9)
  
  ==== train 데이터 샘플 ====
          RI     Na    Mg    Al     Si     K    Ca   Ba    Fe  Type
  0  1.51829  14.46  2.24  1.62  72.38  0.00  9.26  0.0  0.00     6
  1  1.51610  13.33  3.53  1.34  72.67  0.56  8.33  0.0  0.00     3
  2  1.52172  13.48  3.74  0.90  72.01  0.18  9.61  0.0  0.07     1
  3  1.51905  13.60  3.62  1.11  72.64  0.14  8.76  0.0  0.00     1
  4  1.51631  13.34  3.57  1.57  72.87  0.61  7.89  0.0  0.00     2
  
  ==== test 데이터 샘플 ====
          RI     Na    Mg    Al     Si     K     Ca    Ba    Fe
  0  1.51748  12.86  3.56  1.27  73.21  0.54   8.38  0.00  0.17
  1  1.52058  12.85  1.61  2.17  72.18  0.76   9.70  0.24  0.51
  2  1.52475  11.45  0.00  1.88  72.19  0.81  13.24  0.00  0.34
  3  1.51690  13.33  3.54  1.61  72.54  0.68   8.11  0.00  0.00
  4  1.52177  13.75  1.01  1.36  72.19  0.33  11.14  0.00  0.00
  
  ==== 데이터 정보(자료형) ====
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 149 entries, 0 to 148
  Data columns (total 10 columns):
   #   Column  Non-Null Count  Dtype  
  ---  ------  --------------  -----  
   0   RI      149 non-null    float64
   1   Na      149 non-null    float64
   2   Mg      149 non-null    float64
   3   Al      149 non-null    float64
   4   Si      149 non-null    float64
   5   K       149 non-null    float64
   6   Ca      149 non-null    float64
   7   Ba      149 non-null    float64
   8   Fe      149 non-null    float64
   9   Type    149 non-null    int64  
  dtypes: float64(9), int64(1)
  memory usage: 11.8 KB
  None
  
  ==== train 결측치 수 ====
  RI      0
  Na      0
  Mg      0
  Al      0
  Si      0
  K       0
  Ca      0
  Ba      0
  Fe      0
  Type    0
  dtype: int64
  
  ==== test 결측치 수 ====
  RI      0
  Na      0
  Mg      0
  Al      0
  Si      0
  K       0
  Ca      0
  Ba      0
  Fe      0
  Type    0
  dtype: int64
  
  ==== target 빈도 ====
  Type
  2    53
  1    49
  7    23
  3     9
  5     8
  6     7
  Name: count, dtype: int64
```
- 데이터 자료형이 모두 수치형 데이터

  - 별도 전처리 없이 베이스라인 구축

- 결측치 없음

- target 은 6가지

<br>

#### (2) 전처리 및 예측

> 코드
```python
  # 4. 데이터 전처리
  target = train.pop('Type')
  
  # 5. 검증 데이터 나누기
  from sklearn.model_selection import train_test_split
  X_train, X_val, y_train, y_val = train_test_split(train, target, test_size=0.2, random_state=0)
  
  # 6. 머신러닝 학습 및 평가
  from sklearn.ensemble import RandomForestClassifier
  rf = RandomForestClassifier(random_state=0)
  rf.fit(X_train, y_train)
  pred = rf.predict(X_val)
  
  from sklearn.metrics import f1_score
  f1 = f1_score(y_val, pred, average='weighted')
  print('f1 :', f1)
  
  # 7. 예측 및 결과 파일 생성
  pred = rf.predict(test)
  submit = pd.DataFrame({'pred':pred})
  submit.to_csv('result3.csv', index=False)
  
  print('\n==== 제출 파일 (샘플 5개) ====')
  print(pd.read_csv('result3.csv').head())
```

> 결과
```python
  f1 : 0.6119801766860591
  
  ==== 제출 파일 (샘플 5개) ====
     pred
  0     1
  1     2
  2     2
  3     2
  4     2
```

<br>

### 02. 성능 개선
- 랜덤포레스는 여러 개의 의사결정 나무로 이루어진 앙상블 모델

  - 트리 기반 모델은 피처의 대소 관계를 중심으로 학습하기 때문에 스케일링에 크게 민감하지 않음
 
- n_estimators 설정으로 성능에 크게 변화가 있을 때 같은 결과라면 낮은 설정 선택

  - n_setimators 값이 크면 트리의 수가 많아져 연산 속도가 느려짐
 
- 데이터 전처리

  - 스케일링 : 성능 변화 X
 
- 하이퍼파라미터 튜닝

  - max_depth : 5, 7, 10
 
  - n_estimators : 200, 500

<BR>

|데이터 전처리/하이퍼파라미터 튜닝|f1|제출|
|-|-|-|
|베이스라인|0.6119801766860591|선택 / 1차 제출|
|스케일링(Standard, Min-Max, Robust)|0.6119801766860591||
|max_depth = 5|0.6410714285714286|선택|
|max_depth = 7|0.6119801766860591||
|max_depth = 10|0.6119801766860591||
|max_depth = 5, n_estimators = 200|0.6507936507936507|선택 / 2차 제출|
|max_depth = 5, n_estimators = 500|0.6507936507936507||

<br>

> 코드
```python
  # 2. 라이브러리 및 데이터 불러오기
  import pandas as pd
  
  train = pd.read_csv('./data/glass_train.csv')
  test =pd.read_csv('./data/glass_test.csv')
  
  # 4. 데이터 전처리
  target = train.pop('Type')
  
  # 스케일링 (효과 X)
  # from sklearn.preprocessing import StandardScaler
  # scaler = StandardScaler()
  # cols = train.columns
  # train[cols] = scaler.fit_transform(train[cols])
  # test[cols] = scaler.transform(test[cols])
  
  # 5. 검증 데이터 나누기
  from sklearn.model_selection import train_test_split
  X_train, X_val, y_train, y_val = train_test_split(train, target, test_size=0.2, random_state=0)
  
  # 6. 머신러닝 학습 및 평가
  from sklearn.ensemble import RandomForestClassifier
  rf = RandomForestClassifier(max_depth=5, n_estimators=200, random_state=0)
  rf.fit(X_train, y_train)
  pred = rf.predict(X_val)
  
  from sklearn.metrics import f1_score
  f1 = f1_score(y_val, pred, average='weighted')
  print('f1 :', f1)
  
  # 7. 예측 및 결과 파일 생성
  pred = rf.predict(test)
  submit = pd.DataFrame({'pred':pred})
  submit.to_csv('result3.csv', index=False)
  
  print('\n==== 제출 파일 (샘플 5개) ====')
  print(pd.read_csv('result3.csv').head())
```

> 결과
```python
  f1 : 0.6507936507936507
  
  ==== 제출 파일 (샘플 5개) ====
     pred
  0     1
  1     5
  2     5
  3     2
  4     2
```

<br>









