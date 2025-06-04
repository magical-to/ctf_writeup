해당 글은 Dreamhack(https://dreamhack.io/)의 포렌식 문제 중 하나인 'Find the USB'의 풀이를 담고 있습니다.<br><br>

Find the USB 문제 주소 : https://dreamhack.io/wargame/challenges/1324<br>
포렌식 문제 자료 주소 : https://dreamhack.io/lecture/forensics-materials<br><br>

문제 설명 : <br>
드림이의 컴퓨터에 누군가가 USB 저장장치를 연결했다가 해제한 것 같아요.<br>
사건이 발생한 시간은 2024년 4월이라고 합니다. Windows 레지스트리를 분석해 연결된 USB 정보를 찾아낼 수 있을까요?<br><br>

메모리 덤프, 레지스트리 파일(예: SYSTEM, SOFTWARE, NTUSER.DAT)
레지스트리 파일은 System32의 Config 파일에 존재한다. Export Files를 통해 파일을 추출한 뒤,<br><br>

Registry Explorer로 이동하여 HKEY_LOCAL_MACHINE\SYSTEM\MountedDevices와 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USBSTOR을 찾아보면 된다.<br>
해당 문제에서는 USB 파일이 하나밖에 없었기 때문에 그대로 플래그를 제출하면 된다.
