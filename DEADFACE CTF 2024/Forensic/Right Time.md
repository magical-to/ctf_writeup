본 게시물은 2024년에 진행된 DEADFACE CTF 2024의 Forensic 부문에 관련된 문제에 대한 해설을 품고 있습니다.<br><br>

![1](https://github.com/user-attachments/assets/d92e72b2-9106-447d-baa0-8019a4c89f16)<br><br>

문제 설명 : <br>
TGRI 직원 Garry Sartoris가 최근 피싱 공격에 속아 넘어갔다.(또 Garry Sartoris야?) DEADFACE의 목표가 무엇이었는지 정확히 알기는 어렵지만<br>
Turbo Tactical에서 공격 흔적을 조사하는 데 도움이 필요하다.<br>
이 메모리 덤프를 확인하고 메모리가 캡처된 시스템 시간을 제출하면 되는 문제이다.<br><br>

내 repo 중에 Forensic_Basic이나 Codecure에 volatility라는 메모리 분석 툴을 사용하는 방법들이 있으니 참고해주면 좋겠다.<br><br>

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

이 정도 명령어가 있으며, 사용 방법은 위에서 말했듯이 다른 repo들을 참고하면 될 것 같다.<br><br>

문제 자체는 입력해야할 명령어가 많지 않다.<br>
![2](https://github.com/user-attachments/assets/445a71de-e05e-4bc0-914c-b213443b0e91)<br>
imageinfo 명령어를 사용하면 분석하고자 하는 raw 파일의 시스템 정보를 분석해서 출력해준다.<br><br>

physmem.raw는 2024년 10월 6일 23시 38분 00초에 사용된 파일이며 커널 Base 주소는 0xf80375800000이다.<br>
어차피 문제에서는 SystemTime을 조회만 하면 되니 flag값은 다음과 같다.<br><br>

flag{2024-10-06 23:38:00+00:00}
















