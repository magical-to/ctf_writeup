해당 글은 Dreamhack(https://dreamhack.io/)의 포렌식 문제 중 하나인 'hacked'의 풀이를 담고 있습니다.<br><br>

hacked 문제 주소 : [https://dreamhack.io/wargame/challenges/1323](https://dreamhack.io/wargame/challenges/1332)<br>
포렌식 문제 자료 주소 : https://dreamhack.io/lecture/forensics-materials<br><br>

문제 설명 : <br>
당신은 해킹 사건을 분석해달라는 의뢰를 맡게 되었습니다.<br>
의뢰자는 이런 말을 덧붙였습니다.<br>
“컴퓨터에 문제가 있어 점검을 맡겼는데… 그 사람이 제 컴퓨터를 해킹한 것 같아요. 바탕화면에 이상한 파일이 갑자기 막 생겨서 얼마나 놀랐는지 몰라요”<br><br>

문제에서 얻을 수 있는 힌트는 바탕화면에 이상한 파일이 생겼다는 것이다. 이를 감안하고 문제를 풀러 가자.<br><br>

++ 해당 문제에서는 Arsenal(그 4스널 아님) Image Mounter라는 프로그램과 kape(또릭 짐머만)라는 프로그램을 사용하였다.<br><br>

gkape를 사용하면서 화면 디스플레이 문제로 인해 노트북에서 풀지 못하고 본체로 문제와 프로그램을 가져와 다시 풀었기 때문에 중간 맺음이 이상한 점은 양해바란다.<br><br>

![1](https://github.com/user-attachments/assets/6550fc03-c69d-4a43-9555-2f224a2c0539)<br>
우선, Arsenal Imager Mounter이다. 문제 파일을 다운 받은 후, 이미지 마운팅을 해준다.<br><br>

![2](https://github.com/user-attachments/assets/8234e241-311c-48ad-8581-f3c16cf0d86b)<br>
다음은 에릭 짐머만 선생님의 gkape를 이용하여 새로 생긴 디스크를 경로로 설정을 하여<br>
target: Chrome, PowerShellConsole, $J, $LogFile, $MFT, EventLogs, EventLogs-RDP, RegistryHivesOther, RegistryHivesSystem, RegistryHiveUser, WindowsFirewall으로 하고
module: Chainsaw, NTFSLogTracker, RegRipper, EvtxECmd, EvtxCmd_RDP로 설정을 할 예정이다.<br><br>

![3](https://github.com/user-attachments/assets/e5787ad0-32dc-48e1-9dc4-2cc845f64662)<br><br>
문제에서 준 힌트를 바탕으로 바탕화면에 이상한 파일이 뭐가 있는지를 확인해보니 똑같은 메모장들이 여러개 복사가 되어 있는 것을 확인할 수 있었다.<br><br>

![4](https://github.com/user-attachments/assets/c19ddff7-8c6a-4b16-9b70-22302b33e0a8)<br>
내용은 다음과 같다. 해킹했으니 비트코인을 보내라는 것이다.<br><br>

![5](https://github.com/user-attachments/assets/08ddfbc5-5aae-46ff-8e24-30fb056bc45d)<br>
또 다른 메모장을 발견하였다.<br><br>

![9](https://github.com/user-attachments/assets/a003f3d0-8942-4126-994d-f054c63171e3)<br>
인터넷 방문기록 뽑아내기(1)<br><br>

![8](https://github.com/user-attachments/assets/6f7ca6fa-7fda-49ed-95a8-935b65107522)<br>
인터넷 방문기록 뽑아내기(2)<br><br>

![7](https://github.com/user-attachments/assets/5d871a9b-e456-4b24-9bb6-cbb09706f358)<br>
인터넷 방문기록 뽑아내기(3)<br><br>

위 내용들을 종합해보니 현재 해킹 상황은 다음과 같이 유추가 된다.<br>
데탑 사용자는 헤드셋에 문제가 생겨서 고객 문의를 하였고. 고객 지원에서 TeamViewer라는 원격 프로그램을 통해서 도와주겠다고 했는데 내부망 pc여서 직원이 직접 방문하였다.<br>
직원이 작업을 하는 사이, 주인이 자리를 비웠고 이후 컴퓨터가 해킹이되어 바탕화면에 저런 메모장들이 생기게 된 것이다.<br><br>

![10](https://github.com/user-attachments/assets/53d4ccde-6298-4af5-bce6-ff94b680b9b6)
무엇을 찾아볼까 하다가, powershell에서 실행된 무엇인가 있는지 확인하기 위해서 ConSoleHost를 확인해보았는데 다음과 같은 명령어가 나와있었다.<br>
솔직히 좀 운의 영역인 것 같았다.<br><br>

![44](https://github.com/user-attachments/assets/573bc776-298c-4413-b848-e8f9fc9452ea)<br>
NTFS Log Tracker를 사용해서 다량의 Powershell 스크립트가 실행된 흔적을 발견할 수도 있다.<br><br>
FTK Imager에서 추출한 LogFile, UsnJrnl, MFT 파일을 각각 업로드한 다음에 Parse 버튼을 눌러주고 생성된 DB는<br>
DB Browser for SQLite를 다운로드하여 확인하였다.<br><br>

![10](https://github.com/user-attachments/assets/d1515e92-68ac-452d-8696-de372500e473)<br>
뭐 어쨌든, 스크립트를 다시 보면<br>
```
cd C:\Users\maple\Desktop\
powershell .\script.ps1
Set-ExecutionPolicy RemoteSigned
powershell .\script.ps1
ipconfig
```
인데, cd C:\Users\maple\Desktop\는 디렉토리 변경하는 명령어이고 powershell .\script.ps1은 script.ps1이라는 PowerShell 스크립트를 실행하는 명령이다.<br>
Set-ExecutionPolicy RemoteSigned는 PowerShell에서 서명된 원격 스크립트만 실행되도록 정책을 설정하는 명령인데 같은 명령어가 반복 실행된 것으로 보아 무언가 권한을 얻고 다시 실행한 것 같다.<br><br>

![13](https://github.com/user-attachments/assets/ee6ba133-00d1-4b92-a1fc-38af73a58d02)<br>
$MFT 파일을 HxD를 이용해서 열어 script.ps1을 찾아보니 다음과 같이 있었고 이를 통해 ConsoleHost로 들어가는 것이 정배였다.<br><br>

![11](https://github.com/user-attachments/assets/533be30f-5dc3-4033-9d60-3d22b4d0b54c)<br>
이벤트 로그(EvtxECmd 결과 csv 파일 전체)에서 스크립트 실행 1초 내의 기록을 살펴보면 새로운 계정이 생겨났음을 알 수 있고, 아래와 같이 로그 상세 내용을 보면 해당 계정의 이름은 “admin” 이다.<br><br>

![12](https://github.com/user-attachments/assets/377b70d4-be49-41e1-be22-7dfd38f5b01c)<br>
아래 사진과 같이 원격 접속(RDP, Remote Desktop Protocol) 흔적을 발견할 수 있는데 공격자는 “admin” 계정을 만들고, 관리자 계정을 부여하였다.<br>
원격 데스크톱과 생성한 계정을 통해 시스템에 자유롭게 드나들 수 있도록 백도어를 숨긴 것이다.<br><br>

로그아웃과 관련된 Event ID는 4634에서 로그아웃한 시간을 알아낼 수 있었고 문제에서 요구하는<br>
A와 B는 각각 script.ps1, 20240501-163302이다.

flag 형식이 DH{MyScript.js_20240502-120357}이므로 flag는 다음과 같다.<br>
DH{script.ps1_20240501-163302}이다!<br><br>

처음 Arsenal Imager Mounter와 gkape만 사용한다고 써두었는데 풀다보니 이래저래 많은 도구들을 사용한 것 같다.<br>
사실 Arsenal Imager Mounter와 gkape만으로는 왠만한 문제를 풀 수 없기에 그러려니 하고 넘어가주면 좋겠다 ㅠ<br>
초보자들은 FTK Imager와 NTFS Log Tracker, HxD의 사용법을 미리 익혀두는 것이 좋을 것 같다.
