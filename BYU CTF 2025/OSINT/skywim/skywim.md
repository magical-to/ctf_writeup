# 🐉 Skywim - BYUCTF 2025

## 📜 문제 설명

> 문제 출제자가 Skyrim 게임에서 좋아하는 NPC 옆에서 스크린샷을 찍었음.  
> 잠시 자리를 비운 사이 적에게 죽었고, 마지막 세이브가 4시간 전이었음.  
> 다시 그 장소를 찾지 못했음.  
> 스크린샷을 보고 이 장소가 **Skyrim 안의 실제 위치 중 어디인지** 찾아야 함.

- 플래그 형식: `byuctf{Named_Location_In_Skyrim}`
- 출제자: The Camel
- 첨부 이미지: `skyrim.jpg` 제공됨

---

## 🔍 문제 분석

- 핵심 목표: **이미지를 통해 Skyrim의 실제 지명 찾기**
- 이미지 왼쪽에 **배(boat)** 가 있고, **큰 아치형 구조물**이 보임 → 이는 **Solitude (솔리튜드)** 도시임
- Solitude 앞쪽에 **하나의 다리**가 있음
- 이미지 촬영 위치는 **약간 높은 절벽 위**

---

## 🗺️ 풀이 과정

1. **이미지의 시각적 단서**를 분석함  
   - Solitude가 배경에 보임  
   - Solitude 앞의 강 위에 **하나의 다리** 존재

2. Skyrim의 **인터랙티브 지도** 사용  
   - 추천 사이트: [MapGenie Skyrim Map](https://mapgenie.io/skyrim/maps/skyrim)

3. Solitude 주변에서:
   - 강을 따라 다리 위치 확인
   - 해당 다리 맞은편의 **절벽 위치** 탐색

4. 해당 절벽 위치에 존재하는 실제 장소 이름:  
   **Dragon Bridge Overlook**

---

## 🏁 최종 플래그

byuctf{Dragon_Bridge_Overlook}
