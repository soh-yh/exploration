# AIFFEL Campus Online 4th Code Peer Review Templete
- 코더 : 소용현
- 리뷰어 : 남희정
평가문항	상세기준
1. 한국어 전처리를 통해 학습 데이터셋을 구축하였다.	공백과 특수문자 처리, 토크나이징, 병렬데이터 구축의 과정이 적절히 진행되었다.
2. 트랜스포머 모델을 구현하여 한국어 챗봇 모델 학습을 정상적으로 진행하였다.	구현한 트랜스포머 모델이 한국어 병렬 데이터 학습 시 안정적으로 수렴하였다.
3. 한국어 입력문장에 대해 한국어로 답변하는 함수를 구현하였다.	한국어 입력문장에 맥락에 맞는 한국어로 답변을 리턴하였다.

# PRT(PeerReviewTemplate)
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.
- [x] 1.코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
- 공백과 특수문자 처리, 토크나이징, 병렬데이터 구축의 과정이 적절히 진행되었습니다. 
- <code> train_data = pd.read_csv('~/aiffel/transformer_chatbot/data/ChatbotData .csv')
train_data.head(30)</code> 
- <code>def preprocess_sentence(sentence):
  sentence = sentence.lower()
  sentence = re.sub(r"([?.!,])", r" \1 ", sentence)
  sentence = re.sub(r'\s+', " ", sentence)#토큰화되서 인풋으로 들어가니 별 의미 없을듯...
  sentence = sentence.strip()
  return sentence</code>
- <code>def load_conversations():
  inputs, outputs = [], []
  for sentence in train_data['Q']:
    inputs.append(preprocess_sentence(sentence))
  for sentence in train_data['A']:
    outputs.append(preprocess_sentence(sentence))
  return inputs, outputs</code>
- 구현한 트랜스포머 모델이 한국어 병렬 데이터 학습 시 안정적으로 수렴하였습니다.
- ![image](https://github.com/soh-yh/exploration/assets/88833290/5fbbe3d0-08b6-4595-a1bf-07e3a20c76fe)
- 한국어 입력문장에 맥락에 맞는 한국어로 답변을 리턴하였습니다.
- <code>sentence_generation('배고파')
sentence_generation('졸려')
sentence_generation('안녕')
sentence_generation('내일 날씨')
sentence_generation('재밌는 얘기 해봐')
sentence_generation('입출력이 뭐야?')</code>
- ![image](https://github.com/soh-yh/exploration/assets/88833290/561d8117-1377-4106-810e-a2058b56523c)
- [ ] 2.주석을 보고 작성자의 코드가 이해되었나요?
- 네.. 주석을 보고 잘 이해가 되었습니다. 코드가 다 같은 코드라서요...
- [ ] 3.코드가 에러를 유발할 가능성이 있나요?
- [ ] 4.코드 작성자가 코드를 제대로 이해하고 작성했나요?
- 제 코드의 잘못된 부분을 발견해 주시는 수준이셨습니다.
- [ ] 5.코드가 간결한가요?
- 네
