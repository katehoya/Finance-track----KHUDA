# 3. 확률 보행   
확률 보행(random walk) : 무작위로 상승 or 하락이 발생할 확률이 동일한 프로세스.  
```
y_t = C + y_t-1 + e_t
```
y_t : 현잿값
y_t-1 : 이전 time step의 값
C : 상수.(if C != 0 : 표류(drift)가 있는 확률보행이라고 한다.)  
e_t : 백색소음(여기서는 분산이 1, 평균이 0인 표준정규분포)  

![image](https://github.com/user-attachments/assets/caa284ce-3e9e-4423-8d1c-fa82fdf1d74f)  
![image](https://github.com/user-attachments/assets/a7311ae3-a9ac-46c5-a3de-76fbddeb8ee4)  
![image](https://github.com/user-attachments/assets/a55ad286-2902-4cb1-918c-44e1ce158499)  
![image](https://github.com/user-attachments/assets/8f02db02-bc4f-48d1-bd77-9726dcb726aa)  
## 3.2 확률 보행 식별하기  
시계열의 관점에서 확률 보행 : 첫 번째 차분이 정상적이고, 상관관계는 없는 시계열.  
![image](https://github.com/user-attachments/assets/79ce1b6d-9a8d-4c7d-97bd-3e20f21994e7)  
![image](https://github.com/user-attachments/assets/fa332819-bc94-4681-a110-4f817e57e786)  
정상적(stationary) 시계열 : 시간이 지나도 통계적 특성이 변하지 않는 시계열.  
 - 평균과 분산이 상수이고, 자기상관관계가 있으며, 이런 특성들이 시간에 따라 변하지 않는 것.
 - 시계열의 평균, 분산, 자기상관관계가 시간에 따라 변하면 정상적이라고 할 수 없다.

non - stationary를 stationary로 변환하는 방법 : 
 - 차분
   ![image](https://github.com/user-attachments/assets/ec48a397-3a20-49d7-978d-333ab1a9b5ac)
   ![image](https://github.com/user-attachments/assets/1161cdb2-4ddb-4554-9599-558958122ea1)

정상성 test 하는 방법  
 - ADF(Augmented Dickey-Fuller) test.
   : ADF 테스트는 단위근의 존재여부를 테스트하므로, 시계열이 정상적인지를 판단하는 데 도움이 된다.
   단위근이 존재하면 시계열이 비정상적인 것이다.
   귀무가설은 단위근이 존재한다는 것으로, 시계열이 비정상적이라는 것을 뜻한다.
![image](https://github.com/user-attachments/assets/4949868b-e266-4daa-ac87-e19b9a9b51da)
이런 식에서 시계열의 근인 a1이 단위 원 내(-1~1)사이에 있을 경우에만 정상적이다. 아니면 비정상적이다.
![image](https://github.com/user-attachments/assets/3a6721c6-3e98-465b-9e70-3ac442c7fed7)
![image](https://github.com/user-attachments/assets/3b98f898-0eed-4bd4-8e4e-5732cb92ea90)
 -- 정상적 시계열은 시간에 무관하게 평균, 분산등이 일정하기 때문.

자기상관관계를 확인하는 법 : 
 - 자기상관함수(ACF) : 시계열 상의 떨어져 있는 값 사이의 선형 관계를 측정한다.
   즉 시계열과 시계열 그 자체 사이의 상관관계를 측정한다.
y_t와 y_t-1 간의 자기상관관계 - 지연 : 1, 계수 : r_1
y_t와 y_t-2 간의 자기상관관계 - 지연 : 2, 계수 : r_2
 - 추세가 존재하는 경우, ACF를 도식화하면 짧은 지연에 대해서는 계수가 높고 지연이 커짐에 따라 계수가 선형적으로 감소한다.
 - 계절성이 존재하는 경우, ACF를 도식화하면 주기적인 패턴을 확인할 수 있다.
 - 비정상적 프로세스 ACF를 도식화하면 해당 프로세스를 직접 도식화할 때와 유사한 수준의 정보만 얻을 수 있다.
 - 하지만 정상적 프로세스의 ACF를 도식화하면 확률보행의 존재를 식별하는 데 도움이 된다.
![image](https://github.com/user-attachments/assets/fb0801ad-be01-4ab9-8f19-172a9dc9e641)
 - ACF 도식. 자기상관계수가 서서히 감소하는 것을 알 수 있다.
 - 지연 20에서도 여전히 자기상관관계가 있으므로, 확률보행이 비정상적임을 뜻한다.
 - 비정상적 확률보행이므로 정상화를 해야 한다. 계절적 패턴은 없이 추세적 변화만 보이므로 1차 차분을 적용한다.
![image](https://github.com/user-attachments/assets/b36bfd06-050e-49cb-a88f-c54742222f7a)
추세가 제거되었고, 분산이 안정되었다.
![image](https://github.com/user-attachments/assets/f5d33cc9-007d-4d63-94bb-ba8b162f4678)
## 3.3 확률 보행 예측하기  
확률 보행을 다루고 있는 상황에서는 단순한 예측 방법만 사용할 수 있다.  
ex) 과거 기간의 평균, 마지막으로 예측된 값, 혹은 표류.
 - 과거 기간의 평균 : training set의 평균을 계산한 뒤, test set도 모두 이 평균과 같은 값일 것이라고 가정.
 - 마지막 값 : training set의 마지막으로 측정된 값이 그 이후에도 유지될 것이라고 가정.
 - 표류 기법 : ![image](https://github.com/user-attachments/assets/931683a2-13d9-4229-abb6-77431a8b9621)
   ![image](https://github.com/user-attachments/assets/bf8ca235-2c1d-4e89-8c03-d82c1c104df0)
   ![image](https://github.com/user-attachments/assets/27b61519-ec79-442d-8ac1-1cca2f3b6d14)
 - 미래의 여러 단계를 예측하는 것은 힘들지만, 그나마 가능한 것은 바로 다음 time step을 예측하는 것이다.
   ![image](https://github.com/user-attachments/assets/5dd1c82a-2706-408c-98ad-05d48a1ec79d)
   ![image](https://github.com/user-attachments/assets/cdf7a4ef-1739-42f7-9a90-c61e45771400)
   확률 보행의 프로세스를 예측해야 하는 경우 단기 예측을 여러 번 하는 게 낫다.
확률 보행의 경우 예측을 할 수 있는 유일한 합리적 방법은 베이스라인 모델을 사용하는 것밖에 없다.
![image](https://github.com/user-attachments/assets/c4c63fa2-c38d-44c3-a787-fe1b43fdbd28)
***  
# 4. 이동평균과정 모델링   
확률 보행 프로세스에 첫 번째 차분을 적용하면, 자기상관관계가 없는 정상 시계열을 얻을 수 있다.(첫 번째 차분된 시계열이 백색소음과 비슷한 성질을 보인다.)  
그러나 일부 정상 시계열은 특정 패턴을 보일 수 있으며, 이 경우 자기 상관관계가 나타난다.  
이러한 시계열 중 일부는 MA, AR, ARMA로 근사할 수 있다.  
![image](https://github.com/user-attachments/assets/73ea402b-81df-4afe-9c40-27daf5b86a7e)  
y : 현재값  
뮤 : 수열의 평균   
e_t : 현재 오차 항  
q : 차수  
e_t-1 .... e_t-q : 과거 오차 항  
![image](https://github.com/user-attachments/assets/b6fc09f2-ef08-441f-bdf4-6877a2f17115)  
 - ADF로 정상성 알아보는 법
```  
from statsmodels.tsa.stattools import adfuller
ADF_result = adfuler(df['widget_sales'])
peint(f'ADF Statistic: {ADF_result[0]}')
print(f'p-value: {ADF_result[1]}')
```
ADF 값이 큰 음수이고, p-value가 0.05보다 작으면 정상적인 수열이다.  
 - 1차 차분 적용하는 법
```  
import numpy as np
widget_sales_diff = np.diff(df['widget_sales'],n=1)
```
이후 ACF 도식  
![image](https://github.com/user-attachments/assets/61870145-a6e8-4262-8fa1-46b4fe96fa0e)  
특정 지연 이후 모든 계수가 유의하지 않다면, MA(q) 프로세스가 있다고 결론 내릴 수 있다.(위의 경우 MA(2))  

## 4.2 이동평균과정 예측하기  
![image](https://github.com/user-attachments/assets/ae26c6cb-b385-4dd0-9375-12286827d57f)

![image](https://github.com/user-attachments/assets/1fb04532-59b1-4ca1-a250-21359d542fd8)  
롤링 예측 : 한 번에 1 or 2번의 time step씩 예측하는 함수를 만들고, 이렇게 반복한다.   
ex) 449 time step에 대해 train하고 450,451번째의 time step을 예측한다. 이후 451개의 time step을 train 하고 452,453을 예측하고, ....   
리스팅 4.1 : 전체 test set에 대한 예측을 완료할 때까지 지정한 기간과 지정한 시간 단계 횟수 동안 반복적으로 모델을 피팅하고 예측을 수행하는 함수.
![image](https://github.com/user-attachments/assets/b4121526-e5c8-4ca3-a168-6711742abfb5)  
![image](https://github.com/user-attachments/assets/5571ec8e-3d13-4163-8c4e-91f7ae34f8d3)  
![image](https://github.com/user-attachments/assets/9d09af43-553d-4544-930a-ea05ae2c4254)   
정상적 수열에 대한 챔피언 모델을 얻었으므로, 예측 결과를 역변환하여 데이터 집합의 변환하지 않은 원래 규모로 되돌려야 한다.  
![image](https://github.com/user-attachments/assets/a25620b5-625c-4691-ba73-cf4caeacf29a)  
y_1 = y_0 + y'_1 = y_0 + y_1 - y_0 = y_1  
y_2 = y_0 + y'_1 + y'_2 = y_0 + y_1 - y_0 + y_2 - y_1 = (y_0 - y_0) + (y_1 - y_1) + y_2 = y_2  
![image](https://github.com/user-attachments/assets/86a116ff-9665-4342-8e86-aece6ee496bb)  
 - 역변환한 MA(2) 예측 결과
![image](https://github.com/user-attachments/assets/bc627746-f85c-476a-bd3e-41a4db9c513f)
![image](https://github.com/user-attachments/assets/ccab2c46-be64-4b09-a055-cd4a098a53d0)
***  
# 5. 자기회귀과정  
![image](https://github.com/user-attachments/assets/f049ee75-9266-4e6d-904b-986e36aae267)   
 - 정상적 시계열이 아닐 가능성이 높다.
## 5.2 자기회귀과정   
자기회귀과정은 변수가 자기 자신에게 회귀하는 프로세스이다. 시계열에서 이는 현잿값이 과거값에 선형적으로 의존한다는 것을 뜻한다.  
![image](https://github.com/user-attachments/assets/182dddb5-b309-47e6-a013-2564d7150296)  

## 5.3 정상적 자기회귀과정의 차수 찾기  
원본 데이터 :   
![image](https://github.com/user-attachments/assets/6cb2013c-bf33-4ea4-9d12-2f457ac55e70)  
차분된 데이터 :   
![image](https://github.com/user-attachments/assets/df2650a0-d8d2-412a-aa58-c565cba07efe)   
ACF :   
![image](https://github.com/user-attachments/assets/49d0a956-53d1-4c05-81ce-7c224dc0b500)  

정상적 자기회귀과정의 차수를 식별하기 위한 방법으로 ACF에서 정보를 얻을 수 없을 때 PACF(partial ACF)를 사용해야 한다.  
PACF : 시계열 내에서 상관관계가 있는 지연된 값들 사이의 영향도를 제거할 때 해당 값들 간의 상관관계를 측정한다.  
그러므로 PACF를 도식화하여 정상화된 AR 프로세스의 차수를 결정할 수 있다.  
지연 p는 그 이후 계수들이 유의하지 않은 값이다.  
![image](https://github.com/user-attachments/assets/f3a8629c-021a-4da7-b3c9-88cd9a6ac88f)  
지연 3까지 유의하므로 차수는 3이다.  

## 5.4 자기회귀과정 예측하기  
원본 수열과 차분된 수열 :   
![image](https://github.com/user-attachments/assets/f2a1e17a-78a3-48c0-a1cf-7c1d195b081a)  
과거 평균, 마지막으로 측정된 값을 베이스라인으로 사용하고, AR(3)모델도 사용한다. 이후 MSE로 성능을 평가한다.  
예측은 롤링 예측 함수를 재사용한다.  

 - 소매점의 주간 평균 유동인구를 차분한 값에 대한 예측 결과 :
 ![image](https://github.com/user-attachments/assets/acfe274a-3beb-423e-946e-291d6f6b37bc)
 - MSE가 가장 낮은 AR(3)모델의 차분하지 않은 예측값 :
![image](https://github.com/user-attachments/assets/df0c6ca1-b231-462e-9c8b-0730bddf9dd1)















