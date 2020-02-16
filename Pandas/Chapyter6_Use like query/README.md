# 6. Use Pandas like query

판다스에서 데이터 프레임을 처리하는 방식들중 데이터베이스의 테이블을 처리하는 방식과 유사한것이 많다. 그 이유는 데이터 프레임의 구조가 테이블과 상당히 닮아있기 때문이다. Chapter6를 통해 데이터베이스의 테이블 처리방식과 판다스의 데이터 프레임 처리방식이 어떻게 유사하고 다른지 확인한다.  

## 1. .merge 메소드  

**.merge** 메소드는 다양한 매개변수를 이용해 두 개의 데이터 프레임 요소들의 병합을 가능하게 한다.  

* 데이터 통합   
데이터를 합치는 과정을 확인하기 위해 행과 열의 인덱스 레이블이 같고 모양도 동일한 두 개의 데이터 프레임을 생성한다.   

<img width="1090" alt="6-1" src="https://user-images.githubusercontent.com/43739827/74600987-2a3eb000-50dc-11ea-8e1c-fb43f68276e1.png"></img>  
> 데이터 요소를 난수로 생성하기 때문에 두 데이터 프레임간에 유일한 차이점은 데이터의 내용이다.  

merge를 실행해보면 열의 레이블 정보만 출력되는것을 확인할 수 있다. 이유는 두 데이터 프레임간 매치되는 데이터가 없기 때문이다.

<img width="1080" alt="6-2" src="https://user-images.githubusercontent.com/43739827/74601061-ed26ed80-50dc-11ea-9d67-1c29a5b9759a.png"></img>  

행과 열의 인덱스 레이블이 같고 데이터의 값들도 같은 두 개의 데이터 프레임을 생성하여 다시 merge 결과를 확인한다.  

<img width="1081" alt="6-3" src="https://user-images.githubusercontent.com/43739827/74601116-90780280-50dd-11ea-9ec5-8dede26cc55a.png"></img>  
> 각 데이터 프레임의 키를 정하기 위해 매개변수 **left_on** 과 **right_on** 을 사용하였으며 inner join으로 지정하였다.  

생성한 두 데이터 프레임의 키를 같은 레이블의 인덱스로 정한다면 매개변수 **on** 을 사용한다. 생성된 데이터 프레임이 위의 결과와 동일한 것을 확인할 수 있다.  

<img width="1083" alt="6-4" src="https://user-images.githubusercontent.com/43739827/74601159-33308100-50de-11ea-9e35-a0c3ba9dacb9.png"></img>  

**.join** 메소드를 사용하여 merge 메소드처럼 두 데이터 프레임을 합칠 수 있다. 차이점은 두 데이터 프레임간 동일한 열을 키로 지정하여 합쳐도 두 키가 모두 출력된다는 것이다.  

<img width="1094" alt="6-5" src="https://user-images.githubusercontent.com/43739827/74601220-2a8c7a80-50df-11ea-9fad-f27fdc55bff1.png"></img>  
> join메소드의 매개변수 **lsuffix** 와 **rsuffix** 를 이용해 동일한 열의 레이블을 구분지을 수 있다.  

두 데이터 프레임간 일치하는 요소가 없어 inner join을 할 수 없다면 **outer join** 을 사용한다. 이 때 일치하지 않는 열은 누락 값 NaN으로 채워진다.  

<img width="1090" alt="6-6" src="https://user-images.githubusercontent.com/43739827/74601268-aab2e000-50df-11ea-984e-f0f0daf495c0.png"></img>  

<img width="1088" alt="6-7" src="https://user-images.githubusercontent.com/43739827/74601361-c8cd1000-50e0-11ea-966b-a6db0ac1fe9c.png"></img>  


이번에는 동일한 데이터 요소를 가지지만 키의 레이블이 다른 두 데이터 프레임의 처리 과정을 알아본다.  

<img width="1096" alt="6-8" src="https://user-images.githubusercontent.com/43739827/74601369-ef8b4680-50e0-11ea-9a94-819ef65fd960.png"></img>  

<img width="1093" alt="6-9" src="https://user-images.githubusercontent.com/43739827/74601389-32e5b500-50e1-11ea-972d-21a21e7a030b.png"></img>  
> 매개변수 left_on과 right_on에 각 데이터 프레임에서 데이터 요소가 일치하는 열을 기입했다.  

merge된 데이터 프레임을 보면 키로 지정된 열의 레이블이 다르기때문에 전부 결과 데이터 프레임에 삽입된 것을 확인할 수 있다. 중복되는 열을 삭제하고자 한다면 merge 과정에서 메소드 체인을 이용해 drop 메소드를 활용한다.  

<img width="1095" alt="6-10" src="https://user-images.githubusercontent.com/43739827/74601462-0c744980-50e2-11ea-9c53-d2f9b542ac1c.png"></img>  

일치하는 데이터를 찾아 두 데이터 프레임을 병합시켰다면 행의 인덱스를 기준으로 통합하는 방법도 존재한다. 두 데이터 프레임을 생성하고 키를 설정하기 위해 하나의 열은 동일하게 생성하였다. 또한 행을 기준으로 병합하기위해 각 데이터 프레임에 .set_index 메소드로 키 열을 지정해주었다.  

<img width="1088" alt="6-11" src="https://user-images.githubusercontent.com/43739827/74601677-23b43680-50e4-11ea-8436-b706d46bf787.png"></img>  

두 데이터 프레임의 인덱스를 기준으로 병합하기 때문에 merge 메소드의 매개변수로 **left_index=True** 와 **right_index=True** 를 기입하였다.  

<img width="1100" alt="6-12" src="https://user-images.githubusercontent.com/43739827/74601746-c10f6a80-50e4-11ea-9362-d8ecbab014c9.png"></img>  

* 데이터 통합 응용  
두 개의 데이터 프레임을 생성하고 각 데이터 프레임내의 데이터중 수정하고자 하는 요소가 있는지 확인한다. 두 데이터 프레임의 데이터에 쉼표가 들어있는것을 확인하였다. 이를 한번에 처리하기위해 하나의 데이터 프레임으로 병합한다.  

<img width="1091" alt="6-13" src="https://user-images.githubusercontent.com/43739827/74602018-bacebd80-50e7-11ea-9a9b-91af2d8b7398.png"></img>  
> 열의 레이블이 일치하지 않기 때문에 행의 인덱스 레이블을 기준으로 통합시킨다.

<img width="1094" alt="6-14" src="https://user-images.githubusercontent.com/43739827/74602001-97a40e00-50e7-11ea-8b74-fedcd2b270e0.png"></img>  

<img width="1094" alt="6-15" src="https://user-images.githubusercontent.com/43739827/74602046-1600b000-50e8-11ea-8226-e84a3309fbce.png"></img>  

## 2. 조건절  

데이터 프레임의 행과 열을 처리할 때 조건을 지정하여 검색이나 정보갱신을 할 수 있다.  

* .query 메소드  
**.query** 메소드는 논리식을 문자열로 처리하면 바로 실행되는 강점을 가진 메소드다.  

<img width="1094" alt="6-16" src="https://user-images.githubusercontent.com/43739827/74602739-6a5b5e00-50ef-11ea-9931-b643926eedac.png"></img>  

query 메소드로 조건을 처리하되 특정 열만을 처리하고자 한다면 인덱스 연산자로 특정 열을 지정한다.  

<img width="1093" alt="6-17" src="https://user-images.githubusercontent.com/43739827/74602768-b5757100-50ef-11ea-9858-bb1d0ff6049d.png"></img>  
> 시리즈로 반환되는것을 확인할 수 있다.  

<img width="1088" alt="6-18" src="https://user-images.githubusercontent.com/43739827/74602780-df2e9800-50ef-11ea-8926-ff4b55316e44.png"></img>  
> 데이터 프레임으로 반환하고자 한다면 인덱스 검색에 열의 레이블을 인덱스 처리하여 기입한다.  

* .where 메소드  
**.where** 메소드는 True일 때의 데이터만 출력하고 나머지는 누락 값으로 나타낸다.  

<img width="1088" alt="6-19" src="https://user-images.githubusercontent.com/43739827/74602867-94f9e680-50f0-11ea-94e5-a60d16ca6403.png"></img>  

디폴트 값을 설정하면 누락 값대신 설정한 값이 들어간다.  

<img width="1095" alt="6-20" src="https://user-images.githubusercontent.com/43739827/74602890-c4105800-50f0-11ea-949c-c8c83d2d222b.png"></img>  

* .mask 메소드  
**.mask** 메소드는 .where 메소드와 반대로 조건이 False일 때의 데이터만 출력하고 나머지는 누락 값으로 나타낸다.  

<img width="1096" alt="6-21" src="https://user-images.githubusercontent.com/43739827/74602916-105b9800-50f1-11ea-9fa0-043084ec9e2e.png"></img>  

.where 메소드와 마찬가지로 디폴트 값을 설정하면 누락 값대신에 설정한 값이 들어간다.  

<img width="1089" alt="6-22" src="https://user-images.githubusercontent.com/43739827/74602954-4e58bc00-50f1-11ea-817d-d250712bbaee.png"></img>  

* .take 메소드  
**.take** 메소드는 매개변수로 가져올 행/열의 위치를 지정하고 그에 맞는 축을 설정하면 선택한 부분만을 반환할 수 있다. 또한 행이나 열의 위치는 여러 개 지정할 수 있다.  

<img width="1093" alt="6-23" src="https://user-images.githubusercontent.com/43739827/74603124-8eb93980-50f3-11ea-85ed-1f84302a368d.png"></img>  

## 3. groupby 메소드  

**.groupby** 메소드는 데이터 프레임 내의 특정한 범주를 가지는 데이터들을 묶어 연산을 할 수 있도록 한다.  

그룹화 과정을 확인하기 위해 데이터 프레임을 만들어 특정 열만을 추출하였다.

<img width="1099" alt="6-24" src="https://user-images.githubusercontent.com/43739827/74603679-72b89680-50f9-11ea-97d9-5bdd9f5c6f5c.png"></img>  

<img width="1095" alt="6-25" src="https://user-images.githubusercontent.com/43739827/74603692-a1367180-50f9-11ea-834e-f600eed643f1.png"></img>  

.groupby 메소드와 함께 **.agg** 메소드를 사용하면 집계 처리할 수 있다.  

<img width="1102" alt="6-26" src="https://user-images.githubusercontent.com/43739827/74603811-b364df80-50fa-11ea-9604-c2c6599b3ce9.png"></img>  

* 여러열의 그룹화  
하나의 열만이 아닌 다수의 열을 키로 지정하여 그룹화하면 복합적인 키를 이용해 처리되는 것뿐 다른 차이는 없다.  

그룹화할 열과 집계처리할 열을 지정하여 멀티인덱스로 구성된 데이터 프레임을 만들 수 있다.  

<img width="1103" alt="6-27" src="https://user-images.githubusercontent.com/43739827/74603854-6cc3b500-50fb-11ea-9ae4-11bc4357484c.png"></img>  

.agg 메소드 대신 **.transform** 메소드를 사용해 단순히 계산된 결과만을 데이터 프레임 내부의 데이터로 채울 수 있다.  

<img width="1103" alt="6-28" src="https://user-images.githubusercontent.com/43739827/74603914-fffcea80-50fb-11ea-9d99-69a42321607a.png"></img>  

transform 메소드에는 사용자 지정 함수를 입력할 수도 있다.  

<img width="1111" alt="6-29" src="https://user-images.githubusercontent.com/43739827/74603939-5bc77380-50fc-11ea-811b-7261dc2d54c9.png"></img>  
> 반환 결과가 시리즈인것을 확인할 수 있다.  

반환 결과를 데이터 프레임으로 만들고자 한다면 팬시 검색을 사용한다.  

<img width="1098" alt="6-30" src="https://user-images.githubusercontent.com/43739827/74603973-9fba7880-50fc-11ea-9693-2be149ae4542.png"></img>  

생성한 데이터 프레임을 csv 파일로 저장하고자 한다면 **to_csv** 메소드를 사용한다.  

<img width="1105" alt="6-31" src="https://user-images.githubusercontent.com/43739827/74604023-3850f880-50fd-11ea-82d6-76a10564cc1c.png"></img>
