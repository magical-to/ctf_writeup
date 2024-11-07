본 게시물은 2024년에 진행된 DEADFACE CTF 2024의 Forensic 부문에 관련된 문제에 대한 해설을 품고 있습니다.<br><br>

![1](https://github.com/user-attachments/assets/c2d9cdf8-ed89-4d4a-badb-08d9f04642d9)<br><br>

문제 설명 : <br>
우리는 Garry Sartoris(또 너야~)가 TGRI에서 제공한 작업용 노트북과 규정을 준수하지 않는 Windows 호스트를 사용하고 있다고 의심하고 있다.<br>
DEADFACE가 유출한 데이터에서 이를 확인할 방법이 있을까?<br>
Garry Sartoris의 머신에 대한 Windows 제품 ID를 알아내면 되는 문제이다.<br><br>

![2](https://github.com/user-attachments/assets/ebef8a9a-e923-4db4-9ef9-0203737017de)<br><br>

해당 패킷을 살펴보게 되면, UDP 패킷 내에 Windows 관련 내용이 있는 것을 확인할 수 있다.<br><br>

![3](https://github.com/user-attachments/assets/5d5d5f70-f6fa-43c7-832f-913097881a02)<br><br>

WindowsRegisteredOwner 부분을 살펴보게 되면 "Garry Sartoris"의 PC임을 알 수 있고, 해당 PC에 대한 WindowsProductID또한<br>
00326-10000-00000-AA973이라는 것을 확인할 수 있게 된다.<br><br>

문제에서 원하는 flag가 Windows 제품 ID이므로, flag 값은<br><br>

flag{00326-10000-00000-AA973}이 되게 된다.
















