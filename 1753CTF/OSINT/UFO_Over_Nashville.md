# 🛸 UFO over Nashville - Writeup

> **카테고리**: OSINT  

---

## 🧩 문제 설명

> 2020년 10월, Mark는 Adobe Premiere Pro를 사용하여 영상을 제작하고 이를 Parler에 업로드했습니다.  
> 이 1분도 채 되지 않는 영상에는 매혹적인 UFO 장면이 담겨 있습니다.  
> 영상 속에는 방문객을 환영하는 네온사인이 있는 레스토랑이 등장합니다.  
> 우리는 이 레스토랑에서 **$3에 판매하는 메뉴**가 무엇인지 알아내야 합니다.  
>  
> 참고로, Mark는 이 영상을 제작할 때 **`ufo_over_nashville.mp4`**라는 파일명을 사용한 것으로 보입니다.  
>  
> **플래그 형식**: `1753c{osint_challenge}`

---

## 🔍 문제 분석

이 문제는 두 가지 핵심 요소를 다루고 있다:

1. **메타데이터 분석**
2. **데이터 유출 활용** — 특히, Parler의 데이터 유출

---

## 🛠️ 해결 방법

1. **Parler 데이터셋 확보**  
   DDoSecrets 플랫폼에서 Parler의 유출된 비디오 데이터셋을 다운로드하였다:  
   👉 [https://ddosecrets.com/article/parler](https://ddosecrets.com/article/parler)  
   전체 데이터를 받을 필요는 없으며, **메타데이터가 포함된 아카이브**만 다운로드하면 된다.

2. **메타데이터 검색**  
   다운로드한 메타데이터 파일들에서 `ufo_over_nashville.mp4`라는 파일명을 검색하였다.  
   예를 들어, 터미널에서 다음과 같은 명령어를 사용할 수 있다:
   ```bash
   grep -r "ufo_over_nashville.mp4" /path/to/metadata/
   ```
   - meta-OVGzl7txWOUA.json
   - meta-BUcWJq4i1WHd.json
   - meta-Ogfy1F4vu1qT.json
3. **GPS 좌표 확인**
   찾은 메타데이터에서 GPS 좌표를 확인하였다.
   이 좌표를 지도 서비스(예: Google Maps)에 입력하여 영상이 촬영된 위치를 파악하였다.
   
4. **레스트랑 좌표 조사**
   해당 위치 근처의 레스토랑을 조사하여, 영상에 등장하는 네온사인과 일치하는 곳을 찾고
   레스토랑의 메뉴판이나 온라인 리뷰 등을 통해 $3에 판매하는 메뉴가 무엇인지 확인하였다.
![image](https://github.com/user-attachments/assets/db731259-51c2-428f-b6c6-352617410c6b)
---

## ✅ 최종 플래그
1753c{moon_pie}
