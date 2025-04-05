# 6. 복잡한 시계열 모델링  

## 6.1 데이터 센터의 대역폭 사용량 예측  
![image](https://github.com/user-attachments/assets/4731152b-80ae-4d90-ad18-6d49ebea4fdb)  
![image](https://github.com/user-attachments/assets/37cd1859-925f-495b-a475-0b96689c7d7d)  
 - ADF 테스트, ACF 함수, PACF 함수를 확인해보면 자기회귀과정과 이동 평균과정의 조합이므로 ARMA모델을 확용한다.
![image](https://github.com/user-attachments/assets/7eeba3ae-c401-4d0f-abab-1ff968aca8dc)
![image](https://github.com/user-attachments/assets/3d1a2dc6-2d6a-4ac9-b4c8-fb705b7c6017)

## 6.3 정상적 ARMA 프로세스 식별하기  
 - 일단 ADF 테스트를 통해 ARMA(1,1)프로세스는 정상적이라는 걸 알 수 있다.
 - ACF 함수 도식
![image](https://github.com/user-attachments/assets/5422be6a-8435-4a56-8859-bc1f1f6202b5)
 - 도식의 sin 패턴은 AR(p) 프로세스가 작동 중임을 뜻한다.
 - 또한 마지막으로유의한 계수가 지연 2에 존재하므로 q = 2라고 추로할 수 있다.
 - 하지만 이는 ARMA(1,1)프로세스이므로 q는 1이어야 한다.
 - 따라서 ACF 도식으로는 ARMA(p,q) 프로세스의 차수q를 추론할 수 없다.
![image](https://github.com/user-attachments/assets/48782439-e7d3-4914-b2eb-06082ffbb140)
 - 역시 PACF도식으로는 ARMA(p,q)의 차수 p를 추정할 수 없다.
![image](https://github.com/user-attachments/assets/7dd6fc98-c587-42ef-9843-2a1590c64c56)

## 6.4 일반적 모델링 절차 고안하기  
ACF와 PACF에 의존하지 않는, 시계열이 비정상적이고, 계절성을 띄는 경우에도 적용할 수 있는, 차수 p와 q를 구할 수 있는 절차를 고안해야 한다.  
![image](https://github.com/user-attachments/assets/f514c1f1-c0cc-4a37-8201-1dd5e1b17d18)  
![image](https://github.com/user-attachments/assets/0f1ae073-25a8-445d-842a-601950345a04)  
k = p + q  
가능도 함수 : 모델이 피팅하기에 적합한지.  
확률 분포 함수는 매개변수가 정해진 모델에서 데이터 요소가 관측될 확률을 측정하는 거라면,   
가능도 함수는 관측된 데이터 집합에서 모델의 여러 가지 매개변수가 관측된 데이터를 생성할 가능성을 추정한다.  
ex) 주사위를 굴려서 [1,5,4,2,3,6,7,2]이 나왔을 때, 가능도 함수는 주사위가 6면일 가능성을 결정한다.  
즉, '내가 관측한 데이터가 ARMA(1,1)모델에서 나올 가능성이 얼마나 될까?'라는 것이다.  
![image](https://github.com/user-attachments/assets/90a3a9dd-d75a-4645-9ea9-73dc05f452bf)  





 




