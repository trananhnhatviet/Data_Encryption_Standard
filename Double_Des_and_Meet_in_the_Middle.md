# Double Des
-   DoubleDES (hay còn gọi là 2DES) là một thuật toán mã hóa đối xứng (symmetric encryption) sử dụng khối (block cipher) được xây dựng trên cơ sở của DES (Data Encryption Standard). DoubleDES sử dụng hai khóa ``Key1`` và ``Key2`` để thực hiện mã hóa và giải mã dữ liệu, mỗi khóa có độ dài 56 bit.
    ![](https://i.imgur.com/YuxXhWI.png)
-   Thuật toán DoubleDES thực hiện việc mã hóa bằng cách sử dụng hai giai đoạn mã hóa DES theo thứ tự liên tiếp.  Vì vậy, DoubleDES có thể được biểu diễn bằng công thức:

    -   ``Ciphertext = E(Key2, E(Key1, Plaintext))``
    -   ``Plaintext = D(Key1 ,D(Key2, Ciphertext))``

-   Trong đó, Plaintext là dữ liệu cần được mã hóa, E(K1, Plaintext) là kết quả sau khi dữ liệu được mã hóa với khóa K1, và E(K2, E(K1, Plaintext)) là kết quả cuối cùng sau khi dữ liệu đã được mã hóa hai lần với hai khóa K1 và K2.
-   Thời gian BruteForce của 2DES là 2^56 x 2^56 = 2^112 --> Rất chi là lâu lunnn

# Attack in the Middle with 2DES
-   Giả sử, Hacker có được 1 cặp Plaintext_1 và Ciphertext_1 tương ứng, Hacker có thể tìm ra được 2 khóa bí mật nhờ kỹ thuật Attack in the Middle để có thể biết được nhiều thông tin hơn sau này
-   Cụ thể như sau, ta thấy công thức mã hóa và giải mã của 2DES là:
    -   ``Ciphertext = E(Key2, E(Key1, Plaintext))``
    -   ``Plaintext = D(Key1 ,D(Key2, Ciphertext))``
    -   ==> ``D(Key2, Ciphertext) = E(Key1, Plaintext)``
-   Giờ ta có 2 nửa là D(Key2, Ciphertext_1) và E(Key1, Plaintext_1), ta cần BruteForce sao cho kết quả 2 bên là như nhau, với tổng thời gian là 2^56 + 2^56 = 2^57, nhỏ hơn rất nhiều so với ban đầu. Như vậy meet in the middle attack đã làm cho 2DES không còn đáng tin cậy để áp dụng cho bảo mật thông tin. Mà thay vào đó là 3DES, hay AES…