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

즉, 여기서 얻을 수 있는 결론은 : ENCD는 flag.jpg의 Base64로 인코딩된 암호화된 내용을 담고 있다.<br>
이것이 암호화된 플래그를 나타내지만, 직접 읽을 수 있는 형식은 아니며 원본 flag.jpg를 복원하려면 AES 키(ENCK)와 IV(ENCV)를 사용하여 데이터를 복호화해야 한다.<br><br>

flag.enc 파일또한 Memory Dump에 존재하지 않았다. 운좋게도 ENCD ENCK와 ENCV는 Windows 환경 변수에 설정되어 있을 가능성이 있다.<br><br>

python3 vol.py -f mem.dmp windows.envars.Envars (windows.envars.Envars plugin helps to scan and extract Windows Environment Variables)<br>
다음과 같은 명령어를 실행하였다.<br><br>











