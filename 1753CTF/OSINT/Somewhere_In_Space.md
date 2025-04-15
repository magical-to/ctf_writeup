# Somewhere in Space - Writeup

> **카테고리** : OSINT  

---

## 🧩 문제 설명

어떤 잘생긴 남자가 아름다운 여성을 바라보고 있습니다.  
플래그는 여성의 얼굴이 저장된 **파일의 이름**입니다.  
**문자 중 90% 이상이 보이는 것만 사용**하세요.

- **플래그 형식**: `1753c{filename}`

<img width="738" alt="img" src="https://github.com/user-attachments/assets/c356d691-cfa6-4e12-bcf1-376a14e882dd" />



---

## 🕵️ 해결 과정

1. 문제에 주어진 **이미지를 구글 이미지 검색**에 업로드해보았다.
2. 검색 결과 중 다음 페이지를 찾게 되었다:
   👉 [vagabundler.com - Streetart in Limassol](https://vagabundler.com/cyprus/streetart-map-limassol/agiou-andreou-253/)
3. 해당 페이지에는 문제 속 **우주비행사 벽화**와 함께, 그 **맞은편에 여성 흉상(아프로디테)**이 그려져 있는 사진이 있었다.
4. 또 다른 사진에서는 해당 아프로디테의 그림이 **파일로 저장된 모습**이 보였다.
5. 파일 이름은 `Aphrodite_final.j` 까지만 보이며, 문제에서 "90% 이상 보이는 문자만 사용"하라는 조건을 고려해 플래그를 작성했다.

---

## ✅ 최종 플래그

1753c{Aphrodite_final.j}
