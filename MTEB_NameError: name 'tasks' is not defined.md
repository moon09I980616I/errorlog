### NameError: name 'tasks' is not defined

MTEB dataset을 이용해서 bert를 이용해서 학습한 classification모델을 검증하려고 하는데 금요일까지 됐던 부분에서 갑자기 오류가 났다. 디버깅도 타보고 깃허브 코드 가이드 문서도 계속 살펴봤는데 해결을 못했다. 이유는 코드가 변경되고 깃허브는 업데이트가 안돼서 오류가 난거다. 그래서 깃허브 코드로 다운받아서 진행했다.
```jsx
from mteb import MTEB
from sentence_transformers import SentenceTransformer

# Define the sentence-transformers model name
model_name = "average_word_embeddings_komninos"

model = SentenceTransformer(model_name)
evaluation = MTEB(tasks=["Banking77Classification"])
results = evaluation.run(model, output_folder=f"results/{model_name}")
```
참고

https://paperswithcode.com/paper/mteb-massive-text-embedding-benchmark#code

https://github.com/embeddings-benchmark/mteb
