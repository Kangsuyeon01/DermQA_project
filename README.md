# [DermQA: 피부 병변 조기 진단을 위한 이미지 분류와 ChatGPT 기반 웹 시스템](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE11652092)




- `개발 기간`: 2023.03 ~ 2023.11 (7개월)
- `참여 인원` : 3
- `사용 언어` : `Python`, `Java`, `JavaScript`, `MySQL`
- `배포 환경` : `Ubuntu 18.04.6`


![image](https://github.com/Kangsuyeon01/DermQA_project/assets/94098065/1ac5b6da-bff1-4b0d-9862-c174d9618330)



## Deep Learning Model

### Dataset
- 피부 병변 이미지 데이터셋: HAM10000
- 7개 피부 병변 유형과 나이, 성별, 병변 위치에 대한 데이터로 구성
- 광선각화증(actinic keratosis), 기저세포암(basal cell carcinoma), 지루각화증(benign keratosis), 섬유종(dermatofibroma), 흑색종(melanoma), 반점(nevus), 혈관종(vascular lesion)
  ![image](https://github.com/Kangsuyeon01/DermQA_project/assets/94098065/1dedb502-d795-42a4-a562-920edeaf26cd)

---
### Model
#### 피부 병변 분류를 위한 딥러닝 모델
  - 합성곱 신경망(Convolutional Neural Network)으로 구성된 모델로 성능 평가
  - 빠른 학습을 위해 ImageNet 데이터셋으로 사전학습 된 모델의 가중치를 활용한 전이학습(Transfer Learning) 활용
    - 성능 비교를 위해 ResNet-D, EfficientNet, DenseNet, Xception 네 가지 네트워크를 학습
<img src="https://github.com/Kangsuyeon01/DermQA_project/assets/94098065/f3e19ffb-7067-461d-aa6d-8945ae486dc8" width ="80%">

#### 피부 병변 조기 진단 정보 제공 시스템
1. 웹에서 사용자가 피부 병변 이미지와 질문 업로드
2. 데이터베이스에 데이터 저장 후, 고유 ID를 소켓통신(Python, JAVA)을 통해 서버로 전송
3. 서버에서 해당 ID의 이미지에 대한 피부 병변 분류
4. 분류 결과와 질문을 통해 프롬프트를 구성하여 ChatGPT API에 입력
5. 생성한 답변을 데이터베이스에 저장하여 웹을 통해 사용자에게 제공
<img src="https://github.com/Kangsuyeon01/DermQA_project/assets/94098065/02b9d608-88af-43a1-b17c-91fe09db56fb" width ="50%">


---
### 실험 환경 및 매개 변수

- 환경
  
| CPU          | GPU            | RAM  | OS        |
|--------------|----------------|------|-----------|
| Intel i9-10900X | RTX 3090 24GB | 256GB | Ubuntu 18.04.6 |

- 매개 변수 (Parameter)

| 매개변수 (parameter) | 값 (Value)  |
|-------------------|-----------|
| Batch Size        | 8         |
| Optimizer         | AdamW     |
| Learning Rate     | 0.0001    |
| Epoch             | 50        |


### Score

![image](https://github.com/Kangsuyeon01/DermQA_project/assets/94098065/d112c77c-6a93-425c-9379-c4332a3d837c)

| Model           | Accuracy | Precision | Recall | F1-score |
|-----------------|----------|-----------|--------|----------|
| Resnet-50D      | 0.9027   | 0.8049    | 0.8043 | 0.7962   |
| Efficientnet B5 | 0.9045   | 0.8141    | 0.8147 | 0.8052   |
| Densenet201     | 0.8953   | 0.7979    | 0.7941 | 0.7856   |
| Xception        | 0.9031   | 0.7967    | 0.7945 | 0.7873   |

성능이 가장 우수한 모델
  → `Efficientnet B5` 을 백본 네트워크로 선정

---

## Web Interface
![image](https://github.com/Kangsuyeon01/DermQA_project/assets/94098065/cbba124f-3c9b-4288-8354-e5191ac7814d)

---
## How to run Python File

#### Train
```
git clone https://github.com/Kangsuyeon01/DermQA.git
CD DermQA/DL
python train.py
```
학습이 완료된 모델은 'models/saved_model' 에 저장됩니다.
#### Inference (test dataset)
```
python pipeline.py
```
#### Run Web application (Socket communication between Java Spring and Python)
```
python server.py --model_saved_path=[trained model path] --OPENAI_API_KEY=[OPENAI_API_KEY]
```
* java Spring Project 실행의 경우 `DermQA_project/java/project/src/main/resources
/application.properties`에서 MySQL 데이터 베이스 연결 후 사용
--- 

