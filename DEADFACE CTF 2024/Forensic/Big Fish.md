본 게시물은 2024년에 진행된 DEADFACE CTF 2024의 Forensic 부문에 관련된 문제에 대한 해설을 품고 있습니다.<br><br>

이전 Steganogrpahy의 풀이들 맨 첫 줄에다가 전부 DEADSPACE로 잘못 썼는데 양해 부탁드립니다....<br><br>

문제 설명 : <br>
TGRI 직원 Garry Sartoris가 최근 피싱 공격에 당했다.<br>
DEADFACE가 노린 것이 무엇인지 파악하기는 어렵지만, Turbo Tactical이 공격 흔적을 분석하는 데 도움을 필요로 하고 있다.<br>
이 PCAP 파일을 확인하여 공격자의 IP 주소를 제출해달라.<br><br><br>


![1](https://github.com/user-attachments/assets/544eee5f-2342-462c-9069-1f9f2c8a885a)<br>
문제에는 Traffic analysis 문제로 공격자의 IP가 flag라고 맨 밑줄에 쓰여있다.<br>
주어진 pcap 파일을 Wireshark(https://www.wireshark.org/download.html)를 통해서 확인해 볼 예정이다.<br><br>

![2](https://github.com/user-attachments/assets/3e5d5933-4310-4454-9278-0af7362e3487)<br>
pcap 파일 내 45.55.201.188이라는 공격자가 GET /nc.exe 를 실행하려는 모습이 패킷에 잡혔다.<br><br>

flag{45.55.201.188}
