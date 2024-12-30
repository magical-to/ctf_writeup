Challenge Category : Osint<br>
Challenge Name : mini-x<br><br>

![image](https://github.com/user-attachments/assets/9f2d5209-25ce-423d-804b-838817f825f8)<br>
A cybercriminal responsible for a series of high-profile ransomware attacks has vanished. The only remaining clue is a fragmented NCIC number hidden within the investigation's scattered files. A corrupted image, found on a dark web server, is believed to be linked to the suspect, who is rumored to be on the FBI's Most Wanted list. Your mission is to reconstruct the NCIC number. Flag Format: 0xL4ugh{WXXXXXXX59}<br><br>

문제를 해석해보자면, 고위급 랜섬웨어 공격을 저지른 사이버 범죄자가 사라졌습니다.<br>
조사 과정에서 남은 단서는 여러 파일에 흩어져 있는 단편적인 NCIC 번호이다.<br>
다크 웹 서버에서 발견된 손상된 이미지가 용의자와 관련이 있는 것으로 보이며, 이 용의자는 FBI의 수배 리스트에 오른 것으로 추정됩니다.<br>
당신의 임무는 NCIC 번호를 복원하는 것이다. 플래그 형식: 0xL4ugh{WXXXXXXX59}<br><br>

우선. NCIC가 뭔지 알아보자.<br>
NCIC는 National Crime Information Center의 약자로, 미국 FBI에서 운영하는 전국 범죄 정보 시스템이다.<br><br>

이 시스템은 범죄자, 실종자, 도난 물품, 그리고 기타 법 집행과 관련된 데이터를 저장하고 이를 지역 경찰, 연방 요원, 기타 법 집행 기관에서 조회할 수 있도록 제공한다.<br><br>

쉽게 말해, 법 집행 기관들을 위한 중앙화된 범죄 데이터베이스라고 볼 수 있다. 예를 들어, 수배 중인 범죄자 정보, 도난 차량, 실종자 보고서 등이 포함되어 있다.<br><br>

NCIC 번호는 이 데이터베이스 내에서 특정 인물이나 물건을 식별하기 위해 사용되는 고유한 식별 번호이다.(고마워요 ChatGPT!)<br><br.

![image](https://github.com/user-attachments/assets/b8197b8a-ed07-4e72-99e9-b611afd1cbfa)<br>
문제에서 주어진 사진을 보아하니, 사람의 실루엣인 것 같은데 빨간색으로 되어 있어서 인식하기가 불가능하다.<br>
사진 편집 어플을 통해서 채도를 조절해보려 했는데 실패했다.<br><br>

문제에서 주어진 2가지 키워드에 집중해보자.<br><br>

1 - Cybercriminal has high-profile ransomware attacks<br>
2 - The FBI's Most Wanted list<br><br>

MOST WANTED CYBERCRIMINALS FOR FBI라는 키워드로 구글에 검색을 해보니 아래 사이트 주소가 가장 먼저 올라와 있다.<br>
(https://www.darkreading.com/cloud-security/fbi-s-most-wanted-cybercriminals)<br><br>

![2](https://github.com/user-attachments/assets/d2b7ec77-3574-45cd-83fc-a3cd59b0e154)<br>
사람들 리스트를 살펴보고 있던 도중, 중간에 처음 본 이미지와 비슷한 실루엣의 사람이 보인다. 다시 한 번 비교해보자.<br><br>

![image](https://github.com/user-attachments/assets/336a081c-c953-4485-9ce6-e838d4c2ae68)
![3](https://github.com/user-attachments/assets/16e184e5-5133-4aba-90fc-3c84d5c7ccb9)<br><br>

그렇다. 이미지의 주인공 이름은 Alexsey Belan이다.<br><br>

Alexsey Belan을 구글링을 해보니 아래 사이트에서 관련된 정보들을 확인할 수 있었다.<br>
(https://www.fbi.gov/wanted/cyber/alexsey-belan)<br><br>

![image](https://github.com/user-attachments/assets/c46570d3-eb39-4943-9b4b-731c822fb5a7)<br>
문제에서 원하는 NCIC 번호가 있는 것을 확인할 수 있다.<br><br>

그러므로, 플래그는 다음과 같게 된다.<br>
0xL4ugh{W507648159}

