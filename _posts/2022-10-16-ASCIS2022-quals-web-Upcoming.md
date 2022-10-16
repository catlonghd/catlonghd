### ASCIS2022-quals-web-Upcoming

Đây là một bài ở vòng sơ khảo cuộc thi SVATTT2022

Vừa vào trang web sẽ cho ta một giao diện như thế này

![image](https://user-images.githubusercontent.com/75677317/196017117-56545347-b5cd-42f4-b3bc-3d8151b2e0ce.png)


Các tính năng ở API này đều không sử dụng được nên mình sẽ tiến hành brute-force tìm các đường dẫn bằng dirb

![image](https://user-images.githubusercontent.com/75677317/196017635-aa5884bf-856c-4111-a143-0f91b4f427a9.png)


Với API "http://34.143.130.87:4002/file" yêu cầu cần có parameter, mình đã thử scan parameter bằng arjun nhưng không ra được kết quả nên sẽ bỏ qua.
Với API "http://34.143.130.87:4002/contact", ở đây ta có thể gửi phản hồi về phía server nhưng cũng không khai thác được gì nên mình sẽ bỏ qua.


Chỉ còn lại API "http://34.143.130.87:4002/about", ta có thể tra cứu thông tin nhân viên công ty. Đầu tiên mình sẽ thử sử dụng sqlmap xem API này có bị SQLi hay không. Sau khi chạy lệnh thì có vẻ như không thể inject với các db trong list.

![image](https://user-images.githubusercontent.com/75677317/196017424-08fe9304-f7b5-41f5-8cf2-36dae786626c.png)

Lúc này mình thử inject bằng tay với các db khác, mình thử với sqlite và may mắn thành công ở lần thử đầu tiên :DD
Mình thử bằng phép nối chuỗi của sqlite

![image](https://user-images.githubusercontent.com/75677317/196017531-aa8fbe7b-3ead-4f59-b934-8586c5e9576d.png)


Khi biết được API này dùng db gì và bị SQLi thì sẽ dễ dàng list ra được các table của db

![image](https://user-images.githubusercontent.com/75677317/196017549-633d21d3-df8e-4af6-811e-f49631de2206.png)


Tiếp đến list ra được các column của table fl4g

![image](https://user-images.githubusercontent.com/75677317/196017569-5440bde3-9197-46c0-a3dc-306701d1574d.png)


Cuối cùng ta có thể lấy được flag thành công

![image](https://user-images.githubusercontent.com/75677317/196017583-97e3cc6f-a97c-4a9c-89a4-c175e65ec22a.png)


Nếu có mình có sai sót gì về kiến thức hay bất kỳ vấn đề gì, xin hãy đóng góp qua mail: dangth2002@gmail.com.


