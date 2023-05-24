# AIFFEL Campus Online 4th Code Peer Review Templete
- 코더 : 소용현
- 리뷰어 : 이효준


# PRT(PeerReviewTemplate)
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.
- [x] 1.코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
- [x] 2.주석을 보고 작성자의 코드가 이해되었나요?
  > 모델의 훈련 내용을 정의하는 부분이 이해하기 쉽도록 잘 나와있어 이해에 많은 도움이 되었다.
```python
#중복코드 제거용
def modelFitTemp(model,X_train,y_train,epochs=20) :
    # validation set 20000건 분리
    x_val = X_train[:len(X_train)//7]   
    y_val = y_train[:len(X_train)//7]

    # validation set을 제외한 나머지 
    partial_x_train = X_train[len(X_train)//7:]  
    partial_y_train = y_train[len(X_train)//7:]
    model.compile(optimizer='adam',
                  loss='binary_crossentropy',
                  metrics=['accuracy'])

    epochs=epochs  # 몇 epoch를 훈련하면 좋을지 결과를 보면서 바꾸어 봅시다. 

    history = model.fit(partial_x_train,
                        partial_y_train,
                        epochs=epochs,
                        batch_size=512,
                        validation_data=(x_val, y_val),
                        verbose=1)
    return history

```
- [ ] 3.코드가 에러를 유발할 가능성이 있나요?
  > 에러를 유발할 내용이 없었다.

- [x] 4.코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 중간중간 동작 점검을 하는 코드가 들어있어 제대로 이해한 것으로 보인다.
```python
word_vectors.wv.most_similar(positive='영화', topn=10)
#간단한 단어는 잘 학습이 되어 있는것 같다.
word_vectors.wv.most_similar(positive='가', topn=10)
```
```python
for tokens in total_data_text :
    if len(tokens)<3 :
        print(tokens)
        
        print(get_decoded_sentence(tokens, index_to_word))
```


- [ ] 5.코드가 간결한가요?
  > 반복이 필요한 부분에 적절하게 함수 정의를 하였고 그 결과 간결하게 코드가 작성되었다.
```python
#epochs에 따른 loss acc 시각화
def drawLossAccuracy(history) :
    acc = history.history['accuracy']
    val_acc = history.history['val_accuracy']
    loss = history.history['loss']
    val_loss = history.history['val_loss']

    epochs = range(1, len(acc) + 1)
#     plt.figure(figsize=(20, 20))

    # "bo"는 "파란색 점"입니다
    plt.plot(epochs, loss, 'bo', label='Training loss')
    # b는 "파란 실선"입니다
    plt.plot(epochs, val_loss, 'b', label='Validation loss')
    plt.title('Training and validation loss')
    plt.xlabel('Epochs')
    plt.ylabel('Loss')
    plt.legend()

    plt.show()
    plt.clf()   # 그림을 초기화합니다
#     plt.figure(figsize=(20, 20))
    plt.plot(epochs, acc, 'bo', label='Training acc')
    plt.plot(epochs, val_acc, 'b', label='Validation acc')
    plt.title('Training and validation accuracy')
    plt.xlabel('Epochs')
    plt.ylabel('Accuracy')
    plt.legend()

    plt.show()

# drawLossAccuracy(history)
```

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
