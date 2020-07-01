# Linear Models

<img width="406" alt="1" src="https://user-images.githubusercontent.com/43739827/86226136-2e202a00-bbc6-11ea-9792-e822f0274565.png"></img>  

<img width="613" alt="2" src="https://user-images.githubusercontent.com/43739827/86226145-30828400-bbc6-11ea-99e0-43b7b18a91e4.png"></img>  

## 정규방정식(Ordinary Least Squares)  

**LinearRegression** 은 데이터셋에서의 대상값(target value)과 선형 모델이 예측한 대상값 사이의 잔차제곱합(residual sum of squares)을 최소화시키는 모델이다.  

정규방정식의 예측 계수는 특징(feature)의 독립성에 의존한다. 만약 독립성을 가지지 못한다면 예측한 대상값에서 발생하는 임의의 에러에 매우 민감해지게된다.  
