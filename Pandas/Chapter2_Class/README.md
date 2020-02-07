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

<img width="1086" alt="2-26" src="https://user-images.githubusercontent.com/43739827/74031735-9ee75f80-49f5-11ea-882c-c6ec5080cff2.png"></img>  
> 딕셔너리로 데이터 프레임을 생성하였다. 시리즈와 다르게 데이터 프레임은 2차원으로 구성되어 있으므로 딕셔너리안에 딕셔너리가 들어가는 형태로 저장해야 한다.  

<img width="1086" alt="2-27" src="https://user-images.githubusercontent.com/43739827/74032121-917ea500-49f6-11ea-8861-dbe4cacdc16c.png"></img>  
> 시리즈로 데이터 프레임을 생성하였다.

<img width="1085" alt="2-28" src="https://user-images.githubusercontent.com/43739827/74032245-d0145f80-49f6-11ea-8848-349813127e23.png"></img>  
> 데이터 프레임의 특정 열 추출 및 원본 시리즈와의 비교 연산자 반환 결과  

<img width="1088" alt="2-29" src="https://user-images.githubusercontent.com/43739827/74032351-1964af00-49f7-11ea-9133-510ec51d795b.png"></img>  
> 시리즈를 딕셔너리형태가 아닌 파이썬의 리스트형태로 데이터 프레임을 생성하면 모양이 달라지는것을 확인할 수 있다. 이것은 키 값이 없기 때문에 시리즈를 행의 레이블로 인식하여 행 단위로 저장하기 때문이다.  

* 데이터 프레임 구성 기본 속성
