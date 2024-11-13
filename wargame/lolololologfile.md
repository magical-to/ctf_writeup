해당 글은 Dreamhack(https://dreamhack.io/)의 포렌식 문제 중 하나인 'lolololologfile'의 풀이를 담고 있습니다.<br><br>

lolololologfile 문제 주소 : https://dreamhack.io/wargame/challenges/727<br><br>

문제 설명 : <br>
Someone deleted the PDF file which has flag!<br>
How can I recover it?<br><br>

문제는 인프런에 디지털 포렌식 강의를 무료로 올려주신 손지훈님이 제출하셨다.(팬이에요!)<br><br>

문제를 보면 누군아가 flag를 가지고 있는 PDF 파일을 지웠는데 그 복구를 물어보고 있다.<br>
이번에 사용할 도구는 FTK Imager(https://www.exterro.com/digital-forensics-software/ftk-imager-temp)이다.<br><br><br>


![1](https://github.com/user-attachments/assets/8c24a268-7b5f-44f5-84b1-8af40f5dfcb7)<br>
다운받은 문제 파일을 FTK Imager에 업로드한 직후의 사진이다. 그 중에서 root 디렉토리 안의 다양한 pdf 자료들이 있는데 삭제된 4개의 자료가 보인다.<br><br>

![2](https://github.com/user-attachments/assets/b21773ea-971a-4fbf-b6cf-d98227082a6d)<br>
unallocated space 디렉토리 아래에 몇가지 파일이 존재하는데, 그 중에서도 02067 파일이 PDF 헤더를 가지고 있으며<br>
"05082" 파일에 PDF 파일의 끝을 나타내는 푸터(footer)인"%%EOF"가 있는 것이 확인되는데, 삭제된 PDF 파일은 이 4개의 파일로 추측할 수 있다.<br><br>

이 4개의 파일을 Export Files 옵션을 통해 추출을 하고, 이제 HxD를 사용할 것이다.<br><br><br>


![3](https://github.com/user-attachments/assets/ca8ebe8c-9829-4e75-b5c1-5c5fa41c5025)<br>
HxD의 도구 기능을 보면, 파일을 연결해주는 기능이 존재하는데, 여기에 4 친구들을 다 넣어줄 것이다.<br><br>

![4](https://github.com/user-attachments/assets/ff5159cc-2bb1-474c-a6f2-2b421b638d00)<br><br>
4 친구들이 다 들어간 결과이다.<br><br>

빈 pdf 파일을 만들어 저장하고 그 파일에 이 4 친구들을 합치기 위해 확인을 누르면,<br><br>

![5](https://github.com/user-attachments/assets/b14a734e-f137-4b9f-b78a-0767adf7d654)<br>
다음과 같은 그림이 나온다.









