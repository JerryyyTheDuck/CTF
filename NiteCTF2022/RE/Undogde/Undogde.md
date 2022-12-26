UNDODGE
====
**UnDodge 100 Point**
<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209565528-6e98b1c5-adb4-480a-8c7f-5bc2ba6c1053.png">
</p>

File có thể tải tại đây: [link](https://github.com/P5ySm1th/CTF/blob/main/NiteCTF2022/RE/Undogde/UnDodge.rar)

Bài này khá là cơ bản =)) đến cả những người mà mình chưa bao giờ đụng tới mảng Reverse mà còn làm được thì mọi người cũng thấy nó dễ tới cỡ nào rồi ấy =)))

Ban đầu mình thử mở cái file `application` lên để xem chương trình chạy như thế nào

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209565763-c0f8a35f-c9a0-4096-97a2-8ca19cbc6791.png">
</p>

Thì đây là một trò chơi được viết bằng unity, trò chơi khá là đơn giản,, chỉ cần không dụng trúng quả bom thì bạn sẽ được điểm. Khi đến một số điểm nhất định thì chúng ta sẽ được chữ để có thể mở ra flag.

Mình là một người chưa đụng đến mảng RE bao giờ nên mình đã lên mạng để tra những tool để có thể dịch ngược lại trò chơi. Và mình đã tìm được [link](https://viblo.asia/p/co-ban-cac-buoc-tiep-can-de-dich-nguoc-mot-game-unity-4dbZNqyLKYM) này.

Trong đây, tác giả có đề cập tới việc file chứa source code của Unity. Đó chính là file `Assembly-CSharp.dll `. Công cụ mình sử dụng đó chính là [dnSpy](https://github.com/dnSpy/dnSpy)

Mở file ra và bắt đầu xem trong file có gì thôi nào !

<p align="center">
  <img src="https://user-images.githubusercontent.com/100250271/209566200-afe8becc-f186-460f-9ea4-3c6b22e28f87.png">
</p>

Để ý kĩ ở đây chúng ta có thể thấy những class `flagchar` trải dài từ `0 tới 15` mình thử vào một trong những class đấy thì thấy như sau:

Mỗi class sẽ có một array kí tự bao gồm các kí tự cơ bản và dấu gạch dưới 
```
	public char[] ab = new char[]
	{
		'a','b','c','d','e','f','g','h',
		'i','j','k','l','m','n','o','p',
		'q','r','s','t','u','v','w','x',
		'y','z','_'
    };
```

Xét tới hàm `void Update(){}` ta thấy rằng cứ tới đúng cái điểm đó thì hàm nó sẽ trả về một kí tự như hàm dưới đây:
```
	private void Update()
	{
		if (Object.FindObjectOfType<Player>().score == 100)
		{
			this.flag.text = this.ab[0].ToString();
		}
	}
```
Như hàm ở trên thì nếu điểm = 100 thì sẽ trả về chữ của mảng ab có index = 0. Tương tự với các hàm flagchar còn lại, cứ tương ứng điểm thì sẽ trả về kí tự

Sau khi hiểu ra được vấn đề, mình bắt đầu viết một python script để giải bài này:

```
import string
ans = ""
arr = [26,22,7,0,19,26,0,26,15,11,0,24,4,17,26,26]
test = string.ascii_uppercase + "_"
for i in arr:
    ans += test[i]
print(ans)
```
==> ans = _WHAT_A_PLAYER___
#### Flag: niteCTF{_WHAT_A_PLAYER__}


