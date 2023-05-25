# AIFFEL Campus Online 4th Code Peer Review Templete
- 코더 : 소용현
- 리뷰어 : 이효준


# PRT(PeerReviewTemplate)
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.
- [x] 1.코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
- [x] 2.주석을 보고 작성자의 코드가 이해되었나요?
  > 상세한 주석으로 코드가 잘 이해 되었습니다.
  > 특히 numpy의 where함수에 대한 설명이 좋았습니다.
```python
def stickObject(img_orig, img_bg_blur, img_mask_color) :
    # np.where(조건, 참일때, 거짓일때)
    # 세그멘테이션 마스크가 255인 부분만 원본 이미지 값을 가지고 오고 
    # 아닌 영역은 블러된 이미지 값을 사용합니다.
    img_concat = np.where(img_mask_color==255, img_orig, img_bg_blur)
    # plt.imshow(): 저장된 데이터를 이미지의 형식으로 표시한다.
    # cv2.cvtColor(입력 이미지, 색상 변환 코드): 입력 이미지의 색상 채널을 변경
    # cv2.COLOR_BGR2RGB: 원본이 BGR 순서로 픽셀을 읽다보니 
    # 이미지 색상 채널을 변경해야함 (BGR 형식을 RGB 형식으로 변경)
    fig, axes = plt.subplots(1, 2, figsize=(15, 10))
    axes[0].imshow(cv2.cvtColor(img_orig, cv2.COLOR_BGR2RGB))
    axes[0].set_title('Original')
    axes[1].imshow(cv2.cvtColor(img_concat, cv2.COLOR_BGR2RGB))
    axes[1].set_title('ShallowFocus')

#     plt.imshow(cv2.cvtColor(img_concat, cv2.COLOR_BGR2RGB))
    plt.show()
```

- [ ] 3.코드가 에러를 유발할 가능성이 있나요?
  > 없었습니다.

- [x] 4.코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네, 특히 사람 객체의 semantic segmentation 오차를 줄이기 위해 시행한 두 가지 방안이 매우 새로웠습니다.
  > dilate연산을 통해 객체 크기를 조절하는 방법
```python
def blurAndMask(seg_map,img_orig) :
    img_mask = seg_map.astype(np.uint8) * 255
    # dilate 연산 적용
    kernel = np.ones((5, 5), np.uint8)
    img_mask = cv2.dilate(img_mask, kernel, iterations=2)

    img_orig_blur = cv2.blur(img_orig, (13,13))# (13,13)은 blurring kernel size를 뜻합니다
    # cv2.cvtColor(입력 이미지, 색상 변환 코드): 입력 이미지의 색상 채널을 변경
    # 이미지 색상 채널을 변경해야함 (BGR 형식을 RGB 형식으로 변경) 
    img_mask_color = cv2.cvtColor(img_mask, cv2.COLOR_GRAY2BGR)

    # cv2.bitwise_not(): 이미지가 반전됩니다. 배경이 0 사람이 255 였으나
    # 연산을 하고 나면 배경은 255 사람은 0입니다.
    img_bg_mask = cv2.bitwise_not(img_mask_color)

    # cv2.bitwise_and()을 사용하면 배경만 있는 영상을 얻을 수 있습니다.
    # 0과 어떤 수를 bitwise_and 연산을 해도 0이 되기 때문에 
    # 사람이 0인 경우에는 사람이 있던 모든 픽셀이 0이 됩니다. 결국 사람이 사라지고 배경만 남아요!
    img_bg_blur = cv2.bitwise_and(img_orig_blur, img_bg_mask)
#     plt.imshow(cv2.cvtColor(img_bg_blur, cv2.COLOR_BGR2RGB))
#     plt.show()
    return img_bg_blur,img_mask_color
```
  > erode연산을 통해 객체 크기를 조절하는 방법
```python
def blurAndMask(seg_map,img_orig) :
    img_mask = seg_map.astype(np.uint8) * 255
    # erode 연산 적용
    kernel = np.ones((15, 15), np.uint8)
    img_mask = cv2.erode(img_mask, kernel, iterations=1)

    img_orig_blur = cv2.blur(img_orig, (13,13))# (13,13)은 blurring kernel size를 뜻합니다
    # cv2.cvtColor(입력 이미지, 색상 변환 코드): 입력 이미지의 색상 채널을 변경
    # 이미지 색상 채널을 변경해야함 (BGR 형식을 RGB 형식으로 변경) 
    img_mask_color = cv2.cvtColor(img_mask, cv2.COLOR_GRAY2BGR)

    # cv2.bitwise_not(): 이미지가 반전됩니다. 배경이 0 사람이 255 였으나
    # 연산을 하고 나면 배경은 255 사람은 0입니다.
    img_bg_mask = cv2.bitwise_not(img_mask_color)

    # cv2.bitwise_and()을 사용하면 배경만 있는 영상을 얻을 수 있습니다.
    # 0과 어떤 수를 bitwise_and 연산을 해도 0이 되기 때문에 
    # 사람이 0인 경우에는 사람이 있던 모든 픽셀이 0이 됩니다. 결국 사람이 사라지고 배경만 남아요!
    img_bg_blur = cv2.bitwise_and(img_orig_blur, img_bg_mask)
#     plt.imshow(cv2.cvtColor(img_bg_blur, cv2.COLOR_BGR2RGB))
#     plt.show()
    return img_bg_blur,img_mask_color
```

- [x] 5.코드가 간결한가요?
  > 여러 함수를 정의하여 간결하게 문제 해결하였습니다.
```python
def blurAndMask(seg_map,img_orig) :
  pass
  
#이미지 배경을 흐리게 
#category는 LABEL_NAMES에 있는것만
def ShallowFocus(img_path,category) :
  pass
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
