# 3. Series & DataFrame

시리즈와 데이터 프레임을 이용해 연산자를 실행하거나 메소드를 처리하는 방법에 대해 알아본다.  

##1. 메소드  

* 시리즈와 데이터 프레임의 공통 메소드  

<img width="1087" alt="3-1" src="https://user-images.githubusercontent.com/43739827/74143715-ab122d80-4c3e-11ea-99e5-11c53eef92de.png"></img>  

* 연산자와 메소드 처리  
순환문을 별도로 사용하지 않아도 시리즈와 데이터프레임은 연산이 가능하다. 이를 확인하기 위해 csv 파일을 불러와 데이터 프레임으로 만들고 각 열의 자료형을 확인한다.  

<img width="1092" alt="3-2" src="https://user-images.githubusercontent.com/43739827/74144191-a306bd80-4c3f-11ea-9446-f5aa0932b7e9.png"></img>  

<img width="1093" alt="3-3" src="https://user-images.githubusercontent.com/43739827/74144405-02fd6400-4c40-11ea-8ed2-dbe895abc07f.png"></img>  
> 이 데이터 프레임에 정수값을 더하려고하면 오류가 발생한다. 문자열은 문자열간의 덧셈만 지원하기 때문이다.  

<img width="1100" alt="3-4" src="https://user-images.githubusercontent.com/43739827/74144643-799a6180-4c40-11ea-9079-31aae771cff0.png"></img>  
> 연산전과 후를 비교해보면 조건에 맞는 열의 값이 변한것을 확인할 수 있다.  

* 열을 기준으로 한 데이터 분석  
데이터 프레임의 열을 계산하기 위해서는 그 열을 따로 분리하여 처리해야 한다. 그러기 위해서는 각 열마다의 자료형을 파악하는것이 중요하다.  

<img width="1093" alt="3-5" src="https://user-images.githubusercontent.com/43739827/74145330-de09f080-4c41-11ea-924d-5a74431fe7a7.png"></img>  

**select_dtypes** 메소드의 **include** 매개변수는 불러오고자하는 열의 자료형을 입력하면 그 열만을 사용한 데이터 프레임을 반환한다.  

<img width="1103" alt="3-6" src="https://user-images.githubusercontent.com/43739827/74145408-16a9ca00-4c42-11ea-8894-e1a5e2729684.png"></img>  
> int64와 number가 동일하게 숫자 자료형을 불러오는것을 확인할 수 있다.  

* 시리즈와 데이터 프레임의 자료값 확인  
시리즈나 데이터 프레임 객체는 다양한 값들이 들어갈 수 있기 때문에 그 값에 대한 범위나 순위등을 파악하면 데이터를 분석하는데에 훨씬 수월하다.  

시리즈에서는 값의 중복횟수를 파악할 수 있는 **.value_count** 메소드가 존재한다.  

<img width="1105" alt="3-7" src="https://user-images.githubusercontent.com/43739827/74145620-a8b1d280-4c42-11ea-822b-fe6e3595d533.png"></img>  

데이터의 빈도수를 퍼센트로 확인하고자 할때는 .value_count 메소드 안에 매개변수로 **normalize=True** 를 입력한다.  

<img width="1100" alt="3-8" src="https://user-images.githubusercontent.com/43739827/74145811-0fcf8700-4c43-11ea-8376-d1c0127321c9.png"></img>  


<img width="1107" alt="3-9" src="https://user-images.githubusercontent.com/43739827/74146070-a4d28000-4c43-11ea-86df-61cb913f25d2.png"></img>  


값의 최대구간과 최소구간을 확인하고 싶다면 **.nlargest** 메소드와 **.nsmallest** 메소드를 사용한다. 왼쪽에는 행의 레이블이 나타나고 오른쪽은 해당 값이 나타난다.  

<img width="1100" alt="3-10" src="https://user-images.githubusercontent.com/43739827/74146464-7608d980-4c44-11ea-915e-70c9092a793b.png"></img>  

<img width="1108" alt="3-11" src="https://user-images.githubusercontent.com/43739827/74146564-ad778600-4c44-11ea-8472-b64e12b2f9e5.png"></img>  
> 데이터 프레임형태로의 결과 반환도 가능하다. 이때는 괄호안에 나타낼 행의 수와 열의 이름을 순서대로 지정해준다.  

<img width="1110" alt="3-12" src="https://user-images.githubusercontent.com/43739827/74147065-cdf41000-4c45-11ea-98d8-f8d8f0865a3b.png"></img>  

## 2. 인덱스 레이블과 누락 값 처리  

판다스는 예외 처리를 하지 않기위해 데이터가 없더라도 값을 자동으로 만들어 채우는데, 이 누락값을 새로운 값으로 대체시키거나 삭제하여 완벽한 데이터 프레임으로 바꾼 뒤 작업해야한다.  

* 인덱스 변경 및 대체  
행의 레이블 이름을 변경할 때는 **.rename** 메소드를 사용한다. 인자로 기존의 레이블과 변경할 레이블을 딕셔너리 형태로 만들어 넣어주면 반환된 결과의 행의 레이블이 달라진것을 확인할 수 있다.  

<img width="1105" alt="3-13" src="https://user-images.githubusercontent.com/43739827/74147912-8a9aa100-4c47-11ea-9d8f-3253e43706c0.png"></img>  

**.reindex** 메소드를 사용하면 레이블 이름 수정 및 위치 변경이 가능하다.  

<img width="1109" alt="3-14" src="https://user-images.githubusercontent.com/43739827/74148519-f7fb0180-4c48-11ea-93c4-b08753b36a73.png"></img>  

시리즈 두개를 생성하고 다른 인덱스 자료형끼리의 연산을 확인하고자 한다.  

<img width="1103" alt="3-15" src="https://user-images.githubusercontent.com/43739827/74149294-c125eb00-4c4a-11ea-89e1-e80e8d79c054.png"></img>  
> 인덱스의 자료형이 서로 달라 매핑되지 못하여 전부 NaN처리 되었다.

<img width="1104" alt="3-16" src="https://user-images.githubusercontent.com/43739827/74149377-f8949780-4c4a-11ea-92a4-f0310bc7b157.png"></img>  
> 레이블의 자료형을 동일하게 만들고 연산을 하면 예상한 결과가 반환되는것을 확인할 수 있다.  

.rename 메소드를 이용해 자료형을 변경할수도 있고 **.index.values** 속성에서 **.astype** 메소드를 이용하여 자료형을 변경할 수도 있다.  

<img width="1106" alt="3-17" src="https://user-images.githubusercontent.com/43739827/74149915-44940c00-4c4c-11ea-83f1-1ab086917969.png"></img>  

* 열의 이름을 이용한 필터링  
**.filter** 메소드는 특정 열에 대한 레이블을 어떠한 기준을 이용해 추출할 때 사용한다.  

<img width="1104" alt="3-18" src="https://user-images.githubusercontent.com/43739827/74150493-59bd6a80-4c4d-11ea-8539-9490ee4f69af.png"></img>  
> 문자열을 검색할때는 데이터베이스처럼 **like** 문을 사용한다.  

filter 메소드의 **regex** 매개변수는 정규표현식을 이용해 열을 선택하는것이 가능하다.  

<img width="1099" alt="3-19" src="https://user-images.githubusercontent.com/43739827/74151014-8d4cc480-4c4e-11ea-9ca8-5e68d4ff0744.png"></img>  
> 언더바를 포함하고있는 열만을 추출하는 정규표현식  

<img width="859" alt="3-20" src="https://user-images.githubusercontent.com/43739827/74151358-5d51f100-4c4f-11ea-8033-ace7c3dd124a.png"></img>  
> 정규표현식의 문자 클래스 [Wikipedia.org](https://ko.wikipedia.org/wiki/%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D, "Wikipedia")  

* 누락 값 변경  
1. 누락 값 처리  
**fillna** 메소드를 사용해 누락 값을 다양하게 대체한다.  

<img width="1097" alt="3-21" src="https://user-images.githubusercontent.com/43739827/74151882-7a3af400-4c50-11ea-969e-47264976528e.png"></img>  
> 매개변수 **fill** 과 **pad** 는 누락 값의 전 값으로 대체한다.  

<img width="1102" alt="3-22" src="https://user-images.githubusercontent.com/43739827/74152056-d6057d00-4c50-11ea-8dd4-cc294b29256a.png"></img>  
> 매개변수 **bfill** 과 **backfill** 는 누락 값의 다음값으로 대체한다.  

누락 값을 변경하기위해서는 어느 열이 누락값을 가지고있는지 확인할 필요가 있다.  

<img width="1096" alt="3-23" src="https://user-images.githubusercontent.com/43739827/74152580-f124bc80-4c51-11ea-89dd-735fc926b0e4.png"></img>  
> 데이터 프레임의 전체 누락 값 개수를 확인하기위해서는 **.isnull().sum().sum()**  

<img width="1100" alt="3-24" src="https://user-images.githubusercontent.com/43739827/74152750-4b258200-4c52-11ea-8a6d-ac5ec8da0962.png"></img>  
> .value_count를 이용해도 누락 값의 개수를 확인할 수 있다. 이때 매개변수 **dropna=False** 를 넣어줘야 누락 값을 포함한 계산을 하게된다.  

데이터 프레임의 'season'열에만 누락 값들이 존재하기 때문에 이 값들을 변경하기 위해 .fillna 메소드에 매개변수로 열을 기준으로 하는 **axis=1** 과 데이터 프레임 내부값을 변경해주는 **inplace=True** 를 설정한다.  

<img width="1091" alt="3-25" src="https://user-images.githubusercontent.com/43739827/74223983-3650f900-4cfb-11ea-92e8-365763a3c81c.png"></img>  
> 누락 값들을 전부 " "(문자형 스페이스)로 바꾸어 누락 값 개수가 0이된것을 확인할 수 있다.  

다른 방법으로는 누락 값에 그 전과 후의 값들을 확인하여 중간값을 대체시키는 것이다. 이때 **.interpolate** 메소드를 사용한다.  

<img width="1091" alt="3-26" src="https://user-images.githubusercontent.com/43739827/74224398-1bcb4f80-4cfc-11ea-8dca-2fd9004199d3.png"></img>  
> 시리즈에서의 interpolate  

<img width="1095" alt="3-27" src="https://user-images.githubusercontent.com/43739827/74224854-f723a780-4cfc-11ea-89de-8061369cd686.png"></img>  
> 데이터 프레임에서의 interpolate  

* 누락 값 삭제  
데이터를 처리하는 과정에서 누락 값을 변경하는것보다 삭제하는것이 더 좋을것이라 판단될 때가 있다. 이때 **.dropna** 나 **.drop** 메소드를 사용한다.  

1. 열 삭제  

<img width="1095" alt="3-28" src="https://user-images.githubusercontent.com/43739827/74225215-9b0d5300-4cfd-11ea-9cdb-c71468f9cdb3.png"></img>  
> 누락 값이 있는 열이 삭제된것을 확인할 수 있다.  

<img width="1082" alt="3-29" src="https://user-images.githubusercontent.com/43739827/74225340-dc9dfe00-4cfd-11ea-856e-e94da31f6251.png"></img>  
> drop 메소드를 사용할때엔 누락값이 들어있는 열을 확인한 뒤에 지정해야 한다.  

2. 행 삭제  

<img width="1089" alt="3-31" src="https://user-images.githubusercontent.com/43739827/74227055-07d61c80-4d01-11ea-96fd-d6f3ba26efdd.png"></img>  
> dropna 메소드안의 매개변수로 axis=0, 즉 행을 지정하여 누락 값을 제거하였다.  

* 중복 값 삭제  
누락 값 뿐만 아니라 중복값 또한 데이터를 분석하는데에 많은 영향을 미친다. 이 중복값을 확인하고 제거하는 방법에 대해서 알아본다.  

**.duplicated** 메소드는 시리즈와 데이터 프레임 내부의 값들이 중복되는지를 확인하여 True나 False로 값을 반환한다.  

<img width="1096" alt="3-32" src="https://user-images.githubusercontent.com/43739827/74227495-e9245580-4d01-11ea-8eab-1a15db45cb03.png"></img>  

특정한 열에 대해서 유일값을 확인하기 위해서는 **.unique** 메소드를 사용한다.  

<img width="1086" alt="3-33" src="https://user-images.githubusercontent.com/43739827/74227706-618b1680-4d02-11ea-9492-a3945550055d.png"></img>  
> 넘파이 배열로 결과가 출력된다.  

중복된 값을 삭제하기 위해서는 **.drop_duplicates** 메소드를 사용한다.  

<img width="1087" alt="3-34" src="https://user-images.githubusercontent.com/43739827/74228009-f68e0f80-4d02-11ea-9e35-643a321a42b9.png"></img>  
> 중복 데이터를 제외한 데이터 정보가 출력되는것을 확인할 수 있다.  

데이터 프레임 내부에 동일한 정보를 가진 열들을 제거하는데에도 사용할 수 있다.  

<img width="1094" alt="3-35" src="https://user-images.githubusercontent.com/43739827/74228985-db240400-4d04-11ea-9e4d-e6b13d3fef14.png"></img>  

## 3. 범주형 데이터 처리  

문자열 데이터를 범주형(categorical)으로 처리하여 분석해야 할 경우가 다수 있다. 범주형에는 성별이나 성공여부처럼 분류를 목적으로하는 **명목형 자료(nominal data)** 와 효과나 성적처럼 순서에 의미를 두는 **순서형 자료(ordinal data)** 로 나뉜다.  

* 범주형 데이터 생성  
시리즈를 생성할 때 dtype를 **category** 로 지정하면 자료형이 category로 바뀌며 그 범주안의 자료형과 정보를 확인할 수 있다.  

<img width="1087" alt="3-36" src="https://user-images.githubusercontent.com/43739827/74229020-e8d98980-4d04-11ea-9137-f6241fdf9e4e.png"></img>  

<img width="1108" alt="3-37" src="https://user-images.githubusercontent.com/43739827/74229152-26d6ad80-4d05-11ea-8620-ccae7bb83c8e.png"></img>  

* 범주형 데이터 클래스  
categorical 생성자에 문자열 리스트를 넣어 실행하면 범주형 객체를 생성할 수 있다.  

<img width="1101" alt="3-38" src="https://user-images.githubusercontent.com/43739827/74229863-94cfa480-4d06-11ea-979f-ceb2896ca0e6.png"></img>  

<img width="1097" alt="3-39" src="https://user-images.githubusercontent.com/43739827/74230043-e5df9880-4d06-11ea-9a7a-e5349e2e48d9.png"></img>  
> 범주형 데이터에만 존재하는 함수들  

범주형 인스턴스를 생성하여 데이터 프레임을 만들어 처리하는 방법을 확인하고자 한다. 일단 pd.Categorical을 통해 범주형 인스턴스를 생성한다.  

<img width="1099" alt="3-40" src="https://user-images.githubusercontent.com/43739827/74230406-a82f3f80-4d07-11ea-98ba-5eb80702b76e.png"></img>  

이후에 데이터 프레임을 생성하면서 위에서 생성한 범주형 인스턴스를 하나의 열로 지정하였다.  

<img width="1093" alt="3-41" src="https://user-images.githubusercontent.com/43739827/74230572-03613200-4d08-11ea-8974-ba00bb1a9814.png"></img>  

**.select_dtypes** 메소드에 매개변수로 exclude=**['object']** 를 선언하여 자료형이 object가 아닌 열을 추출했다.  

<img width="1097" alt="3-42" src="https://user-images.githubusercontent.com/43739827/74230698-43281980-4d08-11ea-9346-e69f18dfc30b.png"></img>  

이 데이터 프레임에 값을 추가 및 갱신하고자 한다. 범주형 자료형일때는 범주에 속한 값만을 이용해야 한다.  

<img width="1107" alt="3-43" src="https://user-images.githubusercontent.com/43739827/74231021-ee38d300-4d08-11ea-9f02-05ae813e7795.png"></img>  

* 범주형 데이터 활용  
데이터를 처리하다보면 문자열이 특정한 범위 내에서 반복적으로 출현하는것을 종종 확인할 수 있다. 이때 이 데이터들을 범주형으로 지정하여 처리하면 메모리 사용을 줄일수도 있으며 임의의 값이 추가되는것에 제약을 줄 수도 있다.  

<img width="1099" alt="3-44" src="https://user-images.githubusercontent.com/43739827/74231543-28ef3b00-4d0a-11ea-9dd1-40dbb8bbd0dc.png"></img>  
> result열의 데이터를 읽어들여 값들의 범주를 확인하였다.  

원본 데이터 프레임에서 추출한 열의 자료형을 위에서 생성한 범주형 자료형으로 변경한다.  

<img width="1100" alt="3-45" src="https://user-images.githubusercontent.com/43739827/74232173-92bc1480-4d0b-11ea-9750-6deec7ba347c.png"></img>  

범주형 열에 범주에 속하지 않은 데이터를 입력하려고 하면 예외가 발생한다.  

<img width="1104" alt="3-46" src="https://user-images.githubusercontent.com/43739827/74232392-06f6b800-4d0c-11ea-9aef-424cb11407b2.png"></img>  

이번에는 특정한 열의 범위를 지정해 그 범위에 속한 데이터를 토대로 범주형 데이터를 가지는 새로운 열을 만들어보려 한다.  

<img width="1097" alt="3-47" src="https://user-images.githubusercontent.com/43739827/74233212-9b154f00-4d0d-11ea-82a8-6930b6f94dc6.png"></img>  
> home_goals열에 0~2의 범위를 **.between** 메소드로 정해주고 그 범위 안에 데이터가 속해있다면 '승'을, 그렇지 않다면 '대승'을 새롭게 생성한 'home_result'열에 삽입하였다.  

생성된 열이 범주형 처리된것을 확인할 수 있다.  

<img width="1107" alt="3-48" src="https://user-images.githubusercontent.com/43739827/74233512-2858a380-4d0e-11ea-8936-5ed679ce3fff.png"></img>
