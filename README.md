# ML study
기존의 머신러닝은 결과가 왜 잘 나오는지 그 과정을 수학적으로 분석할 수 있었다.  
하지만 딥러닝 에서는 결과는 잘 나오지만 왜 그런지 해석할 수 없는 부분이 있다.

https://youtu.be/6W6PVWByhc0

이 영상을 바탕으로 딥러닝에 관한 insight 및 intuition을 한번 정리해 보려고 한다.

---

# 우리가 딥러닝에 대해 알고있는 부분

## 1. 딥러닝 네트워크가 커질수록 성능이 잘 나온다.
일반적으로 큰 규모의 (layer와 node가 많은) 네트워크가 잘 작동한다.  
최근 NLP에서 핫한 GPT-3의 경우 12-billion 개의 파라미터를 사용했다.
인간의 뇌에는 10^11개의 뉴런이 있고 
뉴런과 파라미터는 다르지만 (뉴런 개수 < 파라미터 개수) 잘 작동하는 네트워크 = 큰 규모의 네트워크 라는것이 일반적으로 적용된다.

## 2. 간단한 optimization으로도 global optima에 도달한다.
딥러닝에서 일반적으로 사용되는 SGD(Stochastic Gradient Descent)는 미분을 한번하는 간단한 알고리즘이지만,
대부분의 딥러닝 네트워크에서 사용되며 좋은 결과를 가져온다.

## 3. Representation은 DNN 안에서 알아서 학습된다.
각각의 layer에서 어떤 feature를 처리할지 일일히 설정해줄 필요가없다.
Network 안에서 일반적인 feature들을 알아서 학습한다.

## 4. 네트워크 architecture를 잘 구성하면 좋은 결과를 얻을 수 있다.
전처리로 augmentation을 한다거나 GAN처럼 네트워크의 구조를 잘 구성함으로써 좋은 결과를 얻을 수 있다.

## 5. 창의적인 시도들이 큰 발전을 이뤄냈다.
딥러닝 분야에서 복잡하지 않더라도 새로운 시도들이 쌓여 큰 발전을 이뤄냈다.

---

# 우리가 딥러닝에서 잘 이해하지 못하는 부분

## 1. Generalization
Bias-Variance Tradeoff 처럼 기존의 ML에서는  
| Train set 에러 - Test set 에러 | 가 train set이 클수록 작아지고 Degree of Freedom 이 클수록 커진다는 수식이 증명되어있다.  
하지만 DNN에서는 Degree of Freedom이 매우 큼에도 불구하고 train data set이 수만장정도만 되어도 학습이 잘되는 경우를 찾아볼 수 있다.(ex. MNIST 50,000장만 사용)
네트워크가 커질수록 성능이 좋은 현상이 발생하지만, 아직 증명할 순 없다.

## 2. Simple optimization work
딥러닝은 millions dimensions 으로 이뤄졌는데 복잡할수록 convex한 function이 아니라는게 일반적이다.  
하지만, 대부분의 경우 SGD를 응용하여 optimization을 진행한다.  
parameter의 초기값을 랜덤하게 주므로 매번 다른 optima 로 학습되는데, 대부분 비슷하게 잘 된다.
실험적으로 아래와 같은 insight 들이 있다.
- Small Learning rate를 사용해야 한다.
- 작은 값으로 random initialization 해야한다.
- Tuning된 SGD를 사용한다.  

위 사항정도만 지켜도 충분히 잘 학습하는걸 볼 수 있다.
관련된 논문들을 살펴보면 아래의 두가지 intuition을 얻을 수 있다.
- Global optima 끼리는 parameter space에서 continuous하게 연결되어 있다.
- All local optima = global optima  

## 3. Representation
ML에서는 일반적으로 data를 어떻게 mapping해서 표현하는지(representation)에 따라 사용하는 알고리즘과 성능이 달라진다.
- 예를들면, 각도를 표현할 때, 0과 2pi는 같은 값이지만 너무 다르게 표시된다.  
sin(x)나 cos(x)등을 사용하면 0과 2pi가 같게 표시되고 0과 1.99pi가 유사한 값이라는걸 알 수 있다.

딥러닝에서는 사람이 열심히 생각해서 representation을 정할 필요가 없다.
Network 안에서 어떻게 잘 학습되기 때문이다.
관련 opinion은 다음과 같은것들이 있다.
- 특정 node들이 특정한 특징에 민감하게 반응한다.
- Representation을 사람이 설계하는것 자체가 잘못된 것.  
AI가 스스로 학습하게 해야하며 인간이 이해할수 있는 representation을 사용하지 않음.

# 결론
딥러닝에서 우리가 증명 또는 해석하지 못하는 부분이 있다.  
이 문제들을 교과서처럼 명징하게 설명하는것은 아직 불가능하다.
관련된 insight, intuition을 조금씩 확장시켜나가고 있다.