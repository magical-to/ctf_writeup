# 🌮 Czechxicans - BYUCTF 2025

## 📜 문제 설명

> Cameron Snider가 유럽에서 살 때, 자주 가던 멕시코 음식점이 있었음.  
> 음식이 꽤 괜찮았지만 몇 년 전에 문을 닫음.  
> 바로 옆에 있는 식당에는 리뷰를 남긴 적이 있다고 함.  
> 그 리뷰가 아직 Google에 남아있음.  
> 찾아보자.

- 출제자: The Camel

---

## 🔍 문제 분석

- 이전 문제(`Czech This Out`)에서 Cameron이 살던 나라는 **체코 공화국**임
- Google 리뷰를 통해 플래그를 얻는 **OSINT 기반 문제**임
- 핵심 단서:  
  1. 체코에 위치한 도시 Olomouc  
  2. 몇 년 전 문 닫은 멕시코 음식점  
  3. 바로 옆 가게의 리뷰에 플래그 존재

---

## 🛠️ 풀이 과정

1. **Olomouc에 있었던 멕시코 음식점** 중 **폐업한 가게**를 검색함  
   - 예: “Olomouc closed Mexican restaurant”

2. 식당 이름이 나왔으면, **바로 옆 가게**를 Google Maps에서 확인함

3. 해당 가게의 Google 리뷰 중에서 **작성자 이름이 Cameron** 또는 **문구에 플래그가 포함된 리뷰**를 찾음

4. 실제 리뷰 링크:  
   [https://maps.app.goo.gl/a7LjsBCLQC8NuMzy6](https://maps.app.goo.gl/a7LjsBCLQC8NuMzy6)

---

## 🏁 최종 플래그

byuctf{La_B0c4_Wa5_Gr4nd3}
