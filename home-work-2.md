1) Получить информацию о HugePages из файла /proc/meminfo. (Там скорее всего будет по нулям и это норма)
2) Получить информацию о количестве ядер cpu из файла /proc/cpuinfo (строка cpu cores)
3) Получить id (3 поле в строке) пользователя www-data офильтровав содержимое файла /etc/passwd
4) Создать в директории inform_фамилия папку text_processing
5) В text_processing создать файл info.csv с таким содержимым
```
Name,Company,Price,Ganre,Multiplayer
Item1,Company1,60000$,Ganre1,Yes
Item2,Company2,70000$,Ganre2,Yes
Item3,Company3,90000$,Ganre1,Yes
Item4,Company4,90000$,Ganre1,Yes
Item5,Company5,110000$,Ganre1,Yes
Item6,Company6,410000$,Ganre2,Yes
```
6) Вывести первые две строки файла info.csv
7) Вывести стобец Price
8) Найти все строки, в которых встречается слово Ganre2
9) Найти все строки, в которых встречается слово Ganre2 и вывести для них столбец Price
10) Дозаписать в файл info.csv с помощью echo строку Item7,Company6,450000\$,Ganre1,No
11) Получить из файла /proc/cpuinfo model name
12) Скачать на машину файл filesmetadata.csv (https://raw.githubusercontent.com/AnastasiyaGapochkina01/linux_home_works/main/files/metadata.csv), разместить его в text_processing
13) Вывести первые двенадцать строчки файла metadata.csv
14) Вывести последнюю строку файла metadata.csv 
15) С помощью grep найти все строки, содержащие слово mutex в файле metadata.csv
16) С помощью grep найти все строки НЕ содержащие слово gauge в файле metadata.csv
17) Вывести первые 5 строк файла, а затем с помощью cut получить только первый столбец этих 5 строк
18) Вывести поле unit_name из metadata.csv (весь столбец)
19) Скачать файл test.ns (https://raw.githubusercontent.com/AnastasiyaGapochkina01/linux_home_works/main/files/test.ns), разместить его в text_processing
20) Вывести все имена в A-записях из файла test.ns
21) Скачать файл coins (https://raw.githubusercontent.com/AnastasiyaGapochkina01/linux_home_works/main/files/coins), разместить его в text_processing
22) Вывести монеты, которые чеканили из золота (gold)
23) Вывести только названия стран, которые чеканили из золота (gold)
24) Вывести монеты, которые чеканили в USA
25) Найти все вхождения www-data во всех файлах в директории /etc
26) Получить все строки, не содержащие nodev из файла /proc/filesystem
