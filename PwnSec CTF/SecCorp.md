Challenge Category : Forensics<br>
Challenge Name : SecCorp<br><br>

Challenge description: SecCorp has been compromised, and we suspect the attackers used stealth tactics. As our top incident responder, your mission is to dive into the logs and uncover their hidden maneuvers, expose their strategies, and help us secure our defenses<br><br>

Flag Format:<br>
PWNSEC{full path of the malicious file_SHA1 of the malicious file _name of the file that the malicious file drops}<br>
Ex:PWNSEC{C:\hello.png_HASH_notmalicious.exe}<br>
Author: CMDJO_QAIS<br>
Hint : Some Osint is needed<br>
Solution: The challenge focuses on Windows Event Logs<br><br>

대충 문제 설명을 보자면, SecCorp가 침해되었습니다. 공격자가 은밀한 전술을 사용한 것으로 의심됩니다. 최고의 사고 대응 전문가로서, 로그를 철저히 분석하여 숨겨진 공격 수법을 밝혀내고, 공격자의 전략을 드러내며 우리의 방어를 강화하세요라고 한다.<br><br>

힌트를 보면 Osint를 사용하며 이 문제는 Windows 이벤트 로그를 분석하는 것에 초점을 둔다고 되어있다.<br><br>

![image](https://github.com/user-attachments/assets/7c87c154-21ff-486a-a913-763ef729c638)<br>
플래그 요구사항을 보면 SHA1이 필요하다는 것을 알 수 있다.<br>
조사한 결과, Windows Defender나 Sysmon 파일에서 SHA1을 추출할 수 있다는 것을 알 수 있다.<br>
로그를 분석하는 과정에서 Microsoft-Windows-PowerShell_Operational.evtx 파일을 확인할 수 있었는데<br><br>

![image](https://github.com/user-attachments/assets/0642c6f2-7e8a-45cc-8fb6-dc6f9b2d5cd1)<br><br>
위 사진을 보면,<br>
해당 로그에서는 lsass.dll 파일을 System32 폴더로 복사하는 작업이 관찰되었으며, 이는 의심스러운 친구이다.<br>
원래 lsass 파일의 이름은 lsass.exe이며, DLL 형식이 아니기 때문이다. 이후, 이 파일을 레지스트리에 추가하여 무언가를 하려는 행동도 보였다.<br>
그 다음으로, Microsoft-Windows-Windows Defender_Operational.evtx 로그를 확인하여 Windows Defender가 이 활동을 탐지했는지, SHA1 해시를 추출할 수 있는지 확인해보았다.<br><br>

![image](https://github.com/user-attachments/assets/6276a9a6-ce35-4fd5-8169-4ab3c7963fff)<br><br>
예상한 대로 Windows Defender가 이를 탐지한 것을 확인할 수 있었다. 또한 악성 파일의 전체 경로도 찾아냈다 : C:\Windows\System32\lsass.dll<br><br>

이제 SHA1만 구하면 된다! 앞서 언급했듯이, Windows Defender나 Sysmon에서 SHA1을 얻을 수 있다. 그러나 Windows Defender에서는 SHA1을 확인할 수 없었고 Sysmon 로그 파일도 없었다. 문제 작성자가 제공한 힌트에 따르면 Osint가 필요하다고 했는데 여기서 사용하면 되지 않을까 싶다.<br>
따라서 Google에서 Threat Name: TrojanSpy:Win64/Stealer!MTB를 검색해보자.<br><br>

![4](https://github.com/user-attachments/assets/9a853154-9c63-41e1-81d9-138053eabc48)<br><br>

![5](https://github.com/user-attachments/assets/18b54530-41e3-4bc0-b6fc-9488f2f0e9ea)<br><br>

위 두 사진은 구글에 검색한 결과이다.<br>
NPPSPY.dll 파일을 발견했고, 이 파일이 TrojanSpy:Win64/Stealer!MTB와 연관된 유일한 파일임을 볼 수 있다!<br><br>

Google에서 NPPSPY.dll과 PSBits를 검색한 결과, NPPSPY.dll과 관련된 GitHub 레포가 보였다.<br>
https://github.com/gtworek/PSBits/tree/master/PasswordStealing/NPPSpy<br><br>

설치 과정이 이전에 확인한 lsass.dll 설치와 유사하다는 것을 눈치챌 수 있다.<br><br>

NPPSPY.dll 파일을 다운로드한 뒤, 명령어 : **sha1sum NPPSPY.dll**를 통해 SHA1 해시를 확인할 수 있다.<br><br>

결과적으로 SHA1 해시는 5e84941be2c10ecec9d796211196fca10e0834dd이었다.<br><br>

세 번째 요구사항은 악성 파일이 생성하는 파일의 이름인데 SHA1 해시를 VirusTotal(https://www.virustotal.com/gui/home/upload)에<br>
입력하여 조사한 결과, 생성된 파일은 NPPSpy.txt임을 알 수 있다.<br><br>

따라서 플래그는<br>
**PWNSEC{C:\Windows\System32\lsass.dll_5e84941be2c10ecec9d796211196fca10e0834dd_NPPSpy.txt}**


