# bai_tap1
TÌM HIỂU CÁC PHƯƠNG PHÁP MÃ HOÁ CỔ ĐIỂN Caesar Affine Hoán vị Vigenère Playfair Với mỗi phương pháp, hãy tìm hiểu:  Tên gọi Thuật toán mã hoá, thuật toán giải mã Không gian khóa Cách phá mã (mà không cần khoá) Cài đặt thuật toán mã hoá và giải mã bằng code C++ và bằng html+css+javascript

# bai lam 
Caesar

Tên gọi: Caesar cipher (Mã Caesar).

Thuật toán mã hoá: dịch mỗi chữ cái theo một dịch chuyển k (0–25).
E(p) = (p + k) mod 26 (với p là vị trí 0..25 của chữ).

Thuật toán giải mã: D(c) = (c - k) mod 26 hoặc E(c, 26-k).

Không gian khoá: 26 khả năng (k = 0..25).

Cách phá mã (không cần khoá): brute-force thử 26 khả năng; hoặc phân tích tần suất (thống kê chữ cái, giả định E xuất hiện nhiều nhất tương ứng với 'E' trong tiếng Anh). Rất yếu vì không gian khoá nhỏ.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d64fd5bb-bfea-49f5-8f1c-6182a8b3d7c9" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8efbf4b3-c451-4b04-a033-1d70f5c27246" />

2) Affine

Tên gọi: Affine cipher (một dạng biến thể tuyến tính của Caesar).

Thuật toán mã hoá: E(x) = (a * x + b) mod 26, với a và b là khoá, và a cần nguyên tố cùng nhau với 26 (gcd(a,26)=1) để có nghịch đảo.

Thuật toán giải mã: D(y) = a^{-1} * (y - b) mod 26, trong đó a^{-1} là nghịch đảo multiplicative của a modulo 26.

Không gian khoá: số a khả dụng × 26 choices cho b. Các a có gcd(a,26)=1 là: 1,3,5,7,9,11,15,17,19,21,23,25 (12 giá trị). Vậy tổng khoá = 12 × 26 = 312 khả năng.

Cách phá mã (không cần khoá): brute-force trên 312 khả năng; hoặc phân tích tần suất để suy a,b (vì là biến đổi tuyến tính của bảng chữ cái, mối quan hệ tần suất vẫn giữ được). Nếu có được vài cặp plaintext–ciphertext (crib) thì giải được nhanh.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e029f2ed-9cb8-404f-b4ce-96e07cbc5fee" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/98fda548-8fa7-4686-80e8-10062d9055f2" />


3) Hoán vị (Substitution cipher)

Tên gọi: Monoalphabetic substitution cipher (mã thay thế đơn bảng) — “Hoán vị” ý chỉ hoán vị 26 chữ cái.

Thuật toán mã hoá: mỗi chữ cái A..Z thay bằng một chữ cái khác theo một hoán vị cố định (mapping từ 26→26).

Thuật toán giải mã: dùng mapping đảo ngược để thay trở lại.

Không gian khoá: 26! (giai thừa 26) — cực lớn (~4×10^26) — tức là rất lớn về mặt lý thuyết.

Cách phá mã (không cần khoá): không thể brute-force. Thực tế phá bằng phân tích tần suất (single-letter frequency), n-gram (digram/trigram), cấu trúc từ (pattern matching, crib), và phương pháp heuristic (simulated annealing, hill-climbing, algorithmic approaches). Với đủ văn bản, substitution cũng dễ bị phá do tần suất giữ nguyên cấu hình.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d7580806-4b26-4fc5-8ee6-1408f988b1b9" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bb15eb5a-24ac-4f7f-8b96-7025434c2010" />

4) Vigenère

Tên gọi: Vigenère cipher (mã dải, mã polyalphabetic cổ điển).

Thuật toán mã hoá: dùng một khóa chữ (ví dụ KEY) lặp lại để tạo các dịch chuyển (như nhiều Caesar xen kẽ). Với khóa K, ký tự thứ i được dịch bởi k_i.
E: C_i = (P_i + K_{i mod m}) mod 26.

Thuật toán giải mã: D: P_i = (C_i - K_{i mod m}) mod 26.

Không gian khoá: phụ thuộc độ dài khoá và chữ cái (26^m nếu khoá độ dài m). Nhưng nếu m không lớn thì dễ tấn công.

Cách phá mã (không cần khoá): dùng Kasiski hoặc dịch chuyển tần suất (Index of Coincidence, Friedman test) để tìm độ dài khóa, sau đó áp dụng phân tích tần suất cho từng chuỗi con (tách theo vị trí modulo m) — tương tự như nhiều Caesar. Với văn bản dài, khóa có thể được tìm ra.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/abb4a560-c747-49c9-a060-4c936ec642cb" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/dc319314-8432-4b05-9a90-7445be1a2b33" />


5) Playfair

Tên gọi: Playfair cipher.

Thuật toán mã hoá:

Tạo ma trận 5×5 từ khóa (thường hợp I/J gộp chung). Ghi đầy theo thứ tự xuất hiện của chữ trong khóa rồi phần còn lại của bảng chữ cái.

Chuẩn hoá plaintext: thay J→I, loại ký tự không phải chữ, tách thành cặp (digraph). Nếu 2 chữ giống nhau trong một cặp thì chèn chữ 'X' (hoặc chữ khác) giữa; nếu còn 1 chữ cuối cùng thì ghép thêm 'X'.

Quy tắc mã hoá cho một cặp: nếu cùng hàng → thay bằng chữ bên phải (dựng vòng); cùng cột → thay bằng chữ dưới; khác hàng & cột → thay bằng hai chữ ở cùng hàng nhưng hoán vị cột (hình chữ nhật): (r1,c2),(r2,c1).

Thuật toán giải mã: đảo ngược các quy tắc (trái, trên, hoán vị cột trái).

Không gian khoá: 25! / ... (vì I/J gộp) — rất lớn về số hoán vị, nhưng cấu trúc 5×5 giảm mức độ ngẫu nhiên.

Cách phá mã (không cần khoá): phân tích digram (tần suất cặp chữ), tấn công bằng heuristic hoặc dựa trên crib/dictionary; không dễ như Caesar nhưng yếu hơn substitution tinh vi. Playfair phá nhanh hơn substitution khi có lượng văn bản lớn do các đặc trưng digram.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f2ca29fd-f6a9-477e-b154-3981a0f0d164" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1cc2c7c7-0440-4555-bad3-946b6e08a322" />

