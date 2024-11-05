본 게시물은 2024년에 진행된 DEADSPACE CTF 2024의 Steganopraphy 부문에 관련된 문제에 대한 해설을 품고 있습니다.<br><br><br>

![1](https://github.com/user-attachments/assets/c6262d8e-62c5-4d4e-a259-d83e249f13c0)<br><br>

문제 설명)<br>
DEADFACE는 Lytton Labs에서 민감한 사진을 얻어왔습니다.<br>
우리가 보기에 이 사진은 단순히 밤에 찍은 평범한 동네 사진일 뿐이지만 사진을 찍은 남자는 무언가 다른 것을 보았다고 주장했다.<br>
아래는 남자의 원래 트윗이며, 이후 그는 다음 이미지를 추가했다.<br><br>

![2](https://github.com/user-attachments/assets/48b17168-f4ce-46bd-b4a0-8d5488160e7b)<br><br>

![3](https://github.com/user-attachments/assets/67517b83-08dd-4f7c-949c-7798394e8ee7)<br><br>

낮은 투명도 설정으로 레이어가 겹쳐져 있는 플래그가 담긴 이미지를 받게 된다.<br>
이미지를 분석하여 숨겨진 텍스트를 확인하려면 Photoshop, GIMP, 또는 stegsolve와 같은 도구를 사용해야 한다.<br><br>

stegsolve 설치법 : <br>
wget http://caesum.com/handbook/Stegsolve.jar -O stegsolve.jar<br>
chmod +x stegsolve.jar<br><br>

stegsolve 실행법 : <br>
java -jar stegsolve.jar&<br><br>

GUI를 사용하여 didyouseeit.png 파일을 열어보게 되면,<br>
이 문제에 포함된 트위터(X) 게시물은 이미지의 빨강, 초록, 파랑 채널을 확인하라는 힌트를 제공한다.<br><br>

stegsolve 창 하단에 왼쪽과 오른쪽 버튼이 있다.<br>
오른쪽 버튼을 클릭하여 "Red plane 0" 또는 "Red plane 1"에 도달할 때까지 이동시키면 플래그가 명확하게 보인다.<br><br>

![4](https://github.com/user-attachments/assets/128a8bdb-b055-4e4f-9d94-bd7bf8755200)<br><br>

flag{ar3_we_410N3??}
