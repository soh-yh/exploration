아이펠캠퍼스 온라인4기 피어코드리뷰

- 코더 : 소용현
- 리뷰어 : 이효준

----------------------------------------------

PRT(PeerReviewTemplate)

- `[O]` 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
- `[O]` 주석을 보고 작성자의 코드가 이해되었나요?
  - 주석과 중간 중간 필요한 시각화를 통해 작성자의 코드가 잘 이해됐습니다.

- `[X]` 코드가 에러를 유발할 가능성이 있나요?
  - 깃허브에서 확인된 프리뷰와 깃클론 후 주피터노트북에서 

- `[O]` 코드 작성자가 코드를 제대로 이해하고 작성했나요? (직접 인터뷰해보기)
  - 주요 주석을 통해 코드뿐만 아니라 LinearRegression에 필요한 Feature가 무엇인지 잘 이해하고 있다고 판단됩니다. 
```python
from sklearn.model_selection import train_test_split
# minute, second 데이터 의미 없어 미포함
# year : 2개연도로는 추세예측에 악영향일 것으로 예상되어 미포함
# casual , registered : 등록여부 미포함
X = train[['season', 'workingday', 'weather', 'temp', 'atemp', 'humidity', 'windspeed',  'month', 'day', 'hour',]].values
y = train[['count']].values
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=2)
```
- `[O]` 코드가 간결한가요?
  - 전반적으로 간결하며 특히 시각화 코드가 이해하기 편하게 잘 작성되었습니다.
  - [용현님 코드]
```python
plt.scatter(X_test[:, 3], y_test)
```
  - [제코드]
```python
sns.scatterplot(data=X_test, x='temp', y='predictions')
```
----------------------------------------------

참고 링크 및 코드 개선
- 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
- 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.

# 파일 용량을 경량화 하기 위한 방법입니다.
## datetime 자료형을 연, 월, 일, 시, 분, 초 6가지로 분리하기
- [개선전] 
```python
train['month'] = pd.DatetimeIndex(train['datetime']).month
```
- [개선후] 
```python
train['month'] = train['datetime'].dt.month 
```
