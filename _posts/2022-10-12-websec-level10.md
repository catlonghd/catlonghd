## websec.fr-level10

Hi mọi người, đây là bài public writeup đầu tiên của mình :D
Chủ đề của bài viết này chính là challenge level10 của websec.fr

Khi truy cập vào challenge, ta được cung cấp source của file index.php.

![image](https://user-images.githubusercontent.com/75677317/195742945-da56ef56-20fa-48a1-935b-1045c1edb669.png)

Đầu tiên biến $hash sẽ được gán bởi giá trị của hàm md5().

Biến $hash và $request được so sánh bởi '==', là 'Loose comparision' nên 2 giá trị sẽ được đưa về cùng một kiểu dữ liệu để so sánh. (các bạn có thể tham khảo tại [đây](https://www.php.net/manual/en/language.operators.comparison.php))

Nếu giá trị 0e... được tạo ra bởi hàm md5() và được so sánh với với giá trị 0 được gán cho biến $request thì hàm if sẽ trở thành True. Khi đó ta có thể xem được nội dung của file flag.php thông qua hàm show_source().

Vì cách thức hoạt động của md5 khá phức tạp (các bạn có thể tham khảo tại [đây](https://vi.wikipedia.org/wiki/MD5)) nên ý nghĩ đầu tiên là brute-force bằng cách chỉnh sửa các giá trị truyền vào hàm md5() đến khi nào có được giá trị 0e... :D

Ta có liên tục thêm './' vào trước 'flag.php' thông qua param 'f' của biến $_REQUEST['f'] đến khi nào ra được giá trị mong muốn. Nhưng nếu làm thế sẽ tăng độ dài của tham số truyền vào và vượt mức cho phép của Apache nên ta có thể thay thế bằng "." + "/"*i + "flag.php"

Mình sẽ viết script để exploit bằng python

![image](https://user-images.githubusercontent.com/75677317/195743096-5481fccf-d014-483f-ac13-a5b9b598f4f9.png)

Brute-force sẽ hơi mất nhiều thời gian, nhưng chờ đợi là hạnh phúc :DD


Nếu có mình có sai sót gì về kiến thức hay bất kỳ vấn đề gì, xin hãy đóng góp qua mail: dangth2002@gmail.com. 

