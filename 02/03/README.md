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

- 문자 형태의 타깃 값에 대해서도 ROC-AUC 계싼 방식은 변경되지 않음

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



<br>

---

<br>

SECTION03 회귀 평가지표
---



<br>
