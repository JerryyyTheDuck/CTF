WONKA-BAR
====
**WONKA-BAR 397 POINTS**

Lưu ý: đây là cách mình đã suy nghĩ xuyên suốt cả bài cho tới khi tìm thấy flag, nếu mọi người muốn nhanh gọn lẹ thì hãy nhảy tới TLDR giúp mình, mình xin cảm ơn 
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209469522-32e55670-0593-4a14-8702-67e5e2681bc7.png">
</p>

Bài này thuộc về phần Forensic, bài này khá thú vị. Bài này mình cảm ơn Bory rất nhiều nếu không có Bory thì chắc mình đã không solve được chal này.

**Link tải file:** [tại đây](https://github.com/P5ySm1th/CTF/blob/main/NiteCTF2022/Forensic/data/CandyStore.pdf)

Download file đề về thì ta có một file `CandyStore.pdf`. Mở ra thì có vẻ như nó có password.

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209469689-3352cea0-78e9-4ec0-b99b-9d099bc71e4d.png">
</p>

File đề thì không có hint hay mô tả, thế là mình đã bắt đầu **bruteforce** file thông qua [john](https://www.kali.org/tools/john/)
<ol>
    <li>dùng command pdf2john [file cần lấy hash] > [output]</li>
    <li>dùng command john --wordlisr=[địa chỉ chứa wordlist] [file chứa mã hash]</li>
</ol>

```
┌──(kali㉿kali)-[~/Desktop]
└─$ pdf2john CandyStore.pdf > pass.hash
```
```
┌──(kali㉿kali)-[~/Desktop]
└─$ john pass.hash --wordlist=/home/kali/Desktop/rockyou.txt  
Using default input encoding: UTF-8
Loaded 1 password hash (PDF [MD5 SHA2 RC4/AES 32/64])
Cost 1 (revision) is 3 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
13euro           (CandyStore.pdf)     
1g 0:00:01:14 DONE (2022-12-24 02:12) 0.01333g/s 176878p/s 176878c/s 176878C/s 13febcumple..13em1ly13
Use the "--show --format=PDF" options to display all of the cracked passwords reliably
Session completed.
```
Ta có password của file pdf là `13euro` sau đó chỉ việc mở file pdf thôi. Trong file pdf có 3 dữ liệu 

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209470010-16d1a047-fb7f-45f9-b364-3700509da170.png">
</p>

Nhấp vào [link](https://bit.ly/w0nkabar) ta sẽ download được một file có tên là `wonka-bar-golden-ticket.zip` Đây là một file có chứa password. Đến này mình suy nghĩ tới hai hướng: 

<ol>
    <li>Dùng john bruteforce lấy password giống cách đã làm với file pdf
    </li>
    <li>Decrypt cipher text để ra password</li>
</ol>

Và mình đã chọn cách thứ 1. Đúng là ngu ngốc :) thử dùng câu lệnh `john` tiếp tục để bruteforce tiếp và sau hàng giờ chờ đợi thì không ra kết quả. Sau đó mình có dùng [cipher identifier](https://www.dcode.fr/cipher-identifier) để tìm cipher thì ra một đống cipher có thể sử dụng. Sử dụng tất cả những cipher thông dụng (Affine, Vingerne) bruteforce cipher text nhưng không ra. Nhưng nhờ **Bory** mình đã để ý chữ **chance** in đậm ấy, add vào giải cipher, và ta có:
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209470305-ca0974fd-c27c-4a82-85e8-48c26f5a2fe1.png">
</p>
==> Password: luckstrikes

Áp nó vào trong file zip, ta được 4 files bên trong

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209470379-7cc2da7e-8d33-4473-83cf-05cc948fe22e.png">
</p>

Kệ những file kia, mình chỉ cần quan tâm tới file obj.file, vọc vạch xíu thì mình biết rằng:
<ol>
    <li>File được làm layer bằng blender (có thể mở bằng 3D viewer)
    </li>
    <li>Nếu zoom lên bằng 3D viewer, chúng ta có thể dễ dàng thấy được một đường link ở bên trong thanh chocolate ấy :))</li>
</ol>

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209470651-2bbcecd0-a5db-4514-9b5a-156bed3bbc93.png">
</p>
 
Khá là khó nhìn, nhưng nó có vẻ là một link bit.ly. Đến đây, mình phải bắt buộc dùng công cụ [blender](https://www.blender.org/). Trong lúc tải blender thì Bory đã ra link luôn rồi @@

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209470757-e116e94e-4a2c-4a9f-a6a4-885c0b33d1fc.png">
</p>

==> `bit.ly/g01d3nt1ck3t`

Truy cập vào [link](bit.ly/g01d3nt1ck3t) ta download được một file `wonkafactory.jpg`. Tới đây tụi mình cao hứng lắm rồi =)) quăng luôn file `wonkafactory.jpg` vào [HxD](https://mh-nexus.de/en/hxd/) và có kết quả:
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209470967-cc20808f-007f-4fa3-9c58-d5b5128e4ab4.png">
</p>

Nhìn vào cứ thoạt nghĩ là giải phương trình ra nghiệm a và b và áp vào `affine cipher` nhưng mình đã cho nó vào công cụ [detect cipher](https://www.dcode.fr/cipher-identifier) thì phát hiện ra nó là `ASCII Shift Cipher` bỏ đoạn strings `kqflsnyjHYK8fwymdxf~xdm8qq5` vào và ta có kết quả 

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209471190-7ad2713c-2f0d-4419-a51e-858bd8136ac8.png">
</p>

### Flag: niteCTF{3arth_says_h3ll0}

TLDR
===
* Dùng john với wordlist là rockyou.txt để lấy password của file `CandyStore.pdf`
* Tải file từ đường link có sẵn, áp cipher text có sẵn với key là chance, ta sẽ có pass của file zip
* Dùng blender để tìm thấy cái link ở bên trong file thanh chocolate :))
* Tải file từ đường link có trong thanh kẹo, dùng HxD hoặc các công cụ có sẵn tìm thấy đoạn strings bên trong file `.jpg`
* Dùng Ascii Shift Cipher để decrypt đoạn flag
