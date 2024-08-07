---
title: Password Reset Poisoning

---

Password Reset

 ![image](https://hackmd.io/_uploads/SJBRjpx90.png)
 Tham khảo thêm tại:
 https://cookiearena.org/hoc-pentester/password-reset-poisoning/
 https://www.invicti.com/learn/password-reset-poisoning/

 **Giải thích cơ chế của lỗ hổng**
![image](https://hackmd.io/_uploads/HkTHJ0ec0.png)

![image](https://hackmd.io/_uploads/HyzSyCg5A.png)

2 bước trên là đang gởi email về cho tk abc@gmail.com, ta đã thay host để khi nhận được yêu cầu reset, email được tạo, email đó sẽ chứa link giả ( host của ta )
Trong trường hợp này, hacker có thể thay thế trường Host Header bằng một tên miền độc hại hoặc của Hacker. Khi ứng dụng (tức server) nhận được yêu cầu reset mật khẩu, nó sẽ sử dụng tên miền độc hại đó để tạo Secret Link đặt lại mật khẩu và gửi cho người dùng qua email cá nhân.
 ![image](https://hackmd.io/_uploads/BylOJAl5C.png)

Bây giờ, ứng dụng web tạo email đặt lại mật khẩu bao gồm liên kết được tạo bằng biến $resetPasswordURL. Email được gửi đến đúng địa chỉ, abc@gmail.com, nhưng liên kết dẫn đến webhook…. thay vì 103….
![image](https://hackmd.io/_uploads/rk5o10xcC.png)

 
http://webhook.site/604640eb-491c-4956-9da3-1c686719bf88/reset_password/OCVBSZVBAKY264RO2WTNK3ZEUJ3RQ67C
tk abc@gmail.com sẽ nhầm tưởng link trên là link thật và nhấn vào

Ngay lập tức webhook trả về cho ta token id. Cơ chế của webhook là, khi ta truy cập link gì có chứa domain webhook thì sẽ trả về cho ta đúng link đó, nghĩa là khi admin truy cập vô link giả của ta ( nói là link giả của ta chứ thực ra server là ng sử dụng domain của ta để tạo ra link đó, rồi gởi email về cho admin), webhook sẽ trả về cho ta link đó
![image](https://hackmd.io/_uploads/Skja10e9R.png)
![image](https://hackmd.io/_uploads/r1nRy0l9C.png)
Khi vô sẽ có giao diện như này, ta thử đki một tài khoản
![image](https://hackmd.io/_uploads/B1p12axcA.png)

 ![image](https://hackmd.io/_uploads/Bk6XhTgc0.png)

abc@gmail.com -->pass: 123
Thử login
![image](https://hackmd.io/_uploads/H1QS26g9R.png)

 
Ta sẽ thấy được gmail admin
![image](https://hackmd.io/_uploads/ryMIhTl9C.png)

Giờ ta sẽ thử dùng gmail của mình, nhấn forgot password xem chuyện gì xảy ra
![image](https://hackmd.io/_uploads/ry0unax90.png)

 
Ta có thể thấy đường link reset pwd là link sau, ta thử vô link đó
 ![image](https://hackmd.io/_uploads/BJcKnpe50.png)

http://103.97.125.56:30569/reset_password/ETES95CTBTWQIV6Z7LO8FLULU0747AQ9
Sẽ ra được trang Reset password, vậy thì đối với tài khoản admin cũng vậy, nhưng link reset đó sẽ ko được gửi cho ta mà gửi cho admin, vậy thì làm tnao để lấy được link reset đó. Ta thấy nếu ta thay đổi host thì email mà server gửi về cho ta sẽ chứa link reset password có chứa host của ta kèm token
![image](https://hackmd.io/_uploads/B1o-pag50.png)
![image](https://hackmd.io/_uploads/B1GXaTlq0.png)
![image](https://hackmd.io/_uploads/r1vETpl5A.png)

Ta forgot password của tài khoản admin
![image](https://hackmd.io/_uploads/S1bsapec0.png)

 
Thông báo rằng email đã được gửi ( sẽ có link reset password )
 
Dùng Webhook để tạo một đường link
![image](https://hackmd.io/_uploads/Skg2pTl90.png)

 
Sau đó dán đường link đó vô phần host, rồi nhấn Send
![image](https://hackmd.io/_uploads/SJnhTax5C.png)

Ta thấy đang chuyển hướng kèm theo cookie session, Ta sẽ vô phần setting, chọn Process cookies in redirection rồi chọn follow redirection
![image](https://hackmd.io/_uploads/rJvATTxq0.png)

 
Ta đã được chuyển đến trang login (GET /login)
 
Ta có thể thấy ở bên tay phải, chỗ User-agent, là admin visited the link, nghĩa là admin đã ấn vào link giả của ta ( tức link do server tạo dựa trên domain của ta kèm token id)
![image](https://hackmd.io/_uploads/HyrlR6xqA.png)

Ta sẽ copy cái token id và dán vô form của đường dẫn link reset của challenge
http://103.97.125.56:30569
+
http://webhook.site/604640eb-491c-4956-9da3-1c686719bf88/reset_password/AZSDCUCDHDXBSVFKW2ZYFQZSX
--> http://103.97.125.56:30569/reset_password/AZSDCUCDHDXBSVFKW2ZYFQZSXBBV8DIQ

truy cập vào link trên dẫn ta đến link reset password
![image](https://hackmd.io/_uploads/HJ08A6g5A.png)
Đặt lại mật khẩu là abc rồi login lại
![image](https://hackmd.io/_uploads/B1GMkCx5C.png)

Ra được flag
![image](https://hackmd.io/_uploads/rJjfyCe90.png)



 
