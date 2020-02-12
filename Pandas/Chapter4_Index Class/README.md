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

<img width="687" alt="4-16" src="https://user-images.githubusercontent.com/43739827/74306391-c9df0400-4da5-11ea-83a1-d74339c79023.png"></img>  

> 시간의 빈도를 나타내는 별칭들  
[Pandas Document<Offset aliases>](https://pandas.pydata.org/docs/user_guide/timeseries.html#timeseries-offset-aliases, "Pandas DOC")  

날짜 인덱스를 자동적으로 채우지 않고 특정한 날짜들을 선별하여 시리즈나 데이터 프레임의 인덱스로 사용할 수 있다. 이때 **pd.DatetimeIndex** 클래스를 사용한다.  

<img width="1091" alt="4-13" src="https://user-images.githubusercontent.com/43739827/74239339-00bc0800-4d1b-11ea-9cd8-62f1b3b7f00d.png"></img>  
> 인덱스가 특정한 날짜로 채워져 **freq=None** 으로 나타난다.  

* 시간 빈도
**.date_range** 함수는 두 개의 특정 날짜를 지정해주면 그 사이의 날짜들을 원소로 하는 DatetimeIndex를 생성한다.  

<img width="1084" alt="4-14" src="https://user-images.githubusercontent.com/43739827/74306027-b4b5a580-4da4-11ea-9d7c-64d8553804c2.png"></img>  

혹은 날짜 하나를 지정하고 **periods=n** 을 매개변수로 입력하면 n만큼의 날짜를 범위로하여 DatetimeIndex를 생성한다.  

<img width="1084" alt="4-15" src="https://user-images.githubusercontent.com/43739827/74306118-00684f00-4da5-11ea-99ca-15ca4b1b1f4c.png"></img>  

<img width="1098" alt="4-17" src="https://user-images.githubusercontent.com/43739827/74306526-17f40780-4da6-11ea-8729-caa9b5b74c2b.png"></img>  
> **freq** 에 시간 주기를 나타내는 항목들을 입력하면 그 기준에 맞는 DatetimeIndex가 생성되는것을 확인할 수 있다.  

**to_period** 함수는 DatetimeIndex를 **PeriodIndex** 로 변경하고자 할 때 사용한다. 괄호안에는 시간 주기를 입력한다.  

<img width="1099" alt="4-18" src="https://user-images.githubusercontent.com/43739827/74306773-d4e66400-4da6-11ea-9105-32ab913d9185.png"></img>  

<img width="931" alt="4-19" src="https://user-images.githubusercontent.com/43739827/74306826-fa736d80-4da6-11ea-8846-a4f0b23a9a26.png"></img>
> [Pandas Document](https://pandas.pydata.org/docs/reference/api/pandas.DatetimeIndex.to_period.html?highlight=to_period, "Pandas DOC")  

PeriodIndex를 별도로 생성하기 위해서는 **period_range** 함수를 사용한다. date_range와 마찬가지로 periods와 freq를 매개변수로 입력하여 생성한다.  

<img width="1098" alt="4-20" src="https://user-images.githubusercontent.com/43739827/74307010-98673800-4da7-11ea-87b3-eb5306bc0b40.png"></img>  

특정 시간을 주기로하는 인덱스를 생성하기 위해서는 **timedelta_rnage** 함수를 사용한다. 여타 시간 인덱스들과 마찬가지로 매개변수로 periods와 freq를 입력하여 생성한다.    

<img width="1097" alt="4-21" src="https://user-images.githubusercontent.com/43739827/74307321-60acc000-4da8-11ea-9cf9-ac9fdabf4ec5.png"></img>  

<img width="943" alt="4-22" src="https://user-images.githubusercontent.com/43739827/74307397-833ed900-4da8-11ea-82a8-02105c482374.png"></img>  
> [Pandas Document](https://pandas.pydata.org/docs/reference/api/pandas.timedelta_range.html?highlight=timedelta_range#pandas.timedelta_range, "Pandas DOC")  

시간과 시간끼리는 서로 벡터화 연산이 되어 배열 전체가 바뀌는것을 확인할 수 있다.  

<img width="1095" alt="4-23" src="https://user-images.githubusercontent.com/43739827/74307561-03fdd500-4da9-11ea-96bb-05e3dea8c2bc.png"></img>  

시간에 대한 인덱스를 분(minute)을 기준으로 생성할 수 있다. 이 때 date_range의 매개변수로 freq='T'를 선언하면 된다.  

<img width="1090" alt="4-24" src="https://user-images.githubusercontent.com/43739827/74307789-cea5b700-4da9-11ea-8d8f-00c6aad34cc0.png"></img>  

특정 시간을 기준으로 시간 데이터들을 그룹화할 수 있다. 이때 **resample** 메소드를 사용한다.  

<img width="1094" alt="4-25" src="https://user-images.githubusercontent.com/43739827/74307963-44118780-4daa-11ea-8ba7-6e3688e5f4ba.png"></img>  

* 날짜 인덱스 처리  

데이터의 인덱스가 날짜로 보이지만 사실은 문자로 처리되어있는 경우가 많다. 이런 경우에는 문자 인덱스를 시간 인덱스로 변경하여 처리해야 한다.  

csv로 날짜를 인덱스로 처리하기 위해서는 매개변수에 **parse_dates** 를 입력한다.  

<img width="1096" alt="4-26" src="https://user-images.githubusercontent.com/43739827/74309994-71acff80-4daf-11ea-9a4c-412724f8b72e.png"></img>  

데이터 프레임 내부의 열들을 연산하여 그 값으로 새로운 열을 만들고자 한다면 **.eval** 메소드를 사용한다.  

<img width="1090" alt="4-27" src="https://user-images.githubusercontent.com/43739827/74310072-a28d3480-4daf-11ea-83fa-1f88254a1b45.png"></img>  

* 범주형 인덱스 처리  

범주형 인덱스를 별도로 생성하기 위해서 **CategoricalIndex** 클래스를 사용한다.  

<img width="1095" alt="4-28" src="https://user-images.githubusercontent.com/43739827/74310321-470f7680-4db0-11ea-9720-a9c152c8a876.png"></img>  

이 범주를 벗어나는 값을 객체로 추가하려하면 예외가 발생하는 것을 확인할 수 있다.  

<img width="1089" alt="4-29" src="https://user-images.githubusercontent.com/43739827/74310456-9fdf0f00-4db0-11ea-800b-73a98eebae2f.png"></img>  

범주형 인덱스에 인덱스 레이블을 추가해도 예외가 발생한다.  

<img width="1092" alt="4-30" src="https://user-images.githubusercontent.com/43739827/74310681-14b24900-4db1-11ea-87de-c00d05b94be7.png"></img>  

레이블을 추가하고자 한다면 기존의 범주형 인덱스를 단순한 파이썬 리스트로 변환하여 추가작업을 한다. 그러기 위해선 **.tolist** 매서드를 사용한다.  

<img width="1092" alt="4-32" src="https://user-images.githubusercontent.com/43739827/74311424-cc942600-4db2-11ea-9f73-4296d62242f7.png"></img>  

<img width="931" alt="4-31" src="https://user-images.githubusercontent.com/43739827/74311341-8d65d500-4db2-11ea-8a63-a84fe4f10592.png"></img>  
> [Pandas Document](https://pandas.pydata.org/docs/reference/api/pandas.Series.tolist.html?highlight=tolist#pandas.Series.tolist, 'Pandas DOC')  

<img width="1091" alt="4-33" src="https://user-images.githubusercontent.com/43739827/74311592-2eed2680-4db3-11ea-97fd-a3574a54b52b.png"></img>  

이후에 다시 범주형 인덱스로 변환하여 범주형으로 사용할 수 있다.  

<img width="1099" alt="4-34" src="https://user-images.githubusercontent.com/43739827/74311707-678d0000-4db3-11ea-89da-e9d0f14af0bb.png"></img>  

## 3. 멀티인덱스  

시리즈 혹은 데이터 프레임의 다차원 처리가 필요한 경우에는 계층적 레이블을 만들어서 프레임의 차원을 확대시켜야 한다. 이 계층적인 레이블을 만들기 위해서는 MultiIndex 클래스를 사용해야 한다.  

* 멀티인덱스 생성  
멀티인덱스를 만들기 위해서는 일단 2개를 원소 쌍으로 하는 튜플을 두 개 만들어서 리스트에 넣는다. 만들어진 객체를 확인하면 인덱스가 튜플형태로 된 것을 확인할 수 있다.  

<img width="1085" alt="4-35" src="https://user-images.githubusercontent.com/43739827/74320171-7e3b5300-4dc3-11ea-8f85-da6e9a1daceb.png"></img>  

이렇게 튜플로 생성된 레이블은 검색또한 튜플 형태로 해주어야 한다.  

<img width="1096" alt="4-36" src="https://user-images.githubusercontent.com/43739827/74320440-f0139c80-4dc3-11ea-95a5-acd0d6abff1e.png"></img>  

이렇게 만들어진 튜플 형태의 레이블을 멀티인덱스로 변환하기 위해 MultiIndex에 있는 클래스 **.from_tuples** 를 사용한다.  

<img width="1095" alt="4-38" src="https://user-images.githubusercontent.com/43739827/74320950-da52a700-4dc4-11ea-97e0-e1c4cff2e99c.png"></img>  

<img width="930" alt="4-37" src="https://user-images.githubusercontent.com/43739827/74320662-61534f80-4dc4-11ea-8e45-272c8c48e613.png"></img>  
> [Pandas Document](https://pandas.pydata.org/docs/reference/api/pandas.MultiIndex.from_tuples.html?highlight=from_tuples#pandas.MultiIndex.from_tuples, 'Pandas DOC')  

이렇게 변환된 인덱스로 시리즈를 생성하고 조회하면 행의 레이블이 위와 다르게 튜플형태가 아닌것을 확인할 수 있다.  

<img width="1099" alt="4-39" src="https://user-images.githubusercontent.com/43739827/74321478-acba2d80-4dc5-11ea-8c58-059f202c1c27.png"></img>  

멀티인덱스는 검색시에 계층별로 분리하여 검색하는것이 가능하다.

<img width="1091" alt="4-40" src="https://user-images.githubusercontent.com/43739827/74321647-fc005e00-4dc5-11ea-9af2-44a0ba8895ac.png"></img>  

또한 멀티인덱스는 인덱스에서 제공하는 기본 검색방식또한 제공한다.  

<img width="1091" alt="4-41" src="https://user-images.githubusercontent.com/43739827/74321910-6ca77a80-4dc6-11ea-9c16-679c4905b689.png"></img>  

멀티인덱스를 만드는 다른 방법으로는 인덱스를 넘파이배열로 생성하는 것이다.  

<img width="1093" alt="4-42" src="https://user-images.githubusercontent.com/43739827/74322451-4cc48680-4dc7-11ea-92bf-e9492ef06301.png"></img>  

생성된 시리즈 객체의 인덱스를 확인하면 멀티인덱스인것을 확인할 수 있다.  

<img width="1094" alt="4-43" src="https://user-images.githubusercontent.com/43739827/74322552-7087cc80-4dc7-11ea-82a4-e0b368c61c2f.png"></img>  

파이썬의 리스트를 이용해 멀티인덱스를 생성할 수 있는데 이때는 **.from_product** 클래스를 사용한다.  

<img width="1092" alt="4-44" src="https://user-images.githubusercontent.com/43739827/74322985-22bf9400-4dc8-11ea-95a5-9ca376e4026d.png"></img>  

<img width="939" alt="4-45" src="https://user-images.githubusercontent.com/43739827/74323099-53073280-4dc8-11ea-920e-aba6f49f7ed1.png"></img>  
> [Pandas Document](https://pandas.pydata.org/docs/reference/api/pandas.MultiIndex.from_product.html?highlight=from_product#pandas.MultiIndex.from_product, 'Pandas DOC')  

생성된 객체의 요소를 확인해보면 FrozenList로 구성되어 있는것을 확인할 수 있다. 이것은 인덱스 정보를 임의로 변경할 수 없음을 보여준다.  

<img width="1104" alt="4-46" src="https://user-images.githubusercontent.com/43739827/74323313-ada08e80-4dc8-11ea-9ddc-7be1489794a0.png"></img>  

멀티인덱스 생성시에 names를 설정하여 시리즈의 출력결과에 names로 지정한 값들이 출력되는것을 확인할 수 있다.  

<img width="1095" alt="4-47" src="https://user-images.githubusercontent.com/43739827/74323664-37e8f280-4dc9-11ea-92ea-eb8fc7924088.png"></img>  

멀티인덱스 내부 값들의 빈도를 파악하고자 한다면 value_counts 메소드를 사용한다.  

<img width="1089" alt="4-48" src="https://user-images.githubusercontent.com/43739827/74324109-dc6b3480-4dc9-11ea-909c-a68fdbfb2c74.png"></img>  

1. 멀티인덱스로 시리즈 생성  

<img width="1094" alt="4-49" src="https://user-images.githubusercontent.com/43739827/74325008-3ddfd300-4dcb-11ea-8e55-c9d0b64aede2.png"></img>  

2. 멀티인덱스로 데이터 프레임 생성  

행과 열의 인덱스를 각각의 멀티인덱스로 생성하고 행 X 열의 사이즈로 데이터를 입력하여 데이터 프레임을 생성한다.  

<img width="1099" alt="4-50" src="https://user-images.githubusercontent.com/43739827/74326241-623caf00-4dcd-11ea-9125-5d1b1107725e.png"></img>  
> 열의 인덱스 크기가 6, 행의 인덱스 크기가 4이므로 4 X 6의 넘파이 배열을 생성하였다.  

<img width="1086" alt="4-51" src="https://user-images.githubusercontent.com/43739827/74326358-944e1100-4dcd-11ea-8109-55828507f957.png"></img>  

인덱스를 검색하면 반환 결과로 튜플이 나오는것을 확인할 수 있다.  

<img width="1093" alt="4-52" src="https://user-images.githubusercontent.com/43739827/74326561-f444b780-4dcd-11ea-9086-9cb9ebf02f0a.png"></img>  

특정열을 지정하여 검색하면 그 아래 레벨의 데이터 프레임이 반환된다.  

<img width="1089" alt="4-53" src="https://user-images.githubusercontent.com/43739827/74326740-438ae800-4dce-11ea-901f-72d73a23e551.png"></img>  

열의 레벨을 차례대로 입력하면 시리즈로 반환된다.  

<img width="1092" alt="4-54" src="https://user-images.githubusercontent.com/43739827/74326912-98c6f980-4dce-11ea-84d7-b56590c24027.png"></img>  

행을 기준으로 검색하고자 할 때는 iloc과 loc 속성을 사용하며 명시적인지 묵시적인지를 확실히 알아야 한다.  

<img width="1097" alt="4-55" src="https://user-images.githubusercontent.com/43739827/74327410-800b1380-4dcf-11ea-8146-9e0a863c641b.png"></img>  

행을 기준으로 하고 열을 튜플로 묶어 검색하면 열을 기준으로 한 검색과 동일한 결과를 보여준다.  

<img width="1086" alt="4-56" src="https://user-images.githubusercontent.com/43739827/74327560-c19bbe80-4dcf-11ea-950a-f89e9faf48c1.png"></img>  

문자열을 조건으로 하고 슬라이스 검색을 했을 때 문자열 레이블이 정렬되어 있지 않으면 오류가 발생한다.  

<img width="1092" alt="4-57" src="https://user-images.githubusercontent.com/43739827/74327852-3e2e9d00-4dd0-11ea-9f99-7b24c72d270a.png"></img>  
> 문자열이 순서대로 정렬되어있지 않아 예외가 발생하는것을 확인할 수 있다.  

<img width="1090" alt="4-58" src="https://user-images.githubusercontent.com/43739827/74328007-851c9280-4dd0-11ea-8aaa-61daebf6ea70.png"></img>

또 다른 슬라이싱 방법으로는 **IndexSlice** 속성을 사용하는 것이다.  

<img width="1090" alt="4-59" src="https://user-images.githubusercontent.com/43739827/74328867-0a547700-4dd2-11ea-846d-c5a677c2f4a7.png"></img>  

<img width="974" alt="4-60" src="https://user-images.githubusercontent.com/43739827/74328933-2b1ccc80-4dd2-11ea-9c64-a7e71e0896ce.png"></img>
> [Pandas Document](https://pandas.pydata.org/docs/reference/api/pandas.IndexSlice.html?highlight=indexslice#pandas.IndexSlice, 'Pandas DOC')  

멀티인덱스 검색을 하기위해 **.xs** 메소드를 사용한다. 이 메소드에는 레이블명을 기입해야 하므로 검색전 확인해야 할 필요가 있다.  

<img width="1097" alt="4-61" src="https://user-images.githubusercontent.com/43739827/74329266-d4fc5900-4dd2-11ea-9fbc-ec66fcdc63d1.png"></img>  
> 반환된 결과물을 보면 행을 기준으로 하는것을 확인할 수 있다.  

열을 기준으로 검색하고자 할때는 axis=1을 매개변수로 입력한다.  

<img width="1092" alt="4-62" src="https://user-images.githubusercontent.com/43739827/74329499-420fee80-4dd3-11ea-94fc-7cfa3ed2dd25.png"></img>  
