## websec.fr-level10

Hi mọi người, đây là bài public writeup đầu tiên của mình :D
Chủ đề của bài viết này chính là challenge level10 của websec.fr


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

Khi truy cập vào challenge, ta được cung cấp source của file index.php, 
       
