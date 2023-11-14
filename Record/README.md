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


## 알츠하이머 치매 프로젝트를 진행하기 위한 논문 리뷰
알츠하이머 치매 프로젝트를 진행하기 위하여 공부했던 내용들이나, 논문을 읽었던 기록등을 업로드
