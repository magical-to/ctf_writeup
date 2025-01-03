Challenge Category : DFIR<br>
Challenge Name : Batman - The Dark Knight<br><br>

![2](https://github.com/user-attachments/assets/8300a60d-1ef5-4b57-9947-11fb892732c2)<br>
Description : <br>
Disaster strikes at Wayne Enterprises!<br>
A cyberattack orchestrated by an unknown adversary has tampered with Bruce Wayne's confidential research files.<br>
These files contained plans for advanced technology designed to fortify Gotham's defenses against its criminal underbelly.<br>
The hacker, who calls themselves The Silent Specter, didn't stop *maniuplating* the file —they also *deleted* it, making it seem like it never existed.<br>
However, Lucius Fox believes there’s still hope. You are brought in to assist.<br>
Using advanced forensic tools, it's up to you to dive into the system and uncover the tampered file by leveraging your investigation skills. pass: a1l4m<br><br>

번역해보자면, 웨인 엔터프라이즈에 재앙이 닥쳤다.<br>
정체불명의 적에 의해 조작된 사이버 공격이 브루스 웨인의 기밀 연구 파일을 손상시킨 상황이다.<br>
이 파일에는 고담시의 범죄를 막기 위해 설계된 첨단 기술 계획이 담겨 있었다.<br>
해커는 자신을 The Silent Specter라 부르며, 파일을 단순히 조작하는 데 그치지 않고, 삭제까지 해 파일이 존재하지 않았던 것처럼 만들어버렸다.<br>
하지만 루시우스 폭스는 여전히 희망이 있다고 믿고 있다. 당신은 도움을 주기 위해 초대받았고 첨단 포렌식 도구를 사용해 시스템에 깊이 들어가, 조작된 파일을 찾아내는 것이 당신의 임무이다.<br><br><br>


Autospy와 FTK Imager를 이용해 이미지 파일을 탐색해보았지만 갈피를 잡기 힘들었다.<br><br>

![3](https://github.com/user-attachments/assets/17d0c6fe-75cb-49c0-9b7f-16d2036d02b3)<br>
Arsenal Image Mounter를 사용하여 이미지를 **쓰기 권한(write access)**으로 마운트한 뒤, Shadow Explorer(다운로드 링크 제공)를 사용하여 마운트된 파티션을 탐색하였다.<br><br>

![4](https://github.com/user-attachments/assets/980a3c34-2d21-4ae9-b421-31433e7ffac8) ㄴ FTK Imager<br><br><br>

![5](https://github.com/user-attachments/assets/c3cda91d-326b-4280-bd0f-d15063ed43e6) ㄴ Shadow Explorer<br><br><br>

FTK Imager에서 확인했던 내용과는 다른 파일이 존재하였다. 바로 Notes에 있는 file.dat 파일이다.<br><br>
이를 $LogFile과 교차 확인하면, 삭제된 파일과 동일한 파일임을 확인할 수 있다.<br><br>

이 친구를 우클릭으로 후딱 추출해내서 임시 폴더에 넣어둔 뒤, 다음과 같이 입력한다.<br><br>

![7](https://github.com/user-attachments/assets/fc679f5d-5e11-4637-92ee-f2aa444f0bc3)<br>
dir /r 명령어는 Windows 명령 프롬프트에서 디렉터리 목록을 표시할 때, 파일의 대체 데이터 스트림(Alternate Data Stream, ADS) 정보를 함께 보여준다.<br><br>

참고로, 윈도우는 Powershell에서가 아닌 cmd에서만 가능하다.<br><br>
```
notepad file.dat:Zone.Identifier:$DATA
```
를 입력하고 나면 메모장에 다음과 같이 표시가 된다.<br><br>

![6](https://github.com/user-attachments/assets/6b7f5bd2-40f7-4cd0-ba76-2c1644ac1b6c)<br>
기다란 hex 값이 바로 플래그이다!
