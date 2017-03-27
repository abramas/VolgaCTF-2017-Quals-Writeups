# Angry Guessing Game - 200 points

Angry Guessing Game

This game is currently in a trial mode. It asks for a license key to continue. Can you find this key?
guessing_game

Hints:
* Binary file was updated. Please reload the file

### Solution

Пробуем запустить нашу программу в linux, мы пытаемся угадать число загаданное в коде с помощью подсказок больше или меньше.  
На третьем уровне программа требует от нас лицензионный ключ для того что-бы играть дальше.  
Окей.  
Открываем наш файл в дизассемблере IDA Pro.  
Первым делом сразу открываем поиск всех строк которые вводит программа или были в коде:

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_1.png)

Находим нужную нам строчку, будем отталкиваться от неё:

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_2.png)

Нажимаем на клавиатуре "x", что бы посмотреть где использовалась фраза о правильном ключе:

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_3.png)

Или с помощью контекстного меню Jump => Jump to xref to operand...

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_4.png)

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_5.png)

Повторяем наши действия:

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_6.png)

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_7.png)

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_8.png)

Теперь когда мы пришли к месту где вызывается этот текст, нажимаем "f5" или как на скриншоте через контекстное меню, смотрим псевдокод на C++ для удобства читаемсти кода:

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_9.png)

Здесь мы видим что присутствуют выводы сообщений как и о правильном ключе, так и о неверном.  
Нажимаем пробел, что бы посмотреть граф этой функции:

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_10.png)

Видим функцию "sub_6660" котрая сверяет ключ и в итоге отправляет нужный ответ нам:

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_11.png)

Открываем эту функцию и смотрим её псевдокод. Смотрим что возвращает функция, и видим что переменная "v4" берётся из функции "sub_67D0".

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_12.png)

Смотрим что в ней:

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_13.png)

Видим значения очень похожие на ASCII значения английского алфавита. Переводим их в символы нажатием на клавиатуре "r":

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_14.png)

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/Angry%20Guessing%20Game/assets/Screenshot_15.png)
