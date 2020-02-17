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

샘플링이란 데이터의 일부를 분석하는 데이터 분석 기법이다. 데이터 프레임으로 데이터를 불러온 뒤 표본을 추출하기위해 샘플링 메소드를 사용하는 방법을 알아본다.  

외부 데이터를 읽어들이기 위해 **pandas_datareader** 모듈을 설치한다.  

<img width="1090" alt="7-7" src="https://user-images.githubusercontent.com/43739827/74631275-ed3bf180-519f-11ea-8094-104d01ae9043.png"></img>  

셀트리온의 주식 정보를 불러와 데이터 프레임으로 만들기 위해 설치한 pandas_datareader 모듈을 임포트하고 읽어들일 정보의 시작일과 끝일을 지정한다. 셀트리온 주식 정보 코드는 "068270.KS" 이고 정보 관리 주체는 "yahoo" 이다.  

<img width="1094" alt="7-8" src="https://user-images.githubusercontent.com/43739827/74631408-3f7d1280-51a0-11ea-8f9c-444c60cd7631.png"></img>  

**.sample** 메소드에 매개변수 **n** 을 지정해 임의의 n개를 가져온다. 실행할 때 마다 새로운 임의의 값을 가져오는것을 알 수 있다.  

<img width="1098" alt="7-9" src="https://user-images.githubusercontent.com/43739827/74631594-b1555c00-51a0-11ea-8b8c-431ff7570b00.png"></img>  

이전에 샘플링한 데이터도 포함해 샘플링하고자 한다면 매개변수로 **replace=True** 를 기입한다.  

<img width="1089" alt="7-10" src="https://user-images.githubusercontent.com/43739827/74631721-fed1c900-51a0-11ea-94bc-78714ed6abb9.png"></img>  

매개변수 n대신 **frac** 을 입력하면 지정한 퍼센트만큼 샘플링하는것을 확인할 수 있다.  

<img width="1092" alt="7-11" src="https://user-images.githubusercontent.com/43739827/74631827-4a847280-51a1-11ea-8f40-19dffa4fd752.png"></img>  
> frac=0.1 즉 10%의 데이터가 출력되었다.  

샘플링한 데이터를 가지고 통계 수치를 측정한다.  

<img width="1084" alt="7-12" src="https://user-images.githubusercontent.com/43739827/74631994-b535ae00-51a1-11ea-9a73-c9077dfd9c73.png"></img>  

* 리샘플링  
판다스에서 데이터를 샘플링하면 데이터 프레임을 만들어서 정적으로 처리한다. 그렇기 때문에 연산이나 갱신을 위해선 정적으로 만들어 처리해야 할 필요가 있다.  

<img width="1094" alt="7-13" src="https://user-images.githubusercontent.com/43739827/74634585-7e629680-51a7-11ea-8bdb-53ab76c5a8db.png"></img>  

<img width="351" alt="7-14" src="https://user-images.githubusercontent.com/43739827/74634702-c08bd800-51a7-11ea-81dc-9d69cf94689a.png"></img>  

<img width="1090" alt="7-15" src="https://user-images.githubusercontent.com/43739827/74634844-182a4380-51a8-11ea-97ae-5210e5c549df.png"></img>
