![image](https://github.com/user-attachments/assets/b6b4a54c-c310-46a7-afa3-73110f9107f7)Challenge Category : Osint<br>
Challenge Name : GhostBot<br><br>

![1](https://github.com/user-attachments/assets/0ee6f0dc-9f7a-4a75-9baa-1154b91c27c0)<br>
I discovered a leaked Discord chat where two individuals discussed a powerful bot used to track cybercriminals. One plans to use the bot to target someone, while the other warns of the risks. I’ve decided to investigate the bot’s origin, its role in cybercrime, and who's controlling it. Flag Format: 0xL4ugh{}<br><br>

문제를 해석해보자면,<br>
나는 두 사람이 사이버 범죄자를 추적하는 강력한 봇에 대해 논의한 유출된 Discord 채팅을 발견했다.<br>
한 사람은 그 봇을 사용해 누군가를 표적으로 삼을 계획을 세우고 있었고, 다른 한 사람은 그 위험성에 대해 경고했다.<br>
나는 이 봇의 기원, 사이버 범죄에서의 역할, 그리고 이를 누가 제어하고 있는지 조사하기로 결정했다.<br>
플래그 형식: 0xL4ugh{}<br><br>

![Image-discord](https://github.com/user-attachments/assets/a99a6aa0-2b4a-4b72-8ecb-609c2bc797e9)<br>
문제에서 주어진 사진이다.<br><Br>

사진 및 문제에서 주요하게 보아야 할 키워드는 다음과 같다.<br>
1. 사이버 범죄자를 추적하는 디스코드 봇
2. 누군가를 표적으로 삼고 봇을 사용할 계획
3. 2021년
4. MM0X라는 이름
5. 디스코드 서버
<br><br>

![image](https://github.com/user-attachments/assets/778d8055-05f2-4ba8-8b23-76e0d09ce38b)<br>
구글링을 통해 MM0X라는 이름을 검색해 보았는데, ctftime.org에서 0xl4ugh 관련해서 유저를 한 명 찾을 수 있었다.<br>

![image](https://github.com/user-attachments/assets/fb6a51c3-07ce-4775-b8f2-6c70ff7630f5)<br>
해당 0xl4ugh ctf 2024 출제위원 중 한 명인 것 같았다. 그렇다면, 아까 얻은 2021년이라는 힌트를 통해서 디스코드 메세지를 살펴보자.<br><br>

참고로 디스코드 메시지는 ctf.ae 디스코드가 아닌 0xl4ugh 디스코드에 직접 들어가야 한다.<br>

![image](https://github.com/user-attachments/assets/dc897fff-3b41-4f8a-94b4-cf1e3a74bbf1)<br>
0xl4ugh 디스코드에 들어와 2021년에 MM0X 유저가 보낸 내용을 살펴보던 중, 다음과 같은 대화 내용을 찾을 수 있었다.<br><br>

![image](https://github.com/user-attachments/assets/72ae6817-4e9b-45f0-97bc-08ea44896a31)<br>
권한이 없어서 mm0x가 보낸 메시지의 내용을 확인할 수 없다.<br><br>

https://discord.com/channels/GuildID[ServerID]/ChannelID/MessageID 디스코드의 URL 주소는 이렇게 가기에 해당 메시지의 link를 복사하여 url을 얻어내보자.<br><br>

https://discord.com/channels/1321167893559382100/1321167894163226737/1321189372854276098<br><br>

![6](https://github.com/user-attachments/assets/9cafef9b-1bcd-4263-8af8-e5c5128f2b20)<br>
discord guild lookup 사이트에 해당 주소를 입력하니 초대장이 나온다....<br>

![image](https://github.com/user-attachments/assets/e6e9d410-e96f-4f58-bf87-aafefecbfbab)<br> 
해당 디스코드 서버에서 문제에서 말했던 봇을 찾아냈다. 이제 봇에게 DM을 보내서 사용해보자.<br><br>

![8](https://github.com/user-attachments/assets/9de409a8-777e-4f86-9fad-9e804d8df191)<br><br>

![9](https://github.com/user-attachments/assets/9fc58181-93bb-4cad-9f24-1580a948dc7b)<br><br>

![10](https://github.com/user-attachments/assets/b0d54992-b204-459c-8b00-e14d74fa5519)<br><br>

![11](https://github.com/user-attachments/assets/387d4fce-e053-4c07-bc02-7b3cc26e2815)<br><br>

부족한 권한을 JWT 토큰을 만들어 내서 로그인을 하는 과정이다. 결과적으로 guest 역할로 로그인을 성공하는 모습이다.<br>
(봇이 로그아웃 상태라서 다른 분의 라업 참고했습니당)<br><br>

![image](https://github.com/user-attachments/assets/55692ec3-fd94-4f7c-841e-d1219a0fd0d0)<br>
또 다른 단서가 생겼다. 7amoksha는 해킹당했으며 ‘Apachei’라고 불린다.<br><br>

![13](https://github.com/user-attachments/assets/1267423a-6028-4289-8dec-f348b9d4bbb4)<br><br>
apachei라는 유저 이름을 사이트를 통해 크롤링해보니 github 주소가 있는 것을 확인할 수 있었다.<br><br>

![image](https://github.com/user-attachments/assets/6085bcb0-f291-4540-aa1e-97f3ebd68935)<br><br>
단 하나의 파이썬 코드 관련 레포가 있었다.<br><br><br>

![15](https://github.com/user-attachments/assets/43dcfb10-eed6-447f-bc67-483c6c8ede4c)<br>
관련 커밋을 뒤져보던 중, SECRET_KEY를 찾아낼 수 있었다!<br><br>

if name == "Elsfa7 Elmrta7":<br>
에서 첫 글자를 소문자로 바꾸면 조건을 우회하고 플래그를 얻을 수 있다.<br><br>

![image](https://github.com/user-attachments/assets/d006ca75-b77e-4baf-bc8d-39e5acd25538)<br>
요건 gist를 활용해서 또다른 SECRET_KEY를 찾은 모습이다.<br><br>

![18](https://github.com/user-attachments/assets/a68d91ef-52de-4ff0-ac4d-94d716fa5d4a)<br>
jwt 디코더로 가서(https://jwt.io/) 다음과 같이 잘 숨겨주고<br><br>

![17](https://github.com/user-attachments/assets/261bda1b-650e-4244-a3bf-c85b03faecc9)<br>
admin 권한으로 로그인을 성공하게 되면, 플래그가 나오게 된다.<br><br>

0xL4ugh{Y0u_So1v3d_m3_bu7_It5_N0t_th3_End}<br><br>


ps.<br>
![19](https://github.com/user-attachments/assets/421bd44e-cd39-44dd-a98f-c573bcc77b45)<br>
주인장 양반....<br><br>

https://tryhackme.com/jr/0xl4ughosintctf<br>
this is a free OSINT Room on TryHackMe if you want to try it. and share it with ur friends (Its Free)....










