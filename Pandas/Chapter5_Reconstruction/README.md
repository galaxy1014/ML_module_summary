# 5. Reconstruction

데이터를 분석함에 있어서 새롭게 입력받은 데이터를 처리하기 전에 기존에 있는 데이터를 새로운 데이터와 함께 처리하기위해 재구성을 해야할 필요가 있다. 인덱스를 정렬한다거나 데이터를 병합 및 변경하는 방법에 대해 알아본다.  

## 1. 정렬 처리  

* 시리즈 정렬  
외부의 값이 들어올 때 인덱스의 레이블과 내부 값이 순차적으로 되어있지 않으면 예외가 발생할 수 있으므로 정렬 처리가 필요하다.  

<img width="1085" alt="5-1" src="https://user-images.githubusercontent.com/43739827/74330817-b64b9180-4dd5-11ea-9046-7aa9a9e0cabf.png"></img>  

값을 정렬을 하기위한 sort_values 메소드는 매개변수 **ascending** 을 지원한다. ascending=True로 했을시에는 오름차순으로 정렬되며 default값은 True로 되어있다.  

<img width="1088" alt="5-2" src="https://user-images.githubusercontent.com/43739827/74331067-370a8d80-4dd6-11ea-9cad-af9120b2ffe3.png"></img>  

내부 값들을 위치를 기준으로 정렬하고자 했을때엔 **.argsort** 메소드를 사용한다. 그러나 이 메소드는 인덱스의 정보가 변경되지 않아 혼란을 줄 수 있다.  

<img width="1099" alt="5-3" src="https://user-images.githubusercontent.com/43739827/74331482-1b53b700-4dd7-11ea-9f1f-508feccce9fb.png"></img>  
> 원본 시리즈의 정보를 보면 F가 0으로 가장작고 다음으로 D : 2 -> B : 4 -> C : 8 순으로 커진다. argsort 메소드를 사용한 결과를 보면 F가 최소값으로 0이며 C가 최대값으로 3임을 확인할 수 있다.  

<img width="910" alt="5-4" src="https://user-images.githubusercontent.com/43739827/74331703-95843b80-4dd7-11ea-92a2-71ea704d6c5e.png"></img>  
> [Pandas Document](https://pandas.pydata.org/docs/reference/api/pandas.Series.argsort.html?highlight=argsort#pandas.Series.argsort, 'Pandas DOC')  

간단하게 최소값과 최대값을 확인하고자 한다면 **idxmin** 메소드와 **idxmax** 메소드를 사용한다.  

<img width="1093" alt="5-5" src="https://user-images.githubusercontent.com/43739827/74331850-e005b800-4dd7-11ea-8126-89179b1f238e.png"></img>  

내부 값을 기준으로 하는것이 아닌 인덱스를 기준으로 하고자 한다면 .sort_index 메소드를 사용한다.  

<img width="1092" alt="5-6" src="https://user-images.githubusercontent.com/43739827/74332066-5a363c80-4dd8-11ea-8a87-6ce0b005654a.png"></img>  

* 데이터 프레임 정렬  
데이터 프레임은 시리즈와 다르게 2차원으로 구성되어 있어 정렬또한 행과 열을 기준으로 해야한다. 행은 시리즈와 같은 방식으로 정렬하기 때문에 열을 기준으로 하는 방식에 대해 알아야할 필요가 있다.  

정렬되어있지 않은 데이터 프레임의 열의 레이블에 어떠한 특정 열을 기준으로 정렬하고자 한다면 .sort_values 메소드에 매개변수로 **by=<기준열 이름>** 을 입력한다.  

<img width="1090" alt="5-7" src="https://user-images.githubusercontent.com/43739827/74332751-c9606080-4dd9-11ea-9121-1a3a760cb737.png"></img>  

이번에는 누락 값이 포함된 데이터 프레임의 정렬결과에 대해 확인해보려고 한다.  

<img width="1095" alt="5-8" src="https://user-images.githubusercontent.com/43739827/74333737-e26a1100-4ddb-11ea-8797-d15026d4fe79.png"></img>  
> 누락 값이 들어있는 열을 기준으로 정렬을 하면 오름차순으로 NaN이 내려가는 것을 확인할 수 있다. 즉 NaN을 제일 큰 수로 인식함을 알 수 있다.  

정렬할때 정렬 기준에 상관없이 누락 값의 위치를 지정할 수 있다. 이럴때는 .sort_values 메소드에 매개변수로 **naposition='last'/'first'** 를 입력한다.

<img width="1097" alt="5-9" src="https://user-images.githubusercontent.com/43739827/74334620-9c15b180-4ddd-11ea-8757-82eccba6e3bf.png"></img>  

데이터 프레임의 특정 열들에 정렬 기준을 정할 수 있다.  

<img width="1096" alt="5-10" src="https://user-images.githubusercontent.com/43739827/74334888-32e26e00-4dde-11ea-8802-3a873ba69e1c.png"></img>

<img width="1093" alt="5-11" src="https://user-images.githubusercontent.com/43739827/74334930-4ee60f80-4dde-11ea-8ba3-c53084543699.png"></img>  

데이터 프레임의 행과 열 레이블을 정렬하고자 하면 매개변수에 axis=0 혹은 1을 입력하여 상황에 맞는 정렬을 할 수 있다.  

<img width="1091" alt="5-12" src="https://user-images.githubusercontent.com/43739827/74335909-8d7cc980-4de0-11ea-98e1-7a81609dcd75.png"></img>  

행과 열의 레이블을 동시에 정렬하는 메소드 체인을 사용할 수 있다. 행의 경우 axis=0이나 default 값이 axis=0으로 되어있으므로 따로 입력하지 않아도 정상적으로 작동하는것을 확인할 수 있다.  

<img width="1093" alt="5-13" src="https://user-images.githubusercontent.com/43739827/74336223-37f4ec80-4de1-11ea-9891-d75cf52485d9.png"></img>

* 순위 및 이동 처리  
데이터 프레임 내부 구조를 변경하지 않고 정렬된 결과를 따로 열로 생성하여 추가할 수 있다. 순위를 담당하는 메소드는 **.rank** , 값 이동은 **.shift** 메소드를 사용한다.  

1. rank  

학생의 정보가 들어있는 데이터 프레임을 생성하고 '점수'열을 기준으로 순위를 매겨 새로운 '성적'열을 생성한다.  

<img width="1101" alt="5-14" src="https://user-images.githubusercontent.com/43739827/74336748-3e379880-4de2-11ea-9dfd-811336b673f9.png"></img>  

<img width="1101" alt="5-15" src="https://user-images.githubusercontent.com/43739827/74336917-9f5f6c00-4de2-11ea-8354-e89293869187.png"></img>  
> rank 메소드의 반환 결과가 float64임을 확인할 수 있다.  

순위를 기준으로 오름차순을 하면 순위는 정상적이지만 행의 레이블이 틀어져버리게 된다. 그렇기 때문에 별도로 레이블을 만들어 데이터 프레임의 인덱스와 교체해주어야 한다.  

<img width="1092" alt="5-16" src="https://user-images.githubusercontent.com/43739827/74337374-83a89580-4de3-11ea-994f-bae7644342b5.png"></img>  

2. shift  

데이터 프레임을 생성하여 내부 값들의 이동절차에 대해 알아보고자 한다.  

<img width="1101" alt="5-17" src="https://user-images.githubusercontent.com/43739827/74337756-4264b580-4de4-11ea-8381-213d48113d24.png"></img>
