# Summary  

## 1. Series & DataFrame  

* Series  
**시리즈(Series)** 는 파이썬의 리스트(list)나 넘파이(Numpy) 배열로 구성된 1차원 객체이다.  

```Python
# 리스트로 시리즈 생성
se = pd.Series([1,3,'One'], index=list('ABC'))  
se  
```  

```
A      1  
B      3  
C    One  
dtype: object    
```

```Python
# 넘파이 배열로 시리즈 생성
n_se = pd.Series(np.random.randn(3), index=list('ABC'))  
n_se
```  

```
A    0.576868  
B    1.161323  
C   -1.290661  
dtype: float64  
```  

시리즈의 데이터 타입은 객체가 생성될때 요소의 자료형을 확인하여 자동적으로 지정된다.  

```Python
# 누락값 데이터 타입 확인
Nan_se = pd.Series([1,np.nan,2])  
Nan_se
```  

```
0    1.0  
1    NaN  
2    2.0  
dtype: float64  
```

> 누락값(NaN)의 데이터 타입이 **float64** 임을 확인할 수 있다.  

* DataFrame  
**데이터프레임(DataFrame)** 은 파이썬의 리스트나 딕셔너리 혹은 넘파이 배열로 생성할 수 있는 테이블형태의 2차원 객체이다.  

```Python
# 리스트로 데이터프레임 생성
df = pd.DataFrame([[1,2,3],[4,5,6],[7,8,9]], index=list('ABC'), columns=['One','Two','Three'])  
df
```  

 | | One | Two | Three |
 |-|:---:|:---:|:-----:|
A	| 1	| 2 |	3
B	| 4 |	5	| 6
C |	7 |	8 |	9


```Python
# 딕셔너리로 데이터프레임 생성
df2 = pd.DataFrame({'One' : [1,2,3], 'Two' : [4,5,6], 'Three' : [7,8,9]}, index=list('ABC'))  
df2
```  


| | One | Two | Three
|-|:---:|:---:|:-----:
A | 1	| 4 | 7
B |	2	| 5	| 8
C |	3	| 6	| 9


```Python
# 넘파이 배열로 데이터프레임 생성
df3 = pd.DataFrame({'One' : np.random.randint(10, size=3),
                   'Two' : np.random.randint(20, size=3),
                   'Three' : np.random.randint(30, size=3)}, index=list('ABC'))  
df3
```   


| | One | Two | Three
|- |:---:|:---:|:-----:
A | 8 | 19 | 3
B |	4	| 14 | 12
C | 6 | 0	| 19


## 2. 데이터 출력  
