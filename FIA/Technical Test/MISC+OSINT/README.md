[MISC] Technical Branch Test
====

Lưu ý: đây là cách mình đã suy nghĩ xuyên suốt cả bài cho tới khi tìm thấy flag. Cảm ơn mọi người rất nhiều
    <ul>
        <li>Đây là một bài test dành cho ban kỹ thuật của câu lạc bộ FIA - FPT Information Assurance Club liên quan tới những kiến thức về CTF</li>
    </ul>



<table align = "center">
<h2 align=center>MỤC LỤC CHALLANGE</h2>
  <tr>
  <td>

STT | Link |
| :--------- | :-- |
| [MISC] A new friend  | [Link](#misc-a-new-friend) | 
| [MISC] Painting like Shiba  | [Link](#misc-painting-like-shiba) | 
| [MISC] Shiba is coming  | [Link](#misc-shiba-is-coming) | 
  </td>
  <td>

STT | Link |
| :--------- | :--: | 
| [Osint] Evil Enemy  | [Link](#osint-evil-enemy) | 
|  [Osint] Run  | [Link](#osint-run) | 
| [Osint] Rescue Shiba  | [Link](#osint-shiba-rescue) | 
  </td>
  </tr>
</table>



------------------------
## [MISC] A new friend 
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217152118-eacc4b2d-c0e7-4b1b-b768-73b0b8005904.png">
</p>
Link đề tải tại đây

Đề bài cho chúng ta một file `Shiba.wav` đây là một file nhạc, khá là chill =)) 
Mọi người có thể mở lên mà nghe, nghe tới đoạn `0:20` tới `0:25` sẽ bị rè. Tới đây mình add thử vào bên trong [Sonic visualizer](https://www.sonicvisualiser.org/) hoặc [Audacity](https://www.audacityteam.org/download/).

Trong Sonic visualizer, và nhấn tổ hợp `Shift + G` để hiện ra spectogram của file. Và chúng ta có: 

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217155034-a93a26ac-da89-4c12-91c0-b38e6f94a969.png">
</p>

Đúng thật, lý do mà không có nghe được ở khoảng `0:20` tới `0:25` là vì nó chứa flag nên không thể nghe được

#### Flag: FIA{W00f_WooF_wOOf_Hi_5h1b4}


-----------------------------
## [MISC] Painting like Shiba
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217155331-e3d1c36d-7661-48c3-86b5-2d483508fb6c.png">
</p>

Mình không biết mọi người sao chứ bài này đối với mình là khó nhất =)) thấy mọi người giải cái 1 còn mình thì mất tới hai ngày để giải nó =))

Đề bài cho chúng ta một file có tên là `Shiba.png`
Link tải: tại đây

Mở file lên thì nó chỉ là một file con chó đơn giản
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217155728-23382cb8-9a1a-430c-a6d9-a37b5efbb76c.png">
</p>
Thật sụ là hardstuck =)) do đã từng làm quá nhiều bài stegno nên đã đi hơi xa nhưng mà từ từ cũng kéo về bờ được 

Mình đã thực hiện đủ trò như zoom hình, binwalk, xem comment bằng exiftool nhưng cũng chả ra kết quả gì.
Nhưng sau đó thì ngộ nhận ra rằng cách tìm ra flag rất rất đơn giản. 

Những dấu chân của con shiba đó chính là flag, thông qua mã màu hex của chúng. Bắng cách sử dụng trang [này](https://bietmaytinh.com/laymamau/):

**VD:** ta có thể dễ dàng thấy được là ba dấu chân đầu của chú chó có mã màu lần lươt `#464646`, `#494949`, `#414141`
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217157317-6a04c98d-7fd0-4e58-82b0-f751608a56a1.png">
</p>

Nếu đem vào những công cụ giải mã hex. Mình thì dùng [Cyberchef](https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')) thì chúng ta có được chữ `FIA`
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217157827-d425cede-40db-4edd-b78f-8d57b849d5dd.png">
</p>

Làm tiếp tục với những chữ còn lại thì ta ra được flag. 
Full input bạn có thể xem [tại đây](https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')&input=NDYgNDkgNDEgN2IgMzUgNjggNjkgNjIgMzQgNWYgNzcgMzQgNmUgNzcgNWYgMzUgMzAgNmQgMzMgNWYgNTIgNDcgNDIgN0Q)

#### Flag: FIA{5hib4_w4nw_50m3_RGB}
------------------------------------
##  [Misc] Shiba is coming 
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217158450-c0a50abd-4ce7-4ae5-8c52-e4cf083abaef.png">
</p>

Đề bài cho chúng ta một file JPG một con Shiba nữa :) 
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217158650-80ee204b-4cde-44b9-b8e8-cb5d326251d5.png">
</p>
Với kinh nghiệm mấy tháng chơi stegno của mình =)) cộng với đọc đề, thì bước thẳng luôn tới việc mở rộng độ dài của hình ra xem như thế nào. Với những bước sau: 

**B1: Xem độ dài của bức ảnh:**

* Bằng cách vào properties của windows, mình thấy được bức ảnh có các thông số sau: `width: 689` , `height: 689 `
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217159395-404066fc-08b2-4ef1-8eb7-d42a0372d7f8.png">
</p>

B2: Kiểm tra thông số hex

* Sau khi biến thông số `height = 689` chúng ta sẽ bắt đầu tìm hex của số `689` bằng python hoặc một tool nào đó. Ở đây mình dùng python. Sở dĩ có số hex này để phục vụ cho bước 3.

```
┌──(kali㉿kali)-[~]
└─$ python3                               
Python 3.10.5 (main, Jun  8 2022, 09:26:22) [GCC 11.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> hex(689)
'0x2b1'

```
Rồi ra số hex của nó rồi đó `02 b1`

**B3:** Thay đổi độ phân giải ảnh
* Tại bước này mình dùng một số công cụ như [HxD](https://mh-nexus.de/en/hxd/) hoặc Hexeditor trên linux. Mình recommend sử dụng HxD.

* Mở file bằng HxD và tìm hex `02 b1`
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217160762-81dff96c-fae7-4b32-a1d1-3f725183a142.png">
</p>

Ở vùng tô xanh đó chính là giá trị của `height` và `width` theo mã hex. Sau đó chúng ta chỉnh lại giá trị height lên là được. Nếu mà nhập `height` bé thì hình sẽ bị cắt ít đi thêm chiều dọc. Tại đây mình sẽ thử giá trị `height = 800` với mã `hex = 03 20`. Lưu lại và mở ra ta có: 
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217161544-d2d5d204-74c3-44a2-a575-fefd42273999.png">
</p>

#### Flag: FIA{D0_noT_joke_With_shiB4}

-----------------
## [Osint] Evil Enemy 
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217161971-5d90e4e2-f5bd-4f8c-9406-2208a0173331.png">
    <img src="https://user-images.githubusercontent.com/100250271/217162042-052c323d-0b92-400a-b5cf-5681bdb3c237.png">
</p>

Đây là một mẩu chuyện ngắn được tác giả viết nên nói về một chú chó đột biến bị mấy thanh niên chạy exciter trộm @@. Và chúng ta nhận được một cái mail tống tiền.

```
[From]: ohtoai8888@gmail.com
[To]: bory@wibu.com
Be attention!!!
I am ohto ai, this is the final caution for you to pay for your dog. After 24h if you do not send me 2.84987171 BTC to this address 1BoatSLRHtKNngkdXEeobR76b53LETtpyT. I will sell your dog away muahaha.
Be smart and becarefull, do not call the police, i am watching you.
```
Đề bài yêu cầu flag là tên của người trộm chó. 

Đọc mail, ta có thể thấy được một địa chỉ gmail được gửi dến bory@wibu.com Đây là một manh mối lớn đề lần ra danh tính người gửi. 

Sử dụng công cụ [Epios](epieos.com/) - đây là một trang web có thể tìm thấy thông tin dựa trên mail. Nhập tên mail người gửi vào, ta dễ dàng biết được tên người đó: 
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217162856-9e46f03f-8950-4110-a24e-6def7730d1f4.png">
</p>

Yess, người này có tên là: `Hak3r M3nnnkkk`

#### Flag: FIA{Hak3r_M3nnnkkk}

-----------------------------  
## [Osint] Run
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217163476-55cf4bdc-b635-462a-8e60-807ed0264438.png">
</p>

Câu này có vẻ là khó nhất, theo mạch của lời giải thì mình giải câu này là cuối cùng.

Sau khi có được username `Hak3r M3nnnkkk` ta bắt đầu đi tìm username này đối với một số trang web thông qua `whatsmyname.app`

Và thu được kết quả: 
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217190169-17ba2a7d-dc51-43c6-a25a-4700267196d7.png">
</p>

Tới đây ta có thể thấy có hai trang đó chính là `easygen` và `wikipedia`

Truy cập thử vào `wikipedia` và chúng ta có flag =))

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217191483-fe009828-fa52-4cec-b03c-52f806f7aee2.png">
</p>

=))) sớn xa sớn xác submit flag xong bị author nó cười vào mặt. Xong sau đó nhận ra rằng bên trong wiki nó có chức năng sửa văn bản. Giống như bạn muốn `commit` một cái gì đó giống trong `github` vậy.

Vào thì thấy những dòng văn bản đã được giấu đi nhưu thế này 

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217193036-53bb4d73-7bdb-48c7-bf2c-dc1c07004e0e.png">
</p>


```
Hehe no one can find my plan on Wikipedia
	
I will escape everything and enjoy my life
	
Hope that the flight will be safe. This is the first time i choose Haneda airport.
	
The plane will left gate 113 at 11:07pm JST today.
	
Goodbye ITSTAR kkk
```
Theo flow thì mình nghĩ rằng tìm được tên chuyến bay thì sẽ ra được thành phố mà tên trộm chó sẽ tới. 

Mình đã thêm 1 lần nữa sớn xác thêm một lần nữa dể đi tìm chuyến bay tại sân bay Haneda Nhật Bản lúc 11:07pm nhưng lại không chú ý kĩ tới ngày edit.

Ngày của tác giả muốn là chúng ta tìm thuộc khoảng `16.01.2023` tới `01.02.2023` nhưng thời điểm edit là `14:28 04.11.2022` nên đây không phải là cái mà tác giả muốn chúng ta tìm.

Kéo lịch sử chỉnh sủa tới ngày `27.01.2023` trên wiki ta có:
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217199050-8ba0234e-51a5-46ee-a141-002b421f0553.png">
</p>

Rồi chuyển từ tìm chuyến bay tại sân bay Henada, giờ chúng ta phải tìm chuyến bay lúc 10:05 sáng tại `sân bay Changi` ở Singapore

Tìm thông tin chuyến bay bằng trang web `flightaware.com`.Trang web này sẽ cho chúng ta có thể thấy được các chuyến bay trong vòng ba tháng trở lại. Truy cập tại [đây](flightaware.com/)

Thử tìm về chuyến bay departure từ `sân bay Changi`. Do web liên tục cập nhật những chuyến bay live nên số liệu tại thời điểm này có lẽ sẽ bị đẩy sâu hơn trong database của trong web

Link tại thời điểm tìm ra flag: [link](https://flightaware.com/live/airport/WSSS/departures?;offset=3720;order=actualdeparturetime;sort=DESC)

**Lưu ý:** Nếu bạn muốn tìm thấy chuyến bay 10:05 sáng này, trên url mà mình đã đưa trên chỉnh số `offset` bằng bội của 40. Lần từ từ cũng ra

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217237282-9e198f51-77a5-4cc6-bd98-532536cd7987.png">
</p>

Thì mình tìm ra chuyến bay từ `sân bay Changi` tới đó chính là `sân bay Jakarta-Soekarno-Hatta`

Tác giả hỏi thành phố nào, tra google thì chúng ta ra kết quả:

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217238186-1f203b62-76f6-429d-841f-0135ef3eaf68.png">
</p>

#### Flag: FIA{TANGERANG}

--------------
## [Osint] Shiba Rescue
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217243060-93360491-1e1e-41a7-a776-7387943f029e.png">
</p>

Tổng hợp lại, đọc lại cái đề thì thú thật là lúc này cũng đang bí, không biết chạy đi đâu. Mà mỗi lần bí thì thường phải tổng hợp lại một cách kĩ càng về những gì mình đang có. Mình đã suy nghĩ tới số tài khoản crypto bên trong mail, thử osint xem ra gì không nhưng kết quả cũng chẳng có gì. 

Đến nước này, trong đầu mình thoáng lên suy nghĩ (lúc này flow làm bài mình là `osint 1 - osint 3 - osint 2`) rằng: "Nếu mà để lại username như thế này ở chal 2, mà chal 3 lại bồi thêm cái câu mà điều tra thiếu, chắc hẳn là username này ngoài sử dụng ở chal 2 còn dùng ở chal 3"

Lập tức ngay sau đó mình có thử tra tên này trên những trang như `github`, `facebook`, `instagram`, và cuối cùng `twitter`. Và kết quả chúng ta có trang `twitter` của `Hak3r M3nnnkkk` tại [đây](https://twitter.com/LaDim54923410)

Lướt qua trang thì toàn là wibu =)) Nhưng khi vào `list` của trang `twitter` này ta thấy một lời nhán đến từ user này: 
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217247785-6ce72f88-b185-4536-a969-ff3a97f92bbc.png">
</p>  

`I serve my special service. Please contact my gmail for more information.`

Thôi thì như vậy rồi thì gửi mail cho bên đó thôi. Lấy địa chỉ mail ban đầu mà chúng ta được nhận. Thật chất đây chỉ là `1 auto mail` nên bạn gửi cái gì nó cũng sẽ reply lại cho bạn thôi 

**Nội dung mail reply từ Hak3r M3nnnkkk**
```
Hak3r M3nnnkkk
	
5 Feb 2023, 08:40 (2 days ago)
	
to me
Hi there !!!
Welcome to my service. Just give me an 0rd3rs, then i will complete it for you.
One of my best achievement is successfully in capturing the Shiba dog. I have sold it to my friend working in the park near here. Soon, that dog will become a dinner of his family ^-^
```
Kèm theo một bức ảnh:
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217251283-9b4d87ec-62f4-4985-a42a-1f07c24ee3b9.png">
</p>

Nhìn bức ảnh thì thôi rồi, osint xem nó ở đâu thôi. Nhanh trí bỏ vào google image xem nó có gì không.

Thoạt đầu, lúc lên google image, ta có thể thấy được đây có lẽ là một công viên, nhưng mà chưa biết là công viên nào.

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/218236262-ece06237-b7a5-4007-bb45-f17c726d7b75.png">
</p>

Đi dạo một hồi thì mình vào được trang web [này](https://www.littledayout.com/12-things-know-chestnut-nature-park-singapore/) và tìm thấy cuốn map này khá giống với map của bức hình tên trộm tró đó đưa:

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217252770-838ee1bd-91e3-4c4b-a814-f019c14dbc6e.png">
</p>

Thì ra đây chính là `Chestnut Nature Park` tại `Singapore`

#### Flag: FIA{Chestnut_Nature_Park}

**P/s** Nếu bạn làm theo flow tác giả (`osint 1 - osint 2 - osint 3`) thì nếu tinh ý, ta sẽ thấy rằng tác giả đã để lại tin nhắn ở **wikipedia** : 

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/217255863-f19b5448-ee8a-4108-b1b5-443563b982ed.png">
</p>

Thì từ đây chúng ta cũng có thể lần được tới `account twitter` mà không phải làm theo cách unintended :)))
