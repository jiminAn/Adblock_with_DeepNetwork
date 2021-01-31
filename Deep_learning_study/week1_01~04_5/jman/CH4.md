# 4강. 분류하는 뉴런을 만듭니다

## 04-1. 초기 인공지능 알고리즘과 로지스틱 회귀를 알아봅니다.
: 로지스틱 회귀를 제대로 이해하기 위해, 로지스틱 회귀로 발전된 초창기 인공지능 알고리즘들을 순서대로 살펴보자

### 퍼셉트론(Perceptron)에 대해 알아봅니다
: 1957년 코넬 항공 연구소의 프랑크 로젠블라트는 이진 분류 문제에서 최적의 가중치를 학습하는 퍼셉트론 알고리즘을 발표함

- 이진 분류(binary classification)란? 임의의 샘플 데이터를 True/False로 구분하는 문제를 말하며, 과일이라는 샘플 데이터가 있을 때 사과인지, 아닌지를 판단하는 것이 이진분류에 해당한다

**퍼셉트론의 전체 구조를 훑어봅니다**

: 퍼셉트론은 선형함수를 통과한 값 z를 계단 함수로 보내 0보다 큰지, 작은지 검사하여 1과 -1로 분류하는 아주 간단한 알고리즘이며 계단 함수의 결과를 사용하여 가중치와 절편을 업데이트한다.

- 퍼셉트론은 직선 방정식을 사용(3장에서 공부한 선형 회귀와 유사한 구조를 가짐)

  -  단, 퍼셉트론은 마지막 단계에서 샘플을 이진 분류하기 위하여 계단 함수(step function) 사용
  -  계단 함수를 통과한 값을 다시 가중치와 절편을 업데이트(학습)하는데 사용

- 뉴런은 입력 신호 w1x1, w2x2, b 를 받아 z를 만든다. 

  - **w1x1 + w2x2 + b = z**  (선형 함수)
  - 즉, 해당 수식에 의해 z를 만들게 됨

- 계단 함수는 z가 0보다 크거나 같으면 1로, 0보다 작으면 -1로 분류

  - 1 : 양성 클래스(positive class)

  - -1 : 음성 클래스(negative class)

  - 해당 함수를 그래프로 그리면 계단모양이 됨 -> step function이라고 부름

    

**지금부터 여러개의 특성을 사용하겠습니다** 
: 앞으로는 여러 특성을 사용하여 문제를 해결하는 경우가 많이 나오므로, 아래와 같이 특성이 n개인 선형 함수 표기법에 익숙해지도록 하자.  

- 특성이 n개인 선형함수(n번째 특성의 가중치와 입력)
  $$
  w_1x_1 + w_2x_2 + ... + w_nx_n + b = z
  $$

  $$
  z = b + \sum\limits_{i=1}^{n} w_ix_i
  $$


### 아달린(Adaline)에 대해 알아봅니다
- 퍼셉트론이 등장한 이후 1960년에 스탠포드 대학의 버나드 위드로우와 테드 호프가 **퍼셉트론을 개선한 적응형 선형 뉴런을 발표함**

- 적응형 선형 뉴런은 **아달린**이라고도 부르며, 선형 함수의 결과를 학습에 사용하고 계단 함수의 결과는 예측에만 활용하는 방식임

- 나머지 요소는 퍼셉트론과 동일

  

### 로지스틱 회귀(logistic regression)에 대해 알아봅니다
: 로지스틱 회귀는 아달린에서 조금 더 발전한 형태를 취함
1. **활성화 함수(activation function)**

   : 선형 함수를 통과시켜 얻은 z를 임계함수에 보내기 전에 변형시키는 함수

2. **임계 함수(threshold function)**

   : 로지스틱 회귀의 마지막 단계에서 사용하는 함수로, 예측을 수행한다. 아달린이나 퍼셉트론의  계단 함수와 역할은 비슷하나 활성화 함수의 출력값을 사용한다는 점이 다르다.

**활성화 함수는 비선형 함수를 사용합니다**

- 활성화 함수로 선형 함수 대신 비선형 함수를 사용하는 이유

  : 활성화 함수(y = kx)와 w1x1 + w2x2 + ... + wnxn + b = z 두 식을 쌓을 경우, 덧셈과 곱셈의 결합법칙과 분배법칙에 의해 정리하면 다시 하나의 큰 선형 함수가 되어 임계 함수 앞에 뉴런을 여러개 쌓아도 결국 선형함수일 것이므로 의미가 없음

- 따라서 활성화 함수는 의무적으로 비선형 함수를 사용하며 로지스틱 회귀에는 '시그모이드 함수'가 활성화 함수로 사용됨

  

## 04-2. 시그모이드 함수로 확률을 만듭니다

### 시그모이드 함수의 역할을 알아봅니다
1. 선형 함수의 출력값 z
2. z는 활성화 함수를 통과하여 a가 됨
3. 시그모이드 함수는 z를 0~1사이의 확률값으로 변환시켜주는 역할을 함
   - 시그모이드 함수 : 로지스틱 회귀에서 사용하는 활성화 함수
4. 즉, 시그모이드 함수를 통과한 값 a를 암 종양 판정에 사용하면 양성 샘플일 확율로 해석할 수 있음
   - 보통 a가 0.5 보다 크면 양성 클래스, 그 이하면 음성 클래스로 구분

### 시그모이드 함수가 만들어지는 과정을 살펴봅니다
: 약간의 수학 기교를 사용하며 만들어지며 해당 함수가 만들어지는 과정은 다음과 같음
**오즈 비 > 로짓 함수 > 시그모이드 함수**

**오즈 비에 대해 알아볼까요?**

- 시그모이드 함수는 오즈 비(odds ratio)라는 통계를 기반으로 만들어진다

  - 오즈 비란? 성공 확률과 실패 확률의 비율을 나타내는 통계  
    $$
    OR = \frac {p}{1-p}
    $$
    : 오즈 비를 그래프로 그릴 경우,  p가 0~1까지 증가할 때 오즈 비의 값은 처음에는 천천히 증가하지만 1에 가까워지면 급격히 증가하게 됨

**로짓 함수에 대해 알아볼까요?**
: 오즈 비에 로그 함수를 취하여 만든 함수를 로짓 함수(logit function)라고 함
$$
 logit(p) = log(\frac{p}{1-p})
$$

- 로짓 함수의 특징
  - p가 0.5일 때 0
  - p가 0,1일 때 각각 무한대로 음수와 양수가 됨

 - 로짓함수의 세로축을 z, 가로 축을 p로 놓으면 확률이 0~1까지 변할 때, z가 매우 큰 음수에서 매우 큰 양수까지 변하며 아래와 같이 식으로 표현 가능
$$
log(\frac {p}{1-p}) = z
$$

**로지스틱 함수에 대해 알아볼까요?**
: 위 식을 다시 z에 대하여 정리하면 아래와 같은 식이 됨
$$
p = \frac {1}{1+e^{-z}}
$$

- z에 대해 정리하는 이유: 가로 축을 z로 놓기 위함 
- 이 식을 로지스틱 함수라고 부름
  - 그래프로 그려보면 로짓 함수의 가로와 세로 축을 반대로 뒤집어 놓은 모양이 됨
  - 또한 그래프는 S자 형태를 띄게 됨
  - 해당 모양에서 착안하여 로지스틱 함수를 시그모이드 함수(sigmoid function)라고도 부름

### 로지스틱 회귀 중간 정리하기

- 로지스틱 회귀는 이진 분류가 목표이므로 (-∞ ~ ∞ ) 범위를 가지는 z의 값을 조절할 방법이 필요했다
- 그래서 시그모이드 함수를 활성화 함수로 사용한 것임
  - 시그모이드 함수를 통과하면 z를 확률처럼 해석할 수 있기 때문. 
- 또한 시그모이드 함수의 확률인 a를 0,1로 구분하기 위하여 마지막에 임계함수를 사용
- 그 결과 입력 데이터  x는 0 또는 1의 값으로 나누어 짐(즉, 이진 분류가 됨)
  - 로지스틱 회귀가 이진분류를 하기 위한 알고리즘인 이유를 알 수 있음
- 그런데 아직 우리는 가중치와 절편을 적절하게 업데이트 할 수 있는 방법을 배우지 않았으므로 다음장에서는 로지스틱 회귀를 위한 손실함수인 로지스틱 손실 함수에 대해 알아보도록 하자


## 04-3. 로지스틱 손실 함수를 경사 하강법에 적용합니다
: 선형 회귀는 정답과 예상값의 오차 제곱이 최소가 되는 가중치와 절편을 찾는 것이 목표인 반면, 로지스틱 회귀와 같은 분류의 목표는 올바르게 분류된 샘플 데이터의 비율 자체를 높이는 것이다.  
하지만, 올바르게 분류된 샘플의 비율은 미분 가능한 함수가 아니기 때문에 경사 하강법의 손실 함수로 사용할 수 없다. 대신 비슷한 목표를 달성할 수 있는 다른 함수 즉, 로지스틱 손실 함수를 사용하면 된다.

### 로지스틱 손실 함수를 제대로 알아봅시다
: 로지스틱 손실 함수는 다중 분류를 위한 손실 함수인 크로스 엔트로피(cross entropy)손실 함수를 이진 분류 버전으로 만든 것이다. 로지스틱 함수는 다음과 같다. 
$$
L = -(ylog(a) + (1-y)log(1-a))
$$

- a = 활성화 함수가 출력한 값, y = 타깃

- 이진 분류의 경우 그렇다(1), 아니다(0)라는 식으로 2개의 정답만 있으므로 타깃의 값 역시 1 또는 0이다. 

  : 따라서 위의 식은 y가 1 이거나 0 인 경우로 정리.

  |                           | L         |
  | ------------------------- | --------- |
  | y가 1인 경우(양성 클래스) | -log(a)   |
  | y가 0인 경우(음성 클래스) | -log(1-a) |

  

- 그런데 앞 두 식의 값을 최소로 만들다 보면 a의 값이 우리가 원하는 목표치가 됨을 알 수 있음
  - 예를 들어 양성 클래스인 경우 로지스틱 손실 함수의 값을 최소로 만들려면 a는 자연스럽게 1에 가까워짐
  - 반대로 음성 클래스인 경우 로지스틱 손실 함수의 값을 최소로 만들면 a가 0에 자연스럽게 가까워짐
  - 이 값을 계단 함수에 통과시키면 올바르게 분류 작업이 수행된다. 
- 즉, 로지스틱 손실 함수를 최소화하면 a의 값이 우리가 가장 이상적으로 생각하는 값이 된다. 이제 로지스틱 손실 함수의 최소값을 만드는 가중치와 절편을 찾기 위해 미분을 해보자

### 로지스틱 손실 함수 미분하기
: 가중치와 절편에 대한 로지스틱 손실 함수의 미분 결과는 다음과 같다. 이 식은 가중치와 절편 업데이트에 사용할 것

1. 가중치에 대한 미분
   $$
   (\frac {∂}{∂w_i})L = -(y-a)x_i
   $$
   
2. 절편에 대한 미분

$$
(\frac {∂}{∂b})L = -(y-a)1
$$

그런데 미분 결과를 확인해보면  ŷ이 a로 바뀌었을 뿐 제곱 오차를 미분한 결과와 동일하다. 

참고 <03장에서 본 제곱 오차의 미분 | 로지스틱 손실 함수의 미분>

![image-20210131133702406](/Users/anjimin/Library/Application Support/typora-user-images/image-20210131133702406.png)

즉 로지스틱 회귀의 구현이 3장에서 만든 뉴런 클래스와 크게 다르지 않다는 것을 알 수 있다.    
이 장에서 가장 중요한 것은 **로지스틱 손실 함수의 미분을 통해 로지스틱 손실 함수의 값을 최소로 하는 가중치와 절편을 찾아야 한다는 점**이다

### 아래는 미분 유도 과정 : (대략적인 큰 흐름만 이해하고 04-5절로 넘어가도 괜찮)

**로지스틱 손실 함수와 연쇄 법칙**

- 로지스틱 손실 함수를 가중치나 절편에 대하여 바로 미분하면 너무 복잡하기 때문에 연쇄법칙을 이용하면 간단

  1. 로지스틱 손실 함수를 활성화 함수의 출력값에 대하여 미분
  2. 활성화 출력값은 선형 함수의 출력값에 대하여 미분
  3. 선형 함수의 출력값은 가중치 또는 절편에 대하여 미분 후 서로 곱함

  1,2,3 과정을 거치면 로지스틱 손실 함수를 가중치에 대하여 미분한 결과를 얻을 수 있음

  - 이 과정은 아래처럼 오른쪽부터 왼쪽까지 역방향으로 진행된다는 것을 알 수 있음
    $$
    (\frac {∂L}{∂w_i})L = (\frac {∂L}{∂a})(\frac {∂a}{∂z})(\frac {∂z}{∂w_i})
    $$
    

**로지스틱 손실 함수를 a에 대하여 미분하기**

- 이제 각각의 도함수를 구하기만 하면 됨

  1. 로지스틱 손실 함수를 a에 대하여 미분 
  2. 계산 결과 나온 log(a)를 a에 대하여 미분하면 1/a이므로 아래와 같이 간단하게 정리됨

  $$
  \frac {∂L}{∂a} = -(y \frac {1}{a} - (1-y) \frac {1}{1-a})
  $$

**a를 z에 대하여 미분하기**

- a는 시그모이드 함수이므로 a를 z에 대한 식으로 표현 가능

- 이를 이용해 a를 z에 대하여 미분하면 아래와 같은 식이 나옴
  $$
  \frac {∂a}{∂z} = a(1-a)
  $$
  

**z를 w에 대하여 미분하기**

- z는 선형 함수이므로 w_i에 대해 미분하면 다른 항은 모두 사라지고 x_i만 남아 아래와 같은 식이 됨
  $$
  \frac {∂z}{∂w_i} = x_i
  $$

**로지스틱 손실 함수를 w에 대하여 미분하기**

- 이제 연쇄법칙을 위해 필요한 계산은 모두 마침

- 각 단계에서 구한 도함수를 곱하기만 하면 됨
  $$
  (\frac {∂L}{∂w_i})L = (\frac {∂L}{∂a})(\frac {∂a}{∂z})(\frac {∂z}{∂w_i})
  = -(y-a)x_i
  $$

  - 해당 결과는 제곱 오차를 미분한 결과와 일치함을 알 수 있음

### 로지스틱 손실 함수의 미분 과정을 정리하고 역전파 이해하기

- 로지스틱 손실 함수는 a에 대하여 미분하고 a는 z에 대하여 미분하고, z는 w에 대하여 미분함
- 또한 각 도함수의 곱을 가중치를 업데이트하는데 사용함을 알 수 있음
- 이렇게 로지스틱 손실 함수에 대한 미분이 연쇄 법칙에 의해 진행되는 구조를 보고 **그레이디언트가 역전파된다**라고 함

### 로지스틱 손실 함수의 미분 과정 정리하고 역전파 이해하기

**가중치 업데이트 방법 정리하기**

- 로지스틱 회귀의 가중치를 업데이트 하려면 로지스틱 손실 함수를 가중치에 대해 미분한 식을 가중치에서 빼면 됨
  $$
  w_i = w_i - \frac {∂L}{∂w_i} = w_i + (y-a)x_i
  $$
  

**절편 업데이트 방법 정리하기**

- 연쇄법칙을 적용하면 쉽게 구할 수 있음

- 절편 업데이트 역시 로지스틱 손실 함수를 절편에 대해 미분한 식을 절편에서 빼면 됨
  $$
  b = b - \frac {∂L}{∂b} = b + (y-a)1
  $$
  



## 04-4. 분류용 데이터 세트를 준비합니다

: 분류 문제를 위해 사이킷런에 포함된 '위스콘신 유방암 데이터 세트'를 데이터 세트를 준비해보자

### 유방암 데이터 세트를 소개합니다.
: 해결할 문제는 유방암 데이터 샘플이 악성 종양인지 혹은 정상 종양인지를 구분하는 이진 분류 문제이다. 
그런데 여기서 주의해야 할 점은 유방암에서 악성이 unnormal, 양성이 normal이나, 이진 분류 문제에서는 해결해야 할 목표를 양성 샘플이라고 한다. 즉 해결과제가 악성 종양 판별이므로 양성샘플이 악성 종양인 셈이다. 이 점을 주의하자. 

[colab ch04-4 code 참고](https://colab.research.google.com/drive/1_f0usEgcf82GWCgDkSKpu3nuxODpgl87)

## 04-5. 로지스틱 회귀를 위한 뉴런을 만듭니다
:  모델을 만들기 전에 성능 평가에 대해 먼저 잠시 알아보자

### 모델의 성능 평가를 위한 훈련 세트와 테스터 세트
- 훈련된 모델의 실전 성능을 일반화 성능(generalization performance)이라고 부름
- 잘못된 모델 성능 측정
  - 만약 모델을 학습시킨 훈련 데이터 세트로 다시 모델의 성능을 평가하면 그 모델은 당연히 좋은 성능이 나올 것이다
  - 이런 성능 평가를 '과도하게 낙관적으로 일반화 성능을 추정한다'고 말함
- 올바른 모델 성능 측정
  -  훈련 데이터 세트를 두 덩이로 나누어 하나는 훈련에, 다른 하나는 테스트에 사용
  -  이 때 각각의 덩어리를 훈련 세트(train set), 테스트 세트(test set)라고 부른다.  
- 훈련 세트, 테스트 세트로 나눌 때에는 다음 2가지 규칙을 지켜야 함
  1. train set > test set
  2. 훈련 데이터 세트를 나누기 전에 양성, 음성 클래스가 훈련 세트나 테스트 세트의 어느 한쪽에 몰리지 않도록 골고루 섞어야 함

[colab ch04-5 code 참고](https://colab.research.google.com/drive/1_f0usEgcf82GWCgDkSKpu3nuxODpgl87)


## 04-6. 로지스틱 회귀 뉴런으로 단일층 신경망을 만듭니다
: 사실 우리는 이미 단일층 신경망을 구현하였다. 로지스틱 회귀는 단일층 신경망과 동일하기 때문이다. 하지만 지금까지는 층이라는 개념을 전혀 사용하지 않았다. 이제 신경망과 관련된 개념을 제대로 정리 해보자.

### 일반적인 신경망의 모습을 알아봅니다
: 일반적으로 신경망은 가장 왼쪽이 입력층, 가장 오른쪽이 출력층, 가운데 층증을 은닉층이라고 부른다. 각 층에 오른쪽에 작은 원으로 표시된 활성화 함수는 은닉층과 출력층의 한 부분으로 간주한다

- 단일층 신경망의 모습을 알아봅니다. 
: 앞에서 배운 로즈스틱 회귀는 은닉층이 없는 신경망이라고 볼 수 있다. 입력층과 출력층만 가지는 신경망을 단일층 신경망이라고 부른다. 사실 입력층은 입력 그 자체여서 프로그램을 구현할 때는 겉으로 드러나지 않는다.

### 단일층 신경망을 구현합니다
: 앞에서 구현한 클래스는 이미 단일층 신경망의 역할을 할 수 있으므로 단일층 신경망을 또 구현할 필요는 없으나 다음의 몇가지 유용한 기능을 추가하기 위해 다시 구현해보자. 

-> gogo colab!!

### 여러가지 경사 하강법에 대해 알아봅니다
: 지금까지 사용한 경사 하강법은 샘플 데이터 1개에 대한 그레디언트를 계산한 것으로 이를 확률적 경사 하강법(stochastic gradient descent)이라고 부른다.   
반면 전체 훈련 세트를 사용하여 한 번에 그레디언트를 계산하는 방식인 배치 경사 하강법(batch gradient descent)과 배치 크기를 작게 하여(훈련 세트를 여러 번 나누어)처리하는 방식인 미니 배치 경사 하강법(mini-batch gradient descent)이 있다.

- 매 에포크마다 훈련 세트의 샘플 순서를 섞어 사용하기. 
: 앞에 나온 모든 경사 하강법들은 매 에포크마다 훈련 세트의 샘플 순서를 섞어 가중치와 최적값을 계산해야 한다. 훈련 세트의 샘플 순서를 섞으면 가중치 최적값의 탐색 과정이 다양해져 가중치 최적값을 제대로 찾을 수 있기 때문이다

-> gogo colab!!

## 04-7. 사이킷런으로 로지스틱 회귀를 수행합니다
: 사이킷런의 경사 하강법이 구현된 클래스는 SGDClassifier 입니다. 이 클래스는 로지스틱 회귀 문제 외에도 여러가지 문제에 경사 하강법을 적용할 수 있습니다. 여기서는 이 클래스를 통해 로지스틱 회귀 문제를 간단히 해결해보겠습니다

-> gogo colab!!