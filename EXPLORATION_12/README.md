# AIFFEL Campus Online 4th Code Peer Review Templete
- 코더 : 소용현
- 리뷰어 : 이효준


# PRT(PeerReviewTemplate)
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.
- [x] 1.코드가 정상적으로 동작하고 주어진 문제를 해결했나요?

- [x] 2.주석을 보고 작성자의 코드가 이해되었나요?
  > 데이터 전처리가 오랜 시간이 소요되는 만큼 object파일을 ``pkl``로 저장하고 불러오는 코드가 매우 흥미로웠습니다. 
```python
def load_processedData() :
    file = 'data.pkl'     # 예제 Textfile
    if os.path.isfile(file):
        dt = pd.read_pickle(file)
    else :
        dt = preprocess()
        dt.to_pickle(file)
    return dt
    
def preprocess() :
    dt = data
    clean_text = []
    for index, row in data.iterrows():
        clean_text.append(preprocess_sentence(row['text']))
    print("Text 전처리 후 결과: ", clean_text[:5])
    
    clean_summary = []
    for index, row in dt.iterrows():
        clean_summary.append(preprocess_sentence(row['headlines'],False))
    print("headlines 전처리 후 결과: ", clean_summary[:5])
    dt['text'] = clean_text
    dt['headlines'] = clean_summary
    # 빈 값을 Null 값으로 변환
    dt.replace('', np.nan, inplace=True)
    dt.dropna(axis=0, inplace=True)
    return dt
```
- [ ] 3.코드가 에러를 유발할 가능성이 있나요?
  > 없습니다.

- [x] 4.코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 추출적 요약을 위한 함수 정의가 필요합니다.
``` python
#텍스트를 입력하면 요약해서 요약텍스트를 리턴해주는 함수
def textSummaryAbs(text) :
    text_preprocess = preprocess_sentence(text)
    text_preprocess = src_tokenizer.texts_to_sequences([text])
    text_preprocess = pad_sequences(text_preprocess, maxlen=text_max_len, padding='post')
    summa = decode_sequence(text_preprocess)
    return summa
```

- [x] 5.코드가 간결한가요?
  > 모델의 임무 수행을 위해 필요한 내용만 간결하게 코드화 되어 있었습니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
# 사칙 연산 계산기
class calculator:
    # 예) init의 역할과 각 매서드의 의미를 서술
    def __init__(self, first, second):
        self.first = first
        self.second = second
    
    # 예) 덧셈과 연산 작동 방식에 대한 서술
    def add(self):
        result = self.first + self.second
        return result

a = float(input('첫번째 값을 입력하세요.')) 
b = float(input('두번째 값을 입력하세요.')) 
c = calculator(a, b)
print('덧셈', c.add()) 
```

# 참고 링크 및 코드 개선
```python
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```
