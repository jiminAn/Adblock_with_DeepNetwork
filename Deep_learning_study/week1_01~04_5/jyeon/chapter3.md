

# Chapter 3. 머신러닝의 기초를 다집니다. - 수치 예측
## 03-1 선형 회귀에 대해 알아보고 데이터를 준비합니다.
### 함수를 이해하는 선형 회귀
선형 회귀는 간단한 1차 함수로 표현할 수 있다.   
`y = ax + b`  
위 1차 함수의 기울기 (slope)는 a이고 절편(intercept)은 b이다.
#### 선형 회귀는 기울기와 절편을 찾아줍니다.
보통 1차 함수 문제에서는 x에 따른 y의 값에 집중한다.  
선형 회귀에서는 이와 반대로 x, y가 주어졌을 때 **기울기와 절편을 찾는데**에 집중한다.
#### 그래프를 통해 선형 회귀의 문제 해결 과정을 이해합니다.
그래프를 옮겨 가면서 주어진 데이터와 잘 맞는 모델을 찾아낸다.  
**그래프를 옮긴다**--> 기울기와 절편을 변화시킨다.  
문제를 해결하면서 만드는 1차 함수들을 **선형 회귀로 만든 모델** 이라고 한다.  
**선형 회귀를 만들어 문제를 해결하는 과정.**  
1. 미리 준비한 입력과 타깃을 가지고 (입력 - x: 3, 4, 5 / 타깃 - y: 25, 32, 39)
2. 모델을 만든 다음 (y = 7x + 4)
3. 새 입력 (6)에 대해 어떤 값(46)을 예상한다.
### 문제 해결을 위해 당뇨병 환자의 데이터 준비하기
현실적인 문제를 해결해 보자.  
목표는 **당뇨병 환자의 1년 후 병의 진전된 정도를 예측하는 모델 만들기**  
#### 사이킷런에서 당뇨병 환자 데이터 가져오기
**사이킷런**: 머신러닝, 딥러닝 패키지  
머신러닝 딥러닝 패키지에는 이공지는 학습을 위한 데이터 세트(data set)가 준비되어 있다.  
여기에서는 사이킷런의 데이터 세트 중 당뇨병 환자의 데이터 세트를 사용한다.
diabetes.data는 442개의 행과 10개의 열로 구성되어 있다.  
**행은 샘플(sample)**, **열은 특성(feature)** 이다. 각 특성들을 모아서 1개의 샘플이 되는 것이다.  
입력 데이터의 특성은 다른 말로 **속성, 독립 변수(independent variable), 설명 변수(explanatory variable)** 등으로 부르는데 여기서는 머신러닝에서 널리 통용되는 용어인 **특성**을 사용할 것이다.  
### 당뇨병 환자 데이터 시각화하기
산점도 그리기 --> 맷플롯립의 scatter( )함수로 그릴 수 있다.
매번 diabetes.data를 입력해서 데이터의 속성을 참고하는 것은 번거로우니까 훈련 시작 전에 입력 데이터와 타깃 데이터를 따로 저장해 두고 모델을 훈련하자.
## 03-2 경사 하강법으로 학습하는 방법을 알아봅니다.
### 그래프로 경사 하강법의 의미를 알아봅니다
여러개의 특성을 가진 데이터를 이용하여 그릴 수 있는 고차원 공간에서의 그래프는 직관적으로 떠올리기 힘들기 때문에   
보동은 여러개의 특성을 가진 데이터를 이용하여 4, 5, 6차원 등의 그래프를 한 번에 그리는 것이 아니라  
특성의 개수를 1, 2개만 사용하여 2차원이나 3차원 그래프로 그리는 경우가 많다.  
이렇게 하면 알고리즘에 대한 직관을 쉽게 얻을 수 있다.
#### 선형 회귀와 경사 하강법의 관계를 이해합시다.
선형 회귀의 목표는 입력 데이터와 타깃 테이더를 통해서 기울기와 절편을 찾는 것, 즉 산점도 그래프를 잘 표현하는 직선의 방정식을 찾는 것이다.   
**경사 하강법 (gradient descent)** 은 모델이 데이터를 잘 표현할 수 있도록 **기울기(변화율)** 를 사용하여 모델을 조금씩 조정하는 최적화 알고리즘이다.   
### 예측값과 변화율에 대해 알아봅니다.
기울기 a ⇒ 가중치 w나 계수 Θ로 표기  
y ⇒ ŷ (y-hat)으로 표기  
앞으로는 y = ax + b를 **ŷ = Θx + b** 로 이해하자.  
여기서 **가중치 w와 절편 b는 알고리즘이 찾은 규칙을 의미하고, ŷ은 우리가 예측한 값(예측값)을 의미** 한다.
#### 예측값이란 무엇일까요?
우리가 입력과 출력 데이터를 통해 만든 모델에 대해 새로운 입력값을 넣으면 어떤 출력이 나오는데 이 값이 모델을 통해 예측한 값이다.  
타깃 데이터(y)와 구분하기 위해서 예측값은 ŷ라는 문자를 사용하는 것이다.   
어쨌든 y와 ŷ는 어떤 결과라는 점은 동일하다. (y는 정답이고 ŷ는 예측한 값이라는 점이 다른 점이다.)
### 예측값으로 올바른 모델 찾기
**훈련 데이터에 잘 맞는  w와 b를 찾는 방법**
1. 무작위로 w와 b를 정합니다. (무작위로 모델 만들기)
2. x에서 샘플 하나를 선택하여 ŷ를 계산합니다. (무작위로 모델 예측하기).
3. ŷ과 선택한 샘플의 진짜 y를 비교합니다. (예측한 값과 진짜 정답 비교하기)
4. ŷ이 y와 더 가까워지도록 w, b를 조정합니다. 
5. 모든 샘플을 처리할 때까지 다시 2~4 항목을 반복합니다.
#### 훈련 데이터에 맞는 w와 b 찾아보기
무작위로 w와 b를 정한 다음에 ŷ을 구해보고, w를 증가시킨 다음에 다시 ŷ를 구해서 ŷ의 변화율을 계산해 본다.  
```python
w_rate = y_hat_inc - y_hat) / (w_inc - w)
```
변화율이 양수가 된다면 w값을 증가시키면 ŷ의 값을 증가시킬 수 있다.  
변화율이 음수일 경우에 ŷ의 값을 증가시켜야 한다면 --> w값을 감소시키면 된다.  
즉 ŷ값을 조정하기위해서 w값을 어떻게 조정해야 하는지를 결정하는 데에는 **변화율** 을 봐야 한다는 것을 알 수 있다. 
### 변화율로 가중치 업데이트하기
#### 변화율이 양수일 때 가중치를 업데이트 하는 방법
ŷ의 값이 y에 못미치는 값일 경우라면 ŷ을 증가시켜야 한다.  
이 상황에서는 w가 증가하면 ŷ도 증가한다.   
이때 변화율이 양수인 점을 이용해서 **변화율을 w에 더하는 방법**으로 w를 증가시킬 수 있다.
#### 변화율이 음수일 때 가중치를 업데이트 하는 방법
변화율이 0보다 작을 때 ŷ을 증가시키려면 어떻게 해야 할까?  
변화율이 음수일 경우에는 w가 증가하면 ŷ이 감소하게 된다. 즉 ŷ를 증가시키기 위해서는 w를 감소시켜야 한다.   
이 때 변화율이 음수인 점을 이용해서 **변화율을 w에 더하는 방법**으로 w를 증가시킬 수 있다.

즉 가중치 w를 업데이트하는 방법은 두 경우 모두 **w + w_rate**이다.
### 변화율로 절편 업데이트하기
절편 b에 대한 변화율을 구한 다음 변화율로 b를 업데이트해보자.  
b가 1만큼 증가하면 ŷ도 1만큼 증가한다. (당연함)  
**b를 업데이트하기 위해서는 변화율이 1이므로 단순히 1을 더하면 된다.**  

하지만 이렇게 ŷ을 증가시켜야 하는 상황을 가정해서 구한 w와 b를 업데이트 하는 방법은 2가지의 상황에서 문제점이 발생하는데  
1. ŷ이 y에 한참 미치지 못하는 값인 경우에 w와 b를 더 큰 폭으로 수정할 수 없다.
2. ŷ이 y보다 커지면 ŷ을 감소시킬 수 없다. 
### 오차 역전파로 가중치와 절편을 더 적절하게 업데이트합니다.
**오차 역전파(backpropagation)** 는 ŷ와 y의 차이를 이용하여 w와 b를 업데이트한다.  
이름에서 알 수 있듯이 이 방법은 오차가 연이어 전파되는 모습으로 수행된다. 
#### 가중치와 절편을 더욱 적절하게 업데이트하는 방법
앞의 방법과는 다르게 이번에는 **ŷ에서 y를 뺀 오차의 양을 변화율에 곱하는 방법** 으로 w를 업데이트해보자.  
이렇게 하면 오차가 크면 w와 b를 많이 바꿀 수 있고, ŷ이 y보다 클 경우에 w와 b의 방향도 바꿀 수 있다.  
보통 경사 하강법에서는 주어진 훈련 데이터로 학습을 여러 번 반복한다. 이렇게 전체 훈련 데이터를 모두 이용하여 한 단위의 작업을 진행하는 것을 **에포크(epoch)** 라고 부른다.   
#### 지금까지 모델을 만든 방법 정리하기
1. w와 b를 임의의 값으로 초기화하고 훈련 데이터의 샘플을 하나씩 대입하여 y와 ŷ의 오차를 구한다.
2. 1에서 구한 오차를 w와 b의 변화율에 곱하고 이 값을 이용하여 w와 b를 업데이트한다.
3. 만약 ŷ이 y보다 커지면 오차는 음수가 되어 자동으로 w와 b가 줄어드는 방향으로 업데이트된다. 
4. 반대로 ŷ이 y보다 작으면 오차는 양수가 되고 w와 b는 더 커지도록 업데이트된다.
## 03-3 손실 함수와 경사 하강법의 관계를 알아봅니다.
경사 하강법을 좀 더 기술적으로 표현하면 '어떤 손실 함수(loss function)가 정의되었을 때 손실 함수의 값이 최소가 되는 지점을 찾아가는 방법'이다.  
**손실 함수** 란 예상한 값과 실제 타깃값의 차이를 함수로 정의한 것이다.   
### 손실 함수의 정체를 파헤쳐봅니다
앞에서 사용한 '오차를 변화율에 곱하여 가중치와 절편 업데이트하기'는 '제곱 오차'라는 손실 함수를 미분한 것과 같다.   
제곱 오차를 수식으로 나타내면 **SE = (y-ŷ)<sup>2</sup>** 이 된다.  
제곱 오차를 최소화하기 위해서는 기울기에 따라 함수의 값이 낮은쪽으로 이동해야 한다. (기울기가 양수인지, 음수인지에 따라 이동하는 방향이 다르니까)  
기울기를 구하기 위해서 제곱오차를 가중치와 절편에 대하여 미분하자.
#### 가중치에 대하여 제곱 오차 미분하기
제곱오차를 가중치에 대하여 편미분한다.  
**미분 결과: -2(y-ŷ)x**  
-2를 없애주기 위해서 앞으로는 제곱 오차 함수를 **-2(y-ŷ)<sup>2</sup>** 으로 정의한다. (손실함수에 상수를 곱하거나 나누어도 가중치나 절편에 영향을 주지 않는다.)  
**미분 결과: -(y-ŷ)x**  
손실 함수의 낮은 쪽으로 값을 이동시켜주기 위해서 w에 변화율을 빼 주는 방법으로 w를 업데이트한다.  
**w = w - (-(y-ŷ)x) = w + (y - ŷ)x**
#### 절편에 대하여 제곱 오차 미분하기
제곱 오차를 절편에 대하여 편미분한다.  
**미분 결과: -y + ŷ**  
**b = b - (-y + ŷ) = b + y - ŷ**  

앞으로는 손실함수에 대해 일일이 변화율의 값을 계산하는 대신 편미분을 사용하여 변화율을 계산한다.  
변화율은 인공지능 분야에서 **그래디언트(gradient)** 라고 부른다. 
## 03-4 선형 회귀를 위한 뉴런을 만듭니다.
앞에서 만든 경사 하강법 알고리즘을 Neuron이라는 이름의 파이썬 클래스로 만들어봅시다.
### Neuron 클래스 만들기
신경망 알고리즘은 뇌의 뉴런과는 아무런 관계가 없기 때문에 요즘 연구자들은 '뉴런' 대신 '유닛(Unit)'이라는 명칭을 즐겨 사용한다.  
```python
# Neuron 클래스의 전체 구조
class Neuron{
	def __init__(self):
	# 초기화 작업 수행
	...
	# 필요한 메소드 추가
	def forpass(self, x):
	def backprop(self, x, err):
	def fit(self, x, y, epochs=100):
}
```
--> 코랩에서 실습해봄
