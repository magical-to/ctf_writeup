본 게시물은 2024년에 진행된 DEADSPACE CTF 2024의 Steganopraphy 부문에 관련된 문제에 대한 해설을 품고 있습니다.<br><br>

![1](https://github.com/user-attachments/assets/ee3a485b-a765-49a4-98e4-de12ff03e0f1)<br><br>
우선, 문제를 해석해보자면<br>
lamia415가 daem0n에게 비밀 정보를 담은 이미지를 보냈다.<br>
이 정보는 그들이 누구를 또는 무엇을 대상으로 캠페인을 준비하고 있는지에 대한 내용을 포함하고 있다.<br>
Turbo Tactical은 DEADFACE의 공격 대상이 될 수 있는 개인 또는 기업에 대비하기 위해 이 정보를 파악하고자 한다. 숨겨진 메시지를 찾아 플래그를 제출해라<br>
정도가 되겠다.<br><br>

결론만 말하자면, 플레이어는 GhostTown에서 관련 대화를 찾을 수 있다.<br>
GhostTown 스레드에는 이미지를 보여주고 숨겨진 데이터를 추출하는 데 사용된 비밀번호가 표시되게 된다.<br><br><br>


![2](https://github.com/user-attachments/assets/d1bdfb97-f525-4d2b-94cb-f8c61afef5c6)<br>
사진에는 여러명의 사람들이 모여있는 모습과 그 밑에 'Yes, the password is our basic **d34df4c3** password.'라고 쓰여져 있다.<br><br>

우리는 숨겨진 파일을 얻어내기 위해 **steghide**를 사용할 예정이다.<br><br>

steghide(https://steghide.sourceforge.net/)<br><br>

steghide extract -sf img20240803.jpg 명령어를 입력하게 되면 <br><br>

유저는 비밀번호 입력을 요청받게 될 것이고, GhostTown 포럼 스레드에 다르면 비밀번호는 **d34df4c3**이다.<br><br>

이 비밀번호를 입력하게 되면 secret.txt.gz 파일이 추출되고 이 파일을 압축 해제해야 한다.<br><br>

gunzip secret.txt.gz gunzip 명령어를 사용하여 파일을 압축 해제하게 된다면 아래와 같은 내용을 얻을 수 있다.<br><br>

Hope you're ready for some fun.<br>
I'm currently at the company off-site morale event, and it's the perfect opportunity to gather intel.<br>
I'll be sending you the details of some of my coworkers soon.<br>
With their info, you can craft some wicked social engineering campaigns.<br>
Get ready to make them dance to our tune.<br><br><br>


flag{S0c14l_3ng1neer1ng_1nt3l_fr0m_0ff-s1t3}
