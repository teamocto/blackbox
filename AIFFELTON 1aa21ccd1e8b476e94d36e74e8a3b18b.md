# AIFFELTON

---

![Untitled](https://user-images.githubusercontent.com/118962335/236109478-f3685e06-7f22-4560-8584-3f30767bd990.png)



# **팀명 : BLACKBOX**

# **팀원 : 신종우(L), 이상준, 김찬진, 정현범**

## 안녕하세요. 저희는 차량 파손 CV task를 맡은 ‘블랙박스’ 입니다.

# 🚘서비스 기획 배경

- 우리가 돕고자 하는 부분은 ‘정비’ 와 관련된 부분입니다.
    
    [NOTION PAGE](https://www.notion.so/610eb17a479746cfa9bb517728ca52e5)
    
   ![%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%93%9C3](https://user-images.githubusercontent.com/118962335/236109543-04a20108-ab7f-4d4c-a09f-b1453723268d.jpg)

   ![%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%93%9C6](https://user-images.githubusercontent.com/118962335/236109553-86983a71-1ad2-4b2f-9e5e-fcf17728f87e.jpg)


---

# 🎈프로젝트 설명

- 차량 파손
    - 차량 이용중 차량 사고시 파손된 부위를 촬영하여 업로드
        
      ![img](https://user-images.githubusercontent.com/118962335/236109579-3081bbf9-00eb-412c-912c-7d10b79d5206.png)

        
- 파손부위의 위치설정
    - 업로드된 사진을 분석하여 정확환 파손부위에 대한 위치를 설정
        
        ![images_(1)](https://user-images.githubusercontent.com/118962335/236109591-95af9ffb-ad81-4d98-990f-8d4484fc3ad1.jpg)

        
- 파손부위에 대한 견적
    - 파손된 위치가 설정이 되면 파손 부위에 대한 자동 견적을 메긴다.
        
       ![2588009812edf2d0e30cc7bfab2c4772_res](https://user-images.githubusercontent.com/118962335/236109607-c2545303-de0a-45fd-92c3-c02f4a59e7c8.png)

        

---

# 🚧데이터 분석 및 전처리

![Untitled 1](https://user-images.githubusercontent.com/118962335/236109640-c03a1aa4-4557-48da-a645-a33d391a61f9.png)

![Untitled 2](https://user-images.githubusercontent.com/118962335/236109643-7bfe5c83-61ad-42a3-99ad-d458fd01b5ae.png)

![Untitled 3](https://user-images.githubusercontent.com/118962335/236109650-451a3aa6-6a42-4fe3-9398-47d2f4f34ec0.png)


# 🚘 모델 설계

![Untitled 4](https://user-images.githubusercontent.com/118962335/236109676-c1592b7d-8984-442b-9f7a-a4f77997f432.png)

![Untitled 5](https://user-images.githubusercontent.com/118962335/236109686-8523da4e-c367-4c8f-b7f6-f241cedc6e33.png)


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

![output_sw82qF1Gcovr_0](https://user-images.githubusercontent.com/118962335/236109714-9d4228bb-f951-4e0e-b4a3-8f91980e25ad.png)


# 🌈모델학습결과

![Untitled 6](https://user-images.githubusercontent.com/118962335/236109738-db3c6032-bd36-4289-96ba-e9113a396bcf.png)

![Untitled 7](https://user-images.githubusercontent.com/118962335/236109754-0966035d-034b-4d91-aed1-04c556141997.png)

![Untitled 8](https://user-images.githubusercontent.com/118962335/236109767-75ea23d6-1713-41d1-a819-3e4e8d8c18c1.png)

![Untitled 9](https://user-images.githubusercontent.com/118962335/236109771-7820ecdd-62e5-448d-b5f1-9d311b47fd35.png)

![Untitled 10](https://user-images.githubusercontent.com/118962335/236109777-6705f5cc-b6cb-4487-83e1-7b1c319d0c45.png)

![Untitled 11](https://user-images.githubusercontent.com/118962335/236109779-25540e32-1e6c-46d8-b454-1d3109725d8c.png)



