Challenge Category : Misc<br>
Challenge Name : Pieces<br><br>

I found a weird file on one of our employee's devices along with a note that says, "Will you be able to assemble the pieces and reveal the secret message?". Des he think he is going to get paid by making CTF challenges instead of working???<br><br>

대충 문제 설명을 보자면, 직원 중 한 명의 기기에서 이상한 파일과 함께 다음과 같은 메모를 발견했습니다: "조각들을 맞추고 비밀 메시지를 밝혀낼 수 있을까요?" <br>
CTF 문제를 만들면서 돈을 벌 생각인 건가요? 일을 안 하고 말이죠???라는 내용이다.ㅋㅋㅋ<br><br>

![image](https://github.com/user-attachments/assets/20896570-99c2-47bf-84c1-d8f92644a556)<br><br>

문제에서는 pieces.zip 파일을 하나 주는데 text 파일을 포함하고 있다.<br><br>

5c62e091b8c0565f1bafad0dad5934276143ae2ccef7a5381e8ada5b1a8d26d2
bc8478052e3ca9de6522b003c9297f7a5319cc5e8477991b48a2402c8c5ced61
6a2a781c47a940d740f7f0e9872c9683088baa559e69a8da81fcad9ad650b990
481dc61a1bb7b3746b48abc1c76b109cecc88315b684317477e26bd9d023b0fd
7c162e1660c7cbb4297479da406a5104eb5824765aadd97ad3dd58c93553264e
4918f93c20b97051fed2fe5472610cda83e5fc5735d2407bd69f322bfe4ed79f
f553d31e321f86488de78fb54fd142482ce66758f4758ab8578598740d9e5588
2027b791c448468af66614f8233b0a305a25e7e1486400a9738395c912958575
330f599093d06de98b4d6e2c91bfb56da7cc2f30cf5005d4b733df4557998f30
863653956b3fa7d93708fb54441d829468982b29f8486eb830c3cc3744e770cb
9400d84df94d54e6acbb9efe8b94ddb51c9cf473a13866dc7b0130adda702f38
3c66b522ebc151a54dcb2b66e72e5d8c31e55b05efaaa4969a2a9b86d970702e
224afb3889c0b052839ca7126c42ddaf50772a6a708a0eb957444b8a680c5fd4
f4361aedcdc453c0da96276471cdae94467cab2ebd88b02c9086bf21530d6edc
8da67b2a949ffc2b197b08d481a68cb1cde0851c30496ecf5666f3d13ebab8c6
cdc070f0c79f59ee69f1a046977c0f40e9cba794c4889e0c6a4a1495e6283b15
58699633392cc29ca2941cba7ba3fe0bdabde1ea44ba810ce055b9910ff1824c
914909dbc1681ffc109d8f3985f4bb22c7b008443b51680a06ab87801c70dfeb
07993332ddd72d8b68bea706ac9692573f7ac9dd361ca30a55fcb7fcbfcda458
649aae446ebceb3b637826f92802ce08fcd9fbfb74b49fe708b4e4ec6d285205
5d900e9175b9ff80ba0b8760f9931382111fa63707c5c37a1c736ec92c651b3d
f53df578cdacacbe5c87fe848d4735c39234edd606ec6dadb4bfebc5bb8756fc
f538ec98530de67114a560d05130b1c96f81d98ce1e84df0a85124968e9a08ef
d6d9c244a6175c1cb2d754fc522c6ae3cefd5f1513d20a16eef81c9616e809e7
1d0cf15bc0cf4bdd1ce1f01b09348373b265b740a70660b7b88709f506d4c4ab
81dae1d1e874c1ced2df47bac30a679a2aada7b80f3d52e36335a6325975c549
bef61ae0d2056b0170b3f49b6ab8e166b371463b0cbacfbb31c9a24d36b1cb28
b3f99d08684f1ad1bc72c6013d865f9fb966fb9fedc2f49b26ebe36b6a5a3259
0528794f6bf8fbeea45c5e9247ec6d1a5d4b1f982af413e936c8907453ade4f0
d03d8771f1434b9207a0dcacc213fa9ae69c98eebe4fa3ed81bd3ebc34b70f98
7a6e768bec9812024059ef88677d98a5a853f78451f9018cd289ed21c116908f
51763613a0f887799e005bfbba34b0e51fbd50efbcdf0709fdb4555e5d3c1fd1
70b891a390d76f7330b82f0f3e9eeed2fbe9c667afb38bd75cafb3093b2de23a
593b0232c991f8eb7fdfe4e92a71226e40f20330e55c0602b8635f93dd5ca8e4
a0ce8dfa972be9ea81e6355c0fc72cb05d1ee2bc03915c6942c82b9f7ddadf3a
ac87341549192bba1b341cbbc98b94f2e15a32bfdee9b182f7744c8ae7797654
5b0a8dfc3701878ba517924de1264281b7b8f3a4b7ee554db2f247974ca45f2c<br><br>

![image](https://github.com/user-attachments/assets/684cd7e1-4df9-4be2-9364-d78e821aec38)<br><br>
https://hashes.com/en/tools/hash_identifier 여기 사이트의 도움으로 SHA256 해쉬라는 것을 알아냈다.<br><br>

다음은 https://crackstation.net/ 사이트로 가서 dec해볼거다.<br><br>

![image](https://github.com/user-attachments/assets/cf47921f-a372-4845-86aa-c8ad557e8679)<br>
근데... 위 4줄 빼고는 밑에가 다 실패했다.<br>
하지만 이를 통해 해시의 패턴을 발견할 수 있다. 잘 보면 각 해시의 줄은 플래그의 시작 부분 서브스트링에 대한 해시 값이라는 것을 눈치챌 수 있다. 이를 확인하기 위해, 문자열 값 **(PWNSE, PWNSEC, PWNSEC{)**에 E, C, {를 추가하고 해시 값을 생성했는데 역시나 이 값들은 다음 세 줄과 일치했다.<br>
이는 플래그가 문자 하나씩 구성된다는 것을 의미하며, 마지막 줄이 플래그 전체의 해시 값이라는 것을 알 수 있다.. 이를 알고 플래그를 문자 단위로 조합하는 방식으로 브루트포스를 진행한다.....<br><br>

모든 출력 가능한 문자를 현재까지 알게 된 플래그 부분에 하나씩 추가하고, 이를 해시한 뒤 파일의 해시 값과 비교하고 만약 일치한다면, 해당 문자가 현재 플래그의 다음 문자임을 알 수 있다. 그런 다음, 이 문자를 현재 플래그에 추가하는 형시긍로 스크립트를 짜보았다..<br><br>

```
import hashlib
import string

with open('pieces.txt', 'r') as f:
    hashes = [line.strip() for line in f]

current_flag = "" 

characters = string.printable.strip()

for i, target_hash in enumerate(hashes[len(current_flag):], start=len(current_flag) + 1):
    found = False
    for char in characters:
        candidate = current_flag + char
        candidate_hash = hashlib.sha256(candidate.encode()).hexdigest()
        
        if candidate_hash == target_hash:
            current_flag += char
            print(f"Found character {i}: {char}")
            found = True
            break
    
    if not found:
        print(f"Could not find a matching character for line {i}")
        break
        
print(f"Full flag: {current_flag}")
```
플래그는 다음과 같다!<br>
Flag: PWNSEC{L34V3_My_C0mpu73R_Y0u_5t4lk3R}
