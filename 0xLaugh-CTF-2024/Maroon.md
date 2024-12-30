Challenge Category : Osint<br>
Challenge Name : Marron<br><br>

![1](https://github.com/user-attachments/assets/2fd5e06b-5aaf-46b1-b13e-99f149cf28d9)<br>
A notorious cheat coder known as Destroyer2009 shook the competitive gaming world by disrupting a major event with a multi-million dollar prize pool, causing the competition to be halted. After vanishing from the scene, he has resurfaced under the radar, sharing a cheat tool for another competitive game on an obscure internet forum. Rumors of his return have surfaced, and traces of his online activity have been uncovered, pointing to a hidden post where he uploaded the cheat. Your mission is to follow the clues and find the full URL of the forum thread where the cheat was posted. Flag Format: 0xL4ugh{Thread Full URL [XXXXX://XXXXXXX.XXX/XXXXXXX/XXXXX/]}<br><br>

문제를 해석해보자면 다음과 같다.<br>
악명 높은 치트 코드 제작자 Destroyer2009가 수백만 달러의 상금이 걸린 주요 대회를 방해하며 경쟁 게임 세계를 뒤흔들었고, 그로 인해 대회가 중단되는 사태가 발생했다.<br>
그는 사건 이후 모습을 감췄지만, 최근 다른 경쟁 게임을 위한 치트 툴을 음지의 인터넷 포럼에 공유하며 은밀히 다시 활동을 시작한 것으로 보인다.<br>
그의 복귀에 대한 소문이 돌기 시작했고, 그의 온라인 활동의 흔적이 발견되어 그가 치트를 업로드한 포럼의 숨겨진 게시글로 이어지는 단서가 드러났다.<br>
당신의 임무는 단서를 따라가 치트가 게시된 포럼 스레드의 전체 URL을 찾는 것이다.<br><br>

플래그 형식 : 0xL4ugh{Thread Full URL [XXXXX://XXXXXXX.XXX/XXXXXXX/XXXXX/]}<br><br>

문제를 보아하니 URL을 찾으면 그게 플래그인 것 같다.<br><br>

문제에서 주요하게 여겨볼 키워드는 다음과 같다.
1 - Destroyer2009라는 이름의 치트 코드 제작자(사용자명)가 수백만 달러의 상금이 걸린 주요 대회를 방해하며 경쟁 게임 세계를 뒤흔들었다는 것<br>
2 - 또 다른 경쟁 게임을 위한 치트 툴을 공유했다는 점<br>
3 - 음지의 인터넷 포럼<br><br>

![image](https://github.com/user-attachments/assets/9815cc0d-5af3-47dc-b4dd-c4116f33e133)<br>
위 사진은 destroyer2009라는 키워드로 구글에 검색을 해 본 결과이다. 이 해커는 Apex Legends라는 게임에서 이미 유명세를 떨치던 해커로 보인다.<br><br>

이미 이름이 알려졌기에 범인은 이름을 바꿔 숨었을 수도 있다.<br>
그렇기에, https://opsecfail.github.io/ 사이트에서 이름을 검색해보았다.<br><br>

![3](https://github.com/user-attachments/assets/b68ecf39-8541-4795-bff1-c53fc3d240aa)<br>
빨간색으로 네모친 칸에서 찾을 수 있었고, 자세히 살펴보니<br><br>

![4](https://github.com/user-attachments/assets/d44dfe5f-69b5-451e-bf10-82c750478317)<br>
timoxa5651라는 닉네임으로도 활동을 한 것으로 보인다.<br>
His email was found through his GitHub commits, which led to further uncovering of his identity.라는 부분에서 github 주소도 있는 것으로 보인다.<br><br>

![image](https://github.com/user-attachments/assets/fd8e3e98-a1bc-45cb-88c5-c72a5773f1e4)<br>
github에서 같은 이름의 단 한 명의 유저를 찾아낼 수 있었다.<br><br>

이제 https://web.archive.org/web 사이트를 통해<br>
해당 깃헙에서 웹사이트의 과거 버전을 저장하고 검색해보려고 한다.<br><br>

https://archive.md/와 https://cachedview.com/, https://timetravel.mementoweb.org/ 이러한 사이트들을 사용할 수도 있다.<br><br>

![image](https://github.com/user-attachments/assets/8d898712-afd6-4eb7-a425-ef5b92a93e02)<br>
사이트의 URLs 부분을 보던 도중 cheat loader 관련 레포가 있는 것을 확인할 수 있다.<br><br>

![image](https://github.com/user-attachments/assets/f6c81cb3-6753-4cc5-ab1d-33c1407fc029)<br>
따라란, Cheat-Loader 관련 레포를 찾아냈다.<br><br>

![image](https://github.com/user-attachments/assets/b75e1952-29f5-40f0-ad14-bd2ccf92b1a5)<br><br>
readme에 있는 주소를 따라가보니 다음과 같은 스레드를 확인할 수 있었다.<br><br>

따라서, 문제에서 필요로 하는 플래그는 다음과 같다.<br>
0xL4ugh{https://yougame.biz/threads/84149/}







