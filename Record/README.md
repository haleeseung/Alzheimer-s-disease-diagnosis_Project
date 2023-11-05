# 알츠하이머 치매 프로젝트 기록

## 알츠하이머 치매 프로젝트 코드 기록
**프로젝트를 진행하면서 작성했던 프로젝트 코드 업로드**    
### 11/5 
* ResNet50 ([💻ResNet50](https://github.com/haleeseung/Alzheimer-s-disease-diagnosis_Project/blob/main/Record/Code/ResNet.ipynb))
  - 결과 : Epoch 10 기준, Train Acc @1: 49.75%, Valid Acc @1: 48.31%  
            Train Acc @5: 49.75%, Valid Acc @5: 48.31%
### 11/6 
**ResNet layer 층 별로 결과 구하기**

* ResNet18 ([💻ResNet18](https://github.com/haleeseung/Alzheimer*s-disease-diagnosis_Project/blob/main/Record/Code/ResNet18.ipynb))
  - 결과 : Epoch 10 기준, Train Acc @1: 0.97%, Valid Acc @1: 1.11%  
              Train Acc @5: 37.94%, Valid Acc @5: 35.94%
* ResNet34 ([💻ResNet34](https://github.com/haleeseung/Alzheimer*s-disease-diagnosis_Project/blob/main/Record/Code/ResNet34.ipynb))
  - 결과 : Epoch 10 기준, Train Acc @1: 47.95%, Valid Acc @1: 48.18%  
              Train Acc @5: 84.79%, Valid Acc @5: 84.44%
* ResNet101 ([💻ResNet101](https://github.com/haleeseung/Alzheim*r-s-disease-diagnosis_Project/blob/main/Record/Code/ResNet101.ipynb))
  - 결과 : Epoch 10 기준, Train Acc @1: 13.69%, Valid Acc @1: 14.45%  
              Train Acc @5: 15.07%, Valid Acc @5: 15.82%
* ResNet152 ([💻ResNet152](https://github.com/haleeseung/Alzheim*r-s-disease-diagnosis_Project/blob/main/Record/Code/ResNet152.ipynb))
  - 결과 : Epoch 10 기준, Train Acc @1: 2.74%, Valid Acc @1: 2.67%  
              Train Acc @5: 23.89%, Valid Acc @5: 25.26%

다음과 같은 결과로 인하여, 평가지표가 잘 나온 ResNet34를 바탕으로 활용할 예정.  

<모델 성능 향상을 위한 다른 방안>
1. Epoch 수 증가. (Epoch=10에서 10씩 늘려, Epoch=100까지 비교하기)
2. Epoch 수를 증가시켰을 때, 시간을 많이 소요할 시 He 초기화를 통해 Epoch수를 줄이되, 일정한 Accuracy 추출.
3. 드롭아웃 혹은 조기종료 방법 이용.

### 11/7


## 알츠하이머 치매 프로젝트를 진행하기 위한 논문 리뷰
알츠하이머 치매 프로젝트를 진행하기 위하여 공부했던 내용들이나, 논문을 읽었던 기록등을 업로드
