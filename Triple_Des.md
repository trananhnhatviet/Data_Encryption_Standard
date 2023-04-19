# Triple Des
-   TripleDES (hay còn gọi là 3DES) là một thuật toán mã hóa đối xứng có khóa độ dài 168-bit, được sử dụng rộng rãi trong các ứng dụng bảo mật thông tin. Nó được xây dựng dựa trên thuật toán DES (Data Encryption Standard), một thuật toán mã hóa đối xứng có khóa độ dài 56-bit. TripleDES sử dụng 3 lần mã hóa DES để tăng độ bảo mật.
-   Thuật toán TripleDES có thể được sử dụng trong hai chế độ mã hóa khác nhau: chế độ EDE (Encrypt-Decrypt-Encrypt) và chế độ EEE (Encrypt-Encrypt-Encrypt). Trong chế độ EDE, plaintext được mã hóa bằng thuật toán DES, sau đó được giải mã bằng thuật toán DES và cuối cùng được mã hóa bằng thuật toán DES lần nữa. Trong chế độ EEE, plaintext được mã hóa bằng thuật toán DES ba lần liên tiếp.

-   Encrypt-Decrypt-Encrypt Mode:

    ![](https://i.imgur.com/wb22xEF.png)
    -   Các bước trong quá trình mã hóa TripleDES chế độ EDE như sau:
        -   Chọn một khóa bí mật có độ dài 192-bit.
        -   Chia khóa thành 3 phần bằng nhau, mỗi phần có độ dài 64-bit.
        -   Sử dụng phần đầu tiên của khóa để mã hóa plaintext bằng thuật toán DES.
        -   Sử dụng phần thứ hai của khóa để giải mã kết quả từ bước trên bằng thuật toán DES.
        -   Sử dụng phần cuối cùng của khóa để mã hóa kết quả từ bước trên bằng thuật toán DES.
        -   Kết quả sau khi mã hóa sẽ là ciphertext.
    -   Các bước trong quá trình giải mã TripleDES chế độ EDE như sau:
        -   Sử dụng phần cuối cùng của khóa để giải mã ciphertext bằng thuật toán DES.
        -   Sử dụng phần thứ hai của khóa để mã hóa kết quả từ bước trên bằng thuật toán DES.
        -   Sử dụng phần đầu tiên của khóa để giải mã kết quả từ bước trên bằng thuật toán DES.
        -   Kết quả sau khi giải mã sẽ là plaintext.

-   Encrypt-Encrypt-Encrypt Mode:

    ![](https://i.imgur.com/ut9MqJP.png)

    -   Các bước trong quá trình mã hóa TripleDES chế độ EEE như sau:

        -   Chọn một khóa bí mật có độ dài 192-bit.
        -   Chia khóa thành 3 phần bằng nhau, mỗi phần có độ dài 64-bit.
        -   Sử dụng phần đầu tiên của khóa để mã hóa plaintext bằng thuật toán DES.
        -   Sử dụng phần thứ hai của khóa để mã hóa kết quả từ bước trên bằng thuật toán DES.
        -   Sử dụng phần cuối cùng của khóa để mã hóa kết quả từ bước trên bằng thuật toán DES.
        -   Kết quả sau khi mã hóa sẽ là ciphertext.

    -   Các bước trong quá trình giải mã TripleDES chế độ EEE như sau:
    
        -   Sử dụng phần thứ ba của khóa để giải mã ciphertext bằng thuật toán DES.
        -   Sử dụng phần thứ hai của khóa để giải mã kết quả từ bước trên bằng thuật toán DES.
        -   Sử dụng phần thứ nhất của khóa để giải mã kết quả từ bước trên bằng thuật toán DES.
        -   Kết quả sau khi giải mã sẽ là plaintext.

-   Lưu ý rằng TripleDES là một thuật toán khá chậm vì nó phải thực hiện 3 lần mã hóa/giải mã trên cùng một khóa. Tuy nhiên, TripleDES vẫn được sử dụng rộng rãi trong các ứng dụng yêu cầu độ bảo mật cao nhưng không cần tốc độ mã hóa/giải mã nhanh như các ứng dụng tài chính, bảo mật thông tin, hệ thống thanh toán điện tử, lưu trữ dữ liệu, v.v.
-   Tuy nhiên, TripleDES cũng có nhược điểm, đó là độ dài khóa chỉ có 112-bit hiệu quả, do đó có thể dễ dàng bị tấn công brute-force nếu attacker có đủ thời gian và tài nguyên. Vì vậy, TripleDES hiện đã được thay thế bởi các thuật toán mã hóa đối xứng hiện đại hơn như AES (Advanced Encryption Standard) với độ dài khóa lên tới 256-bit và tốc độ mã hóa/giải mã nhanh hơn.
