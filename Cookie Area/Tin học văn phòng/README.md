====
**TIN HỌC VĂN PHÒNG CƠ BẢN 200 POINTS**

Lưu ý: đây là cách mình đã suy nghĩ xuyên suốt cả bài cho tới khi tìm thấy flag, nếu mọi người muốn nhanh gọn lẹ thì hãy nhảy tới TLDR giúp mình, mình xin cảm ơn 

Link tải file [tại đây]()

Download file đề về thì ta có một file `Challange.doc`.  

Dựa vào description:
```
Sau khi tham gia một khóa Tin học văn phòng cơ bản, Hòa đã có thể tự tạo một tệp tài liệu độc hại và anh ta có ý định sẽ dùng nó để hack cả thế giới
```

Ta có thể thấy rằng đây là một file word chứa mã độc `Macro`. Có thể tìm và đọc một số tài liệu về `Macro` tại [link](https://whitehat.vn/threads/virus-vba-macro.4443/) này. Nói nôm na có thể được hiểu như sau: 
* Macro là một đoạn code để trong các ứng dụng Office
* Macro được viết bằng Visual Basic
- Tương ứng với đoạn code ví dụ như là khi chúng ta mở file Excel, thì nếu trong Macro có đoạn hàm gọi tới mở file excel tương ứng thì nó sẽ thực hiện hàm. Nôm na như việc gọi hàm vậy 

Tại đây chúng ta sẽ sử dụng công cụ `olevba` có trong bộ công cụ [oletools](https://pypi.org/project/oletools/0.04/) sử dụng bên trong `linux`

Sau đó sử dụng câu lệnh sau để có thể scan được bên trong file doc có đoạn macro nào không ? 

```
┌──(kali㉿kali)-[~/Desktop/arenas2-forensics-tin-hoc-van-phong-co-ban]
└─$ olevba Challenge.doc 
```

Full đoạn code được xem [tại đây]()

### Flag: CHH{If_u_w4nt_1_will_aft3rnull_u}  

TLDR
===
- Đọc đề nhận biết đây là VBA Macro chứa mã độc
- Kiểm tra bằng các công cụ như oletools để kiểm tra đoạn mã độc
- Ra flag
