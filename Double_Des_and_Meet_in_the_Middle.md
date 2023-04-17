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


# PKCS#7 Padding

-   PKCS#7 Padding là một phương thức đệm dữ liệu (padding) trong mật mã học để đảm bảo độ dài của dữ liệu được mã hóa phù hợp với kích thước khối của thuật toán mã hóa khối.

-   Trong PKCS#7 Padding, các byte đệm được sử dụng để điền vào các byte trống trong khối cuối cùng của dữ liệu cần mã hóa. Giá trị của các byte đệm sẽ bằng với số byte đệm cần thêm vào. Ví dụ, nếu chỉ còn thiếu 2 byte để đạt độ dài khối, thì 2 byte đệm có giá trị là 0x02 sẽ được thêm vào cuối khối. Nếu cần thêm 5 byte đệm, thì 5 byte đệm có giá trị là 0x05 sẽ được thêm vào.

-   Có các cách để sử dụng PKCS#7 Padding trong python, bạn có thể tham khảo
```
length = 16
def PKCS7(s):
    pad = len(s) % length
    if pad != 0:
        s += bytes([pad]*(16 - pad))
    return s
print(PKCS7(b'Tran_Anh_Nhat_Viet_dep_trai_qua_<3'))
print(len(PKCS7(b'Tran_Anh_Nhat_Viet_dep_trai_qua_<3')))
#b'Tran_Anh_Nhat_Viet_dep_trai_qua_<3\x02\x02\x02\x02\x02\x02\x02\x02\x02\x02\x02\x02\x02\x02'
#48
```
Hoặc có thể đệm dữ liệu để có thể đủ kích thước để mã hóa AES
```
from Crypto.Cipher import AES

# Dữ liệu cần mã hóa
data = b'nhatziet'


# Đệm dữ liệu trước khi mã hóa
block_size = AES.block_size
padding_length = block_size - (len(data) % block_size)
padding = bytes([padding_length] * padding_length)
padded_data = data + padding
print(padded_data)
#b'nhatziet\x08\x08\x08\x08\x08\x08\x08\x08'
```
Hoặc có thể dùng hàm pad của Python
```
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad

# Dữ liệu cần mã hóa
data = b'nhatziet'

# Đệm dữ liệu trước khi mã hóa
padded_data = pad(data, AES.block_size, style='pkcs7')
print(padded_data)
#b'nhatziet\x08\x08\x08\x08\x08\x08\x08\x08'
```

-   Khi giải mã, quá trình giải mã được thực hiện bằng cách xóa các byte đệm thêm vào cuối cùng của khối cuối cùng. Giá trị của byte cuối cùng được sử dụng để xác định số lượng byte đệm cần phải xóa.

-   PKCS#7 Padding được sử dụng trong nhiều thuật toán mã hóa khối như AES, DES, Triple DES, và Blowfish. Tuy nhiên, nó cũng có một số nhược điểm như là nó chỉ có thể được sử dụng khi độ dài của dữ liệu được mã hóa chính xác bằng một số nguyên bội của kích thước khối của thuật toán mã hóa.