# Class  
판다스의 주요 클래스인 시리즈와 데이터 프레임의 인스턴스를 생성하고 슬라이싱, 검색, 인덱서등을 알아본다.  

## 1. 시리즈와 데이터 프레임 구조  

* 시리즈  
배열은 인덱스와 해당 값을 갖는 구조로 만들어진다. 판다스의 시리즈또한 배열을 나타내지만 일반적인 배열과 차이점이 있다. 시리즈는 인덱스에 레이블을 추가적으로 붙여 사용할 수 있는 구조이다. 즉, 특정 이름으로 검색이 가능하다는 것이다. 이것은 파이썬의 딕셔너리와 비슷한 형태를 가지지만 차이점은 시리즈의 모든 값은 단일 자료형이라는 것이다.  

<img width="1078" alt="2-1" src="https://user-images.githubusercontent.com/43739827/73939244-662f8380-492c-11ea-8c5f-6c9790df4366.png"></img>  

* 시리즈 구성  
시리즈는 판다스에서 제공하는 1차원 배열이면서 판다스 모듈의 기본적인 클래스다. 배열의 데이터에 접근할 때 레이블이 부여된 값들에 접근하는데 1차원 배열로 구성되면 이 레이블을 다양한 형태(ex. 숫자, 문자열, 날짜 등)로 구성할 수 있다. 또한 인덱스는 지켜야할 순서가 없어 사용자 임의로 지정 가능하다.  

파이썬의 리스트와 딕셔너리를 이용해서 데이터와 인덱스로 구성된 시리즈를 생성할 수 있다.

<img width="1081" alt="2-2" src="https://user-images.githubusercontent.com/43739827/73939781-857ae080-492d-11ea-9978-725862ba6344.png"></img>  

시리즈 클래스의 생성자(constructor, 일종의 메소드로써 멤버 변수를 초기화함)를 이용해 시리즈를 만들고자 한다면 매개변수 data, index, name에 값을 지정한다.  

<img width="1075" alt="2-3" src="https://user-images.githubusercontent.com/43739827/74022938-e5cb5a00-49e1-11ea-876a-1e92cf4fc610.png"></img>  

<img width="892" alt="2-4" src="https://user-images.githubusercontent.com/43739827/74023056-19a67f80-49e2-11ea-8e43-5dc4ac31a2b7.png"></img>  
> 판다스의 생성자 [Pandas Github(Series)](https://github.com/pandas-dev/pandas/blob/v1.0.1/pandas/core/series.py#L122-L4567, "Pandas Github")

시리즈에 name을 확인해보면 생성시에 지정한 'ex_series'가 반환되는것을 알 수 있다. 또한 chapter1에서 언급한것처럼 자료형을 따로 지정하지 않아도 요소들을 확인해 자료형을 자동으로 인식하는데 객체를 생성할때 짝수인 정수들을 선언했으므로 **int64** 가 반환되는것을 알 수 있다.  

<img width="1076" alt="2-5" src="https://user-images.githubusercontent.com/43739827/74023429-00ea9980-49e3-11ea-8a66-b484ff258f85.png"></img>

시리즈나 데이터 프레임의 형태와 차원을 알고싶다면 **.shape** 와 **.ndim** 을 사용한다. 앞서 생성한 시리즈인 'series'에는 5개의 정수가 들어있기 때문에 (5,)라는 튜플로 출력이되며 1차원이므로 .ndim은 1을 반환한다. 마찬가지로 데이터 프레임을 생성하고 shape와 ndim을 사용하면 모양과 차원이 반환되는것을 알 수 있다.

<img width="1078" alt="2-6" src="https://user-images.githubusercontent.com/43739827/74024016-4c517780-49e4-11ea-80be-3bd0e66b1c87.png"></img>

<img width="1083" alt="2-7" src="https://user-images.githubusercontent.com/43739827/74024154-8fabe600-49e4-11ea-9b4f-727b5bac74ee.png"></img>  
> 데이터 프레임에서는 .name을 사용할 수 없다. 이유는 name은 시리즈에서만 생성자로 사용되기 때문이다.  

<img width="884" alt="2-8" src="https://user-images.githubusercontent.com/43739827/74024299-ec0f0580-49e4-11ea-9d79-d5c1d61902f9.png"></img>  
> 데이터 프레임 생성자 [Pandas Github(Data Frame)](https://github.com/pandas-dev/pandas/blob/v1.0.1/pandas/core/frame.py#L319-L8448, "Pandas Github")

시리즈와 데이터 프레임은 **.size** 를 사용하여 크기를 알 수 있다.  
<img width="1083" alt="2-9" src="https://user-images.githubusercontent.com/43739827/74024558-80796800-49e5-11ea-9ff9-98b9836957da.png"></img>  
> 크기가 정수로 반환된것을 확인할 수 있다.

앞서 생성한 시리즈에 인덱스를 지정해줬었다. 이 인덱스를 확인하기 위해서는 **.index** 를 사용한다. 'series' 객체를 생성할 때 인덱스를 문자형 '12345'를 리스트로 쪼개어 분할 지정해주었기 때문에 자료형이 판다스의 자료형인 'object'로 반환되었다.  

<img width="1087" alt="2-10" src="https://user-images.githubusercontent.com/43739827/74025021-655b2800-49e6-11ea-98f7-5a529c17e588.png"></img>  
> 인덱스의 선언방식에 따라 정수도 가능하다.

* 데이터 프레임  

데이터 프레임은 열을 기반으로 되어있기에 각 차원의 원소가 1차원인 시리즈로 저장된다. 또한 데이터 프레임은 두 개의 인덱스(.index, .column)로 구성되어 있으며(즉 행과 열에 라벨링되어 있다는 의미이다.) 자료를 검색할 때는 .values 속성을 이용해 인덱스를 참조하여 원하는 요소를 찾는 구조이다.

기본적으로 파이썬 리스트나 딕셔너리를 이용해 데이터를 넣어 생성할 수 있다.  

<img width="1073" alt="2-11" src="https://user-images.githubusercontent.com/43739827/74025611-b3246000-49e7-11ea-941d-c34150f68f91.png"></img>  

데이터 프레임도 생성자를 이용한 생성이 가능하다. 단, 시리즈와 달리 2차원이기에 생성자의 종류가 다르기 때문에 이 차이를 확실히 알고 있어야 한다. 기본적으로는 data, index, columns를 선언하며 data에는 저장될 요소가 들어가고 index는 행, columns는 열의 레이블을 설정한다.

<img width="1085" alt="2-22" src="https://user-images.githubusercontent.com/43739827/74025915-5bd2bf80-49e8-11ea-9849-1dffc5d3bde1.png"></img>  
> 행과 열에 레이블과 값들이 매핑된것을 확인할 수 있다.  

데이터 프레임은 2차원이기 때문에 .index속성과 **.columns** 속성을 제공한다. 이 두 속성으로 행과 열의 레이블과 그것의 자료형을 확인할 수 있다.  

<img width="716" alt="2-13" src="https://user-images.githubusercontent.com/43739827/74026140-dac7f800-49e8-11ea-925d-92febdede172.png"></img>

데이터 프레임의 간결한 정보를 확인하고 싶다면 **.info** 메소드를 사용한다.

<img width="715" alt="2-14" src="https://user-images.githubusercontent.com/43739827/74026355-59bd3080-49e9-11ea-9211-78b32bfdb242.png"></img>  
> 요소의 정보나 메모리에 대한 정보까지도 확인할 수 있다.  

* 시리즈와 데이터 프레임 내부 멤버 확인  

<img width="886" alt="9" src="https://user-images.githubusercontent.com/43739827/73745585-bbd22780-4796-11ea-991d-d8d136cb36cf.png"></img>  
> dir 함수로 시리즈와 데이터 프레임 클래스의 내부 멤버를 확인한다.  

<img width="883" alt="10" src="https://user-images.githubusercontent.com/43739827/73745747-11a6cf80-4797-11ea-9f16-3f6c96257a2b.png"></img>  
> 차집합을 사용해 시리즈에만 속한 멤버만 출력한다.

<img width="890" alt="11" src="https://user-images.githubusercontent.com/43739827/73745843-49157c00-4797-11ea-8fb9-92faf3249637.png"></img>  
> 차집합을 사용해 데이터 프레임에만 있는 멤버만 출력한다.

<img width="1086" alt="2-15" src="https://user-images.githubusercontent.com/43739827/74026992-a48b7800-49ea-11ea-97ab-c643ed8a8558.png"></img>    
> 교집합을 사용해 시리즈와 데이터 프레임에 공통으로 있는 멤버만 출력한다.


<img width="470" alt="2-16" src="https://user-images.githubusercontent.com/43739827/74027246-21b6ed00-49eb-11ea-9e51-f8c7e0def158.png"></img>  
> 출력 결과


* 파일에 저장된 멤버 정보 읽고 확인하기  

판다스에서 제공하는 .read_csv 함수를 통해 csv 파일을 읽으면 csv 파일이 기본 2차원 데이터이기 때문에 데이터 프레임으로 변환된다. 이때 각 열에 대한 정보를 usecols 매개변수를 이용해서 처리한다.  

또한 파일이 저장된 텍스트를 utf-8을 기준으로 변환해야 encoding 매개변수에 변환 기준인 euc-kr로 인코딩한다.  

저장된 df_f 변수에 데이터 프레임이 할당되어 있으므로 점 연산자를 통해서 .head 메소드로 내부의 값을 조회한다.  

판다스에는 csv 파일을 읽어 데이터 프레임으로 변환할 수 있는 **.read_csv** 함수가 존재한다. 이때 각 열에 대한 정보는 **usecols** 매개변수를 이용한다.

<img width="1087" alt="2-17" src="https://user-images.githubusercontent.com/43739827/74027741-1c0dd700-49ec-11ea-8ee8-5c0a69a1f6e4.png">  
> head를 이용해 위 5개행을 출력하여 확인.  

이 데이터 프레임의 행과 열에 대한 정보에서 모양(.shape) 속성을 확인하면 행은 19개이고 열은 2개인 것을 알 수 있다.  

<img width="888" alt="15" src="https://user-images.githubusercontent.com/43739827/73746888-9a266f80-4799-11ea-8d87-bd9c4b554657.png"></img>  

데이터 프레임에서 하나의 열을 조회하려면 인덱싱 연산자([])를 이용해 열의 이름을 문자열로 넣어서 조회한다. 한 차원으로 축소된 열이 조회되어 이것을 시리즈로 보여준다. 이를 .head 메소드로 조회하면 상위 5개에 대한 정보를 확인할 수 있다.  

<img width="890" alt="16" src="https://user-images.githubusercontent.com/43739827/73747078-f5f0f880-4799-11ea-90ef-8a3955ec7903.png"></img>  

각 열의 누락값의 개수를 확인하기 위해 각 열을 검색 조건으로 지정하고 **.isnull().sum()** 을 하였다. 만약 각 열마다 누락값이 존재한다면 그에 맞는 정수가 반환될것이다.  

<img width="1085" alt="2-18" src="https://user-images.githubusercontent.com/43739827/74028084-e0bfd800-49ec-11ea-858e-a52790fc477b.png"></img>  
> 파이썬의 bool 클래스가 int 클래스를 상속하기 때문에 .sum이 사용가능하다. 단순히 isnull을 사용하면 True 혹은 False의 결과가 출력될것이다.

데이터 프레임 각 열에 비교연산자를 사용한 결과가 시리즈로 출력되는것을 확인할 수 있으며 내부 데이터는 True혹은 False의 bool값으로 채워지는것을 알 수 있다.

<img width="887" alt="17" src="https://user-images.githubusercontent.com/43739827/73747301-829bb680-479a-11ea-96d1-61a85189e7a3.png"></img>  

## 2. 시리즈 생성 방법  
* 시리즈 생성자   
시리즈는 크게 리스트, 딕셔너리, 넘파이를 이용해 생성할 수 있다.  

<img width="1085" alt="2-19" src="https://user-images.githubusercontent.com/43739827/74029368-e4089300-49ef-11ea-846b-6bdc90282351.png"></img>  
> 리스트로 시리즈를 생성하였다. **.values** 속성을 사용하면 시리즈의 값들이 넘파이 배열로 표시된다.  

<img width="1084" alt="2-20" src="https://user-images.githubusercontent.com/43739827/74029554-4b264780-49f0-11ea-9d3c-af51082d5629.png"></img>  
> index를 설정하지 않아 암묵적인 RangeIndex가 설정되었다. 또한 일정 범위의 정수이므로 자료형은 int64이다.

<img width="754" alt="2-21" src="https://user-images.githubusercontent.com/43739827/74029958-372f1580-49f1-11ea-84f7-10a9175f298f.png"></img>  
> .dtype속성의 자료형들<출처: 손에 잡히는 판다스 p.51. 문용준 저>  

<img width="1083" alt="2-22" src="https://user-images.githubusercontent.com/43739827/74030234-e835b000-49f1-11ea-9a85-f879bc06f3aa.png"></img>  
> 딕셔너리로 시리즈를 생성하였다. 또한 name을 설정하여 시리즈에 따로 이름을 부여하였다.  

<img width="1086" alt="2-23" src="https://user-images.githubusercontent.com/43739827/74030623-d9033200-49f2-11ea-8488-472b27de7111.png"></img>  
> 넘파이로 시리즈를 생성하였다.  

* 시리즈 구성 속성  

<img width="1082" alt="2-24" src="https://user-images.githubusercontent.com/43739827/74031100-01d7f700-49f4-11ea-9a83-dd04f821596a.png"></img>  
> **.empty** 속성은 시리즈의 내부가 비어있는지 확인할 때 사용한다.  

## 3.데이터 프레임 생성  
* 데이터 프레임 생성자  
데이터 프레임은 크게 리스트, 딕셔너리, 시리즈를 이용해 생성할 수 있다.  

<img width="1086" alt="2-25" src="https://user-images.githubusercontent.com/43739827/74031672-79f2ec80-49f5-11ea-87e7-9efc8b0d578b.png"></img>  
> 리스트로 데이터 프레임을 생성하였다.  

<img width="1076" alt="2-30" src="https://user-images.githubusercontent.com/43739827/74083162-491dc080-4aa4-11ea-8530-d66898c4f6f6.png"></img>  
> 두 개의 리스트를 zip으로 묶어 마치 딕셔너리처럼 만든 후에 데이터 프레임을 생성할 수도 있다.  

<img width="1086" alt="2-26" src="https://user-images.githubusercontent.com/43739827/74031735-9ee75f80-49f5-11ea-882c-c6ec5080cff2.png"></img>  
> 딕셔너리로 데이터 프레임을 생성하였다. 시리즈와 다르게 데이터 프레임은 2차원으로 구성되어 있으므로 딕셔너리안에 딕셔너리가 들어가는 형태로 저장해야 한다.  

<img width="1086" alt="2-27" src="https://user-images.githubusercontent.com/43739827/74032121-917ea500-49f6-11ea-8861-dbe4cacdc16c.png"></img>  
> 시리즈로 데이터 프레임을 생성하였다.

<img width="1085" alt="2-28" src="https://user-images.githubusercontent.com/43739827/74032245-d0145f80-49f6-11ea-8848-349813127e23.png"></img>  
> 데이터 프레임의 특정 열 추출 및 원본 시리즈와의 비교 연산자 반환 결과  

<img width="1088" alt="2-29" src="https://user-images.githubusercontent.com/43739827/74032351-1964af00-49f7-11ea-9133-510ec51d795b.png"></img>  
> 시리즈를 딕셔너리형태가 아닌 파이썬의 리스트형태로 데이터 프레임을 생성하면 모양이 달라지는것을 확인할 수 있다. 이것은 키 값이 없기 때문에 시리즈를 행의 레이블로 인식하여 행 단위로 저장하기 때문이다.  

## 4. 인덱스 검색  
시리즈는 행 단위로 구성되어 있어 인덱스 검색을 하게되면 행을 기준으로 검색한다. 그러나 데이터 프레임은 2차원 구조로써 열 단위로 구성되어 있기 때문에 인덱스 검색을 하게되면 열 단위로 조회가 가능하다.  

<img width="1076" alt="2-31" src="https://user-images.githubusercontent.com/43739827/74083453-85065500-4aa7-11ea-83f1-b7c838202d3d.png"></img>  
> csv파일을 불러와 데이터 프레임으로 생성하였다.   

**팬시 인덱싱** 을 통한 검색도 가능하다.  

<img width="1093" alt="2-32" src="https://user-images.githubusercontent.com/43739827/74083481-eaf2dc80-4aa7-11ea-9b09-5e3da0256eef.png"></img>  
> 팬시 인덱싱이란 열의 레이블을 리스트형으로 지정하거나 행을 **콜론(:)** 으로 지정하여 검색하는 방식을 사용한다.  

<img width="1093" alt="2-33" src="https://user-images.githubusercontent.com/43739827/74083529-77050400-4aa8-11ea-8555-16a9714107dc.png"></img>  
> loc과 iloc을 사용한 검색도 가능하다. 결과는 동일하지만 두 속성이 가지는 매개변수의 차이점을 명확히 알고 있어야 한다.  

<img width="1089" alt="2-34" src="https://user-images.githubusercontent.com/43739827/74083552-c1868080-4aa8-11ea-9846-3fe5c28f4efb.png"></img>  
> .drop을 사용해서 지정한 조건을 제외한 데이터 프레임을 보여줄수도 있다. 괄호안에는 추출할 열과 축(0은 열 1은 헹)을 지정한다.  

1. 일반 검색  

<img width="1092" alt="2-35" src="https://user-images.githubusercontent.com/43739827/74083716-a583de80-4aaa-11ea-9d42-d20ae12321c3.png"></img>  
> 데이터를 확인할때는 행과 열의 개수는 필수적으로 확인해야할 사항이다.  

2. [] 검색  

<img width="1087" alt="2-36" src="https://user-images.githubusercontent.com/43739827/74083797-538f8880-4aab-11ea-8664-7d5a6384561d.png"></img>  

3. [] 슬라이싱  
슬라이싱 검색은 행을 기준으로 처리하며 열을 기준으로 처리하는것은 불가능하다.  

<img width="1091" alt="2-37" src="https://user-images.githubusercontent.com/43739827/74083853-e16b7380-4aab-11ea-824b-5bf6884c738d.png"></img>  

* 마스킹 검색  
판다스는 인덱스 검색 조건을 다양하게 지정할 수 있도록 되어있다. 예로 논리식을 사용해 내부 요소를 True or False로 찾아낼 수도 있다. 이것을 **Boolean Masking** 이라 한다.  

<img width="1088" alt="2-39" src="https://user-images.githubusercontent.com/43739827/74084307-31006e00-4ab1-11ea-9605-77c770b958ae.png"></img>  
> 단일 논리식에 의한 불리언 검색결과  

<img width="1089" alt="2-38" src="https://user-images.githubusercontent.com/43739827/74084347-89d00680-4ab1-11ea-8f2f-851587778681.png"></img>
> 다중 논리식에 의한 불리언 검색결과  

* 팬시 검색  

<img width="1088" alt="2-39" src="https://user-images.githubusercontent.com/43739827/74084519-44acd400-4ab3-11ea-9848-211da8913e50.png"></img>  
> 많은 정보가 들어있는 csv 파일을 불러와 데이터 프레임으로 만들었다.  

<img width="1088" alt="2-40" src="https://user-images.githubusercontent.com/43739827/74084575-ca308400-4ab3-11ea-93d4-015cfb718767.png"></img>  
> 열의 레이블을 리스트형으로 지정하여 필요한 정보만 추출하였다.**isnull().sum()** 을 사용하여 누락값이 있는지를. 확인하였다.  

<img width="1091" alt="2-41" src="https://user-images.githubusercontent.com/43739827/74084623-2eebde80-4ab4-11ea-8b7c-9293f92bc7e5.png"></img>  
> 시리즈또한 팬시 검색이 가능하다.  

## 5. 인덱서 검색  

데이터 프레임은 인덱스 검색을 하게되면 열을 기준으로 처리한다고 설명했었다. 만약 행을 기준으로 처리하고자 한다면 인덱서 클래스의 속성으로 처리할 수 있다. 또한 인덱서 검색은 복합 조회도 가능해 행과 열을 동시에 지정할 수 있다.  

인덱서는 크게 명시적인 레이블을 사용하는 .loc과 암묵적인 레이블을 사용하는 .iloc이 있다.  

* 명시적 인덱서  
명시적이란 시리즈와 데이터 프레임이 가지는 행과 열에 레이블의 정보를 이용한다는 뜻이다.  

<img width="1098" alt="2-42" src="https://user-images.githubusercontent.com/43739827/74084746-61e2a200-4ab5-11ea-9c15-9cff8094a5ae.png"></img>  
> 행과 열의 레이블을 모두 입력하면 해당 정보를 얻을 수 있다.  

파이썬 슬라이싱의 경우도 행과 열에서 모두 사용할 수 있다.  

<img width="1098" alt="2-42" src="https://user-images.githubusercontent.com/43739827/74084746-61e2a200-4ab5-11ea-9c15-9cff8094a5ae.png"></img>  
> 시리즈로 출력되는것을 확인할 수 있다.  

<img width="1088" alt="2-43" src="https://user-images.githubusercontent.com/43739827/74084814-24cadf80-4ab6-11ea-8f8a-d3eedc51afdf.png"></img>  
> 데이터 프레임으로의 출력도 가능하다.  

시리즈와 데이터 프레임의 공통적인 메소드중 **.xs()** 는 행과 열을 중심으로 데이터를 가져올 수 있다. 기본적으로는 행 단위 정보를 가져온다.  

<img width="1087" alt="2-44" src="https://user-images.githubusercontent.com/43739827/74084893-14673480-4ab7-11ea-8353-c627a7a3e315.png"></img>  
> 열 단위로 정보를 가져오고 싶다면 특정 열을 지정해주고 axis=1(1만 써주어도 된다.)를 지정하면 된다.  

<img width="1095" alt="2-45" src="https://user-images.githubusercontent.com/43739827/74084990-c56dcf00-4ab7-11ea-9e8b-dda70a8f32ad.png"></img>  
> 특정 행과 열의 레이블을 지정해 값을 출력하는 **.lookup()** 메소드는 해당값을 넘파이 배열로 반환한다.

* 암묵적 인덱서  
암묵적 인덱서는 레이블에 관련 없이 모두 0에서부터 시작하여 접근한다.

<img width="1099" alt="2-46" src="https://user-images.githubusercontent.com/43739827/74085067-b3406080-4ab8-11ea-9566-d95419350478.png"></img>  
> 반환값을 시리즈로 하기 위해서는 열의 위치에 리스트를 넣으면 된다.  

<img width="1096" alt="2-47" src="https://user-images.githubusercontent.com/43739827/74085092-f3074800-4ab8-11ea-84c6-fa31dc3456b1.png"></img>  
> 여러 열에 대한 정보를 얻기위해선 열의 리스트에 원하는 포지션 넘버를 지정해주면 된다.  

<img width="1096" alt="2-48" src="https://user-images.githubusercontent.com/43739827/74085147-598c6600-4ab9-11ea-8d7f-ee2872519c1b.png"></img>  
> 행과 열에 콜론을 넣어 슬라이스를 해주면 그 범위만큼의 데이터 프레임이 반환된다.  

* 복합 검색  

<img width="1097" alt="2-49" src="https://user-images.githubusercontent.com/43739827/74085246-6d849780-4aba-11ea-81f3-2828d72b5bbc.png"></img>  
> 조건문을 통한 명시적 인덱서를 통해 조건에 부합하는 데이터 프레임을 생성할 수 있다.  

* 문자열 값  
인덱서는 문자열로 된 레이블을 처리할 때 문자열의 순서로 검색할 수 있도록 내부적으로 지원한다. 특히 슬라이스는 문자의 순서가 중요하기 때문에 정렬하지 않으면 예외가 발생할 수 있다.  

<img width="1097" alt="2-50" src="https://user-images.githubusercontent.com/43739827/74085721-6e6bf800-4abf-11ea-9196-7dd6a6808654.png"></img>  
> 지정한 열의 정보가 인덱스로 만들어진다.   

<img width="1099" alt="2-51" src="https://user-images.githubusercontent.com/43739827/74085760-ecc89a00-4abf-11ea-9978-bfc85b09f47b.png"></img>  
> 행의 인덱스가 정렬된것을 확인할 수 있다.  

##  6. 갱신과 삭제  

* 열 및 원소 추가 및 갱신  
데이터 프레임의 열을 단순 추가 및 갱신할 때는 파이썬의 **__setitem__** 메소드를 사용한다. 이렇게하면 인덱스 검색과 할당 연산자를 동시에 사용해 할당 연산자 다음에 값을 넣어 처리한다.  

<img width="893" alt="2-52" src="https://user-images.githubusercontent.com/43739827/74100088-3ff92600-4b6e-11ea-86c8-545cc49b3468.png"></img>  
> 데이터 프레임의 __setitem__ [Pandas DataFrame Github](https://github.com/pandas-dev/pandas/blob/v1.0.1/pandas/core/frame.py#L319-L8448, "Pandas Github")  

<img width="1081" alt="2-53" src="https://user-images.githubusercontent.com/43739827/74100269-3a9cdb00-4b70-11ea-8f3c-4516f560e047.png"></img>  
> usecols를 사용하여 특정한 열만을 csv파일로부터 읽어들여 데이터 프레임을 만들었다.

<img width="1082" alt="2-54" src="https://user-images.githubusercontent.com/43739827/74100327-037af980-4b71-11ea-987c-dd4270d7552a.png"></img>  
> 'count'라는 열을 생성하고 초기값을 스칼라(상수)값 0을 지정하였다. loop문 없이도 판다스는 자동적으로 브로드캐스팅하여 열의 길이를 맞춰준다.  

<img width="1105" alt="2-55" src="https://user-images.githubusercontent.com/43739827/74100627-92d5dc00-4b74-11ea-8227-f3f22b7f9ead.png"></img>  
> 인덱스를 불러와 + 1을 해주고 'count'열에 삽입하였다. 누락된 값이 없는것을 확인할 수 있다.  

**.insert** 메소드를 이용해 열을 추가할 수 있다.

<img width="1091" alt="2-56" src="https://user-images.githubusercontent.com/43739827/74100759-99b11e80-4b75-11ea-9371-0202c5456b2d.png"></img>  
> **replace** 는 데이터값을 변환할때 사용하며 변환할 값과 변환한 후의 값을 명시해야 한다.  

<img width="1089" alt="2-57" src="https://user-images.githubusercontent.com/43739827/74100829-4be8e600-4b76-11ea-88c9-88ced3dc200c.png"></img>  
> **get_loc** 메소드로 지정한 열의 위치를 정수값으로 얻을 수 있다.  

* 특정 원소 갱신  

<img width="1090" alt="2-58" src="https://user-images.githubusercontent.com/43739827/74101696-fdd8e000-4b7f-11ea-85b8-4d0fc11d428f.png"></img>  
> 행과 열의 레이블을 입력하여 특정 데이터만을 변경할 수 있다.

* 행 및 열 삭제  
시리즈와 데이터 프레임의 행과 열을  삭제할때는 **.drop** 메소드를 이용한다.  

데이터 프레임은 .drop 메소드를 사용할 때 축(axis)를 지정한다. 행 단위 삭제는 axis=0, 열 단위 삭제는 axis=1임을 기억한다.  

<img width="1091" alt="2-59" src="https://user-images.githubusercontent.com/43739827/74101846-5e1c5180-4b81-11ea-9e30-53394a516854.png"></img>


<img width="1092" alt="2-60" src="https://user-images.githubusercontent.com/43739827/74101886-bf442500-4b81-11ea-95c4-07069a131fa9.png"></img>  

데이터 프레임 내부를 변경하기 위해서는 **inplace=True** 를 인자로 넣어야 한다. 데이터의 양이 많다면 자신을 변경하는 것에 문제가 발생할 수 있으므로 지속적인 삭제가 도움이 될 수 있다.  

<img width="1088" alt="2-61" src="https://user-images.githubusercontent.com/43739827/74101983-9a03e680-4b82-11ea-8f74-adeec1b0808e.png"></img>  
> inplace의 여부에 따라 반환되는 데이터 프레임이 다른것을 알 수 있다.  

## 7. 문자열 데이터 처리  

* 문자열 조회  
문자열을 처리하기 위해 하나의 열을 지정하여 시리즈로 만들었다.  

<img width="1087" alt="2-62" src="https://user-images.githubusercontent.com/43739827/74102049-34642a00-4b83-11ea-969c-2a6c6157f2d8.png"></img>  

<img width="1085" alt="2-63" src="https://user-images.githubusercontent.com/43739827/74102104-cbc97d00-4b83-11ea-9b30-53f84cdb0da7.png"></img>  

<img width="1091" alt="2-64" src="https://user-images.githubusercontent.com/43739827/74102130-0a5f3780-4b84-11ea-9517-ea4fd4b7690d.png"></img>  

<img width="1093" alt="2-65" src="https://user-images.githubusercontent.com/43739827/74102170-5f9b4900-4b84-11ea-8444-fb6e05781ae3.png"></img>  

* 문자열 변경  
문자열은 변하지 않는 값으로써 변경이 불가능하다. 그렇기 때문에 새로운 값으로 대체하여 마치 변경한것처럼 하는것이 가능하다.  

<img width="1088" alt="2-66" src="https://user-images.githubusercontent.com/43739827/74102339-13510880-4b86-11ea-8bc8-5b141c6a7b2a.png"></img>  

<img width="768" alt="2-67" src="https://user-images.githubusercontent.com/43739827/74102376-59a66780-4b86-11ea-8cdb-2117d9b17da0.png"></img>  
> strip은 시리즈에서는 가능하나 데이터 프레임에서는 사용할 수 없다.  

**split** 메소드는 문자열을 특정 단위로 나눌 때 사용한다.  

<img width="1088" alt="2-68" src="https://user-images.githubusercontent.com/43739827/74102494-35975600-4b87-11ea-9a23-887708b03f09.png"></img>  

split 메소드에 **expand=True** 를 넣어주면 시리즈를 데이터 프레임으로 변환하는것이 가능하다. 또한 **n** 을 지정하면 문자열을 조건대로 분할할때의 제한을 둘 수 있다.  

<img width="1097" alt="2-69" src="https://user-images.githubusercontent.com/43739827/74102579-24027e00-4b88-11ea-8548-0871092c21db.png"></img>  
> rsplit과 split에 따라 같은 n=1임에도 반환되는 데이터 프레임이 달라지는것을 확인할 수 있다.  

문자열에 특정 단어를 바꾸고자 할때는 **.replace** 메소드를 사용한다.  

<img width="1097" alt="2-70" src="https://user-images.githubusercontent.com/43739827/74102605-67f58300-4b88-11ea-9da4-a8617f4053d5.png"></img>   

**.cat** 메소드는 문자열을 통합시키는 역할을 하며 합쳐질 단어마다 구분을 하고 싶다면 **sep** 에 특정한 심볼을 넣어준다.  

<img width="1101" alt="2-71" src="https://user-images.githubusercontent.com/43739827/74102625-befb5800-4b88-11ea-85de-3039290bc019.png"></img>  

기존의 객체에 새롭게 추가하고자 할 때는 행의 개수가 일치하도록 해야 한다.  

<img width="1103" alt="2-72" src="https://user-images.githubusercontent.com/43739827/74102667-0eda1f00-4b89-11ea-93cd-1cf23c9044b4.png"></img>
> 행의 개수가 맞지않아 오류가 발생하였다.
