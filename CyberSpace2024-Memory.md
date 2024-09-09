**해당 라이트업은 CyberSpace2024 대회에서의 Forensic 분야의 Memory 문제의 풀이를 담고 있습니다.<br><br><br><br>**



![1](https://github.com/user-attachments/assets/8052b775-1be1-4753-b3e1-56f543490c29)<br>
mem.dmp 파일은 MS Windows 64비트 크래시 dump 파일이기 때문에 string으로 변환하여 분석을 위해 텍스트 파일로 저장하고자 하였다.<br><br>

![2](https://github.com/user-attachments/assets/e1c19a6f-00c9-4117-a22e-5b32551727c6)<br>
flag를 기반으로 검색을 하던 도중 흥미로운 것을 발견하였다.<br><br>

여기서 주목할 점은 flag.jpg와 flag.enc이다. flag.jpg는 삭제되었지만, flag.enc는 암호화되었다.<br>

1. $ifPath : 데스크탑 폴더 경로와 파일명 flag.jpg를 결합한다. 이 경로는 원본 파일인 flag.jpg를 가리킨다.<br><br>
2. $efPath: 데스크탑 폴더 경로와 파일명 flag.enc를 결합한다. 이 경로는 flag.jpg의 암호화된 버전을 저장하는 데 사용된다.<br><br>
3. AES 암호화 설정: 키 사이즈, 블록 사이즈, AES 키, IV 키 등과 같은 암호화 설정이 있다.<br><br>
4. $cee = [System.Convert]::ToBase64String($aes.Key): AES 키를 Base64 문자열로 변환하여 $cee에 저장한다.<br><br>
5. $vee = [System.Convert]::ToBase64String($aes.IV): AES IV를 Base64 문자열로 변환하여 $vee에 저장한다.<br><br>
6. [System.IO.File]::WriteAllText($efPath, $encryptedBase64): Base64로 인코딩된 암호화 데이터를 데스크탑의 flag.enc라는 파일에 저장한다.<br><br>
7. Base64로 인코딩된 암호화 데이터(ENCD), AES 키(ENCK), 그리고 IV(ENCV)를 환경 변수로 저장한다.<br><br>
8. if (Test-Path $ifPath) { Remove-Item $ifPath -Force }: 원본 flag.jpg가 존재하면 강제로 삭제한다.<br><br>

즉, 여기서 얻을 수 있는 결론은 : ENCD는 flag.jpg의 Base64로 인코딩된 암호화된 내용을 담고 있다는 것이다.<br>
암호화된 플래그를 나타내지만, 직접 읽을 수 있는 형식은 아니며 원본 flag.jpg를 복원하려면 AES 키(ENCK)와 IV(ENCV)를 사용하여 데이터를 복호화해야 한다.<br><br>

flag.enc 파일또한 Memory Dump에 존재하지 않았다. ENCD ENCK와 ENCV는 Windows 환경 변수에 설정되어 있을 가능성이 있다.<br><br>

python3 vol.py -f mem.dmp windows.envars.Envars (windows.envars.Envars plugin helps to scan and extract Windows Environment Variables)<br><br>
해당 명령어는 메모리 덤프 파일(mem.dmp)에서 Windows 환경 변수(Environment Variables)를 추출하는 역할을 한다.<br><br>
python3 : Python 3를 실행하는 명령어<br>
vol.py : Volatility 메모리 포렌식 툴을 실행하는 스크립트<br><br>
-f mem.dmp: 분석할 메모리 덤프 파일을 지정하는 옵션입니다. 여기서는 mem.dmp라는 파일을 사용<br><br>
windows.envars.Envars: Volatility 플러그인 중 하나로, Windows 환경 변수를 스캔하고 추출하는 역할<br><br><br>


![4](https://github.com/user-attachments/assets/e07faf37-0df1-46fc-8705-323ceac21697)<br><br>

![5](https://github.com/user-attachments/assets/fc5a54f4-8826-4430-bb4c-cff511a934e8)<br><br>
위 명령어 덕분에 ENCD, ENCK, ENCV 값을 획득할 수 있다.<br><br>

![6](https://github.com/user-attachments/assets/10a35be6-0408-4bce-b5a3-35a6b9f12c6c)<br>
이제 각 값을 decrypt한다.<br><br>

![7](https://github.com/user-attachments/assets/6072c6b8-10eb-4d08-afe3-ac553a25aa30)<br><br>

스크립트를 돌리게 되면 헤더가 없는 flag.jpg라는 파일을 얻을 수 있으며,<br><br>

아래 사이트를 이용해 ENCD의 값을 넣으면 flag 값을 획득할 수 있다.<br><br>

(https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true,false)AES_Decrypt(%7B'option':'Base64','string':'dF3luZxgMqMjdv26DTzAZqhRHyQsLOiQCajdl6IapdE'%7D,%7B'option':'Base64','string':'A8701A28A919CBYf1YXfocPY/iDTpVUsfklA%3D%3D44D2769846608DA3AE'%7D,'CBC/NoPadding','Raw','Raw',%7B'option':'Hex','string':'EF56C829E0B1A510F3CB5EC18E3B5141'%7D,%7B'option':'Hex','string':''%7D)&oeol=FF)<br><br>

![flag](https://github.com/user-attachments/assets/75698ae2-18b9-45ef-83ac-e56d009c2f78)<br>









