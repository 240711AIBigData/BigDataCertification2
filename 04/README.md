# INDEX

|No|Title|Link|
|-|-|-|
|01|예시문제|[바로가기](./01)|
|02|기출 2회|[바로가기](./02)|
|03|기출 3회|[바로가기](./03)|
|04|기출 4회|[바로가기](./04)|
|05|기출 5회|[바로가기](./05)|
|06|기출 6회|[바로가기](./06)|
|07|기출 7회|[바로가기](./07)|
|08|기출 8회|[바로가기](./08)|

<br>

---

<br>

#### 💡 Statsmodels 로지스틱 회귀 주요 속성 및 메서드

|속성/메서드|설명|
|:-:|-|
|model.params|회귀 계수 (Coefficients)|
|model.pvalues|각 독립변수에 대한 p-value|
|model.summary()|모델의 요약 결과표 (Coefficients, Pseudo R-squared 등 포함)|
|model.llf|모델의 로그-우도 (Log-Likelihood of the fitted model)|
|model.llnull|Null 모델의 로그-우도|
|model.bic|Bayesian Information Criterion (BIC)|
|model.aic|Akaike Information Criterion (AIC)|
|model.df_model|사용된 독립변수의 개수|
|model.df_resid|자유도 잔차 (Residual degrees of freedom)|
|model.pred_table()|Confusion Matrix (예측 vs 실제값)|
|model.fittedvalues|학습 데이터에 대한 예측값 (확률)|
|model.resid_dev|잔차 이탈도 (Deviance Residuals)|
|model.bse|회귀 계수의 표준 오차 (Standard Errors)|

<br>

---

<br>

#### 💡 Statsmodels 선형 회귀 주요 속성 및 메서드

|속성/메서드|설명|
|:-:|-|
|model.params|회귀 계수 (Coefficients)|
|model.pvalues|각 독립변수에 대한 p-value|
|model.rsquared|결정 계수 (R-squared, 모델 적합도)|
|model.rsquared_adj|조정된 결정 계수 (Adjusted R-squared)|
|model.summary()|모델 요약 결과표 (Coefficients, R-squared 등 포함)|
|model.fvalue|F-statistic 값 (모델 전체 유의성 테스트)|
|model.f_pvalue|F-statistic에 대한 p-value|
|model.aic|Akaike Information Criterion (AIC)|
|model.bic|Bayesian Information Criterion (BIC)|
|model.resid|잔차 (Residuals)|
|model.fittedvalues|학습 데이터에 대한 예측값|
|model.predict()|새로운 데이터에 대한 예측|

<br>
