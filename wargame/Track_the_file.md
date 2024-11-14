해당 글은 Dreamhack(https://dreamhack.io/)의 포렌식 문제 중 하나인 'Track_the_file'의 풀이를 담고 있습니다.<br><br>

Track_the_file 문제 주소 : https://dreamhack.io/wargame/challenges/1325<br>
포렌식 문제 자료 주소 : https://dreamhack.io/lecture/forensics-materials<br><br>

문제 설명 : <br>
드림이는 컴퓨터를 살펴보다가 수상한 점을 발견했습니다.<br>
바로 malware.exe라는 프로그램이 컴퓨터에 생성되어 있다는 것이었어요.<br>
드림이는 누군가가 USB를 연결해 파일을 복사해온 것으로 추측하고 있습니다.<br>
시스템 로그를 분석해 malware.exe 파일이 시스템에 복사된 시간을 찾아보세요!<br><br>

FLAG = DH{yyyy_MM_dd_hh_mm_ss}<br>
yy, MM, dd, hh, mm, ss는 시간을 표현하는 방식으로 각각 연, 월, 일, 시, 분, 초를 나타냅니다.<br>
예를 들어 시간이 2024-01-02 03:04:05라면, FLAG는 DH{2024_01_02_03_04_05}입니다.<br>
시간은 UTC+9를 기준으로 합니다.<br><br>

사용할 도구 : FTK Imager(https://www.exterro.com/ftk-product-downloads/ftk-imager-4-7-3-81), NTFS log Tracker(https://sites.google.com/site/forensicnote/ntfs-log-tracker)<br><br>

1. malware.exe<br>
2. '파일을 복사해 온 것으로 추측'<br>
3. '시스템 로그를 분석'<br><br>

세 가지 힌트를 바탕으로, 우리는 시스템 로그를 분석을 해야 한다.<br><br>

시스템 로그를 분석하기 위해서는 $LogFile과 $UsnJrnl을 이용한 문제이다.<br><br>

![2](https://github.com/user-attachments/assets/19dcffd5-4f6e-47d7-b7fb-00556fea449a)<br>
root 디렉토리 아래에서 $MFT와 $LogFile을 줍줍하고, Extend 디렉토리 아래에서 $J 파일을 줍줍할 것이다.<br><br><br>


간단하게 설명 들어가자면,<br>
[$LogFile]<br>
저널링(Jounaling)<br>
데이터 변경을 디스크에 반영하기 전에 행위를 기록하여 추후 오류 복구에 활용한다.<br>
데이터를 기록하는 동안 시스템에 문제가 생기면 데이터가 손실되므로 문제가 발생하기 전에 "어떤 데이터를, 언제, 어디에 쓰는지"를 기록한다.<br>
문제가 발생하면 기록을 토대로 작업이 이루어지기 전 상태로 시스템을 복원한다.<br><br>

트랜잭션(Transaction)<br>
"쪼갤 수 없는 업무 처리의 최소 단위"로 파일이나 디렉토리 생성, 수정, 삭제, MFT 레코드 변경 등의 이벤트 등을 말한다.<br>
$LogFile에는 메타 데이터의 트랜잭션 저널 정보가 들어있다. 메타 데이터는 파일이 가지고 있는 속성 데이터이다.<br><br>

[MFT(Master File Table)]<br>
MFT는 NTFS 파일 시스템에서 파일, 디렉터리를 관리하기 위한 구조이다.<br>
하나의 파일당 하나의 MFT 엔트리를 가지며, $MFT는 MFT 엔트리들의 집합을 말한다.<br>
이때, $는 Windows 환경에서의 시스템 파일을 의미한다.<br>
MFT 엔트리는 파일의 이름, 생성·수정·변경시간, 크기, 속성 등을 가지고 있으며 파일의 디스크 내부 위치, 파일의 시스템 경로를 알 수 있다.<br><br><br>


각각의 파일을 추출한 뒤,<br>
![1](https://github.com/user-attachments/assets/d42624e1-6fbd-4490-bc34-28e59cc3abe2)<br>
NTFS Log Tracker를 킨다.(UI가 조금 튀어나간 건 감성이다.)<br><br>

빼낸 $LogFile과 $UsnJrnl:$J, $MFT 파일을 각각 넣어주면 된다.<br><br>

![3](https://github.com/user-attachments/assets/ac03a8df-be1b-4e60-91cd-98a3f4963614)<br>
이렇게 이쁘게 넣어줬으면, 파싱을 하면 된다!<br><br><br>


![4](https://github.com/user-attachments/assets/01395a08-bb7f-42e7-ad5d-9d67f04eff90)<br>
아래 나온 결과에서 Search 기능을 이용해 malware를 검색해주고 malware.exe 파일을 찾아내면 된다.<br>









