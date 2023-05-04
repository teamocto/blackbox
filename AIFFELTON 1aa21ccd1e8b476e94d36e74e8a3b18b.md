# AIFFELTON

---

![Untitled.png](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/Untitled.png)

# **팀명 : BLACKBOX**

# **팀원 : 신종우(L), 이상준, 김찬진, 정현범**

## 안녕하세요. 저희는 차량 파손 CV task를 맡은 ‘블랙박스’ 입니다.

# 🚘서비스 기획 배경

- 우리가 돕고자 하는 부분은 ‘정비’ 와 관련된 부분입니다.
    
    [NOTION PAGE](https://www.notion.so/610eb17a479746cfa9bb517728ca52e5)
    
    ![슬라이드3.JPG](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/%25EC%258A%25AC%25EB%259D%25BC%25EC%259D%25B4%25EB%2593%259C3.jpg)
    
    ![슬라이드6.JPG](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/%25EC%258A%25AC%25EB%259D%25BC%25EC%259D%25B4%25EB%2593%259C6.jpg)
    

---

# 🎈프로젝트 설명

- 차량 파손
    - 차량 이용중 차량 사고시 파손된 부위를 촬영하여 업로드
        
        ![img.png](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/img.png)
        
- 파손부위의 위치설정
    - 업로드된 사진을 분석하여 정확환 파손부위에 대한 위치를 설정
        
        ![images (1).jpg](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/images_(1).jpg)
        
- 파손부위에 대한 견적
    - 파손된 위치가 설정이 되면 파손 부위에 대한 자동 견적을 메긴다.
        
        ![2588009812edf2d0e30cc7bfab2c4772_res.png](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/2588009812edf2d0e30cc7bfab2c4772_res.png)
        

---

# 🚧데이터 분석 및 전처리

![Untitled](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/Untitled%201.png)

![Untitled](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/Untitled%202.png)

![Untitled](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/Untitled%203.png)

# 🚘 모델 설계

![Untitled](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/Untitled%204.png)

![Untitled](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/Untitled%205.png)

1. 자동차 큰 부위를 Segmeatation 한다. (anotation을 한다. )
- 키워드, 임베딩, 어노테이션등 공유
2. 파손 부위를 정확히 식별해 낸다.
(파손되지 않은 이미지를 가지고 학습이 되어 있어야 하나?)
- 파손부위를 알아내야 한다.(헤드라이트, 프론트 범퍼, 프론트 도어, 타이어 휠 등)
3. 파손부위 범위에 걸쳐져 있는 자동차의 부품 부위를 식별해 낸다.
4. 스크래치, 찌그러짐, 등등 파손에 대한 손상 정도를 분류한다.
5. 자동차의 전체 손상정도를 진단한다.(1차 진단 결과)
6. 정비소의 수리 공정으로 매치한다. (우리가 가지고 있는 견적서 데이터에 있는 차량 손상에 대한 라벨링 데이터의 경우 차량의 이름, 데이터 날짜, 이미지 크기, annotation, segmentation, area, boundingbox, damage의 종류, 손상 part, 연식, 색상, 수리 공정에 대한 정보)
7. Output - 견적서를 도출해낸다.

---

# 🎗U-NET 모델 훈련 설정

## 🅰모델 컴파일 및 훈련

```
OUTPUT_CLASSES = 3

model = unet_model(output_channels=OUTPUT_CLASSES)
model.compile(optimizer='adam',
              loss=tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True),
              metrics=['accuracy'])
```

## 🅱모델 아키텍처 플로팅

```jsx
tf.keras.utils.plot_model(model, show_shapes=True)
```

![output_sw82qF1Gcovr_0.png](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/output_sw82qF1Gcovr_0.png)

# 🌈모델학습결과

![Untitled](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/Untitled%206.png)

![Untitled](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/Untitled%207.png)

![Untitled](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/Untitled%208.png)

![Untitled](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/Untitled%209.png)

![Untitled](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/Untitled%2010.png)

![Untitled](AIFFELTON%201aa21ccd1e8b476e94d36e74e8a3b18b/Untitled%2011.png)