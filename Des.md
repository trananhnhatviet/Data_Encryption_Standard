# Data Encryption Standard
-   Data Encryption Standard (DES) là một thuật toán mã hóa đối xứng được sử dụng để mã hóa dữ liệu điện tử. Đây là một trong những thuật toán mã hóa đầu tiên và phổ biến nhất được sử dụng trong những năm 1980 và đầu những năm 1990.
-   DES là một thuật toán mã hóa đối xứng, có nghĩa là nó sử dụng cùng một khóa để mã hóa và giải mã dữ liệu. Trong thuật toán DES, khóa được sử dụng để biến đổi dữ liệu theo các chu kỳ của hoán vị và thay thế, tạo ra một bản mã của dữ liệu đó. Khóa của DES có độ dài là 56 bit, có thể được mã hóa bằng nhiều phương pháp khác nhau.
    ![](https://i.imgur.com/LeOQgBD.png)
-   Thuật toán DES hoạt động dựa trên một chu kỳ rất lớn của các hoán vị và thay thế. Khi mã hóa, DES chia dữ liệu thành các khối 64 bit và sử dụng một khóa 56 bit để tạo ra một bản mã của dữ liệu đó. Khi giải mã, cùng một khóa được sử dụng để giải mã dữ liệu đã được mã hóa trước đó.

**#Thuật toán DES**
___
-   Nếu bạn chán đọc chữ thì bạn có thể xem video này [Click here](https://www.youtube.com/watch?v=B7PSAeb7jL0)
-   Sơ đồ khái quát sẽ như sau:
    ![](https://i.imgur.com/d7cJYdr.png)
-   Trước hết, ta cần phải hiểu thuật toán sinh khóa của nó

**1. Thuật toán sinh khóa**
-   Sơ đồ tổng quát sẽ như sau:
    ![](https://i.imgur.com/ArAhFn2.png)
-   Ban đầu, ta đưa 1 khóa chính KEY 64 bit, sau đó KEY sẽ bước vào PC-1 để hoán vị
    -   PC-1 là 1 thuật toán hoán vị, sắp xếp lại KEY như sau:

        ![](https://i.imgur.com/bYGo3pH.png)
    -   Lưu ý, sẽ không có các số [8,16,24,32,40,48,56,64] -->  đưa ra 1 key_56 chỉ có 56 bit
    -   Sau khi thu được key_56, ta chia đôi ra thành 2 nửa là C0 và D0, mỗi bên 28 bit
    -   Đến bước LS, đây là 1 phép chuyển dịch vòng sang trái:
        -   Chuyển dịch 1 vị trí nếu i = 1,2,9,16
        -   Chuyển dịch 2 vị trí với các i còn lại
        -   Ví dụ, ta có chuỗi bit (theo lẽ là binary, nhưng mình ghi thế này cho dễ hiểu): 12345678 --> 1 vị trí -->  23456781 --> 1 vị trí 34567812
    -   Sau khi đi qua LS, ta thu được Ci, Di (i=1,2,...,16), thì sẽ đi PC-2 (cũng là 1 thuật toán hoán vị) như sau:

        ![](https://i.imgur.com/22yx3aW.png)
    -   Sau khi qua PC-2, ta sẽ thu được Keyi tương ứng nhaaaa <3

**2. Quá trình mã hóa**
___
![](https://i.imgur.com/DQrDnHQ.png)

-   Plaintext (64 bit) sẽ được đưa vào IP, IP cũng là 1 thuật toán hoán vị và sẽ sắp xếp lại như sau:

    ![](https://i.imgur.com/lklXVRy.png)

-   Sau khi đi qua IP, ta chia đôi ra thành 2 phần L0, R0 (mỗi bên 32 bit)
-   Ta lấy R0, ta cho đi qua Function F như sau:
    -   Giá trị đầu vào gồm:
        -   Ri: 32 bit
        -   Keyi: 48 bit
    -   Ban đầu, Ri 32 bit, sẽ đi qua phép hoán vị E như sau:

        ![](https://i.imgur.com/5QA2hlI.png)
    -   Khi ra thì sẽ thu được 1 chuỗi 48 bit, rồi ta lấy XOR với Keyi, ta thu được 1 chuỗi After_XOR 48 bit 
    -   Chia After_XOR thành 8 khối (tương đương với 8 Security box), mỗi khối 6 bit (gọi là After_Split[i] ). Các S-box sẽ như sau:

        ![](https://i.imgur.com/Z8T0r5y.png)
    
    -   Ví dụ ta có 1 đoạn After_Split[1] = 101110, ta sẽ làm như sau:
        -   Lấy kí tự thứ 1 và thứ 6 của After_Split[1], ta được 10 đổi sang Decimal là 2 --> lấy hàng thứ 2 (có 4 hàng là 0, 1, 2, 3)
        -   Lấy kí tự thứ 2, 3, 4, 5 của After_Split[1], ta thu được 0111 đổi sang Decimal là 7 --> lấy cột thứ 7
    -   ==> 101110 = 11 (Decimal) = 1011 (Binary)
    -   Ví dụ ta có 1 đoạn After_Split[2] = 011000 thì sau khi đi qua S-box[2], ta thu được 12 (Decimal) = 1100 (Binary)
-   Sau khi thu được 8 phần, ta sẽ được 1 đoạn F(Ri, Keyi) là 32 bit
-   Ta lấy F(Ri, Keyi) ⊕ Li --> R tiếp theo
-   Còn L tiếp theo chính là R trước
-   Sau 16 lần như thế, ta lại đưa vào FP (Final permutation), cũng là 1 thuật toán hoán vị và sắp xếp lại như sau:
    ![](https://i.imgur.com/X0LJH5B.png)
-   Sau khi qua FP, ta sẽ thu được ciphertext
lll

**3. Quá trình giải mã**
___
-   Quá trình giải mã DES cũng tương tự quá trình mã hóa. Chỉ khác là sẽ khác các khóa. Thay vì là từ 1 --> 16 thì giờ sẽ ngược lại và là 16 --> 1
    ![](https://i.imgur.com/56GelpZ.png)
