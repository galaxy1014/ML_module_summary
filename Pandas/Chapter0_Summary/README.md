# Summary  

## 1. Series & DataFrame  

* Series  
**시리즈(Series)** 는 파이썬의 리스트(list)나 넘파이(Numpy) 배열로 구성된 1차원 객체이다.  

'''python
# 리스트로 시리즈 생성
se = pd.Series([1,3,'One'], index=list('ABC'))  
se  
'''  


A      1
B      3
C    One
dtype: object  
