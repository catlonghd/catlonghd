### websec.fr-level13
Tiếp tục seri các challenge của websec.fr là write-up của level 13

Vào chall ta sẽ được cung cấp source code như sau

![image](https://user-images.githubusercontent.com/75677317/202204932-60efb14a-4964-471f-8031-b1e6953606c6.png)


Ở dòng số 4, chương trình sẽ sử dụng hàm create_function để tạo một function với tham số truyền vào là $flag và với đoạn code từ là giá trị của parameter 'c' do người dùng nhập vào

Sau khi đọc document từ https://www.php.net/manual/en/function.create-function.php ta biết được dòng số 4 sẽ tương đương như sau

![image](https://user-images.githubusercontent.com/75677317/202208209-36c00758-f72e-4bf4-a9d1-59b2614e9a4c.png)

Khi đó để bypass và chạy được code như mong muốn, ta sẽ thoát ra khỏi function bằng cách thêm dấu "}" như khi ta muốn thoát khỏi câu query gốc của chủng lỗi SQLi.
Ta có payload như sau: c=};echo $flag;//

<img width="376" alt="image" src="https://user-images.githubusercontent.com/75677317/202210619-2a2c52af-1ab7-452b-8fc8-82f3c9197d94.png">



Nếu có mình có sai sót gì về kiến thức hay bất kỳ vấn đề gì, xin hãy đóng góp qua mail: dangth2002@gmail.com.
