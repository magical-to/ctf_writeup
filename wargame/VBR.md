해당 글은 Dreamhack(https://dreamhack.io/)의 포렌식 문제 중 하나인 'VBR'의 풀이를 담고 있습니다.<br><br>

VBR 문제 주소 : https://dreamhack.io/wargame/challenges/1188<br><br>

문제 설명 : <br>
주어진 VBR을 분석하고, 플래그를 계산하시오.<br>
FLAG = DH{(A + B + C)} (단, 더한 값을 십진수로 변환할 것)<br>
A: 파일시스템이 FAT32면 1, NTFS면 2<br>
B: 해당 볼륨의 크기<br>
C: 볼륨 시리얼 번호<br>
예를 들어 파일시스템이 NTFS, 볼륨의 크기가 0x100000, 그리고 볼륨 시리얼 번호가 0x12341234면, 2 + 0x100000 + 0x12341234 = 0x12441236 = 306450998 (십진수) 이므로 DH{306450998} 을 제출하시면 됩니다.<br><br>

사용할 도구 : Hxd(https://mh-nexus.de/en/hxd/)<br><br>

문제 파일을 다운 받고 압축을 풀게 되면 vbr.bin이라는 파이너리 파일이 존재한다.<br>
해당 파일을 HxD에 던져놓아보자.<br><br>

![2](https://github.com/user-attachments/assets/543a0238-12dd-4552-aabd-fb08060b197d)<br>
문제 파일을 HxD에 던진 직후의 모습이다. 우측 Decoded text에 보면 FAT32라고 쓰여져 있는 것이 보인다.<br>
문제에서, A: 파일시스템이 FAT32면 1, NTFS면 2이기 때문에 **A의 값은 1**이 되게 된다.<br><br>

![1](https://github.com/user-attachments/assets/ad70b327-5222-43ce-a0e3-358fd17f9491)<br>
다음으로는 FAT32의 파일 구조를 살펴볼 것이다.<br>
우리가 구해야 하는 값은 해당 불륨의 크기(B)와 불륨 시리얼 번호(C)이기 때문에<br>
0x20줄의 글은 Dreamhack(https://dreamhack.io/)의 포렌식 문제 중 하나인 'VBR'의 풀이를 담고 있습니다.<br><br>

VBR 문제 주소 : https://dreamhack.io/wargame/challenges/1188<br><br>

문제 설명 : <br>
주어진 VBR을 분석하고, 플래그를 계산하시오.<br>
FLAG = DH{(A + B + C)} (단, 더한 값을 십진수로 변환할 것)<br>
A: 파일시스템이 FAT32면 1, NTFS면 2<br>
B: 해당 볼륨의 크기<br>
C: 볼륨 시리얼 번호<br>
예를 들어 파일시스템이 NTFS, 볼륨의 크기가 0x100000, 그리고 볼륨 시리얼 번호가 0x12341234면, 2 + 0x100000 + 0x12341234 = 0x12441236 = 306450998 (십진수) 이므로 DH{306450998} 을 제출하시면 됩니다.<br><br>

사용할 도구 : Hxd(https://mh-nexus.de/en/hxd/)<br><br>

문제 파일을 다운 받고 압축을 풀게 되면 vbr.bin이라는 파이너리 파일이 존재한다.<br>
해당 파일을 HxD에 던져놓아보자.<br><br>

![2](https://github.com/user-attachments/assets/543a0238-12dd-4552-aabd-fb08060b197d)<br>
문제 파일을 HxD에 던진 직후의 모습이다. 우측 Decoded text에 보면 FAT32라고 쓰여져 있는 것이 보인다.<br>
문제에서, A: 파일시스템이 FAT32면 1, NTFS면 2이기 때문에 **A의 값은 1**이 되게 된다.<br><br>

![1](https://github.com/user-attachments/assets/ad70b327-5222-43ce-a0e3-358fd17f9491)<br>
다음으로는 FAT32의 파일 구조를 살펴볼 것이다.<br>
우리가 구해야 하는 값은 해당 불륨의 크기(B)와 불륨 시리얼 번호(C)이다.<br>
0x20줄의 00부터 03까지 있는 Total Sector 32를 살펴보면 되는데, 대부분의 디스크 구조는 리틀엔디안으로 이루어져있기 때문에<br>
0x00 80 3E 00 -> 0x00 3E 80 00 -> 0x3E8000 -> 4,096,000 이다.<br><br>

여기서 조금 복잡할 수 있는데, <br>
보통 볼륨의 크기를 나타내는 단위는 바이트 단위이므로 섹터 단위에서 바이트 단위로 바꿔줘야한다.<br>
위 사진에서의 Byte per Sector는 0x00의 10.5 ~ 12.5 사이에 존재한다.<br>
1개의 섹터가 갖는 바이트는 0x00 02 이다.<br>
이 또한 리틀엔디안이므로 0x00 02 -> 0x02 00 -> 0x200 -> 512 이다.<br>
그러므로 볼륨의 크기 = 섹터의 개수 * 섹터당 바이트 = 4,096,000 * 512 = 2,097,152,000 이다.<br><br>

따라서, **B의 값은 2,097,152,000**이다.<br><br>

마지막으로 구해야하는 불륨 시리얼 번호는 0x40 줄의 'Volume ID'이다.<br>
0x40 줄의 03-06 까지의 값을 리틀엔디안으로 더해 주면 그 값이 C이다.<br>
그렇게 되면 0x8A EE A8 0E 이고 중요한건 시리얼 넘버 또한 리틀엔디안으로 표기되기에 변환을 해줘야 한다.<br>
0x8A EE A8 0E -> 0x0E A8 EE 8A -> 245,952,138 이다.<br><br>

따라서, **C의 값은 245,952,138**이다.<br><br>

A = 1, B = 2,097,152,000, C = 245,952,138<br>
A와 B와 C를 전부 더해주면 된다.




