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

```Python  
# 시리즈로 데이터프레임 생성(s1)
s1 = pd.Series(np.random.randint(10, size=4), index=list('ABCD'))
s1
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
s2 = pd.Series(np.random.randint(20, size=4), index=list('ABCD'))
s2
```  

```
A     4  
B    16  
C     0  
D    17  
dtype: int64  
```

```Python
df4 = pd.DataFrame({'One' : s1 , 'Two' : s2})  
df4
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
df.head()
```  

<img width="517" alt="0-3" src="https://user-images.githubusercontent.com/43739827/74827693-2b2c4780-5351-11ea-9541-b5880bef8751.png"></img>  

```Python
# 아래에서 7개의 행 출력
df.tail(7)
```    

<img width="573" alt="0-4" src="https://user-images.githubusercontent.com/43739827/74827973-a1c94500-5351-11ea-9fa6-0c0c0f24371c.png"></img>  

```Python
# 행의 레이블 확인
df.index
```  

```
RangeIndex(start=0, stop=3668, step=1)
```  

```Python
# 열의 레이블 확인
df.columns
```  

```
Index(['home_team', 'away_team', 'home_goals', 'away_goals', 'result','season'],
      dtype='object')
```  

**DataFrame.to_numpy** 메소드는 데이터프레임의 데이터를 넘파이 모듈의 ndarray로 반환하여 보여준다. 각 열마다의 값의 자료형이 다르다면 수행시간이 전부 동일한 자료형을 가지는 데이터프레임보다 오래 걸리게 된다.  

```Python
df.head(3).to_numpy()
```  

```
array([['TottenhamHotspur', 'ManchesterCity', 0, 0, 'D', '2010-2011'],
       ['AstonVilla', 'WestHamUnited', 3, 0, 'H', '2010-2011'],
       ['BlackburnRovers', 'Everton', 1, 0, 'H', '2010-2011']],
      dtype=object)
```  

```Python
df2 = pd.DataFrame({'One' : [1,2,3], 'Two' : [4,5,6], 'Three' : [7,8,9], 'Four' : [10,11,12], 'Five' : [13,14,15], 'Six' : [16,17,18]})  

df2.to_numpy()
```  

```
array([[ 1,  4,  7, 10, 13, 16],
       [ 2,  5,  8, 11, 14, 17],
       [ 3,  6,  9, 12, 15, 18]])  
```  
> **DataFrame.to_numpy()** 메소드의 출력결과는 행과 열의 레이블을 포함하지 않는다.  


**describe** 메소드는 데이터프레임의 간략한 통계 수치를 확인할 때 사용한다.  

```Python
df.describe()
```  

<img width="222" alt="0-5" src="https://user-images.githubusercontent.com/43739827/74829415-57959300-5354-11ea-8855-5d293356c719.png"></img>  

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
df2.sort_index(axis=1, ascending=False)
```  

 | | Two | Three | Six | One | Four | Five  
 |-|:---:|:-----:|:---:|:---:|:----:|:----:  
 0 | 4 | 7 | 16 | 1 | 10 | 13  
 1 | 5 | 8 | 17 | 2 | 11 | 14  
 2 | 6 | 9 | 18 | 3 | 12 | 15  

 ```Python
 # 열의 레이블 정렬(오름차순)
 df2.sort_index(axis=1, ascending=True)
 ```  

 | | Five | Four | One | Six | Three | Two  
 |-|:----:|:----:|:---:|:---:|:-----:|:----:  
 0 | 13 | 10 | 1 | 16 | 7 | 4  
 1 | 14 | 11 | 2 | 17 | 8 | 5  
 2 | 15 | 12 | 3 | 18 | 9 | 6  


```Python  
df3 = pd.DataFrame({'A' : [1,2,3,4], 'B' : [5,6,7,8]}, index=list('DACB'))  
df3
```  

 | | A | B  
 |-|:-:|:-:  
 D | 1 | 5  
 A | 2 | 6  
 C | 3 | 7  
 B | 4 | 8  

```Python  
 # 행의 레이블 정렬(내림차순)
 df3.sort_index(axis=0, ascending=False)
```  

 | | A | B  
 |-|:-:|:-:  
 D | 1 | 5  
 C | 3 | 7  
 B | 4 | 8  
 A | 2 | 6  

```Python
# 행의 레이블 정렬(오름차순)
df3.sort_index(axis=0, ascending=True)
```  

| | A | B  
|-|:-:|:-:  
A | 2 | 6  
B | 4 | 8  
C | 3 | 7  
D | 1 | 5  


```Python
# 시리즈의 행 레이블 정렬
series = pd.Series(np.random.randint(5, size=3), index=list('BAC'))  
series.sort_index(axis=0)
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
df.sort_values(by='home_team').head()
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
 df.sort_values(by='home_team', ascending=False).head()
 ```  
 | | home_team | away_team | home_goals | away_goals | result | season  
 |-|:---------:|:---------:|:----------:|:----------:|:------:|:------:  
 685 | Wolverhampton Wanderers | Bolton Wanderers | 2 | 3 | A | 2011-2012  
 517 | Wolverhampton Wanderers | Sunderland | 2 | 1 | H | 2011-2012  
 3267 | Wolverhampton Wanderers | Leicester City | 4 | 3 | H | 2018-2019  
 3275 | Wolverhampton Wanderers | West Ham United | 3 | 0 | H | 2018-2019  
 533 | Wolverhampton Wanderers | Stoke City | 1 | 2 | A | 2011-2012  

   
