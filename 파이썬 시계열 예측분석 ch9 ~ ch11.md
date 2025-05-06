# CH9. 모델에 외생 변수 추가하기  
SARIMAX : SARIMA + 외생변수의 영향도 추가.   
![image](https://github.com/user-attachments/assets/8d607a8e-0154-4c19-8c6c-bb0b449d2083)  
GDP = C + G + I + NX (C: 소비, G : 정부 지출, I : 투자, NX : 순수출)  
![image](https://github.com/user-attachments/assets/03f1b160-4901-4d3d-84f2-21a17b323542)  
기본적으로 외생 변수는 이산 값이고, 외생 변수의 선형 조합을 추가한다.  
![image](https://github.com/user-attachments/assets/22f22053-b0e8-4f1e-a1d8-224d769fd066)  
 - 그러나 외생변수는 미래 time step의 값을 예측하기 어렵다.
   그래서 목표 변수를 예측하기 위해 외생 변수를 예측해야 하는 경우에는 오차가 커진다.
   미래의 더 많은 time step을 예측할수록 정확도가 급격히 낮아진다.
   ![image](https://github.com/user-attachments/assets/0375ae1f-3db0-4964-ba24-5d11ed51f415)
![image](https://github.com/user-attachments/assets/7b269846-e689-41e8-8abc-93ddad36e68a)





