# BicycleRentalPrediction

*데이콘(DACON) 따릉이 대여량 예측 경진대회*

*기간 : 2021.11.01 ~ 2021.11.12 17:59*

## 1. 데이터 불러오기

![image](https://user-images.githubusercontent.com/87981867/140029711-bd6b4bf2-d83c-4566-a682-d408f632ddbc.png)

- train.csv : 학습 데이터

- test.csv : 테스트 데이터

- sample_submission.csv : 제출 양식

![image](https://user-images.githubusercontent.com/87981867/140029893-41a347e2-2347-4934-8648-1c2e1f46b7d3.png)

## 2. 변수 탐색

number_of_rentals : 따릉이 대여량(Y값), date_time : 날짜, wind_direction : 풍향

sky_condition : 하늘 상태(1 : 맑음, 3 : 구름 많음, 4 : 흐림, 하루에 8번 측정한 값 평균)

precipitation_form : 강수 형태(0 : 맑음, 1 : 비, 마찬가지로 하루에 8번 측정한 값 평균)

wind_speed : 풍속, humidity : 습도, low_temp : 최저기온, high_temp : 최고기온, precipitation_Probability : 강수확률

결측값 없음

### (1) 이상치 확인

![image](https://user-images.githubusercontent.com/87981867/140032049-d6570ab3-590b-43ab-8a3d-762d5107aadc.png)

이상치는 없는 것으로 보임

### (2) 유의미하지 않는 변수

![image](https://user-images.githubusercontent.com/87981867/140031749-33fb6801-9fad-4445-a7ff-3f05420af8a6.png)

wind_direction 풍향 변수 확인

풍향은 자전거 대여에 유의미한 변수가 아니라고 판단

![image](https://user-images.githubusercontent.com/87981867/140030550-a857dccf-1828-440e-a987-876eeca2be97.png)

![image](https://user-images.githubusercontent.com/87981867/140030601-6c31ccc7-6ac0-49a6-8c2b-2a27645168cb.png)

비가 오는 상황을 예측하는 두 변수 precipitation_form와 Precipitation_Probability간 상관관계는 높음

다만 Precipitation_Probability는 강우 확률 예측 변수

때문에 일일 강우 단기예측 기록인 precipitation_form 변수가 하루 비가 오는 날을 더 잘 표현

비슷한 부분을 설명하는 두 변수이기 때문에 precipitation_form 변수만 사용

precipitation_form 변수는 하늘 상태를 나타내는 sky_condition 변수와도 상관관계가 높지만 극단적이지 않음

날씨가 흐린것 자체가 따릉이 대여량에 부정적인 영향을 받는다 생각하기 때문에 sky_condition 변수는 사용

![image](https://user-images.githubusercontent.com/87981867/140031832-dcf196b6-a768-4436-8c3b-4f1ac43c1619.png)

연도별 따릉이 이용자수

시간이 지날수록 이용자수가 증가하는 것을 보아 연도 변수는 매우 중요

![image](https://user-images.githubusercontent.com/87981867/140031893-ccda909b-c6a0-4d7a-973f-c023cba1e60a.png)

요일별 따릉이 이용자수를 나타내는 그래프 (weekday 변수는 0은 월요일, 6은 일요일을 나타내는 요일 변수)

직관적으로 확인했을때 일요일에 따릉이 이용자수가 유의미하게 적음

![image](https://user-images.githubusercontent.com/87981867/140030977-af9e1b82-cd4f-4e90-a55d-429a8e61efd4.png)

유의미하지 않는 변수들 제거

## 3. 모델 적합

![image](https://user-images.githubusercontent.com/87981867/140031091-63d44f6e-d73e-42e1-b469-0707858d409f.png)

랜덤포레스트 모델을 사용하여 적합 후 따릉이 대여량 예측

대회 결과 : 0.5989161781(110등/597명 참여)

