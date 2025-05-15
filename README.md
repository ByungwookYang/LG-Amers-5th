# 🏭 LG전자 제조 공정 불량률 예측
[대회 참고](https://lgaimers.ai/)

## 📌 **공모전/해커톤 개요**

**해결 과제 :** 차량용 디스플레이 제조 과정에서 발생하는 불량을 AI 기반으로 예측하고 판별하는 모델 개발 및 F1-score 고도화

---
## 📣 **공모전/해커톤 정보**

- **대회명 :** LG aimers 해커톤 5기
- **주최기관 :** LG전자
- **진행기간 :** 2024.08.01 - 2024.07.30 (온라인 해커톤), 2024.09.28 - 2024.09.29 (오프라인 해커톤)
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

## ⚙️ **구현 과정**
