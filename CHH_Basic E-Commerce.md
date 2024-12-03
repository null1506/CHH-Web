---
title: CHH\Basic E-Commerce

---

**Basic E-Commerce**
https://battle.cookiearena.org/challenges/web/basic-e-commerce
![image](https://hackmd.io/_uploads/H1jsXC7qR.png)
Ta thấy ta có thể đọc được đơn orders của người khác, vậy đầu tiên ta cần phải có đơn hàng đã, tức phải mua cái gì đó
Truy cập vào link, giao diện hiển thị như sau
![image](https://hackmd.io/_uploads/r1QrEAXcR.png)
Đầu tiên ta cần đăng kí tài khoản mua hàng
username=guest, password=guest
![image](https://hackmd.io/_uploads/r1PdNAX9R.png)
Đăng nhập bằng tk guest vừa tạo
![image](https://hackmd.io/_uploads/SkenVR79C.png)
Giao diện hiển thị như dưới đây, gõ /products để xem sản phẩm, /orders để xem đơn hàng đã mua
![image](https://hackmd.io/_uploads/S1KTVR7cC.png) 
Đầu tiên gõ /products để xem sản phẩm
Chọn Buy tại sản phẩm Apple iPhone 11 Pro
![image](https://hackmd.io/_uploads/HyYMHCXcC.png)
Nhập địa chỉ và sdt
![image](https://hackmd.io/_uploads/HJM8H0Q9R.png)
Nhập lại /products để xem sp và mua
![image](https://hackmd.io/_uploads/Sk6DHRXcA.png)
Chọn Buy
![image](https://hackmd.io/_uploads/HJwtSRm9C.png)
Chọn số lượng mua là 1
![image](https://hackmd.io/_uploads/Hy6qrCX5R.png)
Sau khi mua, gõ /orders để xem đơn hàng đã mua
![image](https://hackmd.io/_uploads/HkZ2BCm9R.png)
Chọn View Order để xem đơn hàng
![image](https://hackmd.io/_uploads/Hy5pr07qR.png)
Đơn hàng hiển thị như dưới đây, để trên thanh url có id=12, vậy ta sẽ thử xem id=13, id=10,...thì sẽ như nào ( vì đề bài nói ta có thể đọc thông tin đơn hàng của những người khác)
![image](https://hackmd.io/_uploads/BJeDEI0m5R.png)
Chuyển qua burpsuit bắt gói request đó
Với id=13 thì ko có thông tin đơn hàng của ai cả,ta thử id=11. Ta chú ý thông tin của người đó gồm Name, Address và Phone, vậy flag có thể ở 1 trong 3 mục này
![image](https://hackmd.io/_uploads/HJy5DCXcR.png)
Ta sẽ test id từ 1-->11
![image](https://hackmd.io/_uploads/rkPOUC7cC.png)
Chuyển qua Intruder, Phần Attack Type chọn Sniper
![image](https://hackmd.io/_uploads/r1qoL0XcR.png)
Chuyển qua tab Payloads, phần Payload type chọn Numbers, Phần Payload settings [Numbers] chọn from 1 to 11 step 1
![image](https://hackmd.io/_uploads/S14CUC7qR.png)
Chuyển qua phần Settings, Ở mục Grep - Extract, đây là mục sẽ hiển thị thông tin mà ta muốn ở Response, Chọn Add, Bôi đen guest (Name), tức là ta muốn hiển thị name của những id khác
![image](https://hackmd.io/_uploads/ByVJ_0QcA.png)
Tương tự ta bôi đen Hanoi (Address) và 123 (Phone)
![image](https://hackmd.io/_uploads/HkhcORQcC.png)
Chọn Start Attack
Tìm thấy Flag
![image](https://hackmd.io/_uploads/rJ-TdCQqR.png)











