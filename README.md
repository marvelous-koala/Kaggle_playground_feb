# Kaggle_playground_feb
https://www.kaggle.com/c/tabular-playground-series-feb-2021


2021 Kaggle Tabular Set 2월
현재 진행 중.

EDA

분포에 관한 EDA 진행  
VIF 검정을 통한 연속형 범주의 다중공선성 확인 및 처리 (기준 VIF = 10)  
Seaborn Library를 통한 범주들의 시각화  

Feature Engineering  
카테고리별 T test, ANOVA 테스트, 유의미한 카테고리 유지, 유사한 카테고리 통합  
pairwise_tukeyhsd 테스트 진행 범주 통합  
IsolationForest 기법을 통한 이상치 제거/이상치 데이터 명시(카테고리 데이터 + IsolationForest Score)  

Machine Learning  

Optuna Library를 활용한 파라미터 최적화  
7가지 Regression Model 비교, XGBoost, LGBM, Catboost 3가지 부스팅 모델 선정  
단일 모델, 3가지 앙상블 모델, Stacking 모델을 생성하여 비교 중.  
