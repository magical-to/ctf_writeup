본 게시물은 2024년에 진행된 DEADSPACE CTF 2024의 Steganopraphy 부문에 관련된 문제에 대한 해설을 품고 있습니다.<br><br>

![1](https://github.com/user-attachments/assets/ad8cd659-3b91-49b4-ac0d-106474ee6b64)<br><br>

문제 설명)<br>
GhostTown에서 이상한 개의 이미지가 돌아다니고 있다.<br>
포럼 대화에 따르면, 이 이미지에는 lamia415가 De Monne Financial에서 추출한 데이터가 포함된 것 같다.<br>
대화의 맥락을 활용하여 무엇이 추출되었는지 확인보자.<br><br><br>


![2](https://github.com/user-attachments/assets/2cb7ab7f-1892-4044-8df5-03234455f9b8)<br><br>

GhostTown의 한 스레드에서 lamia415가 이 사진을 보여주며, 그녀의 개가 사료 그릇 위에 서 있는 사진이라고 주장한다.<br>
이는 사진에 겉으로 드러나지 않은 추가적인 정보가 숨겨져 있다는 암시로 해석할 수 있다.<br>
이미지를 더 면밀히 분석하거나 스테가노그래피와 같은 방법을 통해 눈에 보이지 않는 데이터를 찾아내야 할 가능성이 매우 높아 보인다.<br><br>

GhostTown 대화에 따르면, 해당 이미지는 De Monne 직원의 액세스 토큰을 탈취하는 데 사용되었다고 한다.<br><br>

binwalk나 기타 스테가노그래피 도구를 사용해 보더라도 효과가 없을 것이다. 왜냐하면 이 이미지는 IHDR 청크의 높이 값이 조작된 상태로, 이미지의 HEX 값을 분석해야 한다.<br><br>

이미지를 CyberChef에 로드하고 **"To Hexdump"** 레시피를 사용하면 아래와 같은 출력이 나타날 것이다.

이 HEX 데이터를 통해 IHDR 청크의 비정상적인 값을 확인하고, 이를 수정하여 숨겨진 정보를 추출할 수 있다. CyberChef를 사용한 HEX 값의 조작과 분석이 문제 풀이의 핵심 요소이다.<br><br>

![3](https://github.com/user-attachments/assets/2582105a-a48e-4c22-b429-53bbc7f40b10)<br><br>

노란색으로 강조된 바이트는 IHDR 청크를 나타낸다. 이미지의 너비는 00000010에서 시작하며, 00 00 04 00 (1024 픽셀)로 표시되어 있다.<br><br>

그 다음 8바이트가 이미지의 높이를 나타내며, 00 00 02 dd로 설정되어 있다. 녹색으로 강조된 부분은 CRC이다.<br><br>

CRC(순환 중복 검사)는 4바이트로, 청크 앞부분의 바이트에 대해 계산된다. 여기에는 청크 타입 코드와 청크 데이터 필드가 포함되지만, 길이 필드는 포함되지 않는다.<br><br>

CRC는 청크에 데이터가 없는 경우에도 항상 존재하며, 데이터의 무결성을 확인하는 역할을 한다.<br><br>

따라서, 청크의 앞부분이 변경되면 CRC 값도 재계산해야기 때문에 CyberChef 또는 다른 HEX 편집 도구에서<br>
청크 데이터를 수정한 후 CRC를 재계산하고 새로 얻은 CRC 값을 업데이트하면 파일의 무결성이 유지되면서 수정한 높이 값이 적용된 이미지를 볼 수 있다.<br><br>

이제 높이를 정상 값으로 변경하고 CRC 값을 재계산하여 이미지 파일을 복구하면, 숨겨진 데이터가 올바르게 표시될 것으로 보인다.<br><br>

높이 값을 변경하고 CRC를 재계산하기 위한 Python Script:<br><br>

import zlib<br><br>

ihdr_data = bytes.fromhex('4948445200000400000005000803000000')<br>
crc = zlib.crc32(ihdr_data) & 0xffffffff<br>
print(f'{crc:08X}')<br><br><br>


![4](https://github.com/user-attachments/assets/4fb58429-ef4f-499c-bd65-318b47b20286)<br><br>

bytes.fromhex 함수에서 사용되는 값은 전체 IHDR 청크(스크린샷에서 노란색으로 강조된 부분)를 포함해야 한다.<br>
이 IHDR에는 수정된 높이 값인 00 00 05 00이 포함되어 있다.<br><br>

위 스크립트를 실행하면 출력값은 EEB4D005로, 이 값이 새로운 CRC 값이므로 기존 CRC 자리(녹색으로 강조된 부분)에 넣어 이미지 파일을 수정하면 된다.<br><br>

CyberChef(https://gchq.github.io/CyberChef/)에서 Render Image 레시피를 사용하여 이미지를 렌더링을 하게 되면 수정된 높이 값과 재계산된 CRC를 적용한 후<br>
이 레시피를 실행하면 이미지가 완전히 드러나게 된다.<br><br>

이제 숨겨진 데이터나 메시지가 포함된 전체 이미지를 아래와 같이 볼 수 있다.<br><br><br>


![5](https://github.com/user-attachments/assets/bae97bbc-4628-4fc1-9fdd-60d30409ec21)
