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

# 10. 다중 시계열 예측하기  
 - 변수가 양방향 관계를 가지는 경우.
   t1이 t2의 예측 변수이고, t2가 t2의 예측 변수이다.
![image](https://github.com/user-attachments/assets/8c1b7895-0642-41fd-a07d-8d8692f34c19)

 - 벡터자기회귀(VAR) : 시간에 따라 변화하는 여러 수열 간의 관계.
   ![image](https://github.com/user-attachments/assets/e2a1b13c-6edc-4d97-b51e-cf170fe81375)
   ![image](https://github.com/user-attachments/assets/cbe8f765-4065-4d37-9939-bb0012e66e50)
   ![image](https://github.com/user-attachments/assets/9a323194-3f80-459b-b7ae-58749145e054)

 - 그레인저 인과관계 테스트 : 한 시계열이 다른 시계열을 예측할 수 있는지 여부.
   VAR(p) 모델은 한 시계열의 과것값을 사용하여 다른 시계열을 예측하기 때문에 이 관계를 테스트하는 것이 중요하다.  
   ![image](https://github.com/user-attachments/assets/f916e67d-b13c-400b-9d0d-886d08fcdc2f)

   귀무가설 : 그레인저 인과관계에 따라 y_2,t가 y_1,t를 유발하지 않는다는 것이다.

# 11. 캡스톤 프로젝트  
![image](https://github.com/user-attachments/assets/12bc9efb-1f97-4f49-a82b-5b29e8e4a05c)  
1. 목표는 12개월 동안의 항당뇨제 처방 건수를 예측하는 것이다.
   롤링 예측을 수행할 수 있도록 데이터 집합에서 지난 36개월을 테스트 집합으로 사용.
2. 시계열을 시각화한다.
3. 시계열 분해를 사용하여 추세 및 계절적 구성요소를 추출한다.
4. 탐색을 기반으로 가장 적합한 모델을 결정한다.
5. 일반적인 단계에 따라 시계열 모델링.
6. 테스트 집합에 대해 12개월의 롤링 예측을 수행한다.
7. 예측을 시각화한다.
8. 모델의 성능을 베이스라인 모델과 비교한다.
9. 모델을 사용해야 할지에 대해 결론을 내린다.
   ![image](https://github.com/user-attachments/assets/b769716b-0452-4854-b242-a56389e61794)
![image](https://github.com/user-attachments/assets/c6d2738e-4f0b-460c-847b-20f5854f484d)




   









