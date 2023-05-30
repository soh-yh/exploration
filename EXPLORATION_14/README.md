# AIFFEL Campus Online 4th Code Peer Review Templete
- 코더 : 소용현
- 리뷰어 : 본인의 이름을 작성하세요.


# PRT(PeerReviewTemplate)
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.
- [⭕] 1.코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
- [⭕] 2.주석을 보고 작성자의 코드가 이해되었나요?
  > 
```python    
# 이전에 배웠던 내용을 토대로 train_step을 구성해주세요.
# Generator를 이용해 가짜 이미지 생성
fake_images = generator(sketch)
# Discriminator를 이용해 진짜 및 가짜이미지를 각각 판별

직접 작업한 부분에 대해 주석을 달아주어서 이해가 쉬웠습니다.
```
- [❌] 3.코드가 에러를 유발할 가능성이 있나요?
  > 
```python            
self.sigmoid = layers.Activation(tf.nn.sigmoid)

문자열이 아닌 상수를 적어주어서 에러 유발할 가능성을 줄였습니다.
```
- [⭕] 4.코드 작성자가 코드를 제대로 이해하고 작성했나요?
```python
def train_step(sketch, real_colored):
    with tf.GradientTape() as gene_tape, tf.GradientTape() as disc_tape:
    # 이전에 배웠던 내용을 토대로 train_step을 구성해주세요.
        # Generator를 이용해 가짜 이미지 생성
        fake_images = generator(sketch)
        # Discriminator를 이용해 진짜 및 가짜이미지를 각각 판별
        real_out = discriminator(sketch,real_colored)
        fake_out = discriminator(sketch, fake_images)
        # 각 손실(loss)을 계산
        gene_loss,l1_loss = get_gene_loss(fake_images, real_colored, fake_out)
        disc_loss = get_disc_loss(fake_out, real_out)

훈련에 들어가는 매개변수들이 잘 들어가있는것을 보니 이해가 잘 되어있으신 것 같습니다.
```
- [⭕] 5.코드가 간결한가요?
```python
self.blocks.append(
    DiscBlock(
        f,
        stride=2 if i<=2 else 1,
        custom_pad=False if i<=2 else True,
        use_bn=False if i!=0 and i!=4 else True,
        act = True if i<=3 else False
        )
)

매개변수에 조건을 달아서 코드가 간결해보였습니다.
```
