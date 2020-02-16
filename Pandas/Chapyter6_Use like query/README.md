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

  
