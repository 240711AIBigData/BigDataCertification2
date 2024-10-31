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



<BR>

---

<BR>

SECTION03 유리 종류 예측
---




<BR>











