TRAVEL
====
**Travel 344 points**

Lưu ý: đây là cách mình đã suy nghĩ xuyên suốt cả bài cho tới khi tìm thấy flag, nếu mọi người muốn nhanh gọn lẹ thì hãy nhảy tới TLDR giúp mình, mình xin cảm ơn 
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209463407-9e1af1a8-4d62-4a9d-8a71-20aa3c19c236.png">
</p>

**Link tải file:** [tại đây](https://github.com/P5ySm1th/CTF/blob/main/NiteCTF2022/Misc/Travel/owl.jpg)

Ban đầu, đề bài cho chúng ta một cái file `owl.jpg`, bắt đầu mở thử lên xem bên trong có gì

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209463647-0660d7ee-cecb-4d89-a119-8b1f18db589a.png">
</p>

Một bức hình bình thường, vào kali và thử dùng kali để [binwalk](https://www.kali.org/tools/binwalk/) xem ra gì không ?

```
┌──(kali㉿kali)-[~/Desktop]
└─$ binwalk owl.jpg   

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
30            0x1E            TIFF image data, big-endian, offset of first image directory: 8
4654          0x122E          Copyright string: "Copyright (c) 1998 Hewlett-Packard Company"
```
Suy cho cùng nó cũng chỉ có những thông tin cơ bản thôi, cũng chả có gì nhiều hết. Lý do mình dùng `binwalk owl.jpg` không phải dùng `binwalk -e owl.jpg` hay `binwalk --d=.* owl.jpg` là để xem trước nếu binwalk thì nó sẽ ra cái gì trước, để đỡ phải xóa folder nếu dữ liệu mình cần không cần thiết @@

Tới đây thì mình lại bị kẹt ( hơi bí xíu) nhưng mà sau đó mình đã quên là mình vẫn chưa coi metadata của chúng @@ lỗi thật sự. Bắt đầu sử dụng công cụ exiftool để xem metadata của chúng

```
┌──(kali㉿kali)-[~/Desktop]
└─$ exiftool owl.jpg 
ExifTool Version Number         : 12.44
File Name                       : owl.jpg
Directory                       : .
File Size                       : 388 kB
File Modification Date/Time     : 2022:12:25 05:06:29-05:00
File Access Date/Time           : 2022:12:25 05:09:32-05:00
File Inode Change Date/Time     : 2022:12:25 05:09:32-05:00
File Permissions                : -rwxrw-rw-
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 96
Y Resolution                    : 96
Exif Byte Order                 : Big-endian (Motorola, MM)
Artist                          : bit.ly/mytodooolist
XP Author                       : bit.ly/mytodooolist
Padding                         : (Binary data 2060 bytes, use -b option to extract)
Profile CMM Type                : Linotronic
Profile Version                 : 2.1.0
```
Để ý một chút là có một cái đường link `bit.ly/mytodooolist`, thử check xem đó là cái gì thì bất ngờ thay đó là một link google jam
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209465207-6bde83ed-8e7b-4fee-b2b1-243d911b2960.png">
</p>
Đây là chế độ read only, chả có thể sửa được một thứ gì trong trỏng, tới đây mình khá là bế tắc =))) bởi chả còn dữ kiện gì để xem. Trong một phút bốc đầu, mình nhớ ra là có **chế độ duplicate (tạo bản sao)**, clone cái Jam này về vào xem coi có những gì. Và sau khi lục tung cái Jam đó lên thì mình có:

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209465510-4c3a4f6b-fe99-4fc9-88d3-5febc7d99990.png">
</p>

Wallah =))) một món quà giáng sinh tuyệt vời =)) **https://tr4v3l1.netlify.app/**

Như bản năng, mình thử vào trang web này xem có những gì

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209465864-16062fcf-0e9e-4c61-93ee-f27cd19df8ac.png">
  <img src= "https://user-images.githubusercontent.com/100250271/209465879-71dd0aad-0213-4fdd-ac49-e61a35668a87.png">
</p>

Có vẻ như là một cái web bình thường, mọi chức năng của web đều không hoạt động được ngoại trừ chức năng gửi mail. Thử dùng [holehe](https://github.com/megadose/holehe) hoặc dùng công cụ [Epios](https://epieos.com/) nhưng mình khuyến khích các bạn dùng holehe :> 

Kết quả là không tìm thấy gì cả, thế là mình đổi hướng đi


Thử mở `source html` của web xem liệu rằng mình có bị lỗi gì không bằng cách nhấn `F12` hoặc `Ctr+ U`. Trong đây mình tìm thấy một đoạn string trong phần note `<!-- ZmxhZy50eHQ= -->` 

Decode bằng base64 thì ta được một đoạn string: `flag.txt` Nhìn là biết sắp ra flag rồi đó =)) sau đó mình có thử nhập đoạn url `https://tr4v3l1.netlify.app/flag.txt` để truy cập vào phần flag.txt, nhưng kết quả trả ra là trắng bốc
<p align = "center">
    <img src = "https://user-images.githubusercontent.com/100250271/209466057-764c61ab-e9f6-4f80-8c74-2c8356695f27.png">
</p>

Mới bất chợt nhớ lại tới lời des của tác giả `Travel back in time for me please`, thế là mình lại dùng [WaybackMachine](https://web.archive.org/). Đây là một công cụ có thể giúp xem lại những gì mà web đó thay đổi. 

Và quả nhiên là tác giả đã có một số chỉnh sửa trong cái url vào ngày 23/12/2022 
<p align = "center">
    <img src = "https://user-images.githubusercontent.com/100250271/209466207-979112b0-bddd-4839-bd63-a1a0475203b2.png">
</p>

Nhấp vào cái link đầu tiên, chúng ta sẽ có flag
<p align = "center">
    <img src = "https://user-images.githubusercontent.com/100250271/209466241-cb06293b-3e80-43e8-bdc4-937f581ad880.png">
</p>

#### Flag: nitectf{y0u_w3nt_b4ck_1n_t1m3}
TLDR
===
* Dùng exiftool tìm ra địa chỉ Google Jam
* Tạo một bản sao của Google Jam tìm ra được một link netlify
* trên url thêm `/flag.txt` để tìm tới link của flag
* Dùng wayback Machine tìm flag dựa trên url đã nhập
