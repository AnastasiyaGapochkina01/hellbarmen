1) Написать скрипт для резервного копирования нашего приложения todo
- нужен бэкап файлов сайта
- нужен дамп БД (командой ```mysqldump```)
- бэкапы сложить в папку /opt/backups
- формат имени файлов: 
  - бд: ```yyyy-mm-dd_hh-mm-ss_db-todo.sql.gz```
  - код: ```yyyy-mm-dd_hh-mm-ss_code-todo.tar.gz```
2) Написать скрипт, который будет проверять работоспособность web-сервера (а точнее сайта на этом сервере)
- проверку можно реализовать с помощью curl и проверки ответа, отдает он код 200 или нет
3) Написать скрипт для создания структуры нового проекта
- создать директорию самого проекта (должна передаваться как аргумент скрипту)
- в директории проекта создать директории
  - src/: исходный код
  - docs/: документация
  - tests/: тесты
  - resources/: ресурсы проекта
- создать файл
  - readme.md : файл с описанием проекта
- вывести созданную структуру на экран