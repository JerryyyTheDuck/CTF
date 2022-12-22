Manipulate
===
#### 470 POINTS

![image](https://user-images.githubusercontent.com/100250271/209122788-c0dc7a97-5d27-4399-8458-9fcd7bafd950.png)


Thật ra bài này nói khó thì không khó, dễ thì cũng không dễ, bài này cũng chỉ ở mức tầm trung so với một đứa chơi ctf chưa bao lâu như mình ( nhưng khá là lâu để mình ngộ nhận ra chân lý xD)
Đây là suy nghĩ hướng đi của mình xuyên suốt bài, không phải là một cách đi thẳng tới đáp án. Nếu muốn thì bạn có thể lướt tới TLDR
Đề bài cho chúng ta một file zip với mật khẩu là: Christmas. 

Unzip file với mật khẩu là Christmas chúng ta có được 3 file.
`Flag.kdbx`
`flag`
`X-mas.jpeg`

![image](https://user-images.githubusercontent.com/100250271/209123838-95750399-d148-4467-a1f1-a9f429b3eb98.png)

OKE, giờ bắt đầu xem thử từng file có gì nào. Trước tiên thì mình luôn bắt đầu xem ở những file như `.jpeg` =))) 
![image](https://user-images.githubusercontent.com/100250271/209125090-668a9357-f00e-471e-90c3-176d6a8ba68e.png)

Nó nhìn như chỉ là một bức ảnh cây thông bình thường. Mở file được thì mình thử dùng [binwalk](https://www.kali.org/tools/binwalk/) xem nó còn có file gì ở bên trong
```bash
┌──(kali㉿kali)-[~/Desktop/Xmas-CFT/manipulated]
└─$ binwalk --dd =* X-MAS.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
```
Welp, có lẻ như cũng chẳng có gì cả :(((. Sau một hồi ngồi suy nghĩ, thì mình mới nhận ra là phần dưới của tấm ảnh cái pixel nó lạ lạ =)) nên quyết định thử resize lại cái hình.Dùng hexeditor hoặc những công cụ mà bạn có ( trong trường
hợp này thì mình dùng [HxD](https://mh-nexus.de/en/hxd/)). Chỉnh độ dài của file lại và chúng ta có 
![X-MAS](https://user-images.githubusercontent.com/100250271/209126765-4895977e-f10d-4543-89e8-4d3ea98987d6.jpg)

Quá là thơm =)) tới đây thì mình inspect thử file nén `flag.zip`. Trong file có một file `passwd.txt`, thử unzip hoặc mở trực tiếp nó ra thì không được, nên mình đã thử áp đoạn string mình
mới tìm được trên file `jpeg` thì nó đã hoạt động
![image](https://user-images.githubusercontent.com/100250271/209127571-da3c028f-c741-416e-aa7a-510e0c2d7eb9.png)
Là một đoạn base64 được encrypt, thử decrypt bằng cyberchef

**Đoạn base64 sau khi decrypt: fVeeR77Jua**

Nó cũng không có nghĩa lắm nhỉ, thôi kệ cứ để đó rồi tính tiếp, mở tới cái file cuối cùng `Flag.kdbx`. Mình thấy đuôi file của nó là kdbx, một đuôi file khá là lạ 
(so với kiến thức của mình hiện biết :< ) thế là mình lên mạng search xem nó là gì. Sau một hồi search, thì mình biết đó là KeePass Password Database, một dạng lưu password
sử dụng phần mềm [KeePass](https://keepass.info/)

Mở chương trình lên bỏ file `Flag.kdbx` vào xem thì mới phát hiện là mình cần phải có thêm một password để mở khóa file
![image](https://user-images.githubusercontent.com/100250271/209129892-c5743978-3455-4afa-bf40-e10ac701b1ef.png)

Rắc rối thật. Lúc này mình cũng có thử cái đoạn base64 mà mình decrypt được vào, thì cũng không có gì xảy ra, báo lỗi. Mình cũng thử luôn cả string base64 trước khi decrypt
mà có vẻ như mọi thứ vẫn không được. Tới lúc này mình phải bruteforce password bằng wordlist.  (nếu chưa tải john thì mấy bạn tải giúp mình nha =))) )

1. dùng command `keepass2john [file cần lấy hash] > [output]`
```
┌──(kali㉿kali)-[~/Desktop/Xmas-CFT/manipulated]
└─$ keepass2john Flag.kdbx > hash.txt
```
Wordlist mình hay dùng là rockyou.txt có thể tìm thế tại `/usr/share/wordlists`
2. dùng command `john --wordlist=[thư mục chứa wordlist] [hash text]`
```
┌──(kali㉿kali)-[~/Desktop/Xmas-CFT/manipulated]
└─$ john --wordlist=/home/kali/Desktop/rockyou.txt hast.txt
```

Chúng ta sẽ ra được password là **dracula**. Submit vào password trong Keepass thì vào được database của chương trình.
Inspect vào trong file, ta thấy được dòng tin nhắn mà tác giả gửi cho chúng ta: 
```
We managed to extract this data but I can't figure out what it is. The attacker said it should be something easy.
We only know that he likes some good cooked fish.

Q2hyNGlzdG1hc0pveQ==

N+ke3xIGF/h//tiT4SxIECOxGG7moZui0dccxtqmUg0=
```
Ở đây chúng ta có hai string, string đầu tiên là mã base64, decrypt ra thì chúng ta có: `Chr4istmasJoy`
Nhìn thấy là có hope rồi ấy =)) nhưng mà đời thì không dễ như vậy =)) còn đoạn string bên dưới thì mình vẫn không biết đó là string gì. Nhưng nhìn tới dòng description 
trong keepass mà tác giả để lại thì **We only know that he likes some good cooked fish.** thì mình đã bắt đầu search `fish decryption` và phát hiện ra (blowfish encryption)[http://sladex.org/blowfish.js/]

Nói nôm na thì blowfish cần giá trị và key, mình đã thử dùng các string mà mình đã tìm được trong lúc làm và áp chúng vào bao gồm: `Chr4istmasJoy (decrypt)`, `ZlZlZVI3N0p1YQ== (encrypt)`,
`fVeeR77Jua (decrypt)`,`Q2hyNGlzdG1hc0pveQ== (encrypt)` thì thật may là `Q2hyNGlzdG1hc0pveQ==` áp vào thì được một đường link (pastebin)[https://pastebin.com/CPzeYJmb]
![image](https://user-images.githubusercontent.com/100250271/209136042-9ce6ce50-a029-4039-816d-0af4eb829b0e.png)

Truy cập vào link, thì thấy nó cần password để vào, pass đó là `fVeeR77Jua` được decrypt từ file `psswd.txt`. Và chúng ta ra được flag của đề 
![image](https://user-images.githubusercontent.com/100250271/209136440-91542848-f05b-4101-bc63-24443f95e3a8.png)

#### Flag: X-MAS{S4Nt4_4nD_h1S_R31nd3ers}

TLDR
====
1. Mở file jpeg và dùng thủ thuật mở rộng chiều dài của hình, ra được pass của file zip
2. Dùng john để bruteforce vào file `flag.kdbx` được hai string `Q2hyNGlzdG1hc0pveQ==` và `N+ke3xIGF/h//tiT4SxIECOxGG7moZui0dccxtqmUg0=`
3. Dùng blowfish để decrypt `N+ke3xIGF/h//tiT4SxIECOxGG7moZui0dccxtqmUg0=` với key là  `Q2hyNGlzdG1hc0pveQ==`
4. Vào được link pastebin dùng pass ở bên trong file `psswd.txt` decypt base64 ra được flag
