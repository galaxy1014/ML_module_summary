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