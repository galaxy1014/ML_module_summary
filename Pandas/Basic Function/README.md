# Basic Functionality  

판다스에서 중요하게 사용되는 기능들에 대해 알아본다. 일단 기능들을 사용하기위해 인덱스, 시리즈, 데이터프레임을 생성한다.  

```Python  
# 인덱스 생성(시계열)
>>> t_idx = pd.date_range('2020-01-01', periods=8, freq='M')  
>>> t_idx  
```

```
DatetimeIndex(['2020-01-31', '2020-02-29', '2020-03-31', '2020-04-30',   
               '2020-05-31', '2020-06-30', '2020-07-31', '2020-08-31'],   
              dtype='datetime64[ns]', freq='M')   
```

```Python  
# 시리즈 생성
>>> s = pd.Series(np.random.randn(8),index = t_idx)   
>>> s  
```

```
2020-01-31   -0.947804  
2020-02-29    0.621019  
2020-03-31    0.526869  
2020-04-30    1.208103  
2020-05-31   -0.112500  
2020-06-30   -0.739076  
2020-07-31    1.419800  
2020-08-31   -2.781923  
Freq: M, dtype: float64  
```  

```Python
# 데이터프레임 생성
>>> df = pd.DataFrame({'One' : [1,2,3,4,5,6,7,8], 'Two' : [8,7,6,5,4,3,2,1,]}, index=t_idx)  
>>> df  
```  

 | | One | Two  
 |-|:---:|:---:  
 2020-01-31 | 1 | 8  
 2020-02-29 | 2 | 7  
 2020-03-31 | 3 | 6  
 2020-04-30 | 4 | 5  
 2020-05-31 | 5 | 4  
 2020-06-30 | 6 | 3  
 2020-07-31 | 7 | 2  
 2020-08-31 | 8 | 1  


## 1.Head & Tail  

시리즈나 데이터프레임의 특정 일부분만 보고자한다면 **head** 나 **tail** 메소드를 사용한다. 괄호안에 숫자를 입력하면 그 범위만큼의 값이 나타나며 기본값은 **5** 이다.  

```Python
# 상위 5개
>>> s.head()
```  

```
2020-01-31   -0.947804  
2020-02-29    0.621019  
2020-03-31    0.526869  
2020-04-30    1.208103  
2020-05-31   -0.112500  
Freq: M, dtype: float64  
```  

```Python  
# 하위 5개  
>>> s.tail(6)
```  

```
2020-03-31    0.526869  
2020-04-30    1.208103  
2020-05-31   -0.112500  
2020-06-30   -0.739076  
2020-07-31    1.419800  
2020-08-31   -2.781923  
Freq: M, dtype: float64  
```  

## 2.Attribute and underlying data  

판다스의 객체(인덱스, 시리즈, 데이터프레임)들은 **shape** 메소드를 사용하여 객체가 가지고있는 축의 차원을 ndarray로 반환하여 보여준다.  

```Python  
# 시리즈 shape
>>> s.shape
```

```
(8,)
```

```Python  
# 데이터프레임 shape
>>> df.shape  
```

```
(8, 2)
```  

```Python  
# 인덱스 shape
>>> t_idx.shape
```  

```
(8,)
```  

판다스는 넘파이 모듈로 구성되어있기 때문에 **슬라이싱(Slicing)** 을 통한 검색이 가능하다.  

```Python  
# 0~3번째의 행을 출력
>>> df[:3]
```

 | | One | Two  
 |-|:---:|:---:  
2020-01-31 | 1 | 8  
2020-02-29 | 2 | 7  
2020-03-31 | 3 | 6  

```Python  
# 2~5번째의 행을 출력
>>> df[2:5]
```  

 | | One | Two  
 |-|:---:|:---:  
2020-03-31 | 3 | 6  
2020-04-30 | 4 | 5  
2020-05-31 | 5 | 4  

판다스의 객체는 **배열(array)** 로 구성되어 값들을 저장하고 있다. 시리즈나 인덱스에서 **array** 속성을 사용하여 내부 데이터와 자료형을 확인할 수 있다.  

```Python  
# 시리즈 내부의 값
>>> s.array
```  

```
<PandasArray>
[ -0.9478040550309271,   0.6210189401447063,   0.5268690969841191,  
   1.2081027538889946, -0.11250048407157869,  -0.7390759558578995,  
   1.4198001438584995,   -2.781922728141299]  
Length: 8, dtype: float64  
```  

```Python  
# 시리즈 인덱스 값(시계열)
>>> s.index.array
```  

```
<DatetimeArray>
['2020-01-31 00:00:00', '2020-02-29 00:00:00', '2020-03-31 00:00:00',  
 '2020-04-30 00:00:00', '2020-05-31 00:00:00', '2020-06-30 00:00:00',  
 '2020-07-31 00:00:00', '2020-08-31 00:00:00']  
Length: 8, dtype: datetime64[ns]  
```  

만약 배열을 넘파이 배열로 확인해야 한다면 **to_numpy** 나 **numpy.asarray** 메소드를 사용한다.  

```Python  
# to_numpy 메소드 사용
>>> s.to_numpy()
```  

```
array([-0.94780406,  0.62101894,  0.5268691 ,  1.20810275, -0.11250048,  
       -0.73907596,  1.41980014, -2.78192273])   
```  

```Python  
# np.asarray 메소드 사용
>>> np.asarray(s)
```  

```
array([-0.94780406,  0.62101894,  0.5268691 ,  1.20810275, -0.11250048,  
       -0.73907596,  1.41980014, -2.78192273])  
```  

to_numpy 메소드는 결과로 반환되는 ndarray의 자료형을 제어한다. 예를들어 타임존이 설정되어있는 시계열 데이터를 메소드를 사용하여 ndarray로 반환한다면, 넘파이는 타임존을 나타내는 방법을 가지고있지 않다. 그렇기때문에 2가지 경우를 사용할 수 있다.  

1. ndarray의 자료형을 **Object** 로 지정하면 반환되는 ndarray에 **tz** 로 타임존의 정보가 나타난다.  
2. ndarray의 자료형을 **datetime64[ns]** 로 지정하면 시간정보가 UTC로 변환되고 타임존은 버린다.  

```Python  
# 타임존을 설정한 시계열 시리즈 생성
>>> t_s = pd.Series(pd.date_range('2020', periods=2, tz='CET'))  
>>> t_s  
```  

```
0   2020-01-01 00:00:00+01:00  
1   2020-01-02 00:00:00+01:00  
dtype: datetime64[ns, CET]  
```  

```Python  
# 자료형 Object  
>>> t_s.to_numpy(dtype=object)  
```  

```
array([Timestamp('2020-01-01 00:00:00+0100', tz='CET', freq='D'),  
       Timestamp('2020-01-02 00:00:00+0100', tz='CET', freq='D')],   
      dtype=object)  
```  

```Python  
# 자료형 datetime64[ns]
>>> t_s.to_numpy(dtype='datetime64[ns]')
```  

```
array(['2019-12-31T23:00:00.000000000', '2020-01-01T23:00:00.000000000'],   
      dtype='datetime64[ns]')  
```  

데이터프레임의 경우 내부 데이터들이 모두 같은 자료형을 가지고 있다면 to_numpy 메소드를 사용한 뒤의 반환결과도 같은 자료형을 가지게 된다. 그러나 만약 내부 자료형이 다른 경우에는 조건에 따라 자료형이 달라진다.
> 만약 문자형이 하나라도 있으면 반환결과의 자료형은 문자형(object)가 되며, 내부값들이 정수와 소수로 구성되어 있으면 반환결과의 자료형은 소수(float64)가 된다.  

```Python  
# 정수, 소수, 문자형이 섞여있는 데이터프레임 생성
>>> df2 = pd.DataFrame({'A' : [1,2,np.nan,'a'], 'B' : [3,4,5,6]})  
>>> df2
```   

 | | A | B  
 |-|:-:|:-:  
0 | 1 | 3  
1 | 2 | 4  
2 | NaN | 5  
3 | a | 6  

```Python  
>>> df2.to_numpy()
```  

```
array([[1, 3],  
       [2, 4],  
       [nan, 5],  
       ['a', 6]], dtype=object)   
```  

```Python  
# 정수와 누락값(소수)으로 구성되어 있는 데이터프레임 생성
>>> df3 = pd.DataFrame({'A' : [1,2,np.nan,3], 'B' : [4,5,6,7]})   
>>> df3
```  

 | | A | B  
 |-|:-:|:-:  
0 | 1.0 | 4  
1 | 2.0 | 5  
2 | NaN | 6  
3 | 3.0 | 7  

```Python  
>>> df3.to_numpy()
```  

```
array([[ 1.,  4.],  
       [ 2.,  5.],  
       [nan,  6.],  
       [ 3.,  7.]])  
```  

## 3.Accelerated operations  

판다스는 **numexpr** 라이브러리와 **bottleneck** 라이브러리를 사용하여 이진 숫자와 불리언 연산의 처리 속도를 가속화할 수 있다. 이 라이브러리들은 특히 큰 데이터 셋을 다룰때 유용하다. 특히 bottleneck은 NaN이 있는 배열을 다룰때 유용하다.  

```Python  
>>> import bottleneck as bn  
>>> import time  
```  

```Python  
# bottleneck 라이브러리 사용   
>>> start = time.time() # 시작시간 측정  
>>> print(bn.nanmean(df['home_goals']), time.time() - start)
```  

```  
1.5517993456924755 0.0002181529998779297
```  

```Python  
# 넘파이 모듈 사용  
start = time.time() # 시작시간 측정
print(np.nanmean(df['home_goals']), time.time() - start)
```  

```  
1.5517993456924755 0.00026988983154296875
```

## 4. Flexible binary operations  

판다스에서 두 데이터프레임간의 연산을 수행하게 되면 두 가지에 중점을 두게된다.  

```
1. 고차원 혹은 저차원의 데이터프레임간 브로드캐스팅  
2. 누락값의 계산
```  

이런 문제를 관리하는 방법들을 아래에 설명한다.  

### Matching / broadcasting behavior  

데이터프레임은 이항 연산을 수행하기 위해 **add(), sub(), mul(), div(), radd(), rsub()** 메소드를 지원한다.  

이 메소드들을 사용하고자 할 땐 행이나 열의 축을 기준으로 잡아야한다.  

```Python  
>>> df = pd.DataFrame({'One' : pd.Series(np.random.randn(4), index=['a','b','c','d']),
                    'Two' : pd.Series(np.random.randn(3), index=['a','c','d']),
                   'Three' : pd.Series(np.random.randn(3), index=['b','c','d'])})  

>>> df
```  

 | | One | Two | Three  
 |-|:---:|:---:|:-----:  
a | 1.008765 | -0.175352 | NaN  
b | 1.748897 | NaN | 0.624603  
c | 1.078679 | -0.866894 | -0.950405  
d | -1.573860 | 0.170444 | 0.322723  

```Python  
# 연산을 할 시리즈 생성(데이터프레임에서 한 행을 추출)
>>> row = df.iloc[1]  
>>> row
```  

```  
One      1.748897  
Two           NaN  
Three    0.624603  
Name: b, dtype: float64
```  

```Python  
>>> df.sub(row, axis='columns')
```  

| | One | Two | Three  
|-|:---:|:---:|:-----:  
a | -0.740132 | NaN | NaN  
b | 0.000000 | NaN | 0.000000  
c | -0.670218 | NaN | -1.575008  
d | -3.322757 | NaN | -0.301881  

```Python  
>>> df.sub(row, axis=1)
```  

| | One | Two | Three  
|-|:---:|:---:|:-----:  
a | -0.740132 | NaN | NaN  
b | 0.000000 | NaN | 0.000000  
c | -0.670218 | NaN | -1.575008  
d | -3.322757 | NaN | -0.301881  

```Python  
# 연산을 할 시리즈 생성(데이터프레임에서 한 열을 추출)
>>> column = df['One']  
>>> column
```  

```
a    1.008765  
b    1.748897  
c    1.078679  
d   -1.573860  
Name: One, dtype: float64
```

```Python  
>>> df.sub(column, axis=0)
```  

| | One | Two | Three  
|-|:---:|:---:|:-----:  
a | 0.0 | -1.184117 | NaN  
b | 0.0 | NaN | -1.124294  
c | 0.0 | -1.945573 | -2.029084  
d | 0.0 | 1.744304 | 1.896582  

```Python  
>>> df.sub(column, axis='index')
```  

| | One | Two | Three  
|-|:---:|:---:|:-----:  
a | 0.0 | -1.184117 | NaN  
b | 0.0 | NaN | -1.124294  
c | 0.0 | -1.945573 | -2.029084  
d | 0.0 | 1.744304 | 1.896582  

멀티인덱스를 가지는 데이터프레임과 시리즈의 연산또한 가능하다.  

```Python  
# 데이터프레임 사본 생성
>>> m_df = df.copy()  
# 멀티인덱스 생성  
>> m_df.index = pd.MultiIndex.from_tuples([(1,'a'),(1,'b'),(1,'c'),(2,'a')], names=['first','second'])
>>> m_df
```  

<img width="304" alt="1" src="https://user-images.githubusercontent.com/43739827/76315244-a911bc00-631b-11ea-9277-7805774509d7.png"></img>  

```Python  
>>> m_df.sub(column, axis=0, level='second')
```

<img width="308" alt="2" src="https://user-images.githubusercontent.com/43739827/76315278-b75fd800-631b-11ea-8ce7-b605a39a1147.png"></img>

**divmod()** 메소드를 사용하여 데이터의 나누기 연산을 했을때의 데이터를 구할 수 있다.  

```Python  
# 0~10까지의 정수를 원소로하는 시리즈 생성
>>> s = pd.Series(np.arange(10))  
>>> s
```  

```
0    0  
1    1  
2    2  
3    3  
4    4  
5    5  
6    6  
7    7  
8    8  
9    9  
dtype: int64
```  

```Python  
>>> div, rem = divmod(s, 3)
```  

```Python
# s를 3으로 나눈 몫
>>> div
```  

```
0    0  
1    0  
2    0  
3    1  
4    1  
5    1  
6    2  
7    2  
8    2  
9    3  
dtype: int64  
```  

```Python
# s를 3으로 나눈 나머지  
>>> rem
```  

```  
0    0  
1    1  
2    2  
3    0  
4    1  
5    2  
6    0  
7    1  
8    2  
9    0   
dtype: int64
```  

특정값들을 요소로 가지는 리스트의 divmod 연산또한 가능하다.  

```Python  
# 리스트를 지정
>>> div, rem = divmod(s, [2,2,2,3,3,3,4,4,4,5])
```  

```Python
# 리스트로 시리즈를 나눈 몫  
>>> div
```  

```
0    0  
1    0  
2    1  
3    1  
4    1  
5    1  
6    1  
7    1  
8    2  
9    1  
dtype: int64
```  

```Python
# 리스트로 시리즈를 나눈 몫  
>>> rem
```  

```
0    0  
1    1  
2    0  
3    0  
4    1  
5    2  
6    2  
7    3  
8    0  
9    4  
dtype: int64
```  

### Missing data / operations will fill values

시리즈와 데이터프레임에서 산술연산을 할 때 둘 중 하나의 요소가 NaN이라면 **fill_value** 매개변수를 이용해 NaN의 값을 특정값으로 대체시킬 수 있다. 그러나 양쪽 객체의 같은 위치에 두 요소가 모두 NaN값이라면 특정값으로 채워지지 않는다.  

```Python
>>> df = pd.DataFrame({'One' : {'a': 1.394981, 'b' : 0.343054, 'c' : 0.695246},
                  'Two' : {'a' : 1.772517, 'b' : 1.912123, 'c' : 1.478369, 'd' : 0.279344},
                  'Three' : {'b' : -0.050390, 'c' : 1.227435, 'd' : -0.613172}})  
>>> df
```  

|    |        One |      Two |      Three |
|:---|-----------:|---------:|-----------:|
| a  |   1.39498  | 1.77252  | nan        |
| b  |   0.343054 | 1.91212  |  -0.05039  |
| c  |   0.695246 | 1.47837  |   1.22744  |
| d  | nan        | 0.279344 |  -0.613172 |  

```Python  
>>> df2 = pd.DataFrame({'One' : {'a' : 1.394981, 'b' : 0.343054, 'c' : 0.695246},
                   'Two' : {'a' : 1.772517, 'b' : 1.912123, 'c' : 1.478369, 'd' : 0.279344},
                   'Three' : {'a' : 1.000000 , 'b' : -0.050390, 'c' : 1.227435, 'd' : -0.613172}})  
>>> df2
```  

|    |        One |      Two |     Three |
|:---|-----------:|---------:|----------:|
| a  |   1.39498  | 1.77252  |  1        |
| b  |   0.343054 | 1.91212  | -0.05039  |
| c  |   0.695246 | 1.47837  |  1.22744  |
| d  | nan        | 0.279344 | -0.613172 |  

```Python  
>>> df + df2
```  

|    |        One |      Two |     Three |
|:---|-----------:|---------:|----------:|
| a  |   2.78996  | 3.54503  | nan       |
| b  |   0.686108 | 3.82425  |  -0.10078 |
| c  |   1.39049  | 2.95674  |   2.45487 |
| d  | nan        | 0.558688 |  -1.22634 |  

```Python  
>>> df.add(df2, fill_value=0)
```  

|    |        One |      Two |    Three |
|:---|-----------:|---------:|---------:|
| a  |   2.78996  | 3.54503  |  1       |
| b  |   0.686108 | 3.82425  | -0.10078 |
| c  |   1.39049  | 2.95674  |  2.45487 |
| d  | nan        | 0.558688 | -1.22634 |

```Python  
>>> df.add(df2, fill_value=1)  
```  

|    |        One |      Two |    Three |
|:---|-----------:|---------:|---------:|
| a  |   2.78996  | 3.54503  |  2       |
| b  |   0.686108 | 3.82425  | -0.10078 |
| c  |   1.39049  | 2.95674  |  2.45487 |
| d  | nan        | 0.558688 | -1.22634 |  

### Flexible comparisons  

시리즈와 데이터프레임은 비교 연산을 수행하는 메소드 **eq, ne, lt, gt, le, ge** 를 지원한다.  

```Python
>>> df.eq(df2)
```  

|    |   One |   Two |   Three |
|:---|------:|------:|--------:|
| a  |  True |  True |    Flase|
| b  |  True |  True |    True |
| c  |  True |  True |    True |
| d  |  Flase|  True |    True |  

```Python  
>>> df.ne(df2)
```  

|    |   One |   Two |   Three |
|:---|------:|------:|--------:|
| a  |  Flase|  Flase|    True |
| b  |  Flase|  Flase|   Flase |
| c  |  Flase|  Flase|   Flase |
| d  |  True |  Flase|   Flase |  

```Python  
>>> df.lt(df2)
```  

|    |   One |   Two |   Three |
|:---|------:|------:|--------:|
| a  |  Flase|  Flase|    Flase|
| b  |  Flase|  Flase|    Flase|
| c  |  Flase|  Flase|    Flase|
| d  |  Flase|  Flase|    Flase|

```  
eq : 객체의 요소끼리가 같으면 True, 다르면 False를 반환한다. 만약 비교하는 요소가 모두 누락값이라면 False를 반환한다.  
ne : eq의 반대개념으로 같으면 False, 다르면 True를 반환한다. 만약 비교하는 요소가 모두 누락값이라면 True를 반환한다.  
lt : less than의 약어로 기준이 되는 요소의 값이 적으면 True, 크거나 같으면 False를 반환한다.  
gt : greater than의 약어로 기준이 되는 요소의 값이 크면 True, 작거나 같으면 False를 반환한다.  
le : less than or equal의 약어로 기준이 되는 요소의 값이 적거나 같으면 True, 크면 False를 반환한다.  
ge : greater than or equal의 약어로 기준이 되는 요소의 값이 크거나 같으면 True, 작으면 False를 반환한다.  
```  

결과의 반환값이 boolean인것을 확인할 수 있다.  

### Boolean reductions  

불리언 결과를 간략하게 보여주는 메소드로 **empty, any(), all(), bool()** 을 제공한다.  

```Python  
>>> (df > 0).all()
```  

```
One      False   
Two       True  
Three    False  
dtype: bool  
```  

```Python  
>>> (df > 0).any()
```  

```
One      True  
Two      True  
Three    True  
dtype: bool  
```  

최종 불리언 값만을 도출할 수 있다.  

```Python  
>>> (df > 0).any().any()
```  

```  
True
```  

판다스 객체가 비어있음을 확인하고 싶으면 **empty** 객체를 사용한다.  

```Python  
>>> df.empty
```  

```  
False
```  

```Python  
>>> pd.DataFrame(columns=list('ABC')).empty
```  

```  
True
```  

판다스의 객체가 불리언 요소를 가지는지 확인하고 싶다면 **bool()** 메소드를 사용한다.  

```Python  
>>> bool(df.iloc[0][0])
```  

```
True
```   

### Comparing if objects are equivalent  

종종 같은 결과를 반환하는 다른 연산을 확인할 수 있다. 예를들어 **df + df** 와 **df * 2** 의 결과는 같다. 그러나 False와 False의 ==연산은 False를 반환하기 때문에 단순한 ==연산으로는 객체의 요소가 같은지 정확하게 확인할 수 없다.  

```Python  
# False 끼리의 논리연산은 False를 반환한다.
>>> df + df == df * 2
```  

|    |   One |   Two |   Three |
|:---|------:|------:|--------:|
| a  |   True|   True|    False|
| b  |   True|   True|     True|
| c  |   True|   True|     True|
| d  |  False|   True|     True|  

**equals()** 메소드를 사용하면 비교하는 대상의 객체들이 같은지를 확인할 수 있다.  

```Python  
>>> (df + df).equals(df * 2)
```  

```  
True
```  

### Comparing array-like objects  

판다스는 리스트를 이용한 간단한 논리연산이 가능하다.  

```Python  
>>> pd.Series(['One', 'Two', 'Three']) == 'Two'  
```  

```
0    False  
1     True  
2    False  
dtype: bool  
```  

```Python  
>>> pd.Index(['Four', 'Five', 'Six']) == 'Five'
```  

```  
array([False,  True, False])
```  

시리즈와 인덱스끼리의 논리연산이 가능하며 이때 각 객체의 길이는 같아야만 한다.  

```Python
>>> pd.Series(['One', 'Two', 'Three']) == pd.Index(['One', 'Five', 'Six'])
```  

```  
0     True  
1    False  
2    False  
dtype: bool  
```  

```Python  
>>> pd.Series(['One', 'Two', 'Three']) == pd.Series(['One', 'Two'])
```  

```  
0     True  
1    False  
2    False  
dtype: bool  
```  

넘파이와의 차이점은 넘파이는 브로드캐스팅이 된다는것이다.  

```Python  
>>> np.array([1,2,3]) == np.array([1])
```  

```
array([ True, False, False])
```  

### Combining overlapping data sets  

두 개의 비슷한 데이터셋을 합칠때 **combine_first()** 메소드를 사용하여 기준이 되는 데이터셋의 누락값이나 가지지 않은 인덱스를 추가할 수 있다.  

```Python  
>>> df1 = pd.DataFrame({'A' : [1., np.nan, 3., 5., np.nan],
                   'B' : [np.nan, 2., 3., np.nan, 6.]})
```  

|    |   A |   B |
|---:|----:|----:|
|  0 |   1 | nan |
|  1 | nan |   2 |
|  2 |   3 |   3 |
|  3 |   5 | nan |
|  4 | nan |   6 |  

```Python  
>>> df2 = pd.DataFrame({'A' : [5., 2., 4., np.nan, 3., 7.],
                   'B' : [np.nan, np.nan, 3., 4., 6., 8.]})
```  

|    |   A |   B |
|---:|----:|----:|
|  0 |   5 | nan |
|  1 |   2 | nan |
|  2 |   4 |   3 |
|  3 | nan |   4 |
|  4 |   3 |   6 |
|  5 |   7 |   8 |  

```Python  
>>> df1.combine_first(df2)
```  

|    |   A |   B |
|---:|----:|----:|
|  0 |   1 | nan |
|  1 |   2 |   2 |
|  2 |   3 |   3 |
|  3 |   5 |   4 |
|  4 |   3 |   6 |
|  5 |   7 |   8 |  

```Python  
>>> df2.combine_first(df1)
```  

|    |   A |   B |
|---:|----:|----:|
|  0 |   5 | nan |
|  1 |   2 |   2 |
|  2 |   4 |   3 |
|  3 |   5 |   4 |
|  4 |   3 |   6 |
|  5 |   7 |   8 |  

## 5.Descriptive statistics  

**기술 통계학(Descriptive statistics)** 을 계산하기 위한 판다스만의 메소드가 존재한다.  

```  
* Series : axis를 지정하지 않는다.  
* DataFrame : 인덱스설정(axis=0)<- 기본값, 컬럼설정(axis=1)
```  

Function | Description  
:-------:|:-----------:  
count | 누락값을 포함하지 않은 요소들의 갯수  
sum | 값들의 합  
mean | 값들의 평균  
mad | 평균절대편차  
median | 값들의 중앙값(median)  
min | 최솟값  
max | 최댓값  
mode | 최빈값(가장 많이 관측되는 수)  
abs | 절댓값  
prod | 값들의 곱  
std | 표준편차의 베셀 보정  
var | 분산  
sem | 표준 오차  
skew | 표본 비대칭도  
kurt | 표본 첨도(kutrosis)  
quantile | 표본 분위수  
cumsum | 누적합(Cumulative sum)
cumprod | 누적곱(Cumulative product)  
cummax | 누적 최댓값  
cummin | 누적 최솟값


```Python  
>>> df
```  

|    |        One |      Two |      Three |
|:---|-----------:|---------:|-----------:|
| a  |   1.39498  | 1.77252  | nan        |
| b  |   0.343054 | 1.91212  |  -0.05039  |
| c  |   0.695246 | 1.47837  |   1.22744  |
| d  | nan        | 0.279344 |  -0.613172 |  

```Python  
>>> df.mean(0)
```  

```  
One      0.811094  
Two      1.360588  
Three    0.187958  
dtype: float64  
```  

```Python  
>>> df.mean(1)
```  

```  
a    1.583749  
b    0.734929  
c    1.133683  
d   -0.166914  
dtype: float64  
```  

여기서 사용되는 모든 메소드는 **skipna** 를 매개변수로 가진다. 이 메소드는 누락값을 확인하는 기능을 하며 기본값은 **True** 이다.  

```Python  
>>> df.sum(0, skipna=False)
```  

```  
One           NaN  
Two      5.442353  
Three         NaN  
dtype: float64  
```  

```Python  
>>> df.sum(axis=1, skipna=True)
```  

```  
a    3.167498  
b    2.204787  
c    3.401050  
d   -0.333828  
dtype: float64  
```  

통계적 계산또한 가능하다. **std()** 메소드는 표준 편차를 구하기위해 사용하는 메소드다.

```Python  
>>> ts_stand = (df - df.mean(0)) / df.std()  
>>> ts_stand.std()
```  

```
One      1.0  
Two      1.0  
Three    1.0  
dtype: float64  
```  

```Python  
>>> xs_stand = df.sub(df.mean(1), axis=0).div(df.std(1), axis=0)  
>>> xs_stand
```  

|    |        One |      Two |      Three |
|:---|-----------:|---------:|-----------:|
| a  |  -0.707107 | 0.707107 | nan        |
| b  |  -0.377425 | 1.13379  |  -0.756361 |
| c  |  -1.09639  | 0.86195  |   0.234443 |
| d  | nan        | 0.707107 |  -0.707107 |  

```Python  
>>> xs_stand.std(1)
```  

```  
a    1.0  
b    1.0  
c    1.0  
d    1.0  
dtype: float64  
```  

**cumsum()** 과 **comprod()** 메소드는 누락값의 위치를 보존한다.  

```Python  
>>> df.cumsum()
```  

|    |       One |     Two |      Three |
|:---|----------:|--------:|-----------:|
| a  |   1.39498 | 1.77252 | nan        |
| b  |   1.73803 | 3.68464 |  -0.05039  |
| c  |   2.43328 | 5.16301 |   1.17705  |
| d  | nan       | 5.44235 |   0.563873 |  

넘파이 모듈을 사용해 데이터프레임의 평균을 구할 수 있다.  

```Python  
>>> np.mean(df['One'])
```  

```  
0.8110936666666667
```  

**Series.nunique()** 메소드는 시리즈에서 누락값을 제외한 유일값의 개수를 반환한다.  

```Python
>>> Series = pd.Series(np.random.randn(500))  
>>> Series[20:200] = np.nan  
>>> Series[10:20] = 5  
>>> Series.nunique()
```  

```  
311
```  

### Summarizing data: describe  

**describe()** 메소드를 사용하면 간략한 통계적 정보를 얻을 수 있다.  

```Python  
>>> series = pd.Series(np.random.randn(1000))  
>>> series[::2] = np.nan  
>>> series.describe()
```  

```  
count    500.000000  
mean      -0.104046  
std        0.973392  
min       -3.459899  
25%       -0.705669  
50%       -0.057655  
75%        0.559557  
max        3.115283  
dtype: float64  
```  

```Python  
>>> df = pd.DataFrame(np.random.randn(1000,5), columns=['a','b','c','d','e'])  
>>> df.iloc[::2] = np.nan  
>>> df.describe()
```  

|       |           a |           b |           c |           d |           e |
|:------|------------:|------------:|------------:|------------:|------------:|
| count | 500         | 500         | 500         | 500         | 500         |
| mean  |  -0.0098391 |  -0.0217725 |  -0.0133153 |   0.0329154 |   0.0208793 |
| std   |   1.04484   |   1.02411   |   1.03689   |   0.991465  |   1.01293   |
| min   |  -3.15347   |  -2.56002   |  -2.98677   |  -2.66778   |  -2.99676   |
| 25%   |  -0.736796  |  -0.682348  |  -0.716998  |  -0.616957  |  -0.754231  |
| 50%   |   0.0153571 |  -0.124131  |  -0.0624372 |   0.0335433 |   0.0098666 |
| 75%   |   0.683469  |   0.678965  |   0.686431  |   0.705677  |   0.736733  |
| max   |   3.26103   |   3.05544   |   3.11557   |   3.24525   |   2.79697   |  

describe 메소드에 매개변수로 **percentiles** 를 사용하면 나타낼 백분율을 설정할 수 있다.  

```Python  
>>> series.describe(percentiles=[.05, .25, .75, .95])
```  

```  
count    500.000000  
mean      -0.104046  
std        0.973392  
min       -3.459899  
5%        -1.804095  
25%       -0.705669  
50%       -0.057655  
75%        0.559557  
95%        1.402325  
max        3.115283  
dtype: float64  
```  

숫자형이 아닌 시리즈객체애 describe 메소드를 사용하면 유일값의 갯수나 가장 빈번하게 발생하는 값의 갯수를 출력한다.  

```Python  
>>> s = pd.Series(['a','a','a','b','b',np.nan,'c','d','a'])  
>>> s.describe()
```  

```  
count     8  
unique    4  
top       a  
freq      4  
dtype: object  
```  

여러 자료형이 섞인 데이터프레임에 describe 메소드를 사용하면 숫자값을 포함하고있는 열만의 정보를 출력한다.  

```Python  
>>> df = pd.DataFrame({'a' : ['Yes','Yes','No','No'], 'b' : range(4)})  
>>> df.describe()
```  

|       |       b |
|:------|--------:|
| count | 4       |
| mean  | 1.5     |
| std   | 1.29099 |
| min   | 0       |
| 25%   | 0.75    |
| 50%   | 1.5     |
| 75%   | 2.25    |
| max   | 3       |  

이 때 매개변수로 **include/exclude** 를 사용하여 출력결과를 조절할 수 있다.  

```Python  
>>> df.describe(include=['object'])
```  

|        | a   |
|:-------|:----|
| count  | 4   |
| unique | 2   |
| top    | No  |
| freq   | 2   |  

```Python  
>>> df.describe(include=['number'])
```  

|       |       b |
|:------|--------:|
| count | 4       |
| mean  | 1.5     |
| std   | 1.29099 |
| min   | 0       |
| 25%   | 0.75    |
| 50%   | 1.5     |
| 75%   | 2.25    |
| max   | 3       |  

```Python  
>>> df.describe(include='all')
```  

|        | a   |         b |
|:-------|:----|----------:|
| count  | 4   |   4       |
| unique | 2   | nan       |
| top    | No  | nan       |
| freq   | 2   | nan       |
| mean   | nan |   1.5     |
| std    | nan |   1.29099 |
| min    | nan |   0       |
| 25%    | nan |   0.75    |
| 50%    | nan |   1.5     |
| 75%    | nan |   2.25    |
| max    | nan |   3       |

### Index of min/max values  

**idxmin()** 과 **idxmax()** 함수는 시리즈와 데이터프레임의 인덱스 레이블의 최소값과 최댓값을 확인하는 기능을 한다.  

```Python  
>>> s1 = pd.Series(np.random.randn(5))  
>>> s1
```  

```
0    0.013833  
1    1.375255  
2   -0.261117  
3   -1.300798  
4    0.550127  
dtype: float64  
```  

```Python  
>>> s1.idxmin(), s1.idxmax()
```  

```
(3, 1)
```  

```Python  
>>> df1 = pd.DataFrame(np.random.randn(5, 3), columns=['A','B','C'])
```  

|    |          A |         B |         C |
|---:|-----------:|----------:|----------:|
|  0 | -0.307946  |  0.96568  |  0.854274 |
|  1 | -0.734701  | -0.763467 |  0.805104 |
|  2 |  0.0317531 |  0.494293 | -0.720657 |
|  3 |  2.08982   |  0.295745 |  1.1382   |
|  4 |  0.260457  |  0.785826 |  0.109045 |  

```Python  
>>> df1.idxmin(axis=0)
```  

```
A    1  
B    1  
C    2  
dtype: int64  
```  

```Python  
>>> df1.idxmax(axis=1)
```  

```
0    B  
1    C  
2    B  
3    A  
4    B  
dtype: object  
```  

만약 최솟값과 최댓값을 찾을 때 행 혹은 열이 중복값을 찾는다면 제일 먼저 찾은값을 찾는다.  

```Python  
>>> df3 = pd.DataFrame([2, 1, 1, 3, np.nan], columns=['A'], index=list('edcba'))  
>>> df3
```  

|    |   A |
|:---|----:|
| e  |   2 |
| d  |   1 |
| c  |   1 |
| b  |   3 |
| a  | nan |  

```Python  
>>> df3['A'].idxmin()
```  

```  
'd'
```  
