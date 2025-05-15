# 🏭 LG전자 제조 공정 불량률 예측
[대회 참고](https://lgaimers.ai/)

## 📌 **공모전/해커톤 개요**

**해결 과제 :** 차량용 디스플레이 제조 과정에서 발생하는 불량을 AI 기반으로 예측하고 판별하는 모델 개발 및 F1-score 고도화

---
## 📣 **공모전/해커톤 정보**

- **대회명 :** LG aimers 해커톤 5기
- **주최기관 :** LG전자
- **진행기간 :** 2024.08.01 - 2024.07.30 (온라인 해커톤), 2024.09.28 - 2024.09.29 (오프라인 해커톤) [증빙 자료](https://drive.google.com/file/d/1DwP5RrFkj08uo15XFSiLvgPH5AGv61uZ/view?usp=sharing)
- **수상 :** 온라인 해커톤 4th / 741teams, 오프라인 해커톤 9th / 32teams (상금 100만원)

---
## 📊 **프로젝트 개요**
- **사용된 데이터셋 :** 차량용 디스플레이 제조 공정 중 Sub Assembly Line(부품 조합 라인)에서 수집된 데이터로, 학습용 데이터 40,506건 (469개 변수), 테스트 데이터 17,361건 (468개 변수)으로 구성

- **데이터 수집 과정 :** 데이터는 Resin 도포 및 반경화, 탈포 과정에서 수집된 데이터

- **과제 정의 :** 최종 생산된 디스플레이가 Normal인지 Abnormal인지 Binary Classification을 수행

- **핵심 목표 :**
  - 제조 공정 중 불량 발생 여부를 사전에 예측할 수 있는 AI 모델을 개발
  - 심각하게 불균형한 타깃 클래스 문제를 해결하기 위한 불균형 처리 전략 적용 필요

---
## ✅ **기법 및 기술 스택 요약**
- **사용한 주요 기법 :** 최종 모델은 6개의 CatBoost 모델을 Soft Voting 방식으로 앙상블

- **추가로 시도한 알고리즘 :** 다양한 모델 간 성능 비교를 위해 ExtraTrees, XGBoost, SVM, Penalized Logistic Regression 등도 비교

- **사용한 기술 및 라이브러리 :**

  - **프로그래밍 언어 :** <img src="https://img.shields.io/badge/Python-3776AB?style=flat&logo=Python&logoColor=white"/>

  - **데이터 처리 및 분석 :** ![pandas](https://img.shields.io/badge/pandas-150458?style=flat&logo=pandas&logoColor=white), ![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)

  - **머신러닝 모델링 :** ![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white), ![XGBoost](https://img.shields.io/badge/XGBoost-0072C6?style=flat&logo=xgboost&logoColor=white), ![CatBoost](https://img.shields.io/badge/CatBoost-EEB211?style=flat)

  - **모델 평가 지표 :** F1-score (불균형 데이터 대응을 위한 주요 지표로 활용)


---
## ⚙️ **분석 과정**
#### 1️⃣ **데이터 전처리**
1. Raw 데이터 확인 과정에서 일부 열이 밀려 있는 문제가 발견되어, 정렬 오류를 수정하는 전처리를 우선적으로 수행

2. 결측치 확인 및 제거를 통해 불완전한 데이터를 제거하고, EDA를 통해 주요 변수 간 분포와 상관관계를 분석한 뒤, 유의미한 파생 변수를 도출

3. 제조 데이터는 수치처럼 보이는 값이라도 의미상 범주형인 경우가 많아 특정 변수 범주형으로 처리

#### 2️⃣ **모델 학습 및 튜닝**
1. ExtraTree, SVM, XGBoost, CatBoost 등 여러 머신러닝 모델을 실험적으로 적용하고, 그 중 가장 우수한 성능을 보인 CatBoost를 중심으로 본격적인 모델링을 진행

2. CatBoost의 cat_features 파라미터를 활용해 범주형 변수 인코딩을 최적화하였고, Optuna를 활용해 하이퍼파라미터 튜닝을 자동화

3. F1-score를 최종 평가 지표로 설정하되, 불균형 데이터 특성을 고려해 Accuracy, Precision, Recall도 함께 검토하며 모델을 평가

4. 클래스 간 불균형을 보완하기 위해 class_weights 조정을 통해 모델의 민감도를 향상

5. 다양한 seed에서의 성능 안정성을 확보를 위해 train-validation split seed를 바꿔가며 실험, K-Fold Cross Validation을 통해 Robust한 모델 성능을 확인

6. 최종적으로 6개의 CatBoost 모델을 Soft Voting 방식으로 앙상블하여, 과적합을 방지하면서도 예측 성능이 안정적인 최종 모델을 완성

---

### 📈 최종 모델 성능 (F1-score)

| 모델                             | Public | Private |
|----------------------------------|--------|---------|
| (Online) CatBoost Ensemble Model | 0.2377 | 0.2609  |
| (Offline) CatBoost Ensemble Model| 0.2847 | 0.2972  |

---

## 💡 **분석 의의**
- 데이터가 밀리는 등 실제 현업에서 사용되는 데이터에 발생할 수 있는 문제점을 경험하고 이를 해결
- 불균형이 심한 데이터를 핸들링
- 과적합을 막고 robust한 모델을 구축

---
## 오프라인 해커톤 사진
[대회 기사](https://n.news.naver.com/article/003/0012809958?sid=101)
