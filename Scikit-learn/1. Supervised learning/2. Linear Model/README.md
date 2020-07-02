# Linear Models

<img width="406" alt="1" src="https://user-images.githubusercontent.com/43739827/86226136-2e202a00-bbc6-11ea-9792-e822f0274565.png"></img>  

<img width="613" alt="2" src="https://user-images.githubusercontent.com/43739827/86226145-30828400-bbc6-11ea-99e0-43b7b18a91e4.png"></img>  

## 정규방정식(Ordinary Least Squares)  

**LinearRegression** 은 데이터셋에서의 대상값(target value)과 선형 모델이 예측한 대상값 사이의 잔차제곱합(residual sum of squares)을 최소화시키는 모델이다.  

정규방정식의 예측 계수는 특징(feature)의 독립성에 의존한다. 만약 독립성을 가지지 못한다면 예측한 대상값에서 발생하는 임의의 에러에 매우 민감해지게된다.  

> [예시 코드 보기](https://github.com/galaxy1014/ML_module_summary/blob/master/Scikit-learn/1.%20Supervised%20learning/2.%20Linear%20Model/Ridge%20Classification.ipynb)  

## Ridge regression and classification  

### Regression  

**Ridge** 회귀는 정규방정식에서 발생하는 계수의 크기를 구하는 데 발생하는 문제들을 다루기위해 사용되었다.  

ridge 계수는 잔차제곱합의 결점을 최소화한다.  

<img width="195" alt="1" src="https://user-images.githubusercontent.com/43739827/86231277-447db400-bbcd-11ea-96e9-9934b53a565e.png"></img>  

복잡도를 나타내는 매개변수 α가 0이상이면 수축량을 조절한다. α가 클수록 수축량은 커지고 이로인해 계수는 다중공선성(collinearity)에 더 강해진다.  

> [예시 코드 보기](https://github.com/galaxy1014/ML_module_summary/blob/master/Scikit-learn/1.%20Supervised%20learning/2.%20Linear%20Model/Ridge%20Regression.ipynb)  

### Classification  

**RidgeClassifier** 는 이진대상값(binary target)을 **{-1, 1}** 로 변환하여 회귀에서 발생했던 문제들을 다루게된다.  

클래스를 예측하여 그 값을 회귀에서의 예측값들의 부호로 사용한다.  

> [예시 코드 보기](https://github.com/galaxy1014/ML_module_summary/blob/master/Scikit-learn/1.%20Supervised%20learning/2.%20Linear%20Model/Ridge%20Classification.ipynb)  

### Setting the regularization parameter: generalized Cross-Validation  

**RidgeCV** 는 알파를 교차검증(cross_validation)하는 ridge 회귀이다.

> [예시 코드 보기](https://github.com/galaxy1014/ML_module_summary/blob/master/Scikit-learn/1.%20Supervised%20learning/2.%20Linear%20Model/RidgeCV.ipynb)
