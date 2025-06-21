
# 📘 KLUE-MRC Prompt 기반 응답 생성

이 노트북은 KLUE-MRC에서 추출한 질문-문맥 데이터셋에 대해 LLM 기반 응답 생성을 위한 프롬프트 기반 처리 과정을 포함합니다.

## 📌 주요 구성

### 1. 라이브러리 및 API 설정
```python
import random
import ast
import pandas as pd
from openai import OpenAI
from google.colab import userdata
import os
import re
from tqdm import tqdm

os.environ['OPENAI_API_KEY'] = userdata.get('OPENAI_API_KEY')
```
- Google Colab 환경에서 OpenAI API 키를 `userdata`를 통해 설정합니다.

### 2. 데이터 로딩 및 샘플링
```python
df = pd.read_csv('klue_mrc_context_question_negative_samples.csv')
df_0_499 = df.iloc[:500].copy()
```
- KLUE-MRC 기반 문맥/질문 페어가 포함된 CSV 파일을 로드하고, 상위 500개 샘플만 선택합니다.
