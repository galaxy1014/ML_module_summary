# Decision Tree

**결정 트리(Decision Tree)** 는 **분류(Classification)** 와 **회귀(Regression)** 에서 사용하는 매개변수에 대한 가정을 전제로 하지 않고  
주어진 데이터에서 직접 학습하는 **비모수(non-parametric) 지도 학습** 메서드이다.  

결정 트리의 장점은 아래와 같다.  
```  
* 단순하여 이해하기에 편리하다. 또한 시각화가 가능하다는 특징이 있다.  
* 다른 머신러닝 메서드들에 비해 적은 데이터를 사용한다. 그러나 누락값에 대한 지원을 하지 않는다.  
* 숫자형 데이터(numeric data)와 범주형 데이터(categorical data)를 전부 다룰 수 있다.  
* 통계적 검증을 이용하여 모델의 성능을 판단할 수 있다.
```  

결정 트리의 단점은 아래와 같다.  
```  
* 결정 트리 알고리즘은 상당히 복잡한 트리를 만들 수 있으며 이는 과적합(overfitting)을 야기한다.  
* 일부 클래스가 제거되면 결정 트리는 편향된 트리를 만들 수 있다.  
```  

## Classification  

**DecisionTreeClassifier** 는 다중 클래스 분류를 수행할 수 있다.  

> [예시 코드 보기](https://github.com/galaxy1014/ML_module_summary/blob/master/Scikit-learn/1.%20Supervised%20learning/1.%20Decision%20Tree/Decision%20Tree%20Classifier.ipynb)

## Regression  

결정 트리에서 회귀 문제(regression problem)를 다루기 위해서는 **DecisionTreeRegressor** 를 사용한다.  

> [예시 코드 보기](https://github.com/galaxy1014/ML_module_summary/blob/master/Scikit-learn/1.%20Supervised%20learning/1.%20Decision%20Tree/DecisionTree%20Regression.ipynb)
