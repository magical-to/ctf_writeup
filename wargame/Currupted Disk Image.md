해당 글은 Dreamhack(https://dreamhack.io/)의 포렌식 문제 중 하나인 'Currupted Disk Image'의 풀이를 담고 있습니다.<br><br>

VBR 문제 주소 : https://dreamhack.io/wargame/challenges/1189<br><br>

문제 설명 : <br>
디스크 이미지가 열리지 않습니다…!<br><br>

주어진 디스크 이미지를 복원하여 플래그를 구해주세요.<br><br>

Info<br>
FLAG: DH{something}<br>
something의 길이는 32자입니다.<br><br><br>


![1](https://github.com/user-attachments/assets/be1f809f-7ecd-450b-8e79-bfa1c0c56119)<br>
위 사진은 파일을 FTK Imager로 오픈을 한 직후의 사진이다.<br><br>

![2](https://github.com/user-attachments/assets/2fa1d16c-521c-4a6c-8083-0df060842d2b)<br>
파일을 보면 위쪽의 데이터들은 알 수 없는 데이터들이 있고, 맨 마지막을 살펴보면 EB 52 90으로 시작하고, 마지막 두 바이트가 0x55AA로 끝나는 것을 보면 NTFS의 파일 시스템이라는 것을 알 수 있다.<br>
파일의 0xD8FFe00 위치를 보면 EB 52 90 4E 54 46 53을 확인할 수 있는데, 이는 NTFS 파일 시스템의 VBR 시그니처임을 확인할 수 있다.<br>
NTFS 파일 시스템은 VBR의 복사본을 볼륨 끝에 저장하므로, 이 것은 복구용 VBR이다.<br><br>

FTK Imager의 Export Disk Image 기능을 이용해 raw 값으로 추출을 하고 HxD를 이용해 오픈해 볼 것이다.<br><br>

![3](https://github.com/user-attachments/assets/61991f13-0f84-4cf3-85ba-01f3596a18aa)<br>
NTFS 파일 시스템의 복구용 VBR을 복사하여 맨 위에 붙여넣는다.<br><br><br>


![4](https://github.com/user-attachments/assets/5ee9a90a-6fb0-418f-b5f9-f9d4785bbcc2)<br>
요롷게 나오면 된다. 이제 이 파일을 저장한 후, FTK Imager로 다시 열어보면...<br><br><br>


![5](https://github.com/user-attachments/assets/6678d77b-d0de-43b3-9d65-335cebea48b5)<br>
첫 사진과는 다르게 안의 내용물들이 보이게 된다.<br><br><br>

![6](https://github.com/user-attachments/assets/f517b781-75d6-427e-81ed-b3518abe122d)<br>
플래그를 구하는데 keyFile이 사용되므로 root에 있는 keyFile을 복호화해준다.<br><br>

HashHalc(https://hashcalc.en.download.it/)프로그램을 이용하여 keyFile을 복호화해준다.<br>
FTK Imager에서 keyFile을 뽑아내주고 그 파일을 HashHalc에 넣으면 된다.<br><br>

![7](https://github.com/user-attachments/assets/35e0bd7c-47f6-4f9d-b0f0-d2517b69389d)<br><br>






