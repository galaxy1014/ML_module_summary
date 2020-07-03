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

> [예시 코드 보기](https://github.com/galaxy1014/ML_module_summary/blob/master/Scikit-learn/1.%20Supervised%20learning/2.%20Linear%20Model/Lasso%20and%20Elastic%20Net%20for%20Sparse%20Signals.ipynb)  
> [예시 코드 보기](https://github.com/galaxy1014/ML_module_summary/blob/master/Scikit-learn/1.%20Supervised%20learning/2.%20Linear%20Model/Compressive%20sensing_tomography%20reconstruction%20with%20L1%20prior%20(Lasso).ipynb)  

### Setting regularization parameter  

매개변수 알파 측정된 계수의 희소성의 정도를 조절한다.  

### Using cross-validation  

scikit-learn에는 α에 대해서 교차검증을 시행하는 Lasso인 **LassoCV** , **LassoLarsCV** 가 있다.  
LassoLarsCV는 **Least Angle Regression** 알고리즘을 기반으로 한다.  

많은 다중공산성을 특징들을 가지는 고차원의 데이터셋인경우 **LassoCV** 가 조금 더 선호되는 경향이 있으나, **LassoLarsCV** 는 알파 매개변수에 더 연관된 값들을 찾고자하는 경우에 더 선호된다. 그리고 만약 특징의 수가 표본의 수보다 작으면 LassoCV보다 더 빠른 경향이있다.

### Information-criteria based model selection  

**LassoLarsIC** 는 AIC(Akaike Information Criterion)와 BIC(Bayes Information Criterion)의 사용을 제안한다. k-폴드 교차검증을 사용할 때  
정규화 경로가 k+1회 대신 한 번만 계산되므로 알파 최적값을 찾는 것이 계산적으로 저렴한 대안이다. 즉, 데이터가 실제로 이 모델에 의해 생성된다고 가정한다.  
또한 문제가 불량하게 조건화되었을 때(표본보다 더 많은 특징) 깨지는 경향이 있다.

> [예시 코드 보기](https://github.com/galaxy1014/ML_module_summary/blob/master/Scikit-learn/1.%20Supervised%20learning/2.%20Linear%20Model/Lasso%20model%20selection_Cross-Validation%2CAIC%2CBIC.ipynb)  

## 4. Multi-task Lasso  

**MultiTaskLasso** 는 다중 회귀 문제에서의 희소 계수값을 측정하는 선형 모델이다. 제약조건으로는 task라 불리는 선택된 특징들이 모든 회귀 문제에서 동일하다는 것이다.  
