# AIFFELTON

---

![Untitled](https://user-images.githubusercontent.com/118962335/236132509-d60f65fd-0594-4c08-902b-328454cf59ea.png)


# **팀명 : BLACKBOX**

# **팀원 : 신종우(L), 이상준, 김찬진, 정현범**

## 안녕하세요. 저희는 차량 파손 CV task를 맡은 ‘블랙박스’ 입니다.

# 🚘서비스 기획 배경

- 우리가 돕고자 하는 부분은 ‘정비’ 와 관련된 부분입니다.
    
    [NOTION PAGE](https://www.notion.so/610eb17a479746cfa9bb517728ca52e5)
    
![%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%93%9C3](https://user-images.githubusercontent.com/118962335/236127945-b4616bc3-1a06-4e68-9d86-5652dafb1828.jpg)

![%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%93%9C6](https://user-images.githubusercontent.com/118962335/236127973-ec983cf3-1cc4-47d7-8f01-4c6599f03c0e.jpg)

![Untitled 1](https://user-images.githubusercontent.com/118962335/236128001-1132c826-5855-4db5-a630-c09975c33612.png)

![Untitled_4](https://user-images.githubusercontent.com/118962335/236128017-c4ceaf4e-fe3f-4a27-88c6-99b0c27802ba.png)

![Untitled_5](https://user-images.githubusercontent.com/118962335/236128027-8e0c620b-4a3e-49af-a20d-17e7acb2651b.png)
  

---

# 🎈프로젝트 설명

- 차량 파손
    - 차량 이용중 차량 사고시 파손된 부위를 촬영하여 업로드
        
        ![img](https://user-images.githubusercontent.com/118962335/236128049-b23f2fa2-1a0d-4ae2-87b4-c97830d5904c.png)

        
- 파손부위의 위치설정
    - 업로드된 사진을 분석하여 정확환 파손부위에 대한 위치를 설정
        
        ![images_(1)](https://user-images.githubusercontent.com/118962335/236128181-a6ab16f1-a587-4af3-bde0-ce1e3d543c94.jpg)

        
- 파손부위에 대한 견적
    - 파손된 위치가 설정이 되면 파손 부위에 대한 자동 견적을 메긴다.
        
      ![2588009812edf2d0e30cc7bfab2c4772_res](https://user-images.githubusercontent.com/118962335/236128250-8bf5049d-873f-4dfb-9c0b-12530e1a549d.png)
        

---

# 🚧데이터 분석 및 전처리

![Untitled 2](https://user-images.githubusercontent.com/118962335/236128302-a5f52e2c-8054-46c2-9fc3-91cbc36d7239.png)

![Untitled 3](https://user-images.githubusercontent.com/118962335/236128331-5553bd0e-1cb9-425b-8776-a12c35375991.png)

![Untitled 4](https://user-images.githubusercontent.com/118962335/236128341-e74208c9-7f41-4ad8-8b16-33ba05217d42.png)

![Untitled 5](https://user-images.githubusercontent.com/118962335/236128348-5f7d2156-d1fc-4a76-bbb0-b6435cd44693.png)

![Untitled 6](https://user-images.githubusercontent.com/118962335/236128359-9288a4c6-c6c8-4dd8-847f-9bc8cdbd0e3f.png)

# 🚘 모델 설계

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

![output_sw82qF1Gcovr_0](https://user-images.githubusercontent.com/118962335/236128406-e67b1d14-7196-4386-b70a-53bae6dcacac.png)


---

# 🌈모델학습결과

![Untitled 7](https://user-images.githubusercontent.com/118962335/236128445-af69fd45-18dd-4182-b7a2-dba714c7d660.png)

![Untitled 8](https://user-images.githubusercontent.com/118962335/236128469-a598b554-4728-41db-92d0-c0f2c6b45722.png)

![Untitled 9](https://user-images.githubusercontent.com/118962335/236128484-f6474644-12aa-4ad9-8911-f0ff3c9a590a.png)

![Untitled 10](https://user-images.githubusercontent.com/118962335/236128502-cdd5ae95-d242-42c6-b27a-158608969f26.png)

![Untitled 11](https://user-images.githubusercontent.com/118962335/236128520-5d74fe2d-6ea9-42b5-866e-535572380c7f.png)

![Untitled 12](https://user-images.githubusercontent.com/118962335/236128529-00332c13-f99b-4d63-8541-8878c27500cf.png)

---

# 📄전체 스케쥴

![Untitled 13](https://user-images.githubusercontent.com/118962335/236128569-fc78768e-77b1-40b7-9a4c-5bd6f46c7c7d.png)
