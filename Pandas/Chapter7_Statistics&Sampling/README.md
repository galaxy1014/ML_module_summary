# 7. Statistics and Sampling

방대한 양의 데이터를 처리해야 할 경우 데이터들의 통계량을 측정하고 샘플링하여 원하는 데이터로 만들어 분석하는 기능들에 대해 알아본다.  

## 1. 통계 메소드  

통계 함수를 사용하고자 한다면 사용할 데이터를 읽어와 데이터 프레임으로 변환하고 수치 계산이 가능한 자료형으로 변형해야 한다.  

<img width="1088" alt="7-1" src="https://user-images.githubusercontent.com/43739827/74628195-5a4b8900-5198-11ea-9f1b-c4ea1869e102.png"></img>  

특정 열에 누락 값이 존재하는것을 확인하여 **.fillna** 메소드를 사용해 다른 값으로 변경하였다.  

<img width="1097" alt="7-2" src="https://user-images.githubusercontent.com/43739827/74628926-430d9b00-519a-11ea-868e-09d282b9f451.png"></img>  

* 통계량 처리  

데이터 프레임을 정제했으면 **.describe** 메소드를 사용해 통계적인 정보를 확인할 수 있다. 기본적으로 개수(count), 평균(mean), 표준편차(std), 최솟값, 최댓값, 백분율을 표시한다.  

<img width="1094" alt="7-3" src="https://user-images.githubusercontent.com/43739827/74629324-49e8dd80-519b-11ea-9826-a158ccc95cc8.png"></img>  

<img width="1085" alt="7-4" src="https://user-images.githubusercontent.com/43739827/74629455-98967780-519b-11ea-9f92-5ffd6a55d6b8.png"></img>  

수치형 데이터 프레임에 .describe 메소드를 실행한 결과와 달리 문자형 데이터 프레임에 .describe 메소드를 실행하면 개수(count), 유일정보(unique), top, 빈도(freq)를 표시한다.  

<img width="1090" alt="7-5" src="https://user-images.githubusercontent.com/43739827/74629958-dd6ede00-519c-11ea-8a46-c3eaab4c0a5f.png"></img>  

.describe 메소드의 매개변수로 **include** 가 있다. include=[np.number]는 열의 자료형이 정수인지 실수인지를 식별해 통계를 산출하고 include=[object]는 문자형 데이터 프레임에 .describe 메소드를 사용한 결과와 동일하다.  

<img width="1087" alt="7-6" src="https://user-images.githubusercontent.com/43739827/74630254-861d3d80-519d-11ea-890c-98eb4e881ddb.png"></img>  

## 2. 샘플링 메소드  

 
