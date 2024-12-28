Challenge Category : Forensics<br>
Challenge Name : Forgot Password<br><br>

I can't login now and to change the password I need security questions but I don't remember this guy. Can you help me recover them?<br>
비밀번호를 까먹어서 로그인을 하지 못하는 상태이고, 비밀번호를 변경하기 위해서는 보안 질문들이 필요로 하는데 이조차 기억을 못하는 상태에서 복구를 도와줘야 하는 문제이다.<br><br>


![1](https://github.com/user-attachments/assets/3c17fd47-c980-4e59-8485-b32b4b98034b)<br><br>

문제를 마주쳤을 때, SAM 레지스트리 Hive를 떠올렸다.(https://www.igloo.co.kr/security-information/%EC%9C%88%EB%8F%84%EC%9A%B0-%EB%A0%88%EC%A7%80%EC%8A%A4%ED%8A%B8%EB%A6%AC-%EB%B6%84%EC%84%9D%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EC%B9%A8%ED%95%B4%EC%82%AC%EA%B3%A0-%EB%B6%84%EC%84%9D-%EA%B8%B0)<br>
SAM은 사용자의 비밀번호를 저장하는 윈도우 시스템에서 사용하는 데이터베이스 파일이다. 시스템 및 원격 로그인을 진행할 때 윈도우 시스템은 SAM 파일을 참조하여 인가되지 않은 사용자의 접근을 제한한다.<br><br>

![image](https://github.com/user-attachments/assets/b807aa0f-1323-4ce3-8394-a662e141b4a9)<br>
FTK Imager를 사용하여 SAM Hive를 추출하였다.<br><br>

![image](https://github.com/user-attachments/assets/5281412a-38ba-42b2-843a-2cb173ec7e87)<br>
 그리고, SAM Hive를 파싱하기 위해 RegRipper 툴을 사용하였다.(갓릭 짐머만 또 당신입니까?)<br><br>

![image](https://github.com/user-attachments/assets/aec3e5a6-80a4-4541-856b-1b75392dc1a3)
다음과 같이 Question과 Answer이 나오는데, Answer 1부터 Answer 3를 이어 붙이게 되면,<br>
Flag : wwf{I_love_security_questions_s0_muChhhhhhhhhhhhhhhhh}가 나오게 된다.<br>
