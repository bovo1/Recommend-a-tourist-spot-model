# 여행지 추천 모델
각 지역의 여행 로그 데이터를 이용하여 사용자가 좋아할 만한 여행지를 추천하는 모델을 개발했습니다.

## 데이터
데이터는 AI허브의 국내 여행 로그 데이터를 사용했습니다.  
https://www.aihub.or.kr/aihubdata/data/list.do?searchKeyword=%EC%97%AC%ED%96%89%EB%A1%9C%EA%B7%B8  

수도권, 동부권, 서부권, 제주도 및 도서지역을 합쳐 13,6806 개의 데이터입니다.  
이 데이터에서 집, 친구집, 사무실 등과 같이 여행지로서 적절하지 않은 데이터와 NULL 데이터를 삭제하여 결과적으로 84,165개의 데이터를 사용했습니다.  

### 데이터 구조도(ERD)
![36ef970d172040699271937b73aeecef](https://github.com/bovo1/-/assets/110110403/4369845e-1764-4d1a-8d2d-a78e84592e1e)

## 학습 모델 선정 기준
국내 여행 로그 데이터인 Input이 존재하고 Output은 선호도입니다.  
이러한 이유로 딥러닝 기반 모델을 사용하지 않고 회귀모델을 사용했습니다.  
회귀모델 Light GBM, XGboost, Catboost 중에서 Catboost를 선정한 이유는 다음과 같습니다.  

1. 데이터의 대부분이 범주형 데이터
2. Catboost는 범주형 데이터가 많을 때 학습 성능이 좋으며 Response encoding과 Categorical Feature Combination 방법이 범주형 데이터를 효율적으로 처리할 수 있습니다.
3. 다른 모델에 비해 속도가 매우 빠릅니다.

## 성능
84,165 개의 데이터  
### 서비스화를 한다고 가정했을 때 사용자가 제공해줄 수 있는 데이터를 골라 데이터 프레임을 만들었습니다.
   
    'GENDER',  
    'AGE_GRP',  
    'TRAVEL_COMPANIONS_NUM',   
    'TRAVEL_TERM',  
    'TRAVEL_PURPOSE',  
    'INCOME',  
    'TRAVEL_LIKE_SIDO_1','TRAVEL_LIKE_SIDO_2',  
    'TRAVEL_STYL_1', 'TRAVEL_STYL_2', 'TRAVEL_STYL_3', 'TRAVEL_STYL_4', 'TRAVEL_STYL_5', 'TRAVEL_STYL_6', 'TRAVEL_STYL_7', 'TRAVEL_STYL_8',  
    'TRAVEL_MOTIVE_1', 'TRAVEL_MOTIVE_2',  

이런 데이터를 Input 하여 사용자에게 추천할 수 있는 선호도가 높은 여행지를 Output 으로 출력합니다.  

![image](https://github.com/bovo1/-/assets/110110403/591a4f4b-a19d-42d8-a0ce-76a62f0ee683)  

이렇게 모델을 학습하였을 때 모델의 성능은 다음과 같습니다.  
학습 시간은 21분 36초 걸렸습니다.  
![image](https://github.com/bovo1/-/assets/110110403/f755476b-f40b-493f-933d-c7e02fdac5fb)  

보통의 머신 러닝에서 쓰이는 데이터 양보다 적다 보니 시간은 적게 걸리나 정확도는 중간 정도의 등급인 것 같습니다.  


#### 모델 사용 예시  
--
INPUT  
![image](https://github.com/bovo1/-/assets/110110403/2c7cae0a-ef86-4241-abfe-bc4942d8c4cc)  
OUTPUT  
![image](https://github.com/bovo1/-/assets/110110403/ea8d31ba-7083-4fb4-9bb2-27820c75b024)  



   

