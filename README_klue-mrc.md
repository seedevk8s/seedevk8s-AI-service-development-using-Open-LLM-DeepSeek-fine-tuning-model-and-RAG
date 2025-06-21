
# 📘 KLUE-MRC Negative Sample Generator

이 노트북은 KLUE-MRC v1.1 데이터셋을 활용하여 context-question 기반의 학습 데이터 전처리 및 negative sample 생성을 위한 파이프라인입니다.

## 📌 주요 구성

### 1. 패키지 설치
```python
%pip install pandas tqdm FlagEmbedding scikit-learn
```

### 2. 데이터 로딩
- `klue-mrc-v1.1_train.json` 파일을 로드합니다.
- 구조는 다음과 같습니다:
  - `data` > `paragraphs` > `qas` > `question`

### 3. context-question 추출
```python
for article in data['data']:
    for para in article['paragraphs']:
        context = para['context']
        for qa in para['qas']:
            question = qa['question']
            contexts.append(context)
            questions.append(question)
```

### 4. DataFrame 생성 및 정제
```python
df = pd.DataFrame({'context': contexts, 'question': questions})
df = df.drop_duplicates(subset='context')
df = df.drop_duplicates(subset='question')
```
