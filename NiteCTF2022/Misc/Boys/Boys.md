BOYS
====
**BOYS 100 points**

Lưu ý: đây là cách mình đã suy nghĩ xuyên suốt cả bài cho tới khi tìm thấy flag, nếu mọi người muốn nhanh gọn lẹ thì hãy nhảy tới TLDR giúp mình, mình xin cảm ơn 
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209466678-96295e4d-dac8-46c3-9121-0d478c3259d1.png">
</p>

Bài này khá là thú vị, nhưng mà không hiểu tại sao mà tác giả lại cho có 200 điểm ban đầu :( không có một file nào, chỉ có một cái description dài :< mình khá là lười đọc tiếng anh. Nhưng có một thông tin cực kì đặc biệt `GitHub user who goes by the name sk1nnywh1t3k1d or face Homelander's wrath.` 

Từ manh mối này mình bắt đầu lên github và search `sk1nnywh1t3k1d`. Theo như github thì có một user duy nhất tên là `sk1nnywh1t3k1d`

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209466990-43fea380-a59d-40df-85b6-cb64a91c1489.png">
</p>

Thử `git clone` xuống xem thử file thì trong 2 file, mình chợt thấy là 2 file này đều mất cả file `log.txt` và `chat.txt` các bạn có thể tham khảo code dưới đây 

```
import socket

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

ip = input("Enter IP: ")
port = int(input("Enter Port Number: "))

server.bind((ip, port))
#server.bind(("localhost", 9999))
server.listen()

client, addr = server.accept()

done = False

f = open('chat.txt', 'w')

while not done:
        received = client.recv(1024).decode('utf-8')
        f.write(received + "\n")
        if received == 'quit':
                done = True
        else:
                print(received)
                sent = input("Message: ")
                f.write("Server: " + sent + "\n")
                client.send(sent.encode('utf-8'))
```

```
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)


ip = input("Enter IP Address: ")
port = int(input("Enter Port Number: "))

client.connect((ip, port))

#client.connect(("localhost", 9999))

done = False

f = open('log.txt', 'w')

while not done:
        sent = input("Message: ")
        f.write("Client: "+sent +"\n")
        client.send(sent.encode('utf-8'))
        received = client.recv(1024).decode('utf-8')
        f.write("Server: " + received+"\n")
        if received == 'quit':
                done = True
        else:
                print(received)
```

Sau một hồi tìm kiếm không thấy thêm một manh mối gì, cái duy nhất mà chúng ta có được đó chính là đây chính là cái github của tác giả đưa, trong một phút vô vọng, mình cố thử vào lịch sử `commit` của githhub ông này xem ông ấy có xóa đi file `txt` không thì tất nhiên không nằm ngoài dự tính @@

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209467128-065f88cc-ed4c-452e-9df7-53b838f0fafc.png">
</p>

Cụ thể hơn là ở `first commit`, tác giả đã upload hết tất cả các file, kể cả file `chat.txt`, Nhưng tới `second commit` thì `chat.txt` đã bị xóa. Vào bên trong `first commit`

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209467247-fe50c790-d85c-4bb7-9c39-4cd1f41340cd.png">
</p>

Ta dễ dàng thấy được trong `chat.txt` có một nội dung quan trọng đó là một đường link `bit.ly/voughtencrypted`

Vào trong đường link đó dẫn tới một file `secret message.wav`. Download về, mở ra xem thì đúng thật là nó không có gì cả :))) Thử mở chúng trong [Sonic Visualiser](https://www.sonicvisualiser.org/) bật chế độ `audio spectogram` (tổ hợp `Shift + G`)
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209468432-7a162560-8da1-4ce5-bde7-1564d9042cf1.png">
</p>

Có vẻ như là chữ nó bị ngược rồi nhưng mà chúng ta vẫn có thể đọc được, nhìn thoáng qua nó là link bit.ly. Phân giải ra thì ta có: 
`bit dot ly forward slash endvought`

==> bit.ly/endvought

Try câp thử [link](https://mega.nz/file/hsMCTTbA#R0OmJ1voZocAsjhy5a_lU7nQyEuF0JheRDKowJm4SaY) ta có một file hình bị xếp lộn xộn
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209468562-f607fde1-d641-4478-bc6f-843c9dc05df9.png">
</p>

Tại đây, các bạn có thể dùng các [tool](https://github.com/nemanja-m/gaps) có sẵn trên github hoặc có thể tự giải tay :)) Mình thấy tool chạy hơi lâu nên đành giải tay. Dùng các điểm có pixel màu đỏ cắt ra và sắp xếp chúng lại. Ta được: 

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209468646-c651f74a-1d44-4968-8441-186060d2f206.png">
</p>

==> HUGHIECAMPBELL392@GMAIL.COM

Tới đây ta sẽ dùng [holehe](https://github.com/megadose/holehe) hoặc [Epieos](https://epieos.com/) đây là một trong hai công cụ khá phổ biến khi Osint một địa chỉ mail. Mình khuyến khích các bạn dùng holehe. Nhưng chal này mình sẽ dùng Epieos xD

Sau khi quét bằng web Epieos, ta có những thông tin sau đây 

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209468812-6d93decd-7f83-4f32-8fac-f3e9d8b95ed0.png">
</p>

Vào từng đường link theo như Epieos đã tìm được, và thật bất ngờ khi flag lại nằm ở bên trong [Google Calendar](https://calendar.google.com/calendar/u/0/embed?src=hughiecampbell392@gmail.com)

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209468897-80d271a3-c19d-4083-a3c6-d71c236750fe.png">
</p>

### Flag: 	niteCTF{v0ught_n33ds_t0_g0_d0wn}

TLDR
===
* Vào `first commit` trên github của `sk1nnywh1t3k1d` vào địa chỉ trong `chat.txt`
* Download file trong `chat.txt`, dùng Sonic Visualiser `add spectogram`
* Download file từ link bên trong file wav vừa add spectogram
* Scamble lại file png dùng tool hoặc bằng tay, ra được địa chỉ mail
* Dùng epios tra địa chỉ mail, vào google calender để lấy flag
