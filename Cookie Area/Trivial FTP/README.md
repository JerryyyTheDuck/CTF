Trivial FTP
====
** Trivial FTP 200 POINTS**

Lưu ý: đây là cách mình đã suy nghĩ xuyên suốt cả bài cho tới khi tìm thấy flag, nếu mọi người muốn nhanh gọn lẹ thì hãy nhảy tới TLDR giúp mình, mình xin cảm ơn 


**Link tải file:** [tại đây]()

Download file đề về thì ta có một file PCAP. 

Tổng quan về file PCAP ta có thể thấy rằng có một số gói được truyền đi dưới giao thức Trivial Transfer Protocol. Như đề đã nói thì có lẽ đây là giao thức mà chúng ta cần lưu tâm tới ngay lúc này
<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/9f4331f8-68cb-4902-8781-049c7db7ab13">
</p>

Bây giờ việc của chúng ta chỉ cần việc filter nó ra và xem stream của nó xem trong đó chứa những gì. Tại filter `udp.stream eq 25` ta thấy được rằng bên trong stream của nó có ghi rằng `flag.pdf.netascii.` 
Theo như phỏng đoán ban đầu thì có lẽ thì nó sẽ dùng tới `netascii` để chuyển file `flag.pdf` đi. Bây giờ chúng ta sẽ dùng filter sau để có thể lọc ra ***header của file PDF*** bằng câu lệnh filter sau trong wireshark: `frame contains "PDF"`. 
- Câu lệnh này sẽ giúp chúng ta lọc ra hết những PDU có chứa từ "PDF"
- Sỡ dĩ dùng filter chứa chữ "PDF" là tại vì chữ PDF là magic header của file PDF
Filter thì ta có kết quả như sau: 

<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/b64f2b08-e3c2-401d-96ba-6affe69dd3b0">
</p>
Follow UDP stream của nó thì ta có kết quả sau: 
<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/4752febd-a549-4545-94cd-61b280ec1275">
</p>
Nhưn bị một cái rằng đây là một file nó sử dụng `netascii` nếu search google một số trang ví dụ như `Wikipedia` thì ta có kết quả sau hoặc có thể xem đầy đủ [tại đây](https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol)
<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/282ff0d0-f8a8-4c0a-ba15-d56f7e219ef7">
</p>
Nói nôm na ta có thể hiểu rằng với `netascii` thì `\n` sẽ được hiểu rằn `\r\n` và `\r\0` thành `\n`

Tới đây chưa xong, nếu xem UDP stream của file PDF được truyền thì ta sẽ thấy rằng, file pdf sẽ được chia nhỏ thành nhiều phần và sẽ được chuyển đi. Với mỗi phần của file pdf được chuyển đi thì nó sẽ gắn thêm 4 byte đầu: `00 03 00 xx`

Vì thế mỗi lần ta phải loại bỏ đi 4 byte đầu là được. Dưới đây là đoạn script được sử dụng để giải bài: 
```
import pyshark 
import re
capture = pyshark.FileCapture('TrivialFTP.pcapng', display_filter='udp.dstport == 58813')
ans = ""
for packet in capture:
    data = packet['UDP'].payload
    print(data)
    data = re.sub(r':','',data)
    data = data.replace('0d0a', '0a').replace('0d00','0d')
    ans += data[8:]

open('test.pdf','wb').write(bytes.fromhex(ans))
```

Và ta có được kết quả như sau bên trong file pdf: 
<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/fc772513-43fc-4568-99f7-cecc0220b7ee">
</p>

### Flag: CHH{FTP_4nd_TFTP_4r3_b0th_un$af3}

TLDR
===
- Đọc đề, kiếm tra các gói tin nhận thấy được truyền bằng `netascii`
- Nhận biết tính chất của netascii và viết script
- Ra flag @@
