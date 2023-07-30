BÁO CÁO DANG DỞ
===

**BÁO CÁO DANG DỞ 300 POINTS**

Lưu ý: đây là cách mình đã suy nghĩ xuyên suốt cả bài cho tới khi tìm thấy flag, nếu mọi người muốn nhanh gọn lẹ thì hãy nhảy tới TLDR giúp mình, mình xin cảm ơn 

Link tải file [tại đây](https://battle.cookiearena.org/challenges/digital-forensics/bao-cao-dang-do)

<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/752c6f11-8048-4d99-ab27-b9c3b1f35b93">
</p>
File sẽ cho ta download một file `Crashdump` vì là `crashdump` nên chúng ta không thể nào xét được phần OS mà nó đang dùng. Tại đây chúng ta có thể dụng `Windbg` có thể check xem rằng OS mà file crashdump này đang sử dụng là gì. Vì quá lười và không thạo `Windbg` và lúc đó đã là 2 giờ sáng nên mình đã sử dụng [Voltality 3](https://github.com/volatilityfoundation/volatility3) để có thể phân tích xem OS mà nó đang sử dụng :v

Vì Voltality3 được chạy dưới file python nên chúng ta cần có python3  để có thể chạy được Voltality3. Sử dụng câu lệnh sau để có thể biết được `system info` của file crash dump: `vol.py -f “/path/to/file” windows.info`

Ta được như hình dưới đây:
<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/e305e4a7-ed95-4bf9-83a0-1cb24cabeac4">
</p>
Nhìn kĩ vào phần `NTBuildLab` ta thấy được rằng đây là `Win7sp1 64bit`. Sau đó ta sẽ dùng `Voltality2` để có tiếp tục phân tích tiếp (Sở dĩ mình không dùng vol3 tiếp tại vì mình không quen dùng, do cú pháp khác nên khá là khó để sử dụng)

Sau khi có profile của file crashdump, ta tiếp tục sử dụng vol2 để có thể xem tất cả các tiến trình đang chạy trên file crashdump ấy: `vol2 -f “/path/to/file” ‑‑profile <profile> pslist`
Dựa trên bài viết [này](https://github.com/volatilityfoundation/volatility/wiki/2.6-Win-Profiles), mình tìm thấy profile để apply vào bên trong vol2. Chính xác profile mà chúng ta sẽ sử dụng là `Win7SP1x64_23418`

Dựa vào phần memdump, ta có thể thấy rằng ở đây có một tiến trình `WINWORD.exe` đang chạy. Ở đây nó chính là phần `Microsoft Office Word` với số `Proccess ID = 1736`

<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/cac84752-8e0b-47af-ae67-9692cd702680">
</p>
Khi đọc kĩ lại description của đề bài đưa ra
```
Hòa đang làm báo cáo bài tập lớn để nộp cho thầy giáo thì bỗng nhiên máy tính của anh ấy bị tắt đột ngột do mất điện mà anh ấy thì chưa kịp lưu báo cáo một lần nào. Tuy nhiên sau đó, thay vì viết báo cáo mới thì Hòa đã chọn cách dành ra 4h đồng hồ để khôi phục báo cáo ban đầu từ tệp crash dump nhưng cuối cùng vẫn thất bại. Hòa thực sự đang cần trợ giúp.
```

Thì mình nhận ra rằng, trong word có một cơ chế gọi là **auto save**. Mỗi máy có một thời gian  auto save khác nhau, và mình bắt đầu tìm hiểu trên mạng thì mình tìm được link [này](https://support.microsoft.com/vi-vn/topic/ca%CC%81ch-th%C6%B0%CC%81c-word-ta%CC%A3o-va%CC%80-phu%CC%A3c-h%C3%B4%CC%80i-ca%CC%81c-t%C3%AA%CC%A3p-t%C6%B0%CC%A3-%C4%91%C3%B4%CC%A3ng-phu%CC%A3c-h%C3%B4%CC%80i-a33ec235-9d68-cf62-e66a-6a740cf51821)

<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/d414707b-df55-4943-8f3f-07706bac1862">
</p>
Bây giờ chúng ta sẽ bắt đầu tìm tới file `asd` này bằng cách sử dụng câu lệnh sau: `vol.py -f “/path/to/file” ‑‑profile <profile> filescan` 

Câu lệnh này sẽ giúp ta quét qua các file bên trong crashdump. Trong trường hợp này mình sẽ lưu dưới một file notepad để có thể dễ xem hơn.

Ta có thể thấy rằng tại Offset `0x000000007e3e2070` có một file `asd` của Microsoft Word::
<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/5ce70714-ba5d-4763-a5b8-426a751391ac">
</p>
Sau đó ta sẽ dùng câu lệnh sau để dump file theo **Offset**: `vol.py -f “/path/to/file” ‑‑profile <profile> dumpfiles ‑‑dump-dir=“/path/to/dir” -Q <offset>`
Sau khi dump ta có được file `dat` như hình dưới: 

<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/b693d6d3-7213-435b-ad65-e3cd4b0eeb5d">
</p>

  Nhưng lại không thể nào mở được. Nhưng vì file Office chính là một file `zip`. Bạn có thể đọc thêm [tại đây](https://www.quora.com/Why-are-Word-docx-files-actually-zip-files)
Vì lười sử dụng [7zip](https://www.7-zip.org/) nên mình sẽ sử dụng [binwalk](https://github.com/ReFirmLabs/binwalk) để có thể giải nén. Ta có được như hình dưới đây: 
  
<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/70336d24-00af-4670-acf8-654dbaba3471">
</p>

Vì tính chất như một file `zip` nên chún ta có thể thấy rằng nó đã extract ra được khá là nhiều thông tin. Sau khi `extract` xong, ta vào bên trong Folder `/word/media/` và ra flag: 

<p align="center">
  <img src="https://github.com/P5ySm1th/CTF/assets/100250271/ded069b1-071f-429a-86a2-5456f900470f">
</p>

### Flag: CHH{4ut0R3c0v3r_s4v3_my_l1f3}

TLDR
===
- Đọc đề, nhận biết đây là crashdump, dùng `windbg` hoặc `vol3` để xem profile
- Thấy có một process là `WINWORD.EXE` 
- Tìm kiếm về file `recovery` của word --> file đuôi `asd`
- Xuất file `asd` trong crashdump ra
- Ra flag @@
