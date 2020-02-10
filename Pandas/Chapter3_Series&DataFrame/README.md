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

 
