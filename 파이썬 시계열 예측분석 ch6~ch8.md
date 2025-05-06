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

 - 마지막 단계로서, 잔차 분석을 수행하여 'Q-Q도식이 직선을 나타내는가'와 '잔차들이 상관관계가 없는가'라는 질문에 답할 수 있다.
   두 질문에 대한 답이 모두 '예'라면, 예측을 수행할 준비가 된 모델이다.
   그렇지 않는다면 다른 (p,q)조합들에 대해 시도해봐야 한다.

![image](https://github.com/user-attachments/assets/65de0b58-fdfc-458e-8371-95038c928936)  
 - ARMA(1,1) 프로세스

![image](https://github.com/user-attachments/assets/9fc97042-71d4-4628-9819-2169d5be5645)  
 - 모델 계수를 완벽하게 추정했다고 가정.
 - 잔차는 모델에서 나온 값과, 시뮬레이션된 프로세스의 실젯값 간의 차이다.
![image](https://github.com/user-attachments/assets/94f8ca71-6d15-4e6f-9226-aad3be9214d9)
 - 완벽하게 모델을 선택한 상황에서 모델의 잔차는 백색소음이다.

### 정성적 분석 : Q-Q 도식 분석  
 - Q-Q 도식으로 모델의 잔차가 정규분포인지 아닌지 알 수 있다.(정규분포이기를 바라기 때문이다)  
 - x축이 정규분포의 사분위수, y축이 잔차의 사분위수라서 만약 잔차가 정규분포에 가깝다면 y=x그래프와 비슷해진다.
![image](https://github.com/user-attachments/assets/bad845ce-23ba-4db4-889e-b0a7bdd53eb9)
![image](https://github.com/user-attachments/assets/e0856272-dc1d-433b-94eb-fd1e927ec0e5)
 - 이런 경우, 모델이 데이터에 적합하지 않다. 다른 p,q값들을 정해봐야 한다.

### 정량적 분석 : 융-박스 테스트 적용하기  
 - 잔차들 간에 상관관계가 있는지.
 - 좋은 모델은 잔차가 백색소음에 가까우므로, 잔차가 정규분포이고, 잔차들 간에 상관관계가 없어야 한다.
![image](https://github.com/user-attachments/assets/c5c923f7-ecf3-4be8-b003-824c1f3e5c03)
***
![image](https://github.com/user-attachments/assets/bc746718-8b47-4ef6-a565-eb4c755a7e89)  
좌 상단: 잔차가 백색소음과 같은 정상성을 보인다.  
우 상단 : 잔차가 정규분포와 비슷해 백색소음에 가깝다는 것을 알 수 있다.  
우 하단 : 잔차에 상관관계가 없다는 것을 알 수 있다.  
![image](https://github.com/user-attachments/assets/cabb69bd-8da8-4520-bd2a-f19b8a2c3ec5)  
 - 융-박스 통계와 p-value

## 6.6 대역폭 사용량 예측하기  
![image](https://github.com/user-attachments/assets/a1627279-ba81-40a7-a5a9-4efa2d4ecabb)  
![image](https://github.com/user-attachments/assets/b1bb0d08-6a70-45de-88a9-087e2700b210)  
![image](https://github.com/user-attachments/assets/0d19160a-afd8-4dc6-8bf6-b4a1e31b20c0)  
***
# 7. 비정상적 시계열 예측하기  
자기회귀누적이동평균과정 : 자기회귀과정 AR(p), 적분 I(d), 이동평균과정 MA(q)의 조합이다.(ARIMA(p,d,q))  
![image](https://github.com/user-attachments/assets/18e16049-291c-4dfa-ad8e-fb37b9025275)  
적분 차수 d는 차분의 반대이다. 수열을 한 번 차분해서 정상적이 되면 d=1, 두 번 차분해서 정상적이 되면 d=2.  
즉, 비정상적 시계열을 차분해서 정상적으로 만들고 ARMA모델을 적용하는 게 ARIMA 모델이다.(d=0이면 ARMA 모델과 동일.)  
![image](https://github.com/user-attachments/assets/57544865-4121-47ee-b12f-f3ba439a8aa7)  
***
# 8. 계절성 고려하기  
![image](https://github.com/user-attachments/assets/21afd0c4-4c47-48cc-9043-cb9b5a3f1e40)  
 - 기본 DATASET

SARIMA(p,d,q)(P,D,Q)_m 모델 : ARIMA모델에서 계절 매개변수를 추가한 것이다.  
P는 계절적 AR(P) 프로세스의 차수, D는 계절적 적분 차수, Q는 계절적 MA(Q)프로세스 차수,  
m은 빈도 또는 계절적 주기당 관측 회수다.  
![image](https://github.com/user-attachments/assets/d17adc4e-00b4-413f-9906-cb2ea6785775)  
![image](https://github.com/user-attachments/assets/7f2b17fd-0aee-4b37-8831-656ff6143189)  
ex) m=12, P=2이면 m의 배수인 지연에 대해 두 개의 과거 시계열값을 포함한다는 뜻이르모 y_t-12, y_t-24의 값을 포함한다.  
## 8.2 시계열에서 계절별 패턴 식별하기  
시계열 분해는 시계열을 추세와 계절적 구성요소, 잔차 이 세 가지 구성요소로 분리하는 작업이다.  
추세 - 시계열의 장기적인 변화를 나타낸다.  
계절적 - 시계열의 주기적인 패턴이다.  
잔차나 노이즈 - 추세 또는 계절적 구성요소로 설명할 수 없는 불규칙성을 나타낸다.  
![image](https://github.com/user-attachments/assets/0bc5c1c2-582d-4c61-8344-1bd4e62b2a0e)  
이 모델을 시계열 분해하면  
![image](https://github.com/user-attachments/assets/6f01ce83-936f-4f1d-b8c9-6200650a2476)  
***
만약 계절성이 없는 선형 시계열이라면  
![image](https://github.com/user-attachments/assets/aa37182c-aaa6-48ce-9c00-20cb42b9dbdb)  
이렇게 수평선으로 표시된다.  
![image](https://github.com/user-attachments/assets/e30b87b8-1f06-48d9-96f7-ff94c5a990d5)  

## 8.3 월간 항공 승객 수 예측하기  
![image](https://github.com/user-attachments/assets/f3e3ea9e-d6f6-4979-80a2-b09661fbf9d0)  
![image](https://github.com/user-attachments/assets/e49bbf32-e9db-411e-81bd-879ed3790f11)  
 - 기본 dataset
 - 베이스라인 모델 : 단순한 계절적 예측
![image](https://github.com/user-attachments/assets/ffc6769d-3b9d-435e-8d5e-cacdec488165)
 - 잔차가 백색소음인, 완벽한 모델이다.
 - 그러나, 융-박스 테스트에 따르면 지연 1,2에서 어느 정도 상관관계가 있기 때문에 ARIMA 모델이 데이터의 모든 정보를 포착하지 못하고 있음을 뜻한다.
따라서 동일한 방식으로 SARIMA 모델을 적용한다.
![image](https://github.com/user-attachments/assets/a3b2adae-0328-459b-a335-84e4ca15c0f9)
 - 잔차가 백색소음일 뿐 아니라, 융-박스 테스트도 잔차가 독립적이고 상관관계가 없다는 결론이 나왔다.
![image](https://github.com/user-attachments/assets/2f1c3703-6f10-42c8-b574-0f707184fc6e)
![image](https://github.com/user-attachments/assets/63ab1bac-f715-4562-94a0-15cd51d0c509)
![image](https://github.com/user-attachments/assets/be516449-316e-4dc5-9a35-4b82c5d3ff93)

































 



 




