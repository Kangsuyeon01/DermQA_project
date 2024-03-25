# DermQA: 

Confence Paper : https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE11652092

### Python 파일 실행 방법

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

