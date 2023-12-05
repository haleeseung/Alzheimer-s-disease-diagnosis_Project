# 알츠하이머 치매 프로젝트 기록

## 알츠하이머 치매 프로젝트 코드 기록
**프로젝트를 진행하면서 작성했던 프로젝트 코드 업로드**    
### 11/5 
* ResNet50 ([💻ResNet50](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/ResNet.ipynb))
  - 결과 : Epoch 10 기준, Train Acc @1: 49.75%, Valid Acc @1: 48.31%  
            Train Acc @5: 49.75%, Valid Acc @5: 48.31%
### 11/6 
**ResNet layer 층 별로 결과 구하기**

* ResNet18 ([💻ResNet18](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/11.5/ResNet18.ipynb))
  - 결과 : Epoch 10 기준, Train Acc @1: 0.97%, Valid Acc @1: 1.11%  
              Train Acc @5: 37.94%, Valid Acc @5: 35.94%
* ResNet34 ([💻ResNet34](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/11.5/ResNet34.ipynb))
  - 결과 : Epoch 10 기준, Train Acc @1: 47.95%, Valid Acc @1: 48.18%  
              Train Acc @5: 84.79%, Valid Acc @5: 84.44%
* ResNet101 ([💻ResNet101](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/11.5/ResNet101.ipynb))
  - 결과 : Epoch 10 기준, Train Acc @1: 13.69%, Valid Acc @1: 14.45%  
              Train Acc @5: 15.07%, Valid Acc @5: 15.82%
* ResNet152 ([💻ResNet152](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/11.5/ResNet152.ipynb))
  - 결과 : Epoch 10 기준, Train Acc @1: 2.74%, Valid Acc @1: 2.67%  
              Train Acc @5: 23.89%, Valid Acc @5: 25.26%

다음과 같은 결과로 인하여, 평가지표가 잘 나온 ResNet34를 바탕으로 활용할 예정.  

<모델 성능 향상을 위한 다른 방안>
1. Epoch 수 증가. (Epoch=10에서 10씩 늘려, Epoch=100까지 비교하기)
2. Epoch 수를 증가시켰을 때, 시간을 많이 소요할 시 He 초기화를 통해 Epoch수를 줄이되, 일정한 Accuracy 추출.
3. 드롭아웃 혹은 조기종료 방법 이용.

### 11/9
Colab Pro 구매후, V100 GPU 이용. (컴퓨팅 단위 : 100개)

**ResNet34를 Epoch수 100까지 증가시킨 후에 확인**

* ResNet34 - Epoch : 100 ([💻ResNet34-Epoch100](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/11.9/ResNet34_Epoch100.ipynb))
  - 결과 : Epoch 100 기준, Train Acc @1: 52.57%, Valid Acc @1: 55.14%   
              Train Acc @5: 86.31%, Valid Acc @5: 85.35%

He초기화 방법을 적용했을 때 따로 첨부하지는 않았지만, 성능이 낮아지는 현상을 발견하였기에 적용하지 않기로 하였습니다.

그리고 계속 프로그램을 돌렸을 때, ResNet의 깊이를 깊게 한 결과를 적용하였을 때 학습률을 따로 바꿔주지 않아 학습을 하는데 바뀌는 속도가 늦었을 것이라 판단하였습니다.
그 결과 ResNet152를 사용한 뒤에 learning rate를 0.001로 수정 후 확인하였습니다.

**ResNet152 Learning rate : 0.001로 적용**

* ResNet152 - Learning Rate : 0.001 ([💻ResNet152 - learning rate : 0.001](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/11.9/ResNet152.ipynb))
  - 결과 : Epoch 10 기준, Train Acc @1: 55.25%, Valid Acc @1: 57.23%   
              Train Acc @5: 57.23%, Valid Acc @5: 86.39%

결과를 확인해본 결과, Train Accuracy보다 Validation Accuracy가 더 높게 나왔기에, 과대적합이 발생했다고 판정하였지만 가장 커다란 문제인 정확도를 더 높이고 과대적합을 제어하는 것이 더 나은 선택지라고 생각하였습니다.

### 11/14
**EfficientNet 모델 이용**

* EfficientNet - Epoch : 10, Learning Rate : 0.001 ([💻EfficientNet](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/11.14/EfficientNet.ipynb))
  - 결과 : Epoch 10 기준, Train Acc @1: 100.00%, Valid Acc @1: 100.00%   
              Train Acc @5: 100.00%, Valid Acc @5: 100.00%

<img width="597" alt="스크린샷 2023-11-14 오후 11 10 38" src="https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/assets/127108173/1977191a-a01f-49e4-b2a4-b72b701d8e5f">

위의 사진을 통해 확인할 수 있듯이 과적합 문제부터 정확도가 초반부터 Training과 Validation 모두 100%가 나오는 문제가 발생하였습니다. 그래서 Scikit-learn 라이브러리를 이용하여 다른 평가지표(Valid Loss, Precision, Recall, F1 - Score)를 확인해보았습니다. 결과는 사진을 첨부하였습니다.

<img width="1053" alt="스크린샷 2023-11-14 오후 11 12 53" src="https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/assets/127108173/3e3bc2a7-0135-4390-975e-0474350cc65e">

  - Precision(정밀도) : 모델이 True라고 분류한 것 중에서 실제 True인 것의 비율입니다. 즉, Non-Demented가 True에 해당한다고 했을 때, 실제로 Non-Demented 인 비율을 의미한다고 보면 될 것 같습니다. 결과값인 0.750인 75 % 확률이기에, 4명의 알츠하이머 환자 중 3명의 환자만 정확하게 분류를 할 수 있다는 뜻이기에, 성능을 더 올릴 필요가 있다고 볼 수 있습니다.

    
  - Recall(재현율) : 실제 True인 것 중에서 모델이 True라고 예측한 것의 비율입니다. 실제로 Non-Demented가 True일 때, Non-Demented라고 예측한 비율로 생각하면 될 것입니다. 결과값이 0.489로 좋지 않은 성능을 보여준다고 볼 수 있습니다.  

  - F1 Score :

Colab Pro를 구매했을 때, 제공되었던 컴퓨팅 단위 100개를 다 사용하다보니 V100 GPU -> TPU로 런타임 유형이 변경되었습니다. 그 결과, Efficient Net의 Validation Accuracy이 fluctuate 하는 현상이 생겼습니다.

<img width="697" alt="스크린샷 2023-11-26 오전 1 29 49" src="https://github.com/haleeseung/Python-Learning-Alone/assets/127108173/59b815e5-d64e-42f0-989a-9d18f2246d3d">

<img width="624" alt="스크린샷 2023-11-26 오전 1 29 57" src="https://github.com/haleeseung/Python-Learning-Alone/assets/127108173/adfdd974-f847-41c3-b00f-19e77c4cb6ca">

어느 부분이 잘못되었는지 파악하지 못하여, 인터넷 및 자료를 찾아보다 하이퍼 파라미터를 튜닝시키면 문제를 해결할 수 있다는 실마리를 발견하였습니다.  
하지만, 저의 목표는 EfficientNet 모델과 ResNet 모델을 앙상블 기법을 적용하여 사용할 예정이여서, 두 모델부터 앙상블 하였습니다.

### 11/26
**EfficientNet & ResNet 앙상블 모델 이용**

* EfficientNet & ResNet Ensemble Model - Epoch : 3, Learning Rate : 1e-7 ([💻EfficientNet & ResNet Ensemble](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/11.26/EfficientNet_%2B_ResNet.ipynb))
  - 결과 : Epoch 3 기준, Train Acc @1:   2.54%, Valid Acc @1:   0.00%   
              Train Acc @5:   5.74%, Valid Acc @5:   0.00%

Epoch가 3까지 이동하였을 때, 모델이 더 이상 학습하지 못하는 것을 발견하였고, 어느 부분이 문제인지 확인하였을 때, 너무 낮은 학습률을 사용한 것이 잘 못 되었다고 생각이 들었습니다. 그래서 Learning Rate를 1e-3으로 바꾸고, 기존 코드를 확인하면 EnsembleModel 클래스의 final_output에서는 Softmax 활성화 함수가 적용되어 있지 않았었습니다. 그래서 CrossEntropyLoss와 함께 사용될 때는 출력 레이어에 Softmax 활성화 함수를 추가하여 보완하였습니다.

### 11/27
**EfficientNet & ResNet Learning Rate를 수정한 앙상블 모델 이용**

* EfficientNet & ResNet Ensemble Model - Epoch : 10, Learning Rate : 1e-4 ([💻EfficientNet & ResNet Ensemble__1](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/11.27/EfficientNet_%2B_ResNet__1.ipynb))

결과를 확인해보니, 다음과 같습니다.

<img width="698" alt="스크린샷 2023-11-27 오전 12 19 13" src="https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/assets/127108173/17056663-d8f1-4978-a7b5-17c2c5ae1f4b">

<img width="622" alt="스크린샷 2023-11-27 오전 12 19 21" src="https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/assets/127108173/e6ab28c0-4a0c-453b-8bdf-3a74dafcc865">

TrainingSet 데이터의 학습 정확도는 100.00%에 모두 수렴하고 있지만, ValidationSet 데이터의 Accuracy는 Epoch 3 부분에서 급격하게 떨어졌다가, 다시 올라갔다가 하는 fluctuate 현상이 다시 발생하였습니다. 이러한 현상이 발생한 요인을 몇가지 생각해보았는데, 첫 번째는 과적합(Overfitting)이 발생했을 수 있다고 생각이 들었습니다. 두 번째로는 처음부터 클래스간의 데이터가 불균형하여, 데이터가 많은 Non-Demented에 대한 이미지 데이터는 2560개인 반면에, Moderate Demented는 52개 데이터로 클래스간의 상당한 차이가 있어, Accuracy로는 확인이 어려울 것이라 생각이 들었습니다. 세 번째는, 하이퍼 파라미터 튜닝을 하지 않아 성능이 오르지 않은 것이라 생각이 들었습니다. 이 중에서 저는 두 번째 부분을 먼저 확인해보기로 하였습니다. Accuracy로 성능을 평가하기 보다, ROC AUG를 이용하여 4개의 클래스를 한 클래스를 잡고 나머지랑 비교하는 형식의 이진분류에서 모델의 성능을 잘 평가할 수 있기에, ROC AUG를 성능지표로 사용하였습니다. ROC AUC는 모델이 다른 클래스를 얼마나 잘 구별할 수 있는지를 나타내는 점수를 제공합니다. 높은 점수는 모델이 클래스 간의 차이를 잘 인식한다는 것을 나타내며, 낮은 점수는 모델이 클래스를 잘 구별하지 못한다는 것을 나타냅니다.

### 11/30
**EfficientNet & ResNet50 앙상블 모델 이용하여 ROC AUC score 확인**

* EfficientNet & ResNet Ensemble Model - Epoch : 10, Learning Rate : 1e-4 ([💻EfficientNet_+_ResNet_ROC_AUC](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/11.30/EfficientNet_%2B_ResNet_ROC_AUC.ipynb))

결과를 확인해보니, 다음과 같습니다.

<img width="938" alt="스크린샷 2023-11-30 오후 2 56 51" src="https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/assets/127108173/4ca68706-d1ca-4732-a96e-d13f8e4d929a">

<img width="634" alt="스크린샷 2023-11-30 오후 2 56 40" src="https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/assets/127108173/8bad6306-09dd-4c98-8275-2d53de069f34">

TrainingSet의 성능이 Train Top-1 Acc과 Train Top-5 Acc 기준으로 Epoch가 진행될수록 점차 학습하여 Accuracy가 상승하는 것을 확인할 수 있었습니다. 하지만 Valid Top-1 Acc와 Valid Top-5 Acc을 확인하였을 때는, 꾸준히 상승하기 보다 중간에 큰 폭으로 값이 변화하는 것을 확인할 수 있었습니다. 그리고 현재 사용하고 있는 데이터셋은 클래스가 불균형하여 ROC AUC Curve를 사용하기로 하여, 추가하여 확인했습니다. Train ROC AUC 점수는 학습되는 것처럼 향상하고 있고, Valid ROC AUC는 Valid Top-Acc와 유사한 방향으로 값이 오르락 내리락하는 것을 확인할 수 있었습니다. 성능을 향상하기 위해 하이퍼파라미터 튜닝을 진행할 예정입니다.  

하이퍼 파라미터 튜닝 방법으로는 
1. **Grid Search CV** : 사용자가 직접 모델의 하이퍼 파라미터의 값을 리스트로 입력하여 값에 대한 경우의 수마다 예측 성능을 측정 평가하여 비교하면서 최적의 하이퍼 파라미터 값을 찾는 과정을 진행합니다. 

- 간단하고 광범위하게 사용되는 hyperparameter 탐색 알고리즘
- 해당 범위 및 Step의 모든 경우의 수를 탐색
- 범위를 넓게 가져갈수록, Step을 작게 설정할 수록 최적해를 찾을 가능성이 높이지지만 시간이 오래 걸림
- 일반적으로 넓은 범위와 큰 Step으로 설정한 후 범위를 좁혀 나가는 방식을 사용하여 시간을 단축

2. **Random Grid Search CV** : Grid Search CV 방법과 유사하지만, 하이퍼 파라미터 값의 리스트 범위 내에서 무작위적으로 선택하여 최적의 하이퍼 파라미터 값을 찾는 과정을 진행합니다.

- 정해진 범위 내에서 Random하게 선택.
- 기본적으로는 더 빠르고 효율적이기 때문에 GridSearch보다 권장되는 방법.
- Grid Serach보다 속도가 빠르지만 optimzed solution이 아닐 수 있음.
- Sample의 수가 많다면 Random Sampling을 통해 최적해를 찾을 가능성이 높아짐.

3. **베이시안 최적화** : 목적 함수의 식을 제대로 알 수 없는 함수에서, 최대 또는 최소의 함수 반환 값을 만드는 최적 입력값을 가능한 적은 시도를 통해 빠르고 효과적으로 찾아주는 방식입니다. 

- Prior Distribution에 기반하여 하나의 탐색 함수 가정
- Exploartion : 매번 새로운 Sampling을 사용해 목적함수를 Test할 시, 해당 정보를 사용하여 새로운 목적함수의 Prior Distribution을 update
- Exploitation : Posterior distribution에 의해 얻은 global minimum이 나타날 가능성이 높은 위치에서 알고리즘을 테스트합니다.

  <주의점>
- 최적해일 가능성이 높은 지점에서 sampling이 계속 일어날 수 있음(exploitation) -> 이 지점이 local minimum이면 거기서 계속 머무르게 되는 것.
- 이 때문에 exploration 및 exploitation 사이에 balance point를 찾게 됨

4. **유전 알고리즘** : 유전 알고리즘은 진화 이론에서 영감을 받은 최적화 알고리즘입니다. 유전 알고리즘은 유전자로 표현된 후보 해들을 선택, 교차, 돌연변이 등의 연산을 통해 최적의 해를 찾는데 사용됩니다. 

저는 다음 하이퍼 파라미터 튜닝 방법 중에 베이시안 최적화 방법과 유전 알고리즘 방법을 둘 중 하나를 이용하여 확인해 볼 예정입니다.

### 12/06
모델의 성능을 향상 시키기 위해 많이 고민도 해보고 찾아본 결과, 하이퍼 파라미터 튜닝은 결국 모델의 적용도 어느정도 되서 성능이 어느정도 나온다는 가정하에 쓰는 것이라 생각이 들었습니다. 그래서 결국 원초적인 문제인, 모델의 성능을 가장 확실하게 향상 시킬 수 있는 방법을 데이터 전처리 단계에서부터 찾아보자고 생각했습니다. 일단 제가 프로젝트를 진행하고 있는 것은 뇌 MRI 이미지 데이터를 이용하여 알츠하이머 치매의 중증 정도를 각 단계에 맞춰 분류를 하는 작업입니다. 그때 문득 든 생각은 뇌 MRI 데이터를 마음대로 수정하여 데이터를 증강시켜도 상관이 없었을까에 대한 물음이 생겼습니다. 이미지 크기를 재설정하는 것과 정규화 단계만 남겨두고 모델을 돌려보기로 마음을 먹었습니다.

**4가지 모델 (기본 데이터 전처리)**
Epoch : 30  
Optimizer = AdamW  
learning_rate = 기본 0.001에서 Epoch 10일때, 0.1배를 줄여줌.  

* ResNet50 ([💻ResNet50](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/12.06/ResNet50.ipynb))

<결과>  
Accuracy  
<img width="684" alt="스크린샷 2023-12-06 오전 1 25 15" src="https://github.com/haleeseung/Python-Learning-Alone/assets/127108173/ea882062-115b-44c8-9b7f-c64402b0f86a">  
Loss  
<img width="674" alt="스크린샷 2023-12-06 오전 1 25 22" src="https://github.com/haleeseung/Python-Learning-Alone/assets/127108173/5c5f4204-b65d-454b-b7f9-d2501f5d41c0">  

* ResNet101 ([💻ResNet101](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/12.06/ResNet101.ipynb))

<결과>  
Accuracy  
<img width="678" alt="스크린샷 2023-12-06 오전 1 33 23" src="https://github.com/haleeseung/Python-Learning-Alone/assets/127108173/5e42f7c5-c933-4419-b442-0258a7eb0846">  
Loss  
<img width="677" alt="스크린샷 2023-12-06 오전 1 33 29" src="https://github.com/haleeseung/Python-Learning-Alone/assets/127108173/0e127377-9148-4efe-8d37-462cec37fc78">  

* EfficientNet ([💻EfficientNet](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/12.06/EfficientNet%20(1).ipynb))

<결과>  
Accuracy  
<img width="671" alt="스크린샷 2023-12-06 오전 1 40 14" src="https://github.com/haleeseung/Python-Learning-Alone/assets/127108173/4799efbc-60cb-4a43-a731-053b0f3f41ae">  
Loss  
<img width="679" alt="스크린샷 2023-12-06 오전 1 40 08" src="https://github.com/haleeseung/Python-Learning-Alone/assets/127108173/616c655a-b21e-4b5f-913c-e6742ab40500">  

확실히 이전에 했던 것에 비하면 성능이 향상된 것을 확인할 수 있습니다. ResNet50을 이용하였을 때, 가장 성능이 높게 나왔고, 하이퍼 파라미터 튜닝 작업만 진행시켜 최적의



## 알츠하이머 치매 프로젝트를 진행하기 위한 논문 리뷰
알츠하이머 치매 프로젝트를 진행하기 위하여 공부했던 내용들이나, 논문을 읽었던 기록등을 업로드
