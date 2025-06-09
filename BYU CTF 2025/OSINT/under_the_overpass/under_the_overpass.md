# 🕵️ Under the Overpass - BYUCTF 2025

## 📜 문제 설명

> 국제 스파이로 의심되는 **Cameron Joseph Snider**가 독일 베를린에서  
> 외국 정부와의 접촉을 시도하고 있음.  
> 최근 독일 입국 시 여권이 조회되었으며, 현재 **주독 대사관 근처**에서 활동 중이라 판단됨.  
>  
> 마지막 이메일에 따르면, 그는 **치통**이 있어 **대사관 옆 치과**에 예약하려 했고  
> 머무는 호텔은 **대사관 반대편**에 있다고 언급함.  
>  
> 그의 위치를 파악하여 **그가 방문 중인 대사관의 국가 이름**과  
> **해당 대사관 반경 100m 내의 보안 카메라 수**를 알아내야 함.  
>  
> 특별히 제공된 도구: [Overpass Turbo](https://overpass-turbo.eu/)  

- 플래그 형식: `byuctf{Country_Name:Number of Cameras}`  
- 예시: `byuctf{France:59}`  
- 출제자: The Camel

---

## 🗺️ 풀이 요약

### 1️⃣ 베를린 내 모든 외교 시설 검색

```overpassql
[out:json][timeout:25];
{{geocodeArea:Berlin}}->.searchArea;
(
  nwr["amenity"="embassy"](area.searchArea);
  nwr["office"="diplomatic"](area.searchArea);
);
out center;
```
> 해당 쿼리는 베를린 지역에서 대사관 및 외교사무소를 모두 검색함

### 2️⃣ 조건에 맞는 대사관 찾기

```
결과 중, El Salvador 대사관이 아래 조건과 일치함:

옆에 치과(dentist) 있음

맞은편에 호텔 있음

실제 위치 좌표 :
lat: 52.5287089, lon: 13.3800402
```

### 3️⃣ 100미터 내 감시 카메라 수 조사

```
[out:json][timeout:25];
(
  nwr(around:100, 52.5287089, 13.3800402)["man_made"="surveillance"];
  nwr(around:100, 52.5287089, 13.3800402)["surveillance"];
);
out body;
```
결과 개수 : 10개의 보안 카메라 확인됨

### 🏁 최종 플래그
byuctf{El_Salvador:10}
