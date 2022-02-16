<h1 align="center" style="display: block; font-size: 2em; font-weight: bold; margin-block-start: 1em; margin-block-end: 1em;">
<img align="center" src="https://user-images.githubusercontent.com/91931949/152942171-0033b5ac-62ec-48ec-adfe-fd9e0f20106a.png" style="width:100%;height:100%"/>

# 딥러닝을 활용한 네트워크 이상 탐지

## 📋 Introduction
- 최근, **네트워크 침입에 따른 사회적 피해**가 증가하고 있으며, 이러한 문제를 해결하고자 프로젝트를 수행합니다.
  - Ex. [고려대·중앙대 수강신청 디도스 공격 관련 기사](https://www.news1.kr/articles/?4032611)
  
- **네트워크 로그의 비정상 흐름(Anomaly Flow)를 탐지할 수 있는 AutoEncoder 모델을 제시합니다.**
  - 최근 새로운 유형의 네트워크 공격이 점점 증가하는 추세로, 모든 공격 유형에 라벨(Label)을 붙여 모델링하는 지도 학습(Supervised Learning)이 현실적으로 어려워지고 있습니다.
  - **TEAM SAMCM는 정상 데이터만을 활용한 반지도 학습(Semi-supervised)을 통해, 네트워크 침입을 탐지하는 오토인코더(AutoEncoder) 모델을 개발했습니다.**

<p align="center"><img src="https://user-images.githubusercontent.com/91931949/152934410-00ffff1d-bdfd-4151-8760-0537cc9f6d9d.png" width="800" height="300"/>

## 🎯 Result
- 우리의 최종 모델은 **TCP Protocol에서 Accuracy 0.7958, F1 Score 0.8627**의 성능을 보입니다.
 
|Threshold별 Score|Loss Comparison (Benign / Anomaly)|
|:------:|:------:|
|![image](https://user-images.githubusercontent.com/91931949/152935464-f7d01740-531f-4673-92b1-8ecfee8d5f3c.png)|![image](https://user-images.githubusercontent.com/91931949/152935770-5533e6b7-5d86-48e4-b1ea-a223dfef1298.png)|

## 🔎 Modeling
### 1. Dataset
- **Logs of the University of New Brunswick’s servers**
- '2018. 02. 14 - 03. 02', Wed, Thu, Fri(9일) 데이터
- 총 8,284,254건의 Flow Data, 80 Features

### 2. Library
- torch를 활용한 AutoEncoder를 설계·개발했습니다.
- 대용량 데이터 스케일링(Scaling)을 위해 dask_ml 라이브러리를 활용했습니다.
```
!pip install torch
!pip install dask_ml
```

### 3. Model setting
- **Base AE, Stacked AE, Denoising AE**로 분화하여 모델 성능을 확인했습니다.
<p align="center"><img src="https://user-images.githubusercontent.com/91931949/152937987-0eec667d-8fdc-4940-8f89-5d29e8be4319.png" width="600" height="280"/>

- 모든 모델에 공통적으로 아래 사항을 적용했습니다. 
```
  - Optimizer : Adam
  - Loss : MSE
  - Layer Activation Func : Relu
  - Output Activation Func : Sigmoid
  - Learning rate : 0.0008
```

- Test는 **정상 데이터의 Loss의 백분위수를 Threshold로 설정**하여 수행했습니다.


### 4. Score
- **Base AE**에서 가장 높은 Score 성과를 보이는 것을 알 수 있습니다.
<p align="center"><img src="https://user-images.githubusercontent.com/91931949/152938786-7de4d26c-268d-47b2-bc79-9e5df1a51a34.png" width="550" height="230"/>


## 📖 Reference
- Amer Abdulmajeed Abdulrahman & Mahmood Khalel Ibrahem. (2020). Toward Constructing a Balanced Intrusion Detection Dataset
- Chaitanya Buragohain & Manash Jyoti Kalita & Santosh Singh & Dhruba K. Bhattacharyya. (2015). Anomaly based DDoS Attack Detection. International Journal of Computer Applications (0975 – 8887) Volume 123 – No.17, August 2015
- Chongzhen Zhang & Yanli Chen & YangMeng & Fangming Ruan & Runze Chen & Yidan Li & Yaru Yang. (2021). A Novel Framework Design of Network Intrusion Detection. Hindawi Security and Communication Networks Volume 2021, p15
- Guansong Pang & Longbing Cao & Charu Aggarwal. (2021). Deep Learning for Anomaly Detection_ Challenges, Methods, and Opportunities
- Koohong Kang. (2020). Network Anomaly Detection Technologies Using Unsupervised Learning AutoEncoders. Journal of The Korea Institute of Information Security & Cryptology
- M Odusami & S Misra & E Adetiba & O Abayomi-Alli & R Damasevicius & R Ahuja. (2019). An Improved Model for Alleviating Layer Seven Distributed Denial of Service Intrusion On Webserver. The 3rd International Conference on Computing and Applied Informatics 2018
- Matthew Yung & Eli T. Brown & Alexander Rasin & Jacob D. Furst & Daniela S. Raicu. (2018). Synthetic Sampling for Multi-Class Malignancy Prediction. KDD MLMH'18, August 2018, London, United Kingdom
- Mohammed Gharib & Bahram Mohammadi & Shadi Hejareh Dastgerdi & Mohammad Sabokrou. (2019). AutoIDS_ Auto-encoder Based Method for Instrusion Detection System
- Byeoungjun Min & Jihoon Yoo & Sangsoo Kim & Dongil Shin & Dongkyoo Shin. (2021). Network Intrusion Detection with One Class Anomaly Detection Model based on Auto Encoder. Journal of Internet Computing and Services(JICS) 2021. Feb.: 22(1): 13-22
- Nicholas Bashour. (2021). Identifying Network Intrusions Using Deep Learning
- Raghavendra Chalapathy & Sanjay Chawla. (2019). DEEP LEARNING FOR ANOMALY DETECTION: A SURVEY
- Razan Abdulhammed & Hassan Musafer & Ali Alessa & Miad Faezipour & Abdelshakour Abuzneid. (2019). Features Dimensionality Reduction Approaches for Machine Learning Based Network Intrusion Detection. Electronics 2019. MPDI Journal
 
## :palms_up_together: Team Members
|Member|See more!|
|:--:|:--:|
|이민호 (Minho Lee)|<a href="mailto:minho5373@gmail.com"><img src="https://img.shields.io/badge/Mail-red?style=flat-sqaure&logo=Gmail&logoColor=ffffff"/></a> <a href="https://github.com/minho5373"><img src="https://img.shields.io/badge/Github-black?style=flat-sqaure&logo=GitHub&logoColor=ffffff"/></a> <a href="https://whimsical-argon-e67.notion.site/Minho-Lee-7fd5586ba1dc4ed5b30964f76adf6417"><img src="https://img.shields.io/badge/Notion-grey?style=flat-sqaure&logo=Notion&logoColor=ffffff"/></a> <a href="https://go-for-data.tistory.com/"><img src="https://img.shields.io/badge/Blog-green?style=flat-sqaure&logo=Storyblok&logoColor=ffffff"/></a>|
|이서영 (Seoyoung Lee)|<a href="mailto:cococindy98@gmail.com"><img src="https://img.shields.io/badge/Mail-red?style=flat-sqaure&logo=Gmail&logoColor=ffffff"/></a> <a href="https://github.com/cococindy98"><img src="https://img.shields.io/badge/Github-black?style=flat-sqaure&logo=GitHub&logoColor=ffffff"/></a> <a href="https://shaded-english-cde.notion.site/Seoyoung-Lee-6c8d2a44a3bd48dbb30256cbfa83c485"><img src="https://img.shields.io/badge/Notion-grey?style=flat-sqaure&logo=Notion&logoColor=ffffff"/></a> <a href="https://blog.naver.com/cococindy98"><img src="https://img.shields.io/badge/Blog-green?style=flat-sqaure&logo=Storyblok&logoColor=ffffff"/></a>|
|강승완 (Seungwan Kang)|<a href="mailto:sdubee10@gmail.com"><img src="https://img.shields.io/badge/Mail-red?style=flat-sqaure&logo=Gmail&logoColor=ffffff"/></a> <a href="https://github.com/sdubee10"><img src="https://img.shields.io/badge/Github-black?style=flat-sqaure&logo=GitHub&logoColor=ffffff"/></a> <a href="https://velog.io/@sdubee10"><img src="https://img.shields.io/badge/Blog-green?style=flat-sqaure&logo=Storyblok&logoColor=ffffff"/></a>|
