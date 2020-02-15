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
> 가장 긴 열을 기준으로 나머지 열들이 누락 값을 채운것을 확인할 수 있다.  

누락 값이 있는 특정한 열을 지정하여 검색하고 그 열에 별도의 시리즈를 생성하여 할당하면 위에서 생성한 데이터 프레임의 내용이 바뀐것을 확인할 수 있다.  

<img width="1084" alt="5-18" src="https://user-images.githubusercontent.com/43739827/74421526-87debc80-4e90-11ea-8cbf-c2c17369dcdf.png"></img>  

누락 값이 없는 열들을 따로 추출하여 새로운 데이터 프레임 변수에 할당하였다. **.shift** 메소드는 열 내부의 원소들을 위 혹은 아래로 이동시킬 수 있으며 원소들을 위로 올리고자 한다면 괄호안에 음수를 입력하고 아래로 내리고자 한다면 양수를 입력한다.  

<img width="1095" alt="5-19" src="https://user-images.githubusercontent.com/43739827/74422907-b65d9700-4e92-11ea-811b-d505dc94e541.png"></img>  

## 2. 데이터 구조 변경  

데이터를 분석함에 있어 **데이터 전처리** 는 많이 사용되는 과정이다. 데이터 전처리란 원본의 데이터를 그대로 사용하지 않고 분석하고자 하는 형태로 재구조화하여 분석을 하는 과정이다. 데이터를 재구조화하는 과정또한 다양한 메소드가 존재한다.  

1. 피봇(pivot)  
-------------  
원래 피봇 테이블은 존재하는 테이블에서 필요한 데이터들만을 뽑아 새로운 표로 만드는 것이다.  

<img width="208" alt="5-20" src="https://user-images.githubusercontent.com/43739827/74424696-c5921400-4e95-11ea-999c-4e4f3d82367c.png"></img>  
> 엑셀에서의 피봇 테이블  

우선 데이터 프레임을 생성하고 피벗테이블을 통해 그룹화 할 열들을 확인한다.  

<img width="1099" alt="5-21" src="https://user-images.githubusercontent.com/43739827/74427304-2b809a80-4e9a-11ea-996f-cc9921cbeefe.png"></img>  

데이터 프레임을 피벗 테이블로 만들기 위해서는 **.pivot** 메소드를 사용한다. 매개변수로는 index, columns, value가 들어간다.  

<img width="1087" alt="5-22" src="https://user-images.githubusercontent.com/43739827/74427408-62ef4700-4e9a-11ea-902f-a87ab2c1d5c0.png"></img>  

피봇 테이블을 만들때 중복되는 데이터가 많아지면 생성이 불가능하기 때문에 어떠한 테이블에서는 중복을 제거해야 할 경우가 필수적일수 있음을 알아야한다.  

<img width="1084" alt="5-23" src="https://user-images.githubusercontent.com/43739827/74427955-74851e80-4e9b-11ea-91cb-aded94cb62cf.png"></img>  

<img width="1085" alt="5-24" src="https://user-images.githubusercontent.com/43739827/74427994-836bd100-4e9b-11ea-9b03-c286299c79bc.png"></img>  

피봇테이블을 생성하는 또 하나의 메소드로는 **.pivot_table** 이 있다. pivot_table은 집계 연산을 할 수 있다는 장점이 있다.  

<img width="1092" alt="5-25" src="https://user-images.githubusercontent.com/43739827/74431265-e2ccdf80-4ea1-11ea-9cc1-bb6f5c95e3b6.png"></img>  

<img width="919" alt="5-26" src="https://user-images.githubusercontent.com/43739827/74432062-13147e00-4ea2-11ea-9762-e7c1c7f84ff5.png"></img>
> [Pandas Document](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.pivot_table.html#pandas.DataFrame.pivot_table, "Pandas DOC")  

2. 스택(Stack)
-------------  
테이터 프레임에서 행이 상대적으로 많거나 혹은 열이 상대적으로 많거나하는 비율이 비대칭한 경우, 행과 열의 구조를 변경한다고 해도 실질적인 값의 변화는 없다. 이 경우 행과 열의 인덱스를 추출해 재구조화해야 하는데 이때 사용하는 메소득가 **.stack** 과 **.unstack** 메소드가 있다.

<img width="1083" alt="5-27" src="https://user-images.githubusercontent.com/43739827/74435255-5de4c480-4ea7-11ea-8fa7-b6c027be9220.png"></img>  

<img width="1086" alt="5-28" src="https://user-images.githubusercontent.com/43739827/74435325-8967af00-4ea7-11ea-9d47-91519116a1d0.png"></img>  
> 행에 비해 열이 커진 형태가 되었다.  

스택메소드로 반환된 결과를 보면 열의 인덱스가 사라져 1차원인 시리즈로 변환된 것을 확인할 수 있다.  

<img width="1087" alt="5-29" src="https://user-images.githubusercontent.com/43739827/74435857-b9638200-4ea8-11ea-8a12-add2d75d291b.png"></img>  

또한 행이 멀티인덱스로 변환된 것을 확인할 수 있다.  

<img width="1095" alt="5-30" src="https://user-images.githubusercontent.com/43739827/74436191-58887980-4ea9-11ea-9d9d-a9bb9cb0d051.png"></img>  

인덱스의 레벨을 확인해보면 set_index로 지정한 열 이외의 열 레이블들이 행의 마지막 레이블로 들어간것을 확인할 수 있다. 또한 시리즈 내부의 값들은 set_index로 지정한 열 이외의 열들의 데이터들로 이루어져 있다.    

<img width="1110" alt="5-31" src="https://user-images.githubusercontent.com/43739827/74436965-ad78bf80-4eaa-11ea-993e-10d63179dc7d.png"></img>  

<img width="1103" alt="5-32" src="https://user-images.githubusercontent.com/43739827/74437534-9f776e80-4eab-11ea-9985-870ed63f1bdf.png"></img>  

<img width="1098" alt="5-33" src="https://user-images.githubusercontent.com/43739827/74438083-b8345400-4eac-11ea-9fc0-66614b2b90db.png"></img>  

만약 시리즈를 데이터 프레임으로 변환하고자 한다면 **.to_frame** 매소드를 사용한다.  

<img width="1104" alt="5-34" src="https://user-images.githubusercontent.com/43739827/74438301-29740700-4ead-11ea-9b01-ab9f5457db9e.png"></img>  

<img width="889" alt="5-35" src="https://user-images.githubusercontent.com/43739827/74512432-95a54800-4f4b-11ea-8479-b7dbd246fc05.png"></img>  
> 열의 인덱스가 RangeIndex로 이루어진것을 확인할 수 있다.  

**unstack** 메소드를 실행하면 행의 인덱스중 하나가 열의 인덱스로 넘어가는것을 확인할 수 있다.  

<img width="1094" alt="5-36" src="https://user-images.githubusercontent.com/43739827/74513523-19603400-4f4e-11ea-96e6-abf07f053269.png"></img>  

<img width="1101" alt="5-37" src="https://user-images.githubusercontent.com/43739827/74513597-4876a580-4f4e-11ea-8813-a93ed6ee2d6f.png"></img>  

<img width="892" alt="5-38" src="https://user-images.githubusercontent.com/43739827/74513690-84116f80-4f4e-11ea-9116-54f60d49f896.png"></img>  
> 데이터 프레임의 round행이 열로 넘어간것을 확인할 수 있다.  

unstack 메소드를 두 번 사용하면 시리즈로 생성되는것을 확인할 수 있다.  

<img width="903" alt="5-39" src="https://user-images.githubusercontent.com/43739827/74513935-000bb780-4f4f-11ea-8f14-15fb67ebd0f4.png"></img>  

이번에는 데이터 프레임에서 특정 열을 추출하여 이 열에 해당하는 행의 멀티인덱스를 가져와 하나의 시리즈를 생성하였다.  

<img width="895" alt="5-40" src="https://user-images.githubusercontent.com/43739827/74514721-84126f00-4f50-11ea-81e4-4ab5f6541dce.png"></img>  

생성된 시리즈를 unstack하면 멀티 인덱스가 각각 행과 열의 레이블로 나뉘어 데이터 프레임을 생성하는것을 확인할 수 있다.  

<img width="900" alt="5-41" src="https://user-images.githubusercontent.com/43739827/74514809-b15f1d00-4f50-11ea-9b16-6066d896a249.png"></img>  

unstack 메소드에 매개변수로 level을 입력하면 행의 멀티 인덱스가 행과 열의 레이블로 바뀔때 위치를 조정할 수 있다.  

<img width="900" alt="5-42" src="https://user-images.githubusercontent.com/43739827/74514991-026f1100-4f51-11ea-9773-40f2267e315b.png"></img>  

3. 데이터 병합  
------------  

하나의 데이터 프레임을 재구조화한것처럼 두 개의 시리즈나 데이터 프레임을 하나로 합치는것이 가능하다. 먼저 데이터 프레임에 공통적으로 들어갈 열(columns)을 설정하고 데이터 프레임에 들어갈 데이터를 넘파이 배열로 만든다. 이 때 데이터의 요소가 행의 기준으로 되어있기 때문에 전치(Transpose)하여 열을 기준으로 하도록 수정한다. 전치는 행과 열의 길이가 같아야 가능한것을 알고있어야 한다.  

<img width="1086" alt="5-43" src="https://user-images.githubusercontent.com/43739827/74588128-43dcea80-503d-11ea-9454-54da10754055.png"></img>  
> 전치가 되기 전과 후의 데이터 프레임이 어떻게 다른지 알 수 있다.  

<img width="918" alt="5-44" src="https://user-images.githubusercontent.com/43739827/74588201-be0d6f00-503d-11ea-87c8-12c259f1a1ca.png"></img>  
> [Pandas Document](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.T.html#pandas.DataFrame.T, "Pandas DOCS")  

<img width="1092" alt="5-45" src="https://user-images.githubusercontent.com/43739827/74588334-d631be00-503e-11ea-85b0-890bdeb5ac38.png"></img>  

두 개의 데이터 프레임의 열이 같다면 **concat** 함수를 사용해 합칠 수 있다.  

<img width="1089" alt="5-46" src="https://user-images.githubusercontent.com/43739827/74588405-9919fb80-503f-11ea-920b-ba9470bf63fc.png"></img>  
> 행의 레이블을 보면 각 데이터 프레임의 행이 그대로 유지되는 것을 알 수 있다.  

행의 레이블을 변경하기 위해 별도의 리스트를 만들어 합쳐진 데이터 프레임에 넣어준다.  

<img width="1088" alt="5-47" src="https://user-images.githubusercontent.com/43739827/74588593-29a50b80-5041-11ea-911e-b59b8bf52a9b.png"></img>  

혹은 데이터 프레임간의 병합 과정에서 concat의 매개변수로 **ignore_index=True** 를 기입하면 별도의 변환과정을 거치지 않아도 된다.  

<img width="1084" alt="5-48" src="https://user-images.githubusercontent.com/43739827/74588659-ccf62080-5041-11ea-98ca-4cfef8a3ebb2.png"></img>  
> RangeIndex로 생성된것을 확인할 수 있다.  

만약 데이터 프레임간의 연결을 가로로 하고싶다면 매개변수에 axis=1을 기입한다.  

<img width="1084" alt="5-49" src="https://user-images.githubusercontent.com/43739827/74588757-ab496900-5042-11ea-8f11-f124ac776c94.png"></img>  

이 때 열의 레이블이 중복되기 때문에 따로 열의 레이블을 따로 생성하여 병합한 데이터 프레임에 넣어야 한다.  

<img width="1085" alt="5-50" src="https://user-images.githubusercontent.com/43739827/74588858-77bb0e80-5043-11ea-976d-ed105b5b4415.png"></img>  

행의 레이블과 마찬가지로 매개변수에 ignore_index=True를 기입하면 별도의 변환 과정을 거치지않고 RangeIndex가 생성된다.  

<img width="1093" alt="5-51" src="https://user-images.githubusercontent.com/43739827/74588909-07f95380-5044-11ea-9a7a-e72bb55cbf54.png"></img>  

* 데이터 추가  

<img width="1086" alt="5-52" src="https://user-images.githubusercontent.com/43739827/74589006-dc2a9d80-5044-11ea-9f97-295c00fd993b.png"></img>  

<img width="1090" alt="5-53" src="https://user-images.githubusercontent.com/43739827/74589108-bf429a00-5045-11ea-8cb0-aa6d16663cad.png"></img>  

* 조인 처리  

concat 함수는 default값으로 axis=0을 가진다. 이때 같은 열의 레이블끼리만 합치고자 한다면 매개변수로 **join='inner'** 를 사용한다.  

<img width="1091" alt="5-54" src="https://user-images.githubusercontent.com/43739827/74589487-26ae1900-5049-11ea-9a4c-404e2bdbd467.png"></img>  

axis=1로 설정하면 같은 행의 레이블을 기준으로 두 개의 데이터 프레임이 연결된 것을 확인할 수 있다.  

<img width="1088" alt="5-55" src="https://user-images.githubusercontent.com/43739827/74589572-b94eb800-5049-11ea-870d-383d5de62b60.png"></img>  

**join='outer'** 는 단순연결을 하고자 할때 사용한다.  

<img width="1092" alt="5-56" src="https://user-images.githubusercontent.com/43739827/74589723-0f702b00-504b-11ea-8683-fd9f477f0cfe.png"></img>  
> outer join을 확인하기 위해 행의 레이블이 일치하지 않는 별도의 데이터 프레임을 생성하였다.  

outer join은 각각의 행 레이블 중에 존재하지 않는 레이블이 있으면 그 행의 데이터를 누락 값으로 채우는 반면 inner join은 값 자체가 없음을 확인할 수 있다.  

<img width="1086" alt="5-57" src="https://user-images.githubusercontent.com/43739827/74589751-5d852e80-504b-11ea-8bdb-11059865305e.png"></img>  

데이터 프레임을 계층적으로 설계하고 싶다면 concat의 매개변수로 keys를 사용한다.  

<img width="1088" alt="5-58" src="https://user-images.githubusercontent.com/43739827/74589889-c620db00-504c-11ea-94dd-f126b3c6e1c9.png"></img>  

**.join** 변수를 사용해 데이터 프레임을 합칠 수 있다. 이때 같은 열의 이름을 구분해야하기 때문에 **lsuffix** 매개변수를 통해 왼쪽 데이터 프레임(원본)의 동일한 열 레이블 끝에 표시할 문자열을, **rsuffix** 매개변수를 통해 오른쪽 데이터 프레임(대상)의 동일한 열 레이블 끝에 표시할 문자열을 지정한다.  

<img width="1086" alt="5-59" src="https://user-images.githubusercontent.com/43739827/74589973-94f4da80-504d-11ea-81d8-b770254d338d.png"></img>  

4. 데이터 변형  
------------  

데이터를 분석할때 여러 열들을 하나의 기준을 정해 그룹화해야할 경우가 있다. 이렇듯 여러 열을 통합해 하나의 변수와 값으로 처리하기 위해 **pd.melt** 함수를 사용한다. 고정하고자 하는 열을 **id_vars** 로 지정하고 값으로 사용하고자 하는 열을 **value_vars** 로 지정한다.  

<img width="1092" alt="5-60" src="https://user-images.githubusercontent.com/43739827/74590372-1bf78200-5051-11ea-96b4-188d7b0da8d6.png"></img>  
> 기준이 되는 열을 제외하면 variable과 value로 기본 설정이 된 것를 확인할 수 있다.  

데이터 분석에 있어 기본값으로 지정된 열의 레이블들에 따로 이름을 부여해 관리해주는것이 좋다. 그러기 위해선 pd.melt 함수에 매개변수로  **var_name** 과 **value_name** 으로 이름을 지정해준다.  

<img width="1090" alt="5-61" src="https://user-images.githubusercontent.com/43739827/74590441-c1125a80-5051-11ea-8c41-e6e61cc4d0a2.png"></img>  

id_vars나 values_vars는 리스트로 지정하면 많은 열들을 지정할 수 있다.  

<img width="1091" alt="5-62" src="https://user-images.githubusercontent.com/43739827/74590488-3716c180-5052-11ea-9b21-4157dba8c05e.png"></img>  

5. .assign 메소드  
-----------------  

**.assign** 메소드의 매개변수를 활용해 새로운 값을 가지는 열을 만들어낼 수 있다.  

<img width="1089" alt="5-63" src="https://user-images.githubusercontent.com/43739827/74590638-7f82af00-5053-11ea-8331-47e61ae3617b.png"></img>  

<img width="1086" alt="5-64" src="https://user-images.githubusercontent.com/43739827/74590695-d12b3980-5053-11ea-9935-80e4da07435a.png"></img>  

* .filter  
.filter 메소드와 .assign 메소드를 사용해 데이터 프레임을 간략하게 할 수 있다.  

<img width="1101" alt="5-65" src="https://user-images.githubusercontent.com/43739827/74590830-7abefa80-5055-11ea-869e-4f527ca4bbea.png"></img>  
> sql문처럼 like는 지정한 문자열이 포함된 문자열을 찾는다.  

<img width="1102" alt="5-66" src="https://user-images.githubusercontent.com/43739827/74590855-c1acf000-5055-11ea-9912-82f9f32c5038.png"></img>  
> .assign 메소드를 통해 원본 데이터 프레임에서 result열을 가져와 생성한 데이터 프레임의 새로운 열로 만들었다.  

6. 여러 열 변형  
-------------  

여러 열을 하나의 특징을 기준으로 하나로 처리하고자 할때 **pd.wide_to_long** 함수를 사용한다.  

<img width="1103" alt="5-67" src="https://user-images.githubusercontent.com/43739827/74591258-c5db0c80-5059-11ea-88bb-416edbde516b.png"></img>  

생성된 데이터 프레임에서 그룹화할 열을 지정한다. 고정할 열은 매개변수 **i** 에 기입하고 새롭게 처리할 열의 이름을 매개변수 **j** 로 지정한다.  

<img width="1104" alt="5-68" src="https://user-images.githubusercontent.com/43739827/74591338-7ea14b80-505a-11ea-8bd2-2f769c0f782c.png"></img>  

데이터 프레임을 다시 원래의 형태로 되돌리고자 한다면 unstack 메소드를 사용한다.  

<img width="1098" alt="5-69" src="https://user-images.githubusercontent.com/43739827/74591478-c7a5cf80-505b-11ea-905a-c106cdd37b1e.png"></img>  
> 행과 열의 인덱스가 멀티인덱스로 구성되었다.  

<img width="1101" alt="5-70" src="https://user-images.githubusercontent.com/43739827/74591523-09cf1100-505c-11ea-91cc-e4f2475906c4.png"></img>  
> **.map** 매소드를 사용해 열의 멀티인덱스를 단일 인덱스로 변형시킨다.  

<img width="1100" alt="5-71" src="https://user-images.githubusercontent.com/43739827/74591535-22d7c200-505c-11ea-9819-c4bd8c2c3793.png"></img>  
> **reset_index** 메소드는 멀티인덱스를 한차원 혹은 그 이상의 차원을 낮추는 기능을 한다.  

<img width="950" alt="5-72" src="https://user-images.githubusercontent.com/43739827/74591585-67635d80-505c-11ea-809f-b90849f18944.png"></img>
> [Pandas Document](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.reset_index.html?highlight=reset_index#pandas.DataFrame.reset_index, 'Pandas DOC')  
