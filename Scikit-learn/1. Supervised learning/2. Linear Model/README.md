# Linear Models

<img width="406" alt="1" src="https://user-images.githubusercontent.com/43739827/86226136-2e202a00-bbc6-11ea-9792-e822f0274565.png"></img>  

<img width="613" alt="2" src="https://user-images.githubusercontent.com/43739827/86226145-30828400-bbc6-11ea-99e0-43b7b18a91e4.png"></img>  

## 1. 정규방정식(Ordinary Least Squares)  

**LinearRegression** 은 데이터셋에서의 대상값(target value)과 선형 모델이 예측한 대상값 사이의 잔차제곱합(residual sum of squares)을 최소화시키는 모델이다.  

정규방정식의 예측 계수는 특징(feature)의 독립성에 의존한다. 만약 독립성을 가지지 못한다면 예측한 대상값에서 발생하는 임의의 에러에 매우 민감해지게된다.  

> [예시 코드 보기](https://github.com/galaxy1014/ML_module_summary/blob/master/Scikit-learn/1.%20Supervised%20learning/2.%20Linear%20Model/Ridge%20Classification.ipynb)  

## 2. Ridge regression and classification  

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

## 3.Lasso  

**Lasso** 는 희소 계수(sparse coefficients)를 측정하는 선형 모델이다. 즉 MSE가 최소값을 갖도록하는 가중치와 편향을 찾으면서 가중치의 절대값들이  
최소값을 가져서 기울기가 작아지도록 해야 하는 것이다. 이 말은 가중치가 0이나 0의 근사값을 가지게 해야 한다는 것이고 이렇게되면 일부 특성들은 모델 생성과정에서 제외된다.  

**lasso_path** 함수는 가질 수 있는 값의 전체 경로를 따라서 계수를 계산하며 간단한 단계의 업무에 유용하다.  
