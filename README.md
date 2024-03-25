# DermQA: 피부 병변 조기 진단을 위한 이미지 분류와 ChatGPT 기반 웹 시스템
![image](https://github.com/Kangsuyeon01/DermQA_project/assets/94098065/1ac5b6da-bff1-4b0d-9862-c174d9618330)

Confence Paper : https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE11652092


## Abstract

## Deep Learning Model

### Dataset
- 피부 병변 이미지 데이터셋: HAM10000
- 7개 피부 병변 유형과 나이, 성별, 병변 위치에 대한 데이터로 구성
- 광선각화증(actinic keratosis), 기저세포암(basal cell carcinoma), 지루각화증(benign keratosis), 섬유종(dermatofibroma), 흑색종(melanoma), 반점(nevus), 혈관종(vascular lesion)
  ![image](https://github.com/Kangsuyeon01/DermQA_project/assets/94098065/1dedb502-d795-42a4-a562-920edeaf26cd)


### Model
![image](https://github.com/Kangsuyeon01/DermQA_project/assets/94098065/02eddf0a-27e8-48a7-865c-b6317a8fd0d1)

![image](https://github.com/Kangsuyeon01/DermQA_project/assets/94098065/7b36a897-6926-448e-929d-8a7a03556fd4)

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



## Web Interface
![image](https://github.com/Kangsuyeon01/DermQA_project/assets/94098065/cbba124f-3c9b-4288-8354-e5191ac7814d)

---
## Python 파일 실행 방법

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
#### Run Web application (Socket communication between Java Spring to Python)
```
python server.py --model_saved_path=[traind model path] --OPENAI_API_KEY=[OPENAI_API_KEY]
nohup java -jar DermQA.jar &
```

--- 

