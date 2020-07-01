# Linear Models

<img width="406" alt="1" src="https://user-images.githubusercontent.com/43739827/86226136-2e202a00-bbc6-11ea-9792-e822f0274565.png"></img>  

<img width="613" alt="2" src="https://user-images.githubusercontent.com/43739827/86226145-30828400-bbc6-11ea-99e0-43b7b18a91e4.png"></img>  

## 정규방정식(Ordinary Least Squares)  

**LinearRegression** 은 데이터셋에서의 대상값(target value)과 선형 모델이 예측한 대상값 사이의 잔차제곱합(residual sum of squares)을 최소화시키는 모델이다.  

정규방정식의 예측 계수는 특징(feature)의 독립성에 의존한다. 만약 독립성을 가지지 못한다면 예측한 대상값에서 발생하는 임의의 에러에 매우 민감해지게된다.  

## Ridge regression and classification  

### Regression  

**Ridge** 회귀는 정규방정식에서 발생하는 계수의 크기를 구하는 데 발생하는 문제들을 다루기위해 사용되었다.  

ridge 계수는 잔차제곱합의 결점을 최소화한다.  

<img width="195" alt="1" src="https://user-images.githubusercontent.com/43739827/86231277-447db400-bbcd-11ea-96e9-9934b53a565e.png"></img>  

복잡도를 나타내는 매개변수 α가 0이상이면 수축량을 조절한다. α가 클수록 수축량은 커지고 이로인해 계수는 다중공선성(collinearity)에 더 강해진다.  

### Classification  
