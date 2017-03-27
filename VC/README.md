# VC - 50 points

There are files A.png and B.png. But where's the flag?
[A.png](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/VC/files/A.png)
[B.png](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/VC/files/B.png)

### Solution
Такой тип заданий, когда даны две картинки и с ними что-то надо сделать, первое что приходит в голову - XOR.  
Собственно открываем в StegSolve картинку A.png

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/VC/assets/Screenshot_1.png)

Далее вкладка Analyse => Image Combiner. Выбираем наше изображение B.png и первым делом видим XOR этих двух картинок.

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/VC/assets/Screenshot_2.png)

![](https://github.com/texh0k0t/VolgaCTF-2017-Quals-Write-Up/blob/master/VC/assets/Screenshot_3.png)
