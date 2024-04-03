#전통적 포트폴리오

1.데이터 로드 및 처리:
코드는 세 개의 다른 금융 자산(브렌트유, 금, 나스닥)에 대한 데이터를 로드한다.
.head() 함수를 사용하여 각 데이터셋의 첫 5행을 출력한다.
이 부분은 데이터의 구조를 이해하고, 누락된 값이나 이상치 등 데이터를 검증하기 위한 초반단계이다.

2.포트폴리오 통계 계산:
각 자산에 대한 일일 수익률을 계산한다. 수익률은 일일 가격 변화의 백분율로 계산되며 로그 수익률로 변환된다.
이 수익률은 포트폴리오 분석에서 자산의 수익성을 평가하는 데 사용된다.
세 자산의 수익률을 하나의 데이터프레임으로 결합한다.
결측치를 제거한다(dropna() 함수 사용).
이후, 연간화된 기대 수익률(평균), 변동성(표준 편차), 상관관계 행렬을 계산한다. 이 통계들은 자산 간의 관계를 이해하고 포트폴리오의 위험을 평가하는 데 중요하다.

3.포트폴리오 최적화:
minimize() 함수를 사용하여 포트폴리오의 변동성을 최소화하는 가중치를 찾는다.
목표 수익률을 설정하고, 이를 달성하면서 위험을 최소화하는 포트폴리오를 찾는 최적화 문제를 정의한다.
이 과정에서 계산된 공분산 행렬은 자산 간의 변동성의 관계를 나타내며 포트폴리오 위험을 계산하는 데 사용된다.

4.효율적 투자선 시각화:
efficient_frontier() 함수는 주어진 수익률 범위 내에서 변동성을 최소화하는 효율적인 포트폴리오의 집합을 계산한다.
이 함수는 다양한 목표 수익률에 대해 변동성을 최소화하는 포트폴리오를 찾는 minimize_volatility() 함수를 반복적으로 호출한다.
그리고 나서 이러한 포트폴리오의 변동성과 기대 수익률을 그래프로 그린다. 이 그래프는 투자의 기대 수익률과 관련된 위험을 시각적으로 보여준다.

포트폴리오 평가:
코드는 또한 최대 기대 수익률을 가진 포트폴리오와 변동성을 최소화한 포트폴리오를 찾아낸다.
이는 투자자가 위험 감수 능력과 수익률 목표에 따라 투자 결정을 내리는 데 도움을 준다.


머신러닝 포트폴리오
1.데이터 로딩 및 확인: Pandas 라이브러리를 이용하여 원유, 금, 나스닥 지수 데이터를 CSV 파일에서 로드하고, 각 데이터의 상위 5개 행을 확인한다. 이는 데이터가 올바르게 로드되었는지와 구조를 이해하기 위한 초기 단계다.

2.데이터 전처리:
날짜 열을 datetime 형식으로 변환하고 인덱스로 설정하여 시간에 따른 분석이 용이하게 한다.
ADF(Augmented Dickey-Fuller) 테스트를 각 데이터에 적용해 시계열의 정상성을 검사한다. 정상 시계열이 아닌 경우, 차분을 통해 정상성을 확보한다.

3.정상성 확보: 원유, 금, 나스닥 데이터에 대하여 차분(diff)을 수행하고, 다시 ADF 테스트를 실시해 차분 후의 데이터가 정상 시계열인지 확인한다.

4.ACF와 PACF 플롯: 차분된 데이터에 대해 자기상관함수(ACF)와 부분 자기상관함수(PACF)를 플롯하여 ARIMA 모델의 매개변수를 추정하는 데 도움을 준다.

5.ARIMA 모델 구축 및 적합: ACF와 PACF 분석 결과를 바탕으로 각 자산 데이터에 ARIMA 모델을 구축하고, 모델을 적합시킨다. 이후 각 모델의 요약 결과를 확인하여 모델의 성능과 적합성을 평가한다.

6.미래 가격 예측: 구축한 ARIMA 모델을 이용하여 각 자산의 미래 가격을 단기(5일) 및 장기(1년)로 예측한다. 이는 향후 자산 가격의 변동성과 예상 수익률을 평가하는 데 사용된다.

7.포트폴리오 구성:
변동성 최소화 포트폴리오: 예측된 가격의 변동성(표준편차)을 기반으로 각 자산의 가중치를 계산하여 변동성을 최소화하는 포트폴리오를 구성한다.
예상 수익률 계산: 변동성 최소화 포트폴리오와 1년 수익률이 가장 높은 자산을 선택하여 구성한 포트폴리오의 예상 수익률을 계산한다.

8.결과 해석 및 평가: 계산된 포트폴리오의 예상 수익률을 바탕으로 투자 전략을 수립한다. 이 과정에서 자산의 변동성, 예상 수익률, 그리고 포트폴리오 구성 전략에 대한 심도 있는 분석이 이루어진다.
