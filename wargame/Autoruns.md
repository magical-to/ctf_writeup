해당 글은 Dreamhack(https://dreamhack.io/)의 포렌식 문제 중 하나인 'Autoruns'의 풀이를 담고 있습니다.<br><br>

Track_the_file 문제 주소 : https://dreamhack.io/wargame/challenges/1323<br>
포렌식 문제 자료 주소 : https://dreamhack.io/lecture/forensics-materials<br><br>

문제 설명 : <br>
드림이의 컴퓨터에 누군가가 USB 저장장치를 연결했다가 해제한 후에, 컴퓨터를 재부팅할 때마다 계산기 프로그램이 실행되고 있어요.<br>
도대체 어떻게 된 일일까요?<br><br>

Windows 레지스트리를 분석해 플래그를 찾아보세요.<br><br>

FLAG = DH{ MD5(File) }
FLAG는 자동 실행되고 있는 exe 파일을 MD5 해시로 계산한 값을 이용해 만듭니다.<br>
예를 들어 대상 파일의 MD5 해시값이 00112233445566778899AABBCCDDEEFF 라면, 플래그는 DH{00112233445566778899AABBCCDDEEFF}입니다.<br><br><br>

문제에서 찾아야하는건 USB를 연결하여 어떠한 프로그램의 MD5 값이다.<br>
문제에서 Windows 레지스트리를 분석해서 플래그를 찾아보라는 힌트가 있기 때문에 시작프로그램의 정보를 담아놓는 레지스트리를 찾아볼 것이다.<br><br>

![1](https://github.com/user-attachments/assets/e51e32ac-9c22-4d20-b6c2-745df62d63b6)<br><br>
NTUSER.DAT를 찾는 과정에서 그 위에 malware.exe라는 프로그램이 있는 것을 발견했다.<br><br>

![2](https://github.com/user-attachments/assets/a77ebc15-979c-4d20-b8c1-b91b9d6c1ca2)<br>
malware.exe를 추출해보니 계산기 모양의 프로그램이다.<br>
문제를 보면, 드림이의 컴퓨터에 누군가가 USB 저장장치를 연결했다가 해제한 후에, 컴퓨터를 재부팅할 때마다 계산기 프로그램이 실행되고 있어요라고 하는데<br>
이 malware.exe 실행파일이 계산기 프로그램을 실행시키는 것 같다.<br><br>

![3](https://github.com/user-attachments/assets/b33ed904-a82d-4351-9d94-106b6541cfd7)<br>
Powershell에서 제공하는 MD5 해쉬 값을 뽑아주는 명령어를 입력해주면 된다.<br>
참고로 소문자로 넣어야 한다..<br><br><br><br><br><br><br>





우연으로 푼 풀이이고, 원래는 Registry Explorer(https://ericzimmerman.github.io/#!index.md)를 사용했는데,<br><br>

![4](https://github.com/user-attachments/assets/dc7f138a-c125-4ac6-b07b-b5381d02fd32)<br>
위 사진은 뽑아낸 NTUSER.DAT를 Registry Explorer에 넣어보았더니<br>
유저명이 victim인 NTUSER.DAT를 읽어 HKCU 안에 있는 Run 키를 확인해 "C:\Users\victim\malware.exe"가 부팅할 때 마다<br>
자동 실행되게 설정 되어있는 것을 확인할 수 있었다.<br><br>

그 후, malware.exe의 해쉬값을 HashCalc나 위의 방법처럼 뽑아내는 것이 정석이다.



