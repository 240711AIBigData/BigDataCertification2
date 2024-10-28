# CAHPTER03 머신러닝 평가지표
- 주요 평가지표를 한두 개씩 학습, 문제에서 암기하지 못한 평가지표가 나올 때 알고 있는 평가지표로 검증 평가

- 대표적인 머신러닝 평가지표는 sklearn.metrics 라이브러리에 포함되어 있음

<br>

SECTION01 이진 분류 평가지표
---
- 이진 분류 평가지표 설명을 위한 데이터셋 생성

  - y_true 변수 : 실제 값
 
  - y_pred 변수 : 예측값
 
  - target 이 숫자가 아닌 문자일 수도 있으므로 y_true_str 과 y_pred_str 을 문자로 1은 A, 0은 B로 변경 

> 코드
```python
  # 이진 분류 데이터
  import pandas as pd
  y_true = pd.DataFrame([1, 1, 1, 0, 0, 1, 1, 1, 1, 0])   # 실제값
  y_pred = pd.DataFrame([1, 0, 1, 1, 0, 0, 0, 1, 1, 0])   # 예측값
  
  y_true_str = pd.DataFrame(['A', 'A', 'A', 'B', 'B', 'A', 'A', 'A', 'A', 'B'])   # 실제값
  y_pred_str = pd.DataFrame(['A', 'B', 'A', 'A', 'B', 'B', 'B', 'A', 'A', 'B'])   # 예측값
```

<br>

### 01. 정확도(Accuracy)
- 전체 데이터 중에서 올바르게 예측된 데이터의 비율

- 데이터가 불균형할 경우 정확도만으로는 충분한 평가 어려움

  - ex) 100명의 데이터 중 2명만 암환자라는 불균형한 상황
 
    - 모든 환자를 암이 아니라고 예측하면 98% 의 높은 정확도 보임

- 결과값은 1에 가까울수록 좋음

<br>

> 코드
```python
  # 정확도(Accuracy)
  from sklearn.metrics import accuracy_score
  accuracy = accuracy_score(y_true, y_pred)
  print('accuracy_score :', accuracy)
  
  accuracy = accuracy_score(y_true_str, y_pred_str)
  print('accuracy_score :', accuracy)
```

> 결과
```python
  accuracy_score : 0.6
  accuracy_score : 0.6
```
- 숫자나 문자의 형태에 따른 차이 없음

<br>

### 02. 정밀도(Precision)
- 양성으로 예측된 데이터 중 실제로 양성인 비율

  - 모델이 양성이라고 예측한 경우 중 얼마나 정확하게 예측했는지 평가하는 지표
 
- 문자 형태의 target 사용시 pos_label='A' 처럼 양성 클래스 명시 필요

  - 숫자인 경우 pos_label 사용 X
 
  - 여기서는 'A' 를 양성(1) 클래스로 설정
 
- 결과는 1에 가까울수록 좋음

<br>

> 코드
```python
  # 정밀도(Precision)
  from sklearn.metrics import precision_score
  precision = precision_score(y_true, y_pred)
  print('precision_score :', precision)
  
  precision = precision_score(y_true_str, y_pred_str, pos_label='A')
  print('precision_score :', precision)
```

> 결과
```python
  precision_score : 0.8
  precision_score : 0.8
```

<br>

### 03. 재현율(Recall)
- 실제 양성인 데이터 중 모델이 양성으로 올바르게 예측한 비율

  - 모델이 실제 양성인 데이터를 얼마나 잘 감지하는지 측정
 
- 문자 형태의 경우 양성 클래스 지정 필요

- 결과는 1에 가까울수록 좋음

<br>

> 코드
```python
  # 재현율(Recall)
  from sklearn.metrics import recall_score
  recall = recall_score(y_true, y_pred)
  print('recall_score :', recall)
  
  recall = recall_score(y_true_str, y_pred_str, pos_label='A')
  print('recall_score :', recall)
```

> 결과
```python
  recall_score : 0.5714285714285714
  recall_score : 0.5714285714285714
```

<br>

### 04. F1 스코어(F1 Score)
- 정밀도와 재현율의 조화 평균

- 불균형 데이터를 평가하는 데 유용

- 문자 형태의 경우 양성(1) 클래스 지정 필요

- 결과는 1에 가까울수록 좋음

<br>

> 코드
```python
  # F1 스코어(F1 Score)
  from sklearn.metrics import f1_score
  f1 = f1_score(y_true, y_pred)
  print('f1_score :', f1)
  
  f1 = f1_score(y_true_str, y_pred_str, pos_label='A')
  print('f1_score :', f1)
```

> 결과
```python
  f1_score : 0.6666666666666666
  f1_score : 0.6666666666666666
```

<br>

### 05. ROC-AUC
- AUC(Area Under the Curve) : ROC 곡선(Receiver Operating Characteristic Curve) 아래 영역

- 모델의 분류 성능을 평가하는 지표

- 양성 클래스(일반적으로 '1'로 표시되는 관심 대상 클래스)에 속할 확률을 예측하기 위해 모델에 predict_proba() 사용

  - predict_proba() : 각 클래스에 속할 확률 반환
 
    - 양성 클래스에 대한 확률을 분석하기 위해 반환된 배열의 두 번째 열(pred[:, 1])의 값 사용
   
    - 이 확률값은 ROC-AUC 계산에 사용됨
   
- ROC-AUC 값이 1에 가까울수록 모델의 성능이 우수함을 의미

<br>

> 코드
```python
  # ROC-AUC
  from sklearn.metrics import roc_auc_score
  
  # 실제값(0: 음석, 1: 양성)
  y_true = pd.DataFrame([0, 1, 0, 1, 1, 0, 0, 0, 1, 1])
  # 예측값 중 양성(1) 확률
  y_pred_proba = pd.DataFrame([0.4, 0.9, 0.1, 0.3, 0.8, 0.6, 0.4, 0.2, 0.7, 0.6])
  
  roc_auc = roc_auc_score(y_true, y_pred_proba)
  print('ROC-AUC :', roc_auc)
```

> 결과
```python
  ROC-AUC : 0.86
```

<br>

- 문자 형태의 타깃 값에 대해서도 ROC-AUC 계산 방식은 변경되지 않음

- y_pred_proba_str 은 B 클래스에 대한 확률로 이를 기반으로 ROC-AUC 점수가 계산됨

- roc_auc_score에서 "positive" 클래스는 알파벳 순서에 따라 결정

  - "A"와 "B"가 있을 때 "B"가 양성(positive)으로 간주
 
  - "B"일 확률이 예측 확률로 주어져야 roc_auc_score이 올바르게 계산

> 코드
```python
  # 실제값
  y_true_str = pd.DataFrame(['A', 'B', 'A', 'B', 'B', 'A', 'A', 'A', 'B', 'B'])
  # 예측값 중 B 확률
  y_pred_proba_str = pd.DataFrame([0.4, 0.9, 0.1, 0.3, 0.8, 0.6, 0.4, 0.2, 0.7, 0.6])
  
  roc_auc = roc_auc_score(y_true_str, y_pred_proba_str)
  print('ROC-AUC :', roc_auc)
```

> 결과
```python
  ROC-AUC : 0.86
```

<br>

---

<br>

SECTION02 다중 분류 평가지표
---
- 이진 분류 평가지표와 유사
  
- 다중 분류로 평가하기 위해 정밀도, 재현율, F1 스코어는 평균을 계산하는 방식(파라미터) 필요

  - Macro 평균(Macro-average) : 각 클래스에 대한 정밀도/재현율/F1 점수의 평균 계산
 
  - Micro 평균(Micro-average) : 모든 클래스에 대한 전체적인 정밀도/재현율/F1 점수 계산
 
  - Weighted 평균(Weighted-average) : 각 클래스에 대한 정밀도/재현율/F1 점수의 가중 평균 계산
 
- 세 가지 클래스(종류)가 있는 다중 분류 데이터 생성

  - 다중 분류는 3개 이상의 클래스(종류) 의미
 
  - 숫자와 문자 형태로 인한 코딩에서의 차이 없음

> 코드
```python
  # 다중 분류 데이터
  y_true = pd.DataFrame([1, 2, 3, 3, 2, 1, 3, 3, 2, 1])   # 실제값
  y_pred = pd.DataFrame([1, 2, 1, 3, 2, 1, 1, 2, 2, 1])   # 예측값
  
  y_true_str = pd.DataFrame(['A', 'B', 'C', 'C', 'B', 'A', 'C', 'C', 'B', 'A'])   # 실제값
  y_pred_str = pd.DataFrame(['A', 'B', 'A', 'C', 'B', 'A', 'A', 'B', 'B', 'A'])   # 예측값
```

<br>

### 01. 정확도(Accuracy)
- 다중 분류에서 정확도의 평가 방법은 이진 분류와 같음

> 코드
```python
  # 정확도(Accuracy)
  from sklearn.metrics import accuracy_score
  accuracy = accuracy_score(y_true, y_pred)
  print('정확도 :', accuracy)
  
  accuracy = accuracy_score(y_true_str, y_pred_str)
  print('정확도 :', accuracy)
```

> 결과
```python
  정확도 : 0.7
  정확도 : 0.7
```

<br>

### 02. 정밀도(Precision)
- average 는 micro, macro, weighted 중 문제에서 요구하는 방식 선택

<br>

> 코드
```python
  # 정밀도(Precision)
  from sklearn.metrics import precision_score
  precision = precision_score(y_true, y_pred, average='macro')    # average = micro, macro, weighted
  print('정밀도 :', precision)
  
  precision = precision_score(y_true_str, y_pred_str, average='macro')
  print('정밀도 :', precision)
```

> 결과
```python
  정밀도 : 0.7833333333333333
  정밀도 : 0.7833333333333333
```

<br>

### 03. 재현율(Recall)

> 코드
```python
  # 재현율(Recall)
  from sklearn.metrics import recall_score
  recall = recall_score(y_true, y_pred, average='macro')      # average = micro, macro, weighted
  print('재현율 :', recall)
  
  recall = recall_score(y_true_str, y_pred_str, average='macro')
  print('재현율 :', recall)
```

> 결과
```python
  재현율 : 0.75
  재현율 : 0.75
```

<br>

### 04. F1 스코어(F1 Score)

> 코드
```python
  # F1 스코어(F1 Score)
  from sklearn.metrics import f1_score
  f1 = f1_score(y_true, y_pred, average='macro')      # average = micro, macro, weighted
  print('F1 스코어 :', f1)
  
  f1 = f1_score(y_true_str, y_pred_str, average='macro')
  print('F1 스코어 :', f1)
```

> 결과
```python
  F1 스코어 : 0.669047619047619
  F1 스코어 : 0.669047619047619
```

<br>

---

<br>

SECTION03 회귀 평가지표
---
- 대부분 오차 측정

  - 오차는 작을수록 좋음 = 0에 가까울수록 성능이 좋은 모델
 
  - 결정 계수(R-squared)만 유일하게 높을수록(1에 가까울수록) 좋음
 
- 회귀 평가지표를 위한 데이터 생성

  - 예측값은 일반적으로 소수값을 포함헤 예측됨
 
> 코드
```python
  # 회귀 데이터
  import pandas as pd
  y_true = pd.DataFrame([1, 2, 5, 2, 4, 4, 7, 9])     # 실제값
  y_pred = pd.DataFrame([1.14, 2.53, 4.87, 3.08, 4.21, 5.53, 7.51, 10.32])    # 예측값
```

<br>

### 01. MSE(Mean Squared Error)
- 실제값과 에측값의 차이를 제곱해 평균한 값

  - 큰 오차에 대해 가중치 부여

> 코드
```python
  # MSE(Mean Squared Error)
  from sklearn.metrics import mean_squared_error
  mse = mean_squared_error(y_true, y_pred)
  print('MSE :', mse)
```

> 결과
```python
  MSE : 0.7339125000000001
```

<br>

### 02. MAE(Mean Absolute Error)
- 실제값과 예측값의 차이를 절대값으로 계산하고 평균한 값

> 코드
```python
  # MAE(Mean Absolute Error)
  from sklearn.metrics import mean_absolute_error
  mae = mean_absolute_error(y_true, y_pred)
  print('MAE :', mae)
```

> 결과
```python
  MAE : 0.68125
```

<br>

### 03. 결정 계수(R-squared)
- 회귀식이 얼마나 잘 예측(설명)하는지 나타내는 지표 = R²

> 코드
```python
  # 결정 계수(R-squared)
  from sklearn.metrics import r2_score
  r2 = r2_score(y_true, y_pred)
  print('결정 계수 :', r2)
```

> 결과
```python
  결정 계수 : 0.8859941747572815
```

<br>

### 04. RMSE(Root Mean Squared Error)
- 실제값과 예측값의 차이를 제곱해 평균을 낸 MSE 에 제곱근을 적용한 값

- 큰 오차에 대해 가중치 부여

> 코드
```python
  # RMSE(Root Mean Squared Error)
  from sklearn.metrics import mean_squared_error
  mse = mean_squared_error(y_true, y_pred)
  rmse = mse ** 0.5       # 또는 mean_squared_error(y_true, y_pred, squared=False)
  print('RMSE :', rmse)
```

> 결과
```python
  RMSE : 0.8566869323154171
```

<br>

### 05. MSLE(Mean Squared Log Error)
- 실제값과 예측값의 로그를 취한 후 차이를 제곱해 평균한 값

- 작은 오차에 더 큰 가중치 부여

> 코드
```python
  # MSLE(Mean Squared Log Error)
  from sklearn.metrics import mean_squared_log_error
  msle = mean_squared_log_error(y_true, y_pred)
  print('MSLE :', msle)
```

> 결과
```python
  MSLE : 0.027278486182156947
```

<br>

### 06. RMSLE(Root Mean Squared Log Error)
- 실제값과 예측값의 로그를 취한 후 차이를 제곱해 평균한 값의 제곱근으로 계산한 값

- 작은 오차에 더 큰 가중치 부여

> 코드
```python
  # RMSLE(Root Mean Squared Log Error)
  from sklearn.metrics import mean_squared_log_error
  rmsle = mean_squared_log_error(y_true, y_pred) ** 0.5
  print('RMSLE :', rmsle)
```

> 결과
```python
  RMSLE : 0.16516199981278062
```

<br>

### 07. MAPE(Mean Absolute Percentage Error)
- 예측값과 실제값 사이의 오차를 백분율로 나타낸 지표

- 예측값(y_pred)이 실제값(y_true)에 얼마나 가까운지를 백분율로 나타내며, MAPE가 낮을수록 예측이 실제에 가까움

> 코드
```python
  # MAPE(Mean Absolute Percentage Error)
  mape = (abs((y_true - y_pred) / y_true)).mean() * 100
  print('MAPE :', mape)
```
- 예측 오차의 절대값을 계산하고 실제값으로 나눔

  - abs(y_true - y_pred) : 실제값과 예측값 간의 차이의 절대값을 계산
 
  - (y_true - y_pred) / y_true : 예측 오차를 실제값으로 나눈 비율을 계산
 
  - abs((y_true - y_pred) / y_true) : 오차 비율의 절대값을 구함
 
- 계산된 MAPE를 백분율로 표시하기 위해 100을 곱함

  - .mean() : 각 데이터 포인트에 대해 계산된 절대 오차 비율의 평균을 구함
 
  - 결과적으로 MAPE는 평균 절대 퍼센트 오차(%)를 나타내는 값이 됨

> 결과
```python
  MAPE : 0    20.319048
  dtype: float64
```

<br>

#### 💡 MAPE 사용할 때 분모에 0 이 있으면?
- 실제값 중에 0이 있다면 계산 불가능

  - 매우 작은 값을 더해 0이 되는 것을 방지하기도 함
 
    - 실제 오차에는 큰 영향 X

> 코드
```python
  epsilon = 1e-10
  mape = (abs((y_true - y_pred) / (y_true + epsilon))).mean() * 100
  print('MAPE :', mape)
```

> 결과
```python
  MAPE : 0    20.319048
  dtype: float64
```

<br>

#### 💡 평가지표를 보고 분류 or 회귀인지 알 수 있음
- 회귀 평가지표에는 R²(결정 계수) 제외하고 Error(오차) 계산하는 단어가 포함되어 있음

<br>
