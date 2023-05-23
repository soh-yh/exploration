# AIFFEL Campus Online 4th Code Peer Review Templete
- 코더 : 소용현
- 리뷰어 : 이효준

## 소검
적젏한 함수 정의로 모든 진행사항들을 일목요연하게 볼 수 있어 좋았습니다.

특히 밝기 조절을 `def brightnessAdjust(img,fileNm)`라는 함수를 통해 해결한 것이 
이미지 에디터를 통해 밝기 조절을 한 것에서 깊은 감명을 받았습니다.

---




# PRT(PeerReviewTemplate)
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.
- [x] 1.코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 네, 잘 해결 되었습니다.
- [x] 2.주석을 보고 작성자의 코드가 이해되었나요?
  > 네! 대부분의 코드에 주석이 있어 쉽게 흐름을 이해할 수 있었습니다.
```python
#얼굴 이목구비를 찾아줍니다.
def faceLandMark(dlib_rects,fileNm) :
    print(dlib_rects)
    list_landmarks = []
    # 랜드마크의 위치를 저장할 list 생성    

    # 얼굴 영역 박스 마다 face landmark를 찾아냅니다
    # face landmark 좌표를 저장해둡니다
    for dlib_rect in dlib_rects:
        points = landmark_predictor(img_rgb, dlib_rect)
            # 모든 landmark의 위치정보를 points 변수에 저장
        list_points = list(map(lambda p: (p.x, p.y), points.parts()))
            # 각각의 landmark 위치정보를 (x,y) 형태로 변환하여 list_points 리스트로 저장
        list_landmarks.append(list_points)
            # list_landmarks에 랜드마크 리스트를 저장

#     print(len(list_landmarks[0]))
    # 얼굴이 n개인 경우 list_landmarks는 n개의 원소를 갖고
    # 각 원소는 68개의 랜드마크 위치가 나열된 list 
    # list_landmarks의 원소가 1개이므로 list_landmarks[1]을 호출하면 IndexError가 발생
    for landmark in list_landmarks:
        for point in landmark:
            cv2.circle(img_show, point, 2, (0, 255, 255), 10)
                # cv2.circle: OpenCV의 원을 그리는 함수
                # img_show 이미지 위 각각의 point에
                # 크기가 2이고 (0, 255, 255)색으로 내부가 채워진(-1) 원을 그림
                # (마지막 인수가 자연수라면 그만큼의 두께의 선으로 원이 그려짐)

    img_show_rgb = cv2.cvtColor(img_show, cv2.COLOR_BGR2RGB)
        # RGB 이미지로 전환
#     plt.figure(figsize=(15, 15))
    plt.imshow(img_show_rgb)
    plt.title(fileNm+' Face landmarks')
    # 이미지를 준비
    plt.show()
    # 이미지를 출력
    return list_landmarks
```
- [x] 3.코드가 에러를 유발할 가능성이 있나요?
  > 사용자 운영체제에 따라 os.getenv('Home')이 제대로 작동하지 않을 수 있습니다.
```python
import os

sticker_path = os.getenv('HOME')+'/aiffel/camera_sticker/images/cat_nose.png'
```

해결 예시
```python
import os

sticker_path = os.path.expanduser("~") + '/aiffel/camera_sticker/images/cat_nose.png'
```

- [x] 4.코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네, 정의한 함수에 친절한 주석 설명이 포함되어 있음을 통해 제대로 이해하였는지 확인 되었습니다.
```python
# 이미지를 불러와서 보여주는 함수
def imageLoad(path):
  pass
  
# 얼굴을 찾아줍니다.
def faceDetect(img_rgb,img_show,fileNm) :
  pass
  
 # 얼굴 이목구비를 찾아줍니다.
def faceDetect(img_rgb,img_show,fileNm) :
   pass
```
- [x] 5.코드가 간결한가요?
  > 함수가 잘 정의되어 있어 코드의 흐름을 이해하기 좋습니다.
```python
# 얼굴을 찾아줍니다
def faceDetect(img_rgb,img_show,fileNm) :
    dlib_rects = detector_hog(img_rgb, 1) # (image, num of image pyramid)
    print("얼굴 영역"+str(dlib_rects))
    for dlib_rect in dlib_rects: # 찾은 얼굴 영역의 좌표
        l = dlib_rect.left() # 왼쪽
        t = dlib_rect.top() # 위쪽
        r = dlib_rect.right() # 오른쪽
        b = dlib_rect.bottom() # 아래쪽

        cv2.rectangle(img_show, (l,t), (r,b), (0,255,0), 2, lineType=cv2.LINE_AA) # 시작점의 좌표와 종료점 좌표로 직각 사각형을 그림

    img_show_rgb =  cv2.cvtColor(img_show, cv2.COLOR_BGR2RGB)
    plt.imshow(img_show_rgb)
    plt.title(fileNm+' Face Rect')
    plt.show()
    return dlib_rects
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
