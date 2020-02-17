# 8. apply&eval&pipe method

## 1. apply method  

**.apply** 메소드를 사용하면 시리즈나 데이터 프레임의 행이나 열을 추출해 연산을 수행할 수 있다.  

<img width="1083" alt="8-1" src="https://user-images.githubusercontent.com/43739827/74635645-c8e51280-51a9-11ea-84e2-23d1e82bdc4d.png"></img>  
> 시리즈에서의 .apply메소드  

데이터 프레임에서의 .apply 메소드는 매개변수로 axis=0이나 axis=1로 행과 열을 지정할 수 있다.  

<img width="1081" alt="8-2" src="https://user-images.githubusercontent.com/43739827/74635821-1d888d80-51aa-11ea-9e7a-3dcd89f28aed.png"></img>

<img width="1087" alt="8-3" src="https://user-images.githubusercontent.com/43739827/74635944-5fb1cf00-51aa-11ea-9b4d-129118a7ee29.png"></img>  
> 제곱근을 구하는 np.sqrt는 행과 열의 계산결과가 동일하다.  

<img width="1093" alt="8-4" src="https://user-images.githubusercontent.com/43739827/74636061-9851a880-51aa-11ea-8476-d2a690411066.png"></img>  

.apply의 매개변수로 사용자 정의 함수를 지정할 수 있다.  

<img width="1089" alt="8-5" src="https://user-images.githubusercontent.com/43739827/74636357-2af24780-51ab-11ea-8e3b-5348697f0e0b.png"></img>  

<img width="1098" alt="8-6" src="https://user-images.githubusercontent.com/43739827/74636614-b7046f00-51ab-11ea-9def-aa29c1dc7183.png">

또 다른 .apply 메소드의 매개변수로 **result_type** 이 있다. 이 매개변수를 지정하기 위해선 반드시 **axis=1** 이어야한다. /또한 result_type에 기입할 수 있는 단어는 'expand', 'reduce', 'broadcast'가 있다.  

<img width="1089" alt="8-7" src="https://user-images.githubusercontent.com/43739827/74640048-4e6cc080-51b2-11ea-9b46-13b459a65a6e.png"></img>  
> 입력한 리스트의 길이만큼 데이터 프레임의 열을 세어 각 열에 리스트의 요소들을 데이터 프레임의 길이만큼 확장해 넣는다.  

<img width="1083" alt="8-8" src="https://user-images.githubusercontent.com/43739827/74640204-870c9a00-51b2-11ea-86df-373151039007.png"></img>  
> 입력한 리스트가 데이터 프레임의 행의 길이와 같은 시리즈로 반환된다.  

<img width="1091" alt="8-9" src="https://user-images.githubusercontent.com/43739827/74640313-b02d2a80-51b2-11ea-85bc-2928bcd6a363.png"></img>  
> 데이터 프레임의 열만큼 입력받은 스칼라값이나 리스트를 확장시킨다.  

## 2. eval method  

판다스의 **.eval** 메소드는 문자열 형태로 열 끼리의 연산결과를 입력하면 그 결과를 반환하는 역할을 한다.  

<img width="1085" alt="8-10" src="https://user-images.githubusercontent.com/43739827/74641116-1a929a80-51b4-11ea-8553-4bc38b94cc0f.png"></img>  

eval의 결과를 데이터 프레임 내부에 직접 변경하고자 한다면 매개변수로 **inplace=True** 를 기입한다.  

<img width="1091" alt="8-11" src="https://user-images.githubusercontent.com/43739827/74641232-49a90c00-51b4-11ea-98e2-7a39eac72a4e.png"></img>  
