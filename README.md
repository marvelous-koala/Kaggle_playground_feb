# Kaggle_playground_feb
https://www.kaggle.com/c/tabular-playground-series-feb-2021


2021 Kaggle Tabular Set 2월
현재 진행 중.

EDA

분포에 관한 EDA 진행  
![image](https://user-images.githubusercontent.com/76254564/107871933-6c662180-6ee9-11eb-91f7-e7b744a9066e.png)  
VIF 검정을 통한 연속형 범주의 다중공선성 확인 및 처리 (기준 VIF = 10)  
![image](https://user-images.githubusercontent.com/76254564/107871954-9ddeed00-6ee9-11eb-977d-871f71aa74d3.png)  
Seaborn Library를 통한 범주들의 시각화  
![image](https://user-images.githubusercontent.com/76254564/107871939-8273e200-6ee9-11eb-9393-d8f0bc51d4d0.png)  


Feature Engineering  
카테고리별 T test, ANOVA 테스트, 유의미한 카테고리 유지, 유사한 카테고리 통합  
![image](https://user-images.githubusercontent.com/76254564/107871950-97e90c00-6ee9-11eb-9f08-f1b8603d4581.png)  
pairwise_tukeyhsd 테스트 진행 범주 통합  
![image](https://user-images.githubusercontent.com/76254564/107871945-8dc70d80-6ee9-11eb-9b8c-7bc67298d03c.png)  
IsolationForest 기법을 통한 이상치 제거/이상치 데이터 명시(카테고리 데이터 + IsolationForest Score)  

Machine Learning  

2월 15일 ~

Optuna Library를 활용한 파라미터 최적화  
7가지 Regression Model 비교, XGBoost, LGBM, Catboost 3가지 부스팅 모델 선정  
단일 모델, 3가지 앙상블 모델, Stacking 모델을 생성하여 비교 중.  

## 2월 22일~~
Kaggle Notebook에 올라온 코드를 활용 할 예정
### 1번 코드
### https://www.kaggle.com/awwalmalhi/extreme-fine-tuning-lgbm-using-7-step-training

특징_ 일단 정한 파라미터로 모델을 train 시키고, 여기에 과적합 규제(L2 규제와 num_leaves, cat_smooth 등)를 완화시켜서 재학습시킴
# 재학습이라는 아이디어로 점수를 많이 올린 듯
### 처음 학습(과적합 규제) - 재학습(규제 완화) -재학습2(좀 더 완화) ---
##### 요런 코드를 사용 함 (0.9로 규제를 완화)

        for i in range(1, 8):
            if i >2:    
            params['reg_lambda'] *= 0.9
            params['reg_alpha'] *= 0.9
            params['num_leaves'] += 40
        
### 2번 코드
### https://www.kaggle.com/craigmthomas/tps-feb-2021-lgb-xgb-combo

특징_ 간단한 앙상블 기법, XGB 파라미터를 어느 정도 정리해서 올려주었음

여기서 파라미터를 가져오던지, 다시 optuna로 최적화를 하던지 해서

XGB도 1번 LGBM의 방식으로 학습시키면 어떨까(학습/재학습) 생각 중

그래서 1번과 2번을 앙상블

(앙상블 비율 산출은 2번 코드에 Find best combo )


## 2월 27일 ~~
### Comparison Method 응용
### https://www.kaggle.com/somayyehgholami/comparative-method-tabular-feb-301

#### 20개의 submission set을 앙상블하는 아이디어
#### 비율만큼 추가하는 방식으로 진행

        def generate(main, support, coeff):

            g = main.copy()    
            for i in main.columns[1:]:

                res = []
                lm, Is = [], []        
                lm = main[i].tolist()
                ls = support[i].tolist()  

                for j in range(len(main)):
                    res.append((lm[j] * coeff) + (ls[j] * (1.- coeff)))            
                g[i] = res

            return g
            
#### 이후 Compare 기법도 사용(다른 n개의 자료에 비해 최종 제출본의 자료가 큰가 / 작은가 - 경우에 따라 후처리 추가 진행)
#### 앞의 1번 코드와 2번 코드를 활용하고 EDA로 정리한 Trainset을 가지고 스스로의 제출본 완성(LB score_0.8420)
#### 본인의 제출본을 3번의 Comparison 기법 Dataset에 추가하여 최종 25개의 Submission을 가지고 앙상블, 비교기법 시도

#### 상위 3%로 경진대회 마무리

![image](https://user-images.githubusercontent.com/76254564/109543745-0644e580-7b0a-11eb-82ad-296f37143980.png)
