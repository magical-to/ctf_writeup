# 🎓 Universal-ty - BYUCTF 2025

## 📜 문제 설명

> Cameron Snider는 고등학생 시절, 관심 있던 대학교를 하루 동안 다녀온 적이 있음.  
> 만약 BYU에 가지 않았다면 이 학교에 진학했을 것이라고 함.  
> 그가 방문했던 대학교의 이름을 찾아야 함.

- 플래그 형식: `byuctf{Name_of_University}`  
- 이미지 제공: `school.jpg`  
- 출제자: The Camel

---

## 🧠 문제 풀이 흐름

### 1️⃣ 단서: 고등학교 당시 거주지

- 출제자(Cameron Snider)의 **고등학교 시절 거주지**는 **인디애나(Indiana)** 주임

### 2️⃣ 조건: **당일치기 방문 가능한 대학교**

- 즉, 인디애나 내 또는 근처에 있는 명문 대학 중 하루 방문이 가능한 곳

### 3️⃣ 이미지 분석 및 후보 대학교 확인

- `school.jpg` 이미지를 기반으로 **건축 양식**, **랜드마크** 등을 대조  
- Google 이미지나 캠퍼스 맵 등을 활용해 비교 분석

- 매칭되는 학교: **University of Notre Dame**  
  - 인디애나주 사우스벤드(South Bend)에 위치  
  - 인디애나 내 대표적인 명문 사립대학

---

## 🏁 최종 플래그
byuctf{University_of_Notre_Dame}
