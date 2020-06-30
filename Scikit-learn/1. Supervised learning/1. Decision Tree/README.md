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

```Python  
>>> from sklearn import tree  
>>> X = [[0, 0], [1,1]]  
>>> Y = [0, 1]  
>>> clf = tree.DecisionTreeClassifier()  
>>> clf = clf.fit(X, Y)  
>>> clf.predict([[2., 2.,]])
```  

```   
array([1])
```  

```Python   
>>> clf.predict_proba([[2., 2.,]])
```  

```  
array([[0., 1.]])
```  

```Python  
>>> from sklearn.datasets import load_iris  
>>> X, y = load_iris(return_X_y = True)  
>>> clf = tree.DecisionTreeClassifier()  
>>> clf = clf.fit(X,  y)  
>>> tree.plot_tree(clf)
```  

```   
[Text(167.4, 199.32, 'X[2] <= 2.45\ngini = 0.667\nsamples = 150\nvalue = [50, 50, 50]'),  
 Text(141.64615384615385, 163.07999999999998, 'gini = 0.0\nsamples = 50\nvalue = [50, 0, 0]'),  
 Text(193.15384615384616, 163.07999999999998, 'X[3] <= 1.75\ngini = 0.5\nsamples = 100\nvalue = [0, 50, 50]'),  
 Text(103.01538461538462, 126.83999999999999, 'X[2] <= 4.95\ngini = 0.168\nsamples = 54\nvalue = [0, 49, 5]'),  
 Text(51.50769230769231, 90.6, 'X[3] <= 1.65\ngini = 0.041\nsamples = 48\nvalue = [0, 47, 1]'),  
 Text(25.753846153846155, 54.359999999999985, 'gini = 0.0\nsamples = 47\nvalue = [0, 47, 0]'),  
 Text(77.26153846153846, 54.359999999999985, 'gini = 0.0\nsamples = 1\nvalue = [0, 0, 1]'),  
 Text(154.52307692307693, 90.6, 'X[3] <= 1.55\ngini = 0.444\nsamples = 6\nvalue = [0, 2, 4]'),  
 Text(128.76923076923077, 54.359999999999985, 'gini = 0.0\nsamples = 3\nvalue = [0, 0, 3]'),  
 Text(180.27692307692308, 54.359999999999985, 'X[2] <= 5.45\ngini = 0.444\nsamples = 3\nvalue = [0, 2, 1]'),  
 Text(154.52307692307693, 18.119999999999976, 'gini = 0.0\nsamples = 2\nvalue = [0, 2, 0]'),  
 Text(206.03076923076924, 18.119999999999976, 'gini = 0.0\nsamples = 1\nvalue = [0, 0, 1]'),  
 Text(283.2923076923077, 126.83999999999999, 'X[2] <= 4.85\ngini = 0.043\nsamples = 46\nvalue = [0, 1, 45]'),  
 Text(257.53846153846155, 90.6, 'X[1] <= 3.1\ngini = 0.444\nsamples = 3\nvalue = [0, 1, 2]'),  
 Text(231.7846153846154, 54.359999999999985, 'gini = 0.0\nsamples = 2\nvalue = [0, 0, 2]'),  
 Text(283.2923076923077, 54.359999999999985, 'gini = 0.0\nsamples = 1\nvalue = [0, 1, 0]'),  
 Text(309.04615384615386, 90.6, 'gini = 0.0\nsamples = 43\nvalue = [0, 0, 43]')]  
```  

## Regression  

결정 트리에서 회귀 문제(regression problem)를 다루기 위해서는 **DecisionTreeRegressor** 를 사용한다.  
