본 게시물은 2024년에 진행된 DEADFACE CTF 2024의 Forensic 부문에 관련된 문제에 대한 해설을 품고 있습니다.<br><br>

![1](https://github.com/user-attachments/assets/f77f0de4-41d2-4a72-937e-e80f807ca10f)<br><br>

문제 해설 : <br>
또 또 또 Garry 씨다. 그 놈이 Garry 씨가 피싱 사기에 속은 후 실행한 악성 파일의 PID는 무엇인지 찾는 문제이다.<br><br>

이전 문제인 'Right Time' 문제를 풀 때 사용했던 Volatility를 이용해서 다시 문제를 풀 것이다.<br><br>

Volatility(https://volatilityfoundation.org/)란?<br>
- 메모리 포렌식에서 메모리 덤프 파일을 분석할 때, 가장 많이 사용되고 있는 도구<br>
- 오픈 소스 기반으로 CLI 인터페이스를 제공하는 메모리 분석 도구<br>
- 컴퓨터(노트북)에서 덤프 된 파일을 분석 가능하며, 프로세스 정보와 네트워크 정보 등을 확인할 수 있다.<br>
- 프로세스 덤프 기능을 제공하여 기존 컴퓨터나 노트북에서 실행되고 있던 프로세스 내용을 확인할 수 있다.<br><br>

대충 명령어들을 정리해주자면,<br>
pslist : 프로세스들의 리스트를 출력<br>
psscan : offset 순서대로 출력<br>
pstree : PID, PPID를 기반으로 구조화해서 출력(PID : 프로세스 아이디, PPID : Parents의 PID)<br>
psxview : pslist와p sscan을 한 눈에 볼 수 있는 명령어<br>
cmdscan : cmd.exe가 실행한 명령어들을 나열<br>
consoles : 사용자가 입력한 명령어가 성공했는지 실패했는지 확인할 수 있는 명령어<br>
cmdline : 프로세스가 실행될 때의 인자 값 확인<br>
filescan : 메모리 내에 존재하는 모든 파일에 대한 정보를 보여준다.<br>
connections : TCP 통신에 대한 정보를 보여준다.<br>
sockets : 응답 받기를 기다리고 있는 모든 프로토콜에 대한 소켓의 정보를 보여준다.<br>
netscan : 메모리를 직접 스캔하여 모든 활성 네트워크 연결 및 리스닝 포트를 찾는다.<br><br>

fornesic_basic이나 codecure repo를 보면 알 수 있듯이, PID를 구하기 위해선 pstree 명령어를 입력하면 된다.<br><br>

![2](https://github.com/user-attachments/assets/ac2f4a97-5e78-4688-9799-14558acf7c19)<br><br>

위 사진은 pstree 명령어를 입력하여 나오는 로그들을 > pstree.log라는 명령어를 통해 뽑아내고 notepad++에 옮긴 모습이다.<br><br>

보통, pstree를 사용하여 프로세스들을 볼 때 전부 구글링을 해보곤 하는데, 구글링해볼 가치가 없는 대충 짠 이름의 프로세스인 945f.exe가 보인다.<br>
추가적으로, 945f.exe의 PID는 12260이며 부모 프로세스는 11532로 부여되었다.<br>
11516의 PID는 1sass.exe로 되어있는데, 이를 보면 알 수 있는 점이,<br>
1sass.exe와 945f.exe를 활용하여 피싱 프로그램이 작동한 것으로 보이고<br>
flag 값은 11260, 11532, 11516, 8460 중 하나 집어 넣으면 된다.<br><br>

flag{8640}

