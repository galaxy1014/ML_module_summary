# Summary  

## 1. Series & DataFrame  

* Series  
**시리즈(Series)** 는 파이썬의 리스트(list)나 넘파이(Numpy) 배열로 구성된 1차원 객체이다.  

```Python
# 리스트로 시리즈 생성
>>> se = pd.Series([1,3,'One'], index=list('ABC'))  
>>> se  
```  

```
A      1  
B      3  
C    One  
dtype: object    
```

```Python
# 넘파이 배열로 시리즈 생성
>>> n_se = pd.Series(np.random.randn(3), index=list('ABC'))  
>>> n_se
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
>>> Nan_se = pd.Series([1,np.nan,2])  
>>> Nan_se
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
>>> df = pd.DataFrame([[1,2,3],[4,5,6],[7,8,9]], index=list('ABC'), columns=['One','Two','Three'])  
>>> df
```  

 | | One | Two | Three |
 |-|:---:|:---:|:-----:|
A	| 1	| 2 |	3
B	| 4 |	5	| 6
C |	7 |	8 |	9


```Python
# 딕셔너리로 데이터프레임 생성
>>> df2 = pd.DataFrame({'One' : [1,2,3], 'Two' : [4,5,6], 'Three' : [7,8,9]}, index=list('ABC'))  
>>> df2
```  


| | One | Two | Three
|-|:---:|:---:|:-----:
A | 1	| 4 | 7
B |	2	| 5	| 8
C |	3	| 6	| 9


```Python
# 넘파이 배열로 데이터프레임 생성
>>> df3 = pd.DataFrame({'One' : np.random.randint(10, size=3),
                   'Two' : np.random.randint(20, size=3),
                   'Three' : np.random.randint(30, size=3)}, index=list('ABC'))  
>>> df3
```   


| | One | Two | Three
|- |:---:|:---:|:-----:
A | 8 | 19 | 3
B |	4	| 14 | 12
C | 6 | 0	| 19

```Python  
# 시리즈로 데이터프레임 생성(s1)
>>> s1 = pd.Series(np.random.randint(10, size=4), index=list('ABCD'))
>>> s1
```  

```
A    0  
B    0  
C    2  
D    6  
dtype: int64
```

```Python
# 시리즈로 데이터프레임 생성(s2)
>>> s2 = pd.Series(np.random.randint(20, size=4), index=list('ABCD'))
>>> s2
```  

```
A     4  
B    16  
C     0  
D    17  
dtype: int64  
```

```Python
>>> df4 = pd.DataFrame({'One' : s1 , 'Two' : s2})  
>>> df4
```

| | One | Two
|-|:---:|:---:
A | 0	| 4
B |	0	| 16
C |	2	| 0
D | 6 | 17



## 2. 데이터 출력  

행과 열의 길이가 긴 데이터프레임이 있다고 하자.  

<img width="1091" alt="0-2" src="https://user-images.githubusercontent.com/43739827/74827138-38950200-5350-11ea-99ec-770591771c1b.png"></img>  

```Python
# 위에서 5개의 행 출력(매개변수의 기본값이 5이다.)
>>> df.head()
```  

<img width="517" alt="0-3" src="https://user-images.githubusercontent.com/43739827/74827693-2b2c4780-5351-11ea-9541-b5880bef8751.png"></img>  

```Python
# 아래에서 7개의 행 출력
>>> df.tail(7)
```    

<img width="573" alt="0-4" src="https://user-images.githubusercontent.com/43739827/74827973-a1c94500-5351-11ea-9fa6-0c0c0f24371c.png"></img>  

```Python
# 행의 레이블 확인
>>> df.index
```  

```
RangeIndex(start=0, stop=3668, step=1)
```  

```Python
# 열의 레이블 확인
>>> df.columns
```  

```
Index(['home_team', 'away_team', 'home_goals', 'away_goals', 'result','season'],
      dtype='object')
```  

**DataFrame.to_numpy** 메소드는 데이터프레임의 데이터를 넘파이 모듈의 ndarray로 반환하여 보여준다. 각 열마다의 값의 자료형이 다르다면 수행시간이 전부 동일한 자료형을 가지는 데이터프레임보다 오래 걸리게 된다.  

```Python
>>> df.head(3).to_numpy()
```  

```
array([['TottenhamHotspur', 'ManchesterCity', 0, 0, 'D', '2010-2011'],
       ['AstonVilla', 'WestHamUnited', 3, 0, 'H', '2010-2011'],
       ['BlackburnRovers', 'Everton', 1, 0, 'H', '2010-2011']],
      dtype=object)
```  

```Python
>>> df2 = pd.DataFrame({'One' : [1,2,3], 'Two' : [4,5,6], 'Three' : [7,8,9], 'Four' : [10,11,12],
 'Five' : [13,14,15], 'Six' : [16,17,18]})  

>>> df2.to_numpy()
```  

```
array([[ 1,  4,  7, 10, 13, 16],
       [ 2,  5,  8, 11, 14, 17],
       [ 3,  6,  9, 12, 15, 18]])  
```  
> **DataFrame.to_numpy()** 메소드의 출력결과는 행과 열의 레이블을 포함하지 않는다.  


**describe** 메소드는 데이터프레임의 간략한 통계 수치를 확인할 때 사용한다.  

```Python
>>> df.describe()
```  

 | | home_goals | away_goals  
 |-|:----------:|:----------:  
 count| 3668.000000 | 3668.000000  
 mean | 1.551799 | 1.198201  
 std  | 1.297052 | 1.169668  
 min  | 0.000000 | 0.000000  
 25%  | 1.000000 | 1.000000  
 50%  | 1.000000 | 1.000000  
 75%  | 2.000000 | 2.000000  
 max  | 8.000000 | 9.000000  

데이터프레임 뒤에 **T** 메소드를 입력하면 전치(Transpose)하게 된다.  

 | | count | mean | std | min | 25% | 50% | 75% | max
 |-|:-----:|:----:|:---:|:---:|:---:|:---:|:---:|:---:  
 home_goals | 3668.0 | 1.551799 | 1.297052 | 0.0 | 1.0 | 1.0 | 2.0 | 8.0  
 away_goals | 3668.0 | 1.198201 | 1.169668 | 0.0 | 0.0 | 1.0 | 2.0 | 9.0  


데이터프레임의 행/열의 인덱스 레이블을 정렬하고자 한다면 **sort_index** 메소드를 사용한다. 매개변수로 axis=1은 열, axis=0은 행의 레이블을 정렬하고 ascending은 오름차순 혹은 내림차순을 지정한다.  

```Python  
# 열의 레이블 정렬(내림차순)
>>> df2.sort_index(axis=1, ascending=False)
```  

 | | Two | Three | Six | One | Four | Five  
 |-|:---:|:-----:|:---:|:---:|:----:|:----:  
 0 | 4 | 7 | 16 | 1 | 10 | 13  
 1 | 5 | 8 | 17 | 2 | 11 | 14  
 2 | 6 | 9 | 18 | 3 | 12 | 15  

```Python
# 열의 레이블 정렬(오름차순)
>>> df2.sort_index(axis=1, ascending=True)
```  

 | | Five | Four | One | Six | Three | Two  
 |-|:----:|:----:|:---:|:---:|:-----:|:----:  
 0 | 13 | 10 | 1 | 16 | 7 | 4  
 1 | 14 | 11 | 2 | 17 | 8 | 5  
 2 | 15 | 12 | 3 | 18 | 9 | 6  


```Python  
>>> df3 = pd.DataFrame({'A' : [1,2,3,4], 'B' : [5,6,7,8]}, index=list('DACB'))  
>>> df3
```  

 | | A | B  
 |-|:-:|:-:  
 D | 1 | 5  
 A | 2 | 6  
 C | 3 | 7  
 B | 4 | 8  

```Python  
# 행의 레이블 정렬(내림차순)
>>> df3.sort_index(axis=0, ascending=False)
```  

 | | A | B  
 |-|:-:|:-:  
 D | 1 | 5  
 C | 3 | 7  
 B | 4 | 8  
 A | 2 | 6  

```Python
# 행의 레이블 정렬(오름차순)
>>> df3.sort_index(axis=0, ascending=True)
```  

| | A | B  
|-|:-:|:-:  
A | 2 | 6  
B | 4 | 8  
C | 3 | 7  
D | 1 | 5  


```Python
# 시리즈의 행 레이블 정렬
>>> series = pd.Series(np.random.randint(5, size=3), index=list('BAC'))  
>>> series.sort_index(axis=0)
```

```
A    3  
B    3  
C    3  
dtype: int64
```  

특정한 열의 값을 기준으로 정렬하고 싶다면 **.sort_values** 사용한다. 매개변수로 **by=<지정할 열>** 을 기입하면 그 열을 기준으로 한다.  

```Python
# home_team열의 값들을 기준으로 정렬(기본값: 오름차순)
>>> df.sort_values(by='home_team').head()
```

 | | home_team | away_team | home_goals | away_goals | result | season  
 |-|:---------:|:---------:|:----------:|:----------:|:------:|:------:  
 2529 | AFC Bournemouth | Manchester City | 0 | 2 | A | 2016-2017  
 2808 | AFC Bournemouth | Southampton | 1 | 1 | D | 2017-2018  
 1952 | AFC Bournemouth | Sunderland | 2 | 0 | H | 2015-2016  
 2352 | AFC Bournemouth | Hull City | 6 | 1 | H | 2016-2017  
 3080 | AFC Bournemouth | Leicester City | 4 | 2 | H | 2018-2019  


```Python  
# home_team열의 값들을 기준으로 내림차순 정렬
>>> df.sort_values(by='home_team', ascending=False).head()
```  
 | | home_team | away_team | home_goals | away_goals | result | season  
 |-|:---------:|:---------:|:----------:|:----------:|:------:|:------:  
 685 | Wolverhampton Wanderers | Bolton Wanderers | 2 | 3 | A | 2011-2012  
 517 | Wolverhampton Wanderers | Sunderland | 2 | 1 | H | 2011-2012  
 3267 | Wolverhampton Wanderers | Leicester City | 4 | 3 | H | 2018-2019  
 3275 | Wolverhampton Wanderers | West Ham United | 3 | 0 | H | 2018-2019  
 533 | Wolverhampton Wanderers | Stoke City | 1 | 2 | A | 2011-2012  


## 3. 선택  

데이터프레임에서 하나의 열을 선택하여 출력하면 1차원의 시리즈로 반환된다.  

```Python
>>> df2['One']
```  

```
0    1  
1    2  
2    3  
Name: One, dtype: int64
```  

```Python
>>> df2.One
```  

```
0    1  
1    2  
2    3  
Name: One, dtype: int64
```  

**[ ]** 를 이용한 검색으로 행을 추출할 수 있다.  

```Python
>>> df3
```  

 | | A | B  
 |-|:-:|:-:  
 D | 1 | 5  
 A | 2 | 6  
 C | 3 | 7  
 B | 4 | 8  

```Python
# 행의 포지션으로 검색  
>>> df3[0:2]
```  

 | | A | B  
 |-|:-:|:-:  
 D | 1 | 5  
 A | 2 | 6  

```Python  
# 행의 레이블로 검색
>>> df3['A':'B']
```  

 | | A | B  
 |-|:-:|:-:  
 A | 2 | 6  
 C | 3 | 7  
 B | 4 | 8  

* 레이블 선택  
**.loc** 속성은 행의 레이블을 명시하여 데이터를 추출하는 기능을하고 있으며, 레이블의 이름을 모른다면 검색할 수 없다는 단점이 있다. 또한 [ ]안에 [행의 레이블, 열의 레이블]순으로 기입하면 해당하는 위치의 데이터를 출력한다.

```Python  
>>> df3.loc['D']
```

```
A    1  
B    5  
Name: D, dtype: int64
```  

```Python
>>> df3.loc['D','A']
```

```
1
```  

**.iloc** 속성은 loc처럼 [ ]안에 행과 열의 정보를 기입하면 해당하는 데이터를 출력하는 기능을 가지고 있지만 레이블을 기입하는것이 아닌 위치를 기입하여 정보를 얻어온다는 차이점이 있다.  

```Python  
>>> df3.iloc[1]
```

```
A    2  
B    6  
Name: A, dtype: int64
```  

```Python  
>>> df3.iloc[0:2, 0]
```

```
D    1   
A    2  
Name: A, dtype: int64
```

파이썬의 리스트 형태로 행과 열의 위치를 입력해도 해당하는 정보들을 출력한다.  

```Python
>>> df.iloc[[0,2],[0,4]]
```

 | | home_team | result  
 |-|:---------:|:------:  
 0 | Tottenham Hotspur | D  
 2 | Blackburn Rovers  | H  

.iloc은 행의 위치정보로 데이터를 추출하기 때문에 가장 마지막행의 열의 레이블을 모르는 상태에서 데이터를 얻고자 한다면 **[-1]** 을 기입한다.  

```Python
>>> df.iloc[-1]
```  

```
home_team           ManchesterUnited  
away_team     WolverhamptonWanderers  
home_goals                         0  
away_goals                         0  
result                             D  
season                           NaN  
Name: 3667, dtype: object
```  


* 논리 인덱싱(Boolean Indexing)  

데이터프레임의 [ ]안에 특정한 하나의 열에대한 조건식을 설정한다면 그 조건에 참인 요소의 행을 출력한다.  

```Python
>>> df3[df3['A'] > 2]
```  

 | | A | B  
 |-|:-:|:-:  
 C | 3 | 7  
 B | 4 | 8  

데이터프레임의 [ ]안에 데이터프레임 전체에 대한 조건식을 설정한다면 그 조건에 참인 요소들은 그대로 출력하고 거짓인 요소들은 누락값인 NaN으로 채워진다.  

```Python
>>> df3[df3 > 2]
```  

| | A | B  
|-|:-:|:-:  
D | NaN | 5  
A | NaN | 6
C | 3.0 | 7  
B | 4.0 | 8  
> NaN의 자료형이 **float64** 이기때문에 해당열의 자료형이 float64로 바뀐것을 확인할 수 있다.  

**isin** 메소드는 필터링을 하는 역할을 하며 ()안에 찾을 데이터값을 기입한다.  

```Python
>>> df[df['result'].isin(['H','A'])].head()
```

 | | home_team | away_team | home_goals | away_goals | result | season  
 |-|:---------:|:---------:|:----------:|:----------:|:------:|:------:  
 1 | Aston Villa | West Ham United | 3 | 0 | H | 2010-2011  
 2 | Blackburn Rovers | Everton | 1 | 0 | H | 2010-2011  
 5 | Wigan Athletic | Blackpool | 0 | 4 | A | 2010-2011  
 6 | Wolverhampton Wanderers | Stoke City | 2 | 1 | H | 2010-2011  
 7 | Chelsea | West Bromwich Albion | 6 | 0 | H | 2010-2011  


* 설정  
데이터프레임에 열을 추가하거나 전체적으로 값들을 바꾸는 것이 가능하다.  

```Python  
# 데이터프레임 생성
>>> df = pd.DataFrame({'One' : [1,2,3,4,5], 'Two' : [6,7,8,9,10]})
>>> df
```

 | | One | Two  
 |-|:---:|:---:  
 0 | 1 | 6  
 1 | 2 | 7  
 2 | 3 | 8  
 3 | 4 | 9  
 4 | 5 | 10  

```Python
# 시리즈 생성
>>> series = np.random.randint(50, size=5)
>>> series
```

```
array([47,  4, 35,  6, 28])
```  

```Python
# 시리즈를 데이터프레임의 새로운 열로 추가
>>> df['Three'] = series  
>>> df
```  

 | | One | Two | Three  
 |-|:---:|:---:|:-----:  
 0 | 1 | 6 | 47   
 1 | 2 | 7 | 4  
 2 | 3 | 8 | 35  
 3 | 4 | 9 | 6  
 4 | 5 | 10 | 28  

```Python
# 특정 열의 전체 데이터값 변경
>>> df.loc[:, 'Two'] = np.array(np.random.randint(100,size=5))
>>> df
```  

| | One | Two | Three  
|-|:---:|:---:|:-----:  
0 | 1 | 1 | 47   
1 | 2 | 85 | 4  
2 | 3 | 51 | 35  
3 | 4 | 5 | 6  
4 | 5 | 71 | 28  

```Python  
# 특정 조건에 의한 데이터프레임 내부 값 변경
>>> df[df > 5] = -df
>>> df
```
| | One | Two | Three  
|-|:---:|:---:|:-----:  
0 | 1 | 1 | -47   
1 | 2 | -85 | 4  
2 | 3 | -51 | -35  
3 | 4 | 5 | -6  
4 | 5 | -71 | -28  

## 4. 누락값

판다스에서는 누락값을 나타내는 표현으로 **np.nan** 을 사용한다. 이 누락값은 해당 열 혹은 행의 연산시에 무시된다.  

```Python
>>> df = pd.DataFrame(data=[[1,2,np.nan],[3,np.nan,4]])
>>> df
```

 | | 0 | 1 | 2  
 |-|:-:|:-:|:-:  
 0 | 1 | 2.0| NaN  
 1 | 3 | NaN | 4.0  

```Python
>>> df[0].sum()
```

```
4
```

```Python
>>> df[1].sum()
```

```
2.0
```

```Python
>>> df[2].sum()
```

```
4.0
```  

특정한 축의 인덱스를 변경/추가/삭제하게되면 그 인덱스의 값은 누락값으로 채워지게 된다.  

인덱스에 추가작업을 하는 메소드는 **reindex** 메소드로, 매개변수는 index와 columns를 사용해 축의 레이블을 설정할 수 있다.  

```Python
>>> df1 = df.reindex(index=np.arange(5))  
>>> df1
```

 | | 0 | 1 | 2  
 |-|:-:|:-:|:-:  
 0 | 1.0 | 2.0 | NaN  
 1 | 3.0 | NaN | 4.0  
 2 | NaN | NaN | NaN  
 3 | NaN | NaN | NaN  
 4 | NaN | NaN | NaN  

누락값을 가지는 행을 삭제하고자 한다면 **dropna** 메소드를 사용한다.  

```Python
>>> df1.dropna(how='any')
```   

 | | 0 | 1 | 2  
 |-|:-:|:-:|:-:  

누락값을 지정한 값으로 채우고자 한다면 **.fillna** 메소드를 사용하며 매개변수로 **value=n** 을 기입하여 채워질 특정 값을 지정할 수 있다.  

```Python
>>> df1.fillna(value=10)
```

 | | 0 | 1 | 2  
 |-|:-:|:-:|:-:  
 0 | 1.0 | 2.0 | 10.0  
 1 | 3.0 | 10.0 | 4.0  
 2 | 10.0 | 10.0 | 10.0  
 3 | 10.0 | 10.0 | 10.0  
 4 | 10.0 | 10.0 | 10.0  

데이터프레임의 요소들이 누락값인지를 불리언값으로 확인하고자 한다면 **pd.isna** 를 사용하여 괄호안에 확인할 데이터프레임명을 기입한다.   

```Python
>>> pd.isna(df1)
```

 | | 0 | 1 | 2  
 |-|:-:|:-:|:-:  
 0 | False | False | True  
 1 | False | True | False  
 2 | True | True | True  
 3 | True | True | True  
 4 | True | True | True  

## 5.연산  

1. 통계(Stats)  
일반적으로 연산을 수행할때 누락값은 예외처리한다.  

산술통계를 처리하는 메소드는 **mean** 를 사용한다. 기본적으로는 열을 기준으로 계산하고 ( )안에 1을 기입하면 행을 기준으로 계산한다.  

```Python  
>>> df = pd.DataFrame({'One' : np.random.randint(20, size=4), 'Two' : np.random.randn(4)},  
                 index=list('ABCD'))  
>>> df
```

 | | One | Two  
 |-|:---:|:---:  
 A | 17 | -0.777915  
 B | 19 | -1.434760  
 C | 2 | 0.921095  
 D | 14 | 0.263641  

```Python
>>> df.mean()
```

```
One    13.000000  
Two    -0.256985  
dtype: float64  
```

```Python
>>> df.mean(1)
```

```
A    8.111043  
B    8.782620  
C    1.460547  
D    7.131821  
dtype: float64   
```  

시리즈와 데이터프레임의 연산을 수행하게되면 판다스는 자동적으로 시리즈를 데이터프레임의 크기에 맞게 브로드캐스팅한다. 만약 시리즈나 데이터프레임에 누락값이 들어있다면 그 데이터의 연산결과는 무조건 누락값이다.  

```Python
# 시리즈와 데이터프레임에 사용할 인덱스 생성(시계열)
>>> t_idx = pd.date_range('2020-01-01', periods=5)  
>>> t_idx
```  

```
DatetimeIndex(['2020-01-01', '2020-01-02', '2020-01-03', '2020-01-04',
               '2020-01-05'],
              dtype='datetime64[ns]', freq='D')
```

```Python
# 시계열 인덱스를 사용하여 5개의 난수를 가지는 시리즈를 생성.
>>> series = pd.Series(np.random.randint(20, size=5), index=t_idx)  
>>> series
```  

```
2020-01-01    17  
2020-01-02    16  
2020-01-03    18  
2020-01-04     6  
2020-01-05     9  
Freq: D, dtype: int64
```  

```Python
# 시리즈의 요소들을 우측으로 1씩 이동
>>> series = series.shift(1)  
>>> series
```  

```
2020-01-01     NaN  
2020-01-02    17.0  
2020-01-03    16.0  
2020-01-04    18.0  
2020-01-05     6.0  
Freq: D, dtype: float64  
```

```Python
# 시계열 인덱스를 가지는 5X2 크기의 데이터프레임을 생성
>>> df = pd.DataFrame({ 'A' : np.random.randn(5), 'B' : np.random.randn(5)}, index=t_idx)  
>>> df
```  

 | | A | B  
 |-|:-:|:-:  
 2020-01-01 | -0.243296 | 0.370846  
 2020-01-02 | -0.320402 | 0.566230  
 2020-01-03 | 0.680802 | -0.485805  
 2020-01-04 | 0.376472 | -1.527842  
 2020-01-05 | -0.404380 | -0.372984  

```Python
# 행을 기준으로 시리즈와 데이터프레임의 차(subtraction)를 구함.
>>> df.sub(series, axis='index')
```  

 | | A | B  
 |-|:-:|:-:  
 2020-01-01 | NaN | NaN  
 2020-01-02 | -17.320402 | -16.433770  
 2020-01-03 | -15.319198 | -16.485805  
 2020-01-04 | -17.623528 | -19.527842  
 2020-01-05 | -6.404380 | -6.372984

```Python  
# 열을 기준으로 시리즈와 데이터프레임의 차(subtraction)를 구함.
>>> df.sub(series, axis='columns')
```  

<img width="789" alt="0-6" src="https://user-images.githubusercontent.com/43739827/74929957-efac7e80-541f-11ea-9d75-0db33339d8dd.png"></img>  

2. 적용(Apply)  
**apply** 메소드를 사용하여 시리즈나 데이터프레임의 값들을 변결할 수 있다.  

```Python  
>>> df.apply(np.sum)
```  

```
A    0.089196  
B   -1.449555  
dtype: float64  
```  

```Python  
>>> df.apply(lambda x : x * 1000)
```  

 | | A | B  
 |-|:-:|:-:  
 2020-01-01 | -243.296000 | 370.845837  
 2020-01-02 | -320.401912 | 566.229513  
 2020-01-03 | 680.802131 | -485.804716  
 2020-01-04 | 376.472100 | -1527.841624  
 2020-01-05 | -404.380176 | -372.984363  

3. 중복값 개수 찾기  

```Python  
>>> series2 = pd.Series(np.random.randint(2, 20, size=10))
>>> series2
```  

```
0     2  
1    16  
2    19  
3     6  
4    16  
5     7  
6     6  
7     4  
8    12  
9     5  
dtype: int64  
```  

```Python
>>> series2.value_counts()
```  

```
6     2  
16    2  
12    1  
7     1  
5     1  
4     1  
19    1  
2     1  
dtype: int64  
```  

4. 문자열 연산(String Methods)  
시리즈의 속성중 **str** 은 문자열 요소간의 연산을 편하게해주는 기능을 하고있다.  

```Python  
>>> s = pd.Series(['Ss','Aa','Bb','Cc',np.nan,'Ff','AbCdEfG'])
>>> s
```  

```
0         Ss  
1         Aa  
2         Bb  
3         Cc  
4        NaN  
5         Ff  
6    AbCdEfG  
dtype: object  
```  

```Python
# 문자열 요소 소문자로 변환
>>> s.str.lower()
```  

```
0         ss   
1         aa  
2         bb  
3         cc  
4        NaN  
5         ff  
6    abcdefg  
dtype: object  
```  

```Python
# 문자열 요소 대문자로 변환
>>> s.str.upper()
```  

```
0         SS  
1         AA  
2         BB  
3         CC  
4        NaN  
5         FF  
6    ABCDEFG  
dtype: object  
```  

## 6.병합(Merge)  

1. 연결(Concat, Concatenate)  

```Python
# 열을 기준으로 시리즈와 데이터프레임을 연결(default axis=0)
>>> pd.concat([df, series])
```  

 | | A | B | 0  
 |-|:-:|:-:|:-:
2020-01-01 | -0.243296 | 0.370846 | NaN  
2020-01-02 | -0.320402 | 0.566230 | NaN  
2020-01-03 | 0.680802 | -0.485805 | NaN  
2020-01-04 | 0.376472 | -1.527842 | NaN  
2020-01-05 | -0.404380 | -0.372984 | NaN  
2020-01-01 | NaN | NaN | NaN  
2020-01-02 | NaN | NaN | 17.0  
2020-01-03 | NaN | NaN | 16.0  
2020-01-04 | NaN | NaN | 18.0  
2020-01-05 | NaN | NaN | 6.0  

```Python  
# 행을 기준으로 시리즈와 데이터프레임을 연결
>>> pd.concat([df, series], axis=1)
```  

 | | A | B | 0  
 |-|:-:|:-:|:-:  
 2020-01-01 | -0.243296 | 0.370846 | NaN  
 2020-01-02 | -0.320402 | 0.566230 | 17.0  
 2020-01-03 | 0.680802 | -0.485805 | 16.0  
 2020-01-04 | 0.376472 | -1.527842 | 18.0  
 2020-01-05 | -0.404380 | -0.372984 | 6.0  

> 데이터프레임에 열을 추가하는것은 행을 추가하는것에비해 상대적으로 빠르다. 행을 추가하고자 하면 데이터프레임의 사본을 만들어 그 사본에 작업을 하기 때문이다. 그렇기때문에 행을 계속 추가하면서 데이터프레임을 구축하기보다는 미리 행을 만들어놓고 추가적으로 값을 갱신하는것이 좋은 방법이다.  

2. Join  
Sql문 형식의 병합을 나타낸다. **merge** 메소드를 사용하며 매개변수로 합칠 데이터프레임의 이름들을 입력하고 **on="기준이되는 열"** 을 입력한다.  

```Python
>>> df = pd.DataFrame({'main' : [1,2,3,4,5], 'PlusOne' : [2,3,4,5,6]})
>>> df
```

 | | main | PlusOne  
 |-|:----:|:-------:  
0 | 1 | 2  
1 | 2 | 3  
2 | 3 | 4  
3 | 4 | 5  
4 | 5 | 6  

```Python
>>> df2 = pd.DataFrame({'main' : [1,2,3,4,5], 'Abs' : [1,4,9,16,25]})
>>> df2
```  

 | | main | Abs  
 |-|:----:|:---:  
 0 | 1 | 1  
 1 | 2 | 4  
 2 | 3 | 9  
 3 | 4 | 16  
 4 | 5 | 25  

```Python  
>>> pd.merge(df, df2, on='main')
```  
 | | main | PlusOne | Abs  
 |-|:----:|:-------:|:---:  
 0 | 1 | 2 | 1  
 1 | 2 | 3 | 4  
 2 | 3 | 4 | 9  
 3 | 4 | 5 | 16  
 4 | 5 | 6 | 25  
> key가 되는 열은 두 데이터프레임이 동일한 데이터를 가지고 있어야한다.  


## 7.그룹화(Grouping)  

그룹화를 하기 위해선 아래 3가지의 처리과정준 하나 이상을 따른다.  

1. 임의의 기준에 맞추어 데이터를 몇가지로 나눈다.  
2. 각 그룹에 독립적으로 함수를 적용시킨다.  
3. 연산된 결과들을 하나로 합친다.  

```Python  

# 데이터프레임 생성
>>> df = pd.DataFrame({'Club' : ['Real Madrid', 'FC Barcelona','Real Madrid', 'FC Barcelona', 'Real Madrid', 'FC Barcelona', 'Real Madrid', 'FC Barcelona'],
                  'Number' : [4, 4, 7, 8, 10, 10, 11, 11],
                  'Name' : ['Sergio Ramos','Ivan Rakitic','Eden Hazard','Arthur','Luka Modric','Lionel Messi','Gareth Bale','Ousmane Dembele'],
                  'Country' : ['Spain', 'Croatia','Belgium', 'Brazil', 'Croatia' , 'Argentina' ,'Wales', 'France']})  
>>> df

```  

 | | Club | Number | Name | Country  
 |-|:----:|:------:|:----:|:-------:  
 0 | Real Madrid | 4 | Sergio Ramos | Spain  
 1 | FC Barcelona | 4 | Ivan Rakitic | Croatia  
 2 | Real Madrid | 7 | Eden Hazard | Belgium  
 3 | FC Barcelona | 8 | Arthur | Brazil  
 4 | Real Madrid | 10 | Luka Modric | Croatia  
 5 | FC Barcelona | 10 | Lionel Messi | Argentina  
 6 | Real Madrid | 11 | Gareth Bale | Wales  
 7 | FC Barcelona | 11 | Ousmane Dembele  

```Python
# 특정한 열을 기준으로 그룹화하여 조건에맞는 개수(count)를 찾음
>>> df.groupby('Number').count()
```  
<img width="207" alt="0-7" src="https://user-images.githubusercontent.com/43739827/75029494-7bd4a980-54e5-11ea-968d-0a0623a9e819.png"></img>  

```Python
# 특정한 두 개의 열을 기준으로 그룹화하여 조건에맞는 개수(count)를 찾음
>>> df.groupby(['Number','Country']).count()
```

<img width="219" alt="0-8" src="https://user-images.githubusercontent.com/43739827/75029656-d110bb00-54e5-11ea-8ac1-004de96f3c69.png"></img>  

## 8.재구조화(Reshaping)  

* 스택(Stack)  
**스택** 은 다차원의 데이터프레임으로부터 열의 차원을 1차원 줄인다.  

```Python
>>> # 멀티인덱스로 지정하기위한 튜플 생성
idx = list(zip(*[['Manchester United', 'Manchester United', 'Manchester City', 'Manchester City',
                 'Liverpool','Liverpool','Chelsea','Chelsea'],
                 ['home_goals','away_goals','home_goals','away_goals',
                  'home_goals','away_goals','home_goals','away_goals']]))

>> idx
```

```
[('Manchester United', 'home_goals'),  
 ('Manchester United', 'away_goals'),  
 ('Manchester City', 'home_goals'),  
 ('Manchester City', 'away_goals'),  
 ('Liverpool', 'home_goals'),  
 ('Liverpool', 'away_goals'),  
 ('Chelsea', 'home_goals'),  
 ('Chelsea', 'away_goals')]  
```

```Python
# 인덱스를 멀티인덱스로 변환
>>> m_idx = pd.MultiIndex.from_tuples(idx, names=['Club','Goals'])  
>>> m_idx
```  

```
MultiIndex([('Manchester United', 'home_goals'),  
            ('Manchester United', 'away_goals'),  
            (  'Manchester City', 'home_goals'),  
            (  'Manchester City', 'away_goals'),  
            (        'Liverpool', 'home_goals'),  
            (        'Liverpool', 'away_goals'),  
            (          'Chelsea', 'home_goals'),  
            (          'Chelsea', 'away_goals')],  
           names=['Club', 'Goals'])  
```

```Python  
>>> df2 = pd.DataFrame({'September' : np.random.randint(8, size=8),
                   'October' : np.random.randint(8, size=8)}, index=m_idx)  

>>> df2
```  

<img width="346" alt="0-9" src="https://user-images.githubusercontent.com/43739827/75031559-e1c33000-54e9-11ea-9926-8b41e29002fd.png"></img>  

```Python  
>>> s_df = df2.stack()  
>>> s_df
```  

```
Club               Goals                
Manchester United  home_goals  September    3  
                               October      4  
                   away_goals  September    1  
                               October      3  
Manchester City    home_goals  September    5  
                               October      2  
                   away_goals  September    4  
                               October      6  
Liverpool          home_goals  September    6  
                               October      2  
                   away_goals  September    3  
                               October      7  
Chelsea            home_goals  September    1  
                               October      6  
                   away_goals  September    7  
                               October      6  
dtype: int64  
```  

스택처리된 데이터프레임이나 시리즈를 되돌리는 연산으로 **unstack** 메소드가 있다. 매개변수로 unstack할 인덱스의 레벨을 기입할 수 있으며 default값은 -1이다.  

```Python  
>>> s_df.unstack()
```  
<img width="346" alt="0-10" src="https://user-images.githubusercontent.com/43739827/75032601-45e6f380-54ec-11ea-90ae-c386fa049acf.png"></img>  

```Python  
>>> s_df.unstack(1)
```
<img width="363" alt="0-11" src="https://user-images.githubusercontent.com/43739827/75032661-6adb6680-54ec-11ea-9393-399ab7ef6f6b.png"></img>  

```Python  
>>> s_df.unstack(0)
```  

<img width="517" alt="0-12" src="https://user-images.githubusercontent.com/43739827/75032718-8e061600-54ec-11ea-8454-4096edec6ee7.png"></img>  

```Python  
>>> s_df.unstack(-1)
```  

<img width="345" alt="0-13" src="https://user-images.githubusercontent.com/43739827/75032764-b261f280-54ec-11ea-9015-af0f5bd2ae47.png"></img>  

* 피벗 테이블(Pivot table)  

피벗 테이블이란 테이블에서 필요한 데이터만을 추출하여 새로운 테이블로 만드는 것이다.  

```Python  
>>> f3 = pd.DataFrame({'Country' : ['Korea', 'Japan','China'] * 4,  
                    'Part' : ['P1', 'P2', 'P3', 'P4'] * 3,  
                    'Boolean' : ['Y','Y','Y','F','F','F'] * 2 ,  
                    'In' : np.random.randn(12),  
                    'Out' : np.random.randn(12)})  
>>> df3
```

 | | Country | Part | Boolean | In | Out  
 |-|:-------:|:----:|:-------:|:--:|:---:  
 0 | Korea | P1 | Y | 0.705770 | 0.170821  
 1 | Japan | P2 | Y | 0.012764 | -0.956052  
 2 | China | P3 | Y | 2.047783 | 0.868328  
 3 | Korea | P4 | F | -0.212842 | 0.106059  
 4 | Japan | P1 | F | 1.487557 | 1.054390  
 5 | China | P2 | F | 0.175353 | -1.497004  
 6 | Korea | P3 | Y | 2.002593 | 0.881311  
 7 | Japan | P4 | Y | -0.306823 | -1.569362  
 8 | China | P1 | Y | 0.231235 | -1.525929  
 9 | Korea | P2 | F | 0.795160 | 0.385938  
 10 | Japan | P3 | F | -1.353346 | -0.596935  
 11 | China | P4 | F | 0.758078 | -1.077861  

```Python  
>>> pd.pivot_table(df3, values='In', index=['Country','Part'], columns='Boolean')
```

<img width="259" alt="0-14" src="https://user-images.githubusercontent.com/43739827/75033784-01a92280-54ef-11ea-96a9-0e0c60ffaea2.png"></img>  

## 9.시계열(Time series)  

```Python
# 시계열 인덱스생성('일'을 주기로 함)
>>> t_idx = pd.date_range('2020-02-22', periods=10, freq='D')  
>>> t_idx
```

```
DatetimeIndex(['2020-02-22', '2020-02-23', '2020-02-24', '2020-02-25',  
               '2020-02-26', '2020-02-27', '2020-02-28', '2020-02-29',  
               '2020-03-01', '2020-03-02'],  
              dtype='datetime64[ns]', freq='D')  
```

```Python
# 시계열 인덱스를 가지는 시리즈를 생성
>>> series = pd.Series(np.random.randn(10),index=t_idx)  
>>> series
```  

```
2020-02-22    1.063848  
2020-02-23   -0.668893  
2020-02-24   -1.695963  
2020-02-25    1.627277  
2020-02-26    0.056666  
2020-02-27    1.745010  
2020-02-28    0.154179  
2020-02-29    2.486828  
2020-03-01   -0.342484  
2020-03-02   -1.869945  
Freq: D, dtype: float64  
```

```Python  
# 3일을 주기로 값들을 합을 계산하여 새로운 시리즈를 반환
>>> series.resample('3D').sum()
```  

```
2020-02-22   -1.301008  
2020-02-25    3.428952  
2020-02-28    2.298523  
2020-03-02   -1.869945  
Freq: 3D, dtype: float64  
```  

**tz_localize** 메소드를 사용하여 특정 지역의 시간대로 시계열 데이터를 지정할 수 있다.  

```Python  
>>> local = series.tz_localize('CET')  
>>> local
```  

```
2020-02-22 00:00:00+01:00    1.063848  
2020-02-23 00:00:00+01:00   -0.668893  
2020-02-24 00:00:00+01:00   -1.695963  
2020-02-25 00:00:00+01:00    1.627277  
2020-02-26 00:00:00+01:00    0.056666  
2020-02-27 00:00:00+01:00    1.745010  
2020-02-28 00:00:00+01:00    0.154179  
2020-02-29 00:00:00+01:00    2.486828   
2020-03-01 00:00:00+01:00   -0.342484  
2020-03-02 00:00:00+01:00   -1.869945  
Freq: D, dtype: float64  
```

위치가 지정되어버린 시계열 데이터의 시간장소를 바꾸고자 한다면 **tz_convert** 메소드를 사용하여 변경할 수 있다.  

```Python  
>>> local.tz_convert('Asia/Seoul')
```

```
2020-02-22 08:00:00+09:00    1.063848  
2020-02-23 08:00:00+09:00   -0.668893  
2020-02-24 08:00:00+09:00   -1.695963  
2020-02-25 08:00:00+09:00    1.627277  
2020-02-26 08:00:00+09:00    0.056666  
2020-02-27 08:00:00+09:00    1.745010  
2020-02-28 08:00:00+09:00    0.154179  
2020-02-29 08:00:00+09:00    2.486828  
2020-03-01 08:00:00+09:00   -0.342484  
2020-03-02 08:00:00+09:00   -1.869945  
Freq: D, dtype: float64  
```

생성되있는 시계열의 시간범위를 변경할 수 있다.  

```Python  
>>> t_idx2 = pd.date_range('2020-01-20', periods=7, freq='Y')  
>>> t_idx2  
```

```
DatetimeIndex(['2020-12-31', '2021-12-31', '2022-12-31', '2023-12-31',  
               '2024-12-31', '2025-12-31', '2026-12-31'],  
              dtype='datetime64[ns]', freq='A-DEC')  
```

```Python
# 시계열의 주기를 파악하여 그 주기만을 잘라내는 메소드
>>> ps = t_idx2.to_period()
>>> ps
```  

```
PeriodIndex(['2020', '2021', '2022', '2023', '2024', '2025', '2026'], dtype='period[A-DEC]', freq='A-DEC')
```

```Python
# 주기에 맞는 시작하는 때를 값으로 갖도록 하는 메소드
>>> ps.to_timestamp()
```

```
DatetimeIndex(['2020-01-01', '2021-01-01', '2022-01-01', '2023-01-01',  
               '2024-01-01', '2025-01-01', '2026-01-01'],  
              dtype='datetime64[ns]', freq='AS-JAN')  
```

## 10.범주형(Categoricals)  

**범주형** 이란 특정 기준을 가지고 반복되는 자료형이다.  

```Python  
>>> df = pd.DataFrame({'A' : ['Red', 'Blue', 'Black', 'White', 'Green', 'Indigo', 'Purple'],
                  'B' : ['x','x','y','y','z','z','z']})  
>>> df
```

 | | A | B  
 |-|:-:|:-:  
 0 | Red | x  
 1 | Blue | x  
 2 | Black | y  
 3 | White | y  
 4 | Green | z  
 5 | Indigo | z  
 6 | Purple | z  

```Python  
>>> df['Value'] = df['B'].astype('category')  
>>> df['Value']
```  

```
0    x  
1    x  
2    y  
3    y  
4    z  
5    z  
6    z  
Name: Value, dtype: category  
Categories (3, object): [x, y, z]
```  

범주형 데이터들의 이름을 좀 더 의미를 가지는 이름으로 변경할 수도 있다.  

```Python  
>>> df['Value'].cat.categories = ['Good', 'Normal', 'Bad']  
>>> df['Value']
```  

```
0      Good  
1      Good  
2    Normal  
3    Normal  
4       Bad  
5       Bad  
6       Bad  
Name: Value, dtype: category  
Categories (3, object): [Good, Normal, Bad]  
```

또한 범주를 재설정하여 새로운 값들로 채울 수 있다.  

```Python  
>>> df['Value'] = df['Value'].cat.set_categories(['Best', 'Good', 'Normal', 'Bad', 'Worst'])  
>>> df['Value']
```

```
0      Good  
1      Good  
2    Normal  
3    Normal  
4       Bad  
5       Bad  
6       Bad  
Name: Value, dtype: category  
Categories (5, object): [Best, Good, Normal, Bad, Worst]  
```

```Python  
# 범주형 데이터들의 갯수 확인
>>> df.groupby('Value').size()
```  

```
Value   
Best      0  
Good      2  
Normal    2  
Bad       3  
Worst     0  
dtype: int64  
```

## 11.그래프화(Plotting)  

```Python
# 판다스의 데이터구조를 시각화하기위한 matplot 모듈을 import
>>> import matplotlib.pyplot as plt  
# 시리즈의 인덱스를 시계열로 생성  
>>> t_idx = pd.date_range('2020-02-01', periods=10)  
>>> t_idx
```

```
DatetimeIndex(['2020-02-01', '2020-02-02', '2020-02-03', '2020-02-04',  
               '2020-02-05', '2020-02-06', '2020-02-07', '2020-02-08',   
               '2020-02-09', '2020-02-10'],  
              dtype='datetime64[ns]', freq='D')  
```  

```Python  
>>> p_s = pd.Series(np.random.randint(100, size=10), index=t_idx)  
>>> p_s
```

```
2020-02-01    69  
2020-02-02    41   
2020-02-03    32  
2020-02-04    42  
2020-02-05    99  
2020-02-06    21  
2020-02-07    35   
2020-02-08    59  
2020-02-09     6  
2020-02-10    20  
Freq: D, dtype: int64    
```

```Python  
# 생성한 시리즈의 누적합(cumulative sum)을 구하여 그 값으로 데이터를 갱신함
>>> p_s = p_s.cumsum()  
>>> p_s
```

```
2020-02-01     69  
2020-02-02    110  
2020-02-03    142  
2020-02-04    184  
2020-02-05    283  
2020-02-06    304  
2020-02-07    339  
2020-02-08    398  
2020-02-09    404  
2020-02-10    424  
Freq: D, dtype: int64  
```  

```Python
# 시각화
>>> p_s.plot()
```  

<img width="469" alt="0-15" src="https://user-images.githubusercontent.com/43739827/75110776-bf5e1d80-5675-11ea-9264-207d1364dcd6.png"></img>  

```Python  
# 시각화하기위한 데이터프레임 생성
>>> t_df = pd.DataFrame({'One' : np.random.randint(100, size=10),  
                     'Two' : np.random.randint(100, size=10),  
                     'Three' : np.random.randint(100, size=10),  
                     'Four' : np.random.randint(100, size=10)}, index=t_idx)  

>>> t_df
```

 | | One | Two | Three | Four  
 |-|:---:|:---:|:-----:|:----:  
 2020-02-01 | 65 | 33 | 62 | 99  
 2020-02-02 | 54 | 67 | 68 | 6  
 2020-02-03 | 53 | 24 | 87 | 18  
 2020-02-04 | 62 | 99 | 97 | 45  
 2020-02-05 | 58 | 88 | 92 | 10  
 2020-02-06 | 28 | 18 | 11 | 45   
 2020-02-07 | 79 | 46 | 45 | 33  
 2020-02-08 | 22 | 20 | 91 | 45  
 2020-02-09 | 79 | 81 | 3 | 32  
 2020-02-10 | 1 | 67 | 60 | 75  

```Python  
# 데이터프레임의 요소들을 누적합으로 변경
>>> t_df = t_df.cumsum()  
>>> t_df
```  
  | | One | Two | Three | Four  
  |-|:---:|:---:|:-----:|:----:  
  2020-02-01 | 65 | 33 | 62 | 99  
  2020-02-02 | 119 | 100 | 130 | 105  
  2020-02-03 | 172 | 124 | 217 | 123  
  2020-02-04 | 234 | 223 | 314 | 168   
  2020-02-05 | 292 | 311 | 406 | 178  
  2020-02-06 | 320 | 329 | 417 | 223  
  2020-02-07 | 399 | 375 | 462 | 256  
  2020-02-08 | 421 | 395 | 553 | 301  
  2020-02-09 | 500 | 476 | 556 | 333  
  2020-02-10 | 501 | 543 | 616 | 408  

```Python  
# 데이터프레임 시각화
>>> t_df.plot()
```

<img width="466" alt="0-16" src="https://user-images.githubusercontent.com/43739827/75110953-de5daf00-5677-11ea-908c-bb9385a3e4c2.png"></img>  


## 12.파일 입/출력  

```Python  
# csv 파일로 저장
>>> t_df.to_csv('test.csv')  
# csv 파일 불러오기
>>> df = pd.read_csv('test.csv')  
>>> df
```  

 | | Unnamed : 0 | One | Two | Three | Four  
 |-|:-----------:|:---:|:---:|:-----:|:----:  
 0 | 2020-02-01 | 65 | 33 | 62 | 99  
 1 | 2020-02-02 | 119 | 100 | 130 | 105   
 2 | 2020-02-03 | 172 | 124 | 217 | 123  
 3 | 2020-02-04 | 234 | 223 | 314 | 168  
 4 | 2020-02-05 | 292 | 311 | 406 | 178  
 5 | 2020-02-06 | 320 | 329 | 417 | 223  
 6 | 2020-02-07 | 399 | 375 | 462 | 256  
 7 | 2020-02-08 | 421 | 395 | 553 | 301  
 8 | 2020-02-09 | 500 | 476 | 556 | 333  
 9 | 2020-02-10 | 501 | 543 | 616 | 408  

```Python  
# HDF 파일로 저장
>>> t_df.to_hdf('test.hdf', 't_df')  
# HDF 파일 불러오기
>>> pd.read_hdf('test.hdf', 't_df')
```

| | One | Two | Three | Four  
|-|:---:|:---:|:-----:|:----:  
2020-02-01 | 65 | 33 | 62 | 99  
2020-02-02 | 119 | 100 | 130 | 105  
2020-02-03 | 172 | 124 | 217 | 123  
2020-02-04 | 234 | 223 | 314 | 168   
2020-02-05 | 292 | 311 | 406 | 178  
2020-02-06 | 320 | 329 | 417 | 223  
2020-02-07 | 399 | 375 | 462 | 256  
2020-02-08 | 421 | 395 | 553 | 301  
2020-02-09 | 500 | 476 | 556 | 333  
2020-02-10 | 501 | 543 | 616 | 408  

```Python  
# 엑셀 파일로 저장
>>> t_df.to_excel('test.xlsx', sheet_name='test')  
# 엑셀 파일 불러오기
>>> pd.read_excel('test.xlsx', 'test', index_col=None, na_values=['NA'])
```  

| | Unnamed : 0 | One | Two | Three | Four  
|-|:-----------:|:---:|:---:|:-----:|:----:  
0 | 2020-02-01 | 65 | 33 | 62 | 99  
1 | 2020-02-02 | 119 | 100 | 130 | 105   
2 | 2020-02-03 | 172 | 124 | 217 | 123  
3 | 2020-02-04 | 234 | 223 | 314 | 168  
4 | 2020-02-05 | 292 | 311 | 406 | 178  
5 | 2020-02-06 | 320 | 329 | 417 | 223  
6 | 2020-02-07 | 399 | 375 | 462 | 256  
7 | 2020-02-08 | 421 | 395 | 553 | 301  
8 | 2020-02-09 | 500 | 476 | 556 | 333  
9 | 2020-02-10 | 501 | 543 | 616 | 408   
