![image](https://github.com/user-attachments/assets/f94b44a8-b031-4015-9b70-f2014be3eead)<br><br>

Insert Guessy forensics challenge description here라고 한다.<br><br>

```
jjgwlsry@ma-gical dist-notsus % /Users/seo/Downloads/bkcrack-1.7.1-macOS-arm64/bkcrack -C files.zip -c notsus.exe -p ./notsus.exe.bin -b "?p"
bkcrack 1.7.1 - 2024-12-21
[14:25:10] Z reduction using 1048569 bytes of known plaintext
5.3 % (55667 / 1048569) 
[14:25:11] Attack on 174 Z values at index 993603
Keys: d1608c35 d11d350a 4bc3da9c
100.0 % (174 / 174)
Found a solution. Stopping.
[14:25:12] Keys
d1608c35 d11d350a 4bc3da9c
[14:25:12] Recovering password
length 0-6...
length 7...
length 8...
length 9...
length 10...
length 11...       
length 12...         
Password: 21SZh=PC89Zb
19.1 % (1728 / 9025)
Found a solution. Stopping.
You may resume the password recovery with the option: --continue-recovery 323158202020
[14:25:25] Password
as bytes: 32 31 53 5a 68 3d 50 43 38 39 5a 62
as text: 21SZh=PC89Zb
jjgwlsry@ma-gical dist-notsus %
```
다음 코드를 사용하였다.<br><br>

bkcrack은 ZIP 파일의 클래식 암호화(Classic ZIP encryption)를 깨는 도구이다. 이 암호 방식은 오래된 방식이라 알려진 평문(known plaintext)을 알고 있다면 빠르게 크랙할 수 있다.<br><br>
ZIP 파일 안의 notsus.exe가 암호화되어 있다고 가정하고, 그 파일의 평문이 notsus.exe.bin이라고 하여 두 파일을 비교해 ZIP의 암호를 알아내는 방식이다.<br><br>

https://pylingual.io/view_chimera?identifier=2e34b3cc1a9a96a1d547b0068678243b7088b223fcefd6c03d0ecd71f9706c3f<br><br>

```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import os
import sys

def rc4(key: bytes, data: bytes) -> bytes:
    """
    RC4 알고리즘으로 data를 암호화/복호화하는 함수.
    암호화할 때와 복호화할 때 동일한 키를 사용하면 원본을 복원할 수 있습니다.
    """
    # Key-Scheduling Algorithm (KSA)
    S = list(range(256))
    j = 0
    for i in range(256):
        j = (j + S[i] + key[i % len(key)]) % 256
        S[i], S[j] = S[j], S[i]

    # Pseudo-Random Generation Algorithm (PRGA)
    i = j = 0
    result = bytearray()
    for byte in data:
        i = (i + 1) % 256
        j = (j + S[i]) % 256
        S[i], S[j] = S[j], S[i]
        K = S[(S[i] + S[j]) % 256]
        result.append(byte ^ K)

    return bytes(result)

def decrypt_yorm_file(yorm_path: str, key: bytes):
    """
    주어진 .yorm 파일을 복호화하여 원본 파일을 생성하고,
    복호화가 완료되면 .yorm 파일은 그대로 두거나 사용자가 직접 삭제하게 둡니다.
    """
    if not yorm_path.lower().endswith('.yorm'):
        print(f"[오류] 파일 확장자가 '.yorm'이 아닙니다: {yorm_path}")
        return

    # 원본 파일명 추출 ('.yorm' 확장자 제거)
    original_path = yorm_path[:-5]  # 마지막 5글자('.yorm')를 잘라냄

    # .yorm 파일 읽기
    try:
        with open(yorm_path, 'rb') as f:
            encrypted_data = f.read()
    except Exception as e:
        print(f"[오류] '{yorm_path}' 파일을 읽을 수 없습니다: {e}")
        return

    # 복호화 수행
    decrypted_data = rc4(key, encrypted_data)

    # 복호화된 데이터를 원본 파일명으로 저장
    try:
        with open(original_path, 'wb') as f:
            f.write(decrypted_data)
        print(f"[성공] '{yorm_path}' -> '{original_path}' 복호화 완료")
    except Exception as e:
        print(f"[오류] '{original_path}' 파일을 생성할 수 없습니다: {e}")

def main():
    """
    사용법:
        python3 decrypt_yorm.py <파일1.yorm> [<파일2.yorm> ...]
    예시:
        python3 decrypt_yorm.py secret.txt.yorm data.bin.yorm
    """
    if len(sys.argv) < 2:
        print("사용법: python3 decrypt_yorm.py <파일1.yorm> [<파일2.yorm> ...]")
        sys.exit(1)

    # RC4 키는 암호화 시 사용된 키와 동일하게 설정
    KEY = b'HACKED!'

    # 인자로 전달된 모든 .yorm 파일을 반복하여 복호화
    for path in sys.argv[1:]:
        if not os.path.isfile(path):
            print(f"[경고] 파일이 존재하지 않거나 경로가 올바르지 않습니다: {path}")
            continue
        decrypt_yorm_file(path, KEY)

if __name__ == "__main__":
    main()
```
코드를 바탕으로<br><br>

grey{this_program_cannot_be_run_in_dos_mode_hehe}가 나오게 된다.
