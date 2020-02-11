# 4. Index Class  

인덱스를 검색하는 방법과 시리즈나 데이터 프레임에서 행/열 레이블을 만드는 방법, 여러 가지 자료형으로 구성된 단일 레이블 혹은 복수 레이블이 어떻게 만들어지고 작동하는지 알아본다.  

## 1. 숫자&문자 인덱스  

시리즈 혹은 데이터 프레임을 생성할 때 레이블을 따로 명시하지 않으면 0부터 시작하는 RangeIndex가 생성되는것를 확인할 수 있다. 만약 레이블을 지정하고자 한다면 index와 columns를 이용하여 명시해야 한다.  

<img width="1084" alt="4-1" src="https://user-images.githubusercontent.com/43739827/74234832-1c221580-4d11-11ea-96d0-f7c194e1fbaf.png"></img>  

* Index 클래스  
**pd.Index** 는 입력한 자료형에 따라 각 자료형에 맞는 인덱스 객체를 생성한다.  

<img width="1094" alt="4-2" src="https://user-images.githubusercontent.com/43739827/74235075-98b4f400-4d11-11ea-957a-d62c822310be.png"></img>  

인덱스 클래스도 배열이기 때문에 슬라이스 처리가 가능하다.  

<img width="1095" alt="4-3" src="https://user-images.githubusercontent.com/43739827/74235403-3c060900-4d12-11ea-9ae8-8ed4d17a2639.png"></img>  

또한 팬시 검색과 인덱스 검색도 가능하다.  

<img width="1088" alt="4-4" src="https://user-images.githubusercontent.com/43739827/74236608-f39c1a80-4d14-11ea-9567-b99330f92140.png"></img>  

인덱스 클래스는 변하지 않는 불변의(immutable) 객체를 생성하기 때문에 내부의 원소를 변경하는 것은 불가능하며, 만약 원소를 변경하고자 할 경우는 같은 형태의 인덱스 클래스를 생성하여 전체를 대체하는 방식으로 변경해야한다.  

<img width="1090" alt="4-5" src="https://user-images.githubusercontent.com/43739827/74236838-7e7d1500-4d15-11ea-9884-1ab411cbed74.png"></img>  

정수 인덱스에 대해 덧셈 연산을 하여 내부 원소들의 정보가 변한것을 확인할 수 있지만 인덱스 클래스는 불변이므로 새로운 객체를 생성해서 반환한것을 알 수 있다.  

<img width="1094" alt="4-6" src="https://user-images.githubusercontent.com/43739827/74236994-dae03480-4d15-11ea-9441-68846b9cb53d.png"></img>  

* 인덱스의 암묵적 처리  
시리즈나 데이터 프레임간의 연산을 할 경우에 각자가 레이블을 곱한 것 만큼의 데이터가 생긴다. 또한 두 개의 시리즈가 연산할때 둘 중 하나만 레이블을 가지고 있다면 그 레이블에 맞추어 연산되지만 다른 시리즈에는 존재하지 않는 레이블에는 누락 값인 NaN이 생성된다.  

같은 크기에 서로 다른 레이블을 가지는 시리즈 두 개를 생성한다.  

<img width="1089" alt="4-7" src="https://user-images.githubusercontent.com/43739827/74237682-745c1600-4d17-11ea-8b47-aa1ac50bc99c.png"></img>  

두 시리즈를 더하면 데이터 베이스의 카테시안 곱이 되는것을 확인할 수 있다.  

<img width="1090" alt="4-8" src="https://user-images.githubusercontent.com/43739827/74237812-bc7b3880-4d17-11ea-8454-52ba16ac9fb5.png"></img>  
> 일치하는 레이블이 없어 누락값이 발생한다.  

만약 레이블의 순서만 바꿔주어도 연산이 가능해진다면 **.sort_index** 메소드를 사용해 레이블의 위치를 일치시키고 **.add** 메소드로 연산할 대상을 지정해주면 된다.  

<img width="1096" alt="4-9" src="https://user-images.githubusercontent.com/43739827/74238096-65299800-4d18-11ea-84d7-7ce937e9fb80.png"></img>  

<img width="1089" alt="4-10" src="https://user-images.githubusercontent.com/43739827/74238221-afab1480-4d18-11ea-8ce1-e527d23504bc.png"></img>  

## 2. 날짜&범주형 인덱스  

인덱스의 레이블이 시간 정보로 되어 있는 데이터를 시계열(time series) 데이터라고 한다. 또한 특정한 값들로 한정되어 있는 데이터를 범주형 데이터라고 하는데 이 범주형 데이터도 인덱스로 사용하는것이 가능하다.  

* 날짜 인덱스  
날짜 정보를 생성할때 **pd.data_range** 함수를 사용하면 날짜 및 시간을 일일히 입력하지 않고 시작일과 종료일 혹은 시작일과 기간을 지정해주면 자동적으로 그 범위의 날짜를 인덱스로 만들어준다.  

<img width="1098" alt="4-11" src="https://user-images.githubusercontent.com/43739827/74238813-e6355f00-4d19-11ea-911b-001fb2bf2048.png"></img>  
> 인덱스의 자료형이 **datetime64** 인것을 확인할 수 있다. 또한 **freq='D'** 는 범위의 주기가 날(Date)란 의미를 가지고 있다.  

<img width="590" alt="4-12" src="https://user-images.githubusercontent.com/43739827/74239064-71aef000-4d1a-11ea-9807-e8e41b386531.png"></img>  
> 시간의 빈도를 나타내는 별칭들 [Pandas Document<Offset aliases>](https://pandas.pydata.org/docs/user_guide/timeseries.html#timeseries-offset-aliases, "Pandas DOC")  

날짜 인덱스를 자동적으로 채우지 않고 특정한 날짜들을 선별하여 시리즈나 데이터 프레임의 인덱스로 사용할 수 있다. 이때 **pd.DatetimeIndex** 클래스를 사용한다.  

<img width="1091" alt="4-13" src="https://user-images.githubusercontent.com/43739827/74239339-00bc0800-4d1b-11ea-9cd8-62f1b3b7f00d.png"></img>  
> 인덱스가 특정한 날짜로 채워져 **freq=None** 으로 나타난다.  

* 시간 빈도
