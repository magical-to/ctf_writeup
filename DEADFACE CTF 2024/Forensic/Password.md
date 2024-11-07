본 게시물은 2024년에 진행된 DEADFACE CTF 2024의 Forensic 부문에 관련된 문제에 대한 해설을 품고 있습니다.<br><br>

![1](https://github.com/user-attachments/assets/b9924c1c-b4c5-4406-9458-4095b87006f7)<br><br>

문제 설명 : <br>
Garry Sartoris가 가짜 로그인 페이지에 자신의 중요 정보를 주고 말았다.<br>
TGRI는 비밀번호 정책이 보안 관행을 강화하도록 보장하고자 할 때, Gary의 비밀번호는 무엇일까?<br><br>

간단하게 말하자면 Garry Satoris 씨가 취약한 로그인 페이지에 접근을 했고 비밀번호가 Wireshark(https://www.wireshark.org/download.html)를 이용해 패킷에 보여지는 문제다.<br><br>

![2](https://github.com/user-attachments/assets/9900461a-7234-47be-9969-794f92bf5ecd)<br><br>

Wireshark를 이용하여 Garry Sartoris가 로그인을 한 페이지에 ID, Password를 입력한 패킷이 포착되었고 해당 내용을 살펴보니,<br>
비밀번호가 **Sr4t0RIS19&&** 인 것을 확인 할 수 있다.<br><br>

flag{Sr4t0RIS19&&}
