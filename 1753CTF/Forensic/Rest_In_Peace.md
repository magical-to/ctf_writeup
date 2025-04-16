# 🪦 Rest In Peace - Writeup

> **카테고리**: 포렌식 

---

## 🧩 문제 설명


> 우리 요원 중 한 명이 임무에서 돌아오지 않았습니다. 적에게 붙잡혀 사망한 것으로 확인되었습니다. 우리가 확보한 것은 이 백업 파일들뿐입니다. 어떻게 접근해야 할지는 모르겠지만, 그가 가족 중 한 사람의 이름을 보안용으로 사용한 것 같습니다.

---

## 🔍 문제 분석

게시문에서 backup 폴더를 확인하면 여러 파일과 포맷이 포함되어 있다.
data, index, keys, locks, snapshot 같은 포맷 이름을 고르고 검색하면 Restic 이라는 백업 도구의 문서가 남는다.

Restic 을 설치하고 백업 상태를 확인하기 위해 다음과 같은 명령을 사용하였다.

```bash
$ restic -r backup snapshots
```

하지만 비밀번호가 필요해 보인다....

```bash
enter password for repository:
```

이를 크랙해야 문제를 풀 수 있는 것으로 보인다.

---

## 🧠 해결 과정

이 파일이 모두 로컬에 있는 경우, 떠올릴 수 있는 것은 바로 **Brute Force**이다.<br>
https://github.com/juergenhoetzel/restic-bruteforce.

이 도구는 첨부된 meson 구성 파일을 사용하여 소스에서 빌드해야 한다.

```bash
$ meson setup builddir && cd builddir && meson compile
```

그런 다음 백업 폴더에서 필요한 암호화 정보를 **가져올 수 있다.**

```bash
$ jq < keys/608e4fa104ef6b656198bc470f980ab147662d6dd7032855b3d04ce399fc9a0b 
{
  "created": "2025-04-06T17:07:05.806434091Z",
  "username": "root",
  "hostname": "f834fc6fec8b",
  "kdf": "scrypt",
  "N": 32768,
  "r": 8,
  "p": 7,
  "salt": "vTvkPe/DpBiHfQ4Hp4loPfnx4Wu1vZR0ZCtf1SMCki5j8xaFXH7uopJkhdBrwNlYEqpjr5TH6Gh3zDgYEIRUCg==",
  "data": "53yWN39gmUZSiqOgdI4JxZ/9xxBhwP/zW144NqYFRvtObK2FwVQDHQpQt0uQNxvEqhHeKL45eLj/HH+aK6LXu/OKWII3Olk+5v3Sfvu0whCngKDFFDgWfPPMgT5oErujVTg2FEe+gu3a2OKRlQNBg9fT/Q6DJKd18MnzAhy57l71NSs9AtjoOjgVngxa/0q2MKzUALEiQC66UTL03vVZYw=="
}
```

그리고 해당 데이터를 사용하여 암호 해독을 수행할 수 있다.

우리에겐 좋은 이름 사전(dictionary) 하나만 있으면 된다.

구글에서 가장 먼저 추천하는 것은 다음 링크다:
https://raw.githubusercontent.com/huntergregal/wordlists/refs/heads/master/names.txt
이걸 사용해 보자....
속도가 빠르지 않기 때문에 약간의 인내심이 필요하다 ㅠ

```bash
$ time ./restic-brute -v -n 32768 -r 8 -p 7 vTvkPe/DpBiHfQ4Hp4loPfnx4Wu1vZR0ZCtf1SMCki5j8xaFXH7uopJkhdBrwNlYEqpjr5TH6Gh3zDgYEIRUCg== 53yWN39gmUZSiqOgdI4JxZ/9xxBhwP/zW144NqYFRvtObK2FwVQDHQpQt0uQNxvEqhHeKL45eLj/HH+aK6LXu/OKWII3Olk+5v3Sfvu0whCngKDFFDgWfPPMgT5oErujVTg2FEe+gu3a2OKRlQNBg9fT/Q6DJKd18MnzAhy57l71NSs9AtjoOjgVngxa/0q2MKzUALEiQC66UTL03vVZYw== <names.txt
```

명령어 결과는 다음과 같다:

```bash
Using parameters (N=32768, r=8, p=7) on 4 Threads
Checked 32 passwords
Checked 60 passwords
Checked 92 passwords
Checked 120 passwords
Checked 152 passwords
Checked 180 passwords
Checked 212 passwords
Checked 240 passwords
Checked 269 passwords
Checked 300 passwords
Checked 328 passwords
Checked 360 passwords
Checked 388 passwords
Checked 420 passwords
Checked 448 passwords
Checked 478 passwords
Checked 508 passwords
Checked 537 passwords
Checked 568 passwords
Checked 597 passwords
Checked 628 passwords
Checked 657 passwords
Checked 688 passwords
Checked 717 passwords
Checked 747 passwords
Checked 777 passwords
Checked 806 passwords
Checked 837 passwords
Checked 866 passwords
Checked 896 passwords
Checked 926 passwords
Checked 955 passwords
Checked 986 passwords
Checked 1015 passwords
Checked 1046 passwords
Checked 1075 passwords
Checked 1106 passwords
Checked 1135 passwords
Checked 1165 passwords
Checked 1195 passwords
Checked 1225 passwords
Checked 1254 passwords
Checked 1283 passwords
Checked 1314 passwords
Checked 1343 passwords
Checked 1373 passwords
Checked 1403 passwords
Checked 1433 passwords
Checked 1463 passwords
Checked 1493 passwords
Found: Christopher

real	4m14.304s
user	16m35.819s
sys	0m20.692s
```

Christopher라... 이제 우리는 **restic 저장소를 살펴볼 수 있다.**

```bash
$ restic -r backup --password-command "echo Christopher" snapshots
repository 83c0e793 opened (version 2, compression level auto)
created new cache in /Users/lukaszwronski/Library/Caches/restic
ID        Time                 Host        Tags        Paths  Size
------------------------------------------------------------------
389a509c  2025-04-06 20:02:12  AgentAlpha              /flag  16 B
------------------------------------------------------------------
1 snapshots
```

해당 명령은 **하나의 스냅샷만**을 보여주며,  
그 안에 어떤 파일이 들어 있는지 다음 명령어로 **확인할 수 있다.**

```bash
$ restic -r backup --password-command "echo Christopher" ls 389a509c
repository 83c0e793 opened (version 2, compression level auto)
[0:00] 100.00%  4 / 4 index files loaded
snapshot 389a509c of [/flag] at 2025-04-06 18:02:12.182221879 +0000 UTC by root@AgentAlpha filtered by []:
/flag1.txt
/flag5.txt
```

플래그 파일이라니 여기서 끝난 줄 알았지만,  
실제로 내용을 출력해보면 **가짜 플래그(fake flag)**가 나온다??????????????

```bash
$ restic -r backup --password-command "echo Christopher" dump 389a509c /flag1.txt
repository 83c0e793 opened (version 2, compression level auto)
[0:00] 100.00%  4 / 4 index files loaded
1753c{fake%      

$ restic -r backup --password-command "echo Christopher" dump 389a509c /flag5.txt
repository 83c0e793 opened (version 2, compression level auto)
[0:00] 100.00%  4 / 4 index files loaded
_flag}%  
```

플래그 2번부터 4번까지는 누락된 것처럼 보인다.
다행히도, 누군가 `prune` 명령을 실행하지 않았다면 Restic은 삭제된 스냅샷을 복구할 수 있다.
복구한 뒤에는 인덱스를 다음과 같이 재구성할 수 있다.

```bash
$ restic -r backup --password-command "echo Christopher" recover

repository 83c0e793 opened (version 2, compression level auto)
load index files
[0:00] 100.00%  1 / 1 index files loaded
load 4 trees
[0:00] 100.00%  4 / 4 trees loaded
load snapshots
done

found 3 unreferenced roots
saved new snapshot d4efceea

$ restic -r backup --password-command "echo Christopher" repair index
```

그런 다음 스냅샷 목록을 확인해보면, 하나가 아닌 두 개의 스냅샷이 표시된다.

```bash
repository 83c0e793 opened (version 2, compression level auto)
ID        Time                 Host                          Tags        Paths     Size
---------------------------------------------------------------------------------------
389a509c  2025-04-06 20:02:12  AgentAlpha                                /flag     16 B
d4efceea  2025-04-06 20:25:21  MacBook-Air.local  recovered   /recover
---------------------------------------------------------------------------------------
2 snapshots
```

이제 ls 명령어를 사용하면 모든 파일이 표시가 된다.

```bash
$ restic -r backup --password-command "echo Christopher" ls d4efceea
repository 83c0e793 opened (version 2, compression level auto)
[0:00] 100.00%  1 / 1 index files loaded
snapshot d4efceea of [/recover] at 2025-04-06 20:25:21.437775 +0200 CEST by hacker@MacBook-Air.local filtered by []:
/405d9e38
/405d9e38/flag1.txt
/405d9e38/flag2.txt
/405d9e38/flag3.txt
/405d9e38/flag4.txt
/405d9e38/flag5.txt
/a5170404
/a5170404/flag1.txt
/a5170404/flag3.txt
/a5170404/flag4.txt
/a5170404/flag5.txt
/c9663b07
/c9663b07/flag1.txt
/c9663b07/flag4.txt
/c9663b07/flag5.txt
```
---

## ✅ 최종 플래그

1753c{faked_my_own_death_to_save_the_flag

