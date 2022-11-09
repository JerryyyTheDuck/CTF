Challenge
===============================
* Tác giả: P5yDuck

Nguồn
================================
File Wireshark: keyboardwarrior.pcap (Có thể download trong directory)

1. Tìm tập phổ biến của dataset
   * Xác định được Minimum Support và Minimum Confidence.
   * Tìm những phần tử có độ xuất hiện (phổ biến) lớn hơn Minimum Support gom lại thành 1 tập hợp
   * Từ tập hợp đó, tìm những tập con của chúng (khác rỗng) và quét trên CSDL và lăp lại bước số 2
2. Khởi tạo luật kết hợp tính liên kết của chúng có bền vững hay không.

CÔNG THỨC TÍNH
===
1. Support (A) = (số lần 'A' xuất hiện trong database)
2. Confidence (A->B) = Support (A U B) / Support (A)


