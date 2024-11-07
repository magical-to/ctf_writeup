본 게시물은 2024년에 진행된 DEADFACE CTF 2024의 Forensic 부문에 관련된 문제에 대한 해설을 품고 있습니다.<br><br>


![1](https://github.com/user-attachments/assets/06324272-ded7-4f1e-9a14-3f350cead510)<br>
문제 설명 : <br>
DEADFACE는 Garry Sartoris를 속이기 위해 이메일에서 Elroy Ongaro라는 IT 멤버로 위장했다.<br>
flag는 이름의 형식이며, flag{firstname lastname}, "Garry Sartoris"에게 가짜 이메일을 보낸 사람을 찾으면 된다.<br><br>

![2](https://github.com/user-attachments/assets/b54fa832-bfdb-4241-8180-fb50fb8703d4)<br><br>

위 사진은 Wireshark(https://www.wireshark.org/download.html)를 통해 가짜 로그인 페이지 tcp stream을 따라간 패킷 중 하나의 내용이다.<br>
이메일을 보낸 사람은 IT Suport Manager인 **William Hadderly**로 나왔으며 우리가 원하는 flag에 대한 값이다.<br><br>

flag{William Hadderly}
