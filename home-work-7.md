# Часть 1: Работа с дисками и LVM
1) Добавить к ВМ дополнительный диск
2) На добавленном диске создать 2 раздела разного размера
3) Установить пакет lvm2, если еще не установлен
4) Создать папку /opt/dbs/mysql
5) Собрать volume group из созданных в п2 разделов
6) Создать logical volume и смонтировать его в папку /opt/dbs/mysql, сделать монтирование постоянным (при ребуте оно не должно отваливаться)
7) Создать еще один logical volume
8) Создать папку /opt/dbs/postgres
9) Смонтировать новый lv в папку /opt/dbs/postgres
10) Добавить к ВМ еще один диск небольшого размера
11) Расширить созданную в п5 volume group на добавленный диск
12) Расширить раздел, смонтированный в /opt/dbs/postgres
# Часть 2: Bash-скрипты
1) Написать скрипт, который будет проверять состояние указанных служб и перезапускать их, если они остановлены. (названия можно захардкодить к скрипте, а не передавать аргементом)
2) Написать скрипт для поиска свободных портов из диапазона 12450-12462
3) Написать скрипт для сбора статистики о процессах:
- об использовании cpu
- об использовании памяти
- выводить парамтеры pid, user, command и cpu/mem
- результат должен записываться в файл /var/log/process_stat.log в формате
```
==> Process stats at 2024-24-10_12-11-35 <==
--------------------------------------------
==> CPU usage <==
%CPU     PID USER     COMMAND
15.8     517 jenkins  /usr/bin/java -Djava.awt.headless=true -jar /usr/share/java/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080
 3.8       1 root     /sbin/init
 1.6     554 root     /sbin/agetty -o -p -- \u --keep-baud 115200,57600,38400,9600 ttyS0 vt220
 0.9     270 root     /lib/systemd/systemd-udevd
==> MEM usage <==
SIZE     PID USER     COMMAND
797876    517 jenkins  /usr/bin/java -Djava.awt.headless=true -jar /usr/share/java/jenkins.war --webroot=/var/cache/jenkins/war --httpPort=8080
26044     431 root     /sbin/dhclient -4 -v -i -pf /run/dhclient.eth0.pid -lf /var/lib/dhcp/dhclient.eth0.leases -I -df /var/lib/dhcp/dhclient6.eth0.leases eth0
26044     458 root     /sbin/dhclient -4 -v -i -pf /run/dhclient.eth0.pid -lf /var/lib/dhcp/dhclient.eth0.leases -I -df /var/lib/dhcp/dhclient6.eth0.leases eth0
18636     519 root     /usr/sbin/rsyslogd -n -iNONE
```
- выводить только первые 5 процессов в списке, отсортированных по нужному параметру
# Часть 3: Раскатка приложений
Запустить то же самое приложение, что и на уроке самостоятельно. Для этого
1) Установить nginx, php, mariadb
2) Содать базу данных todo и табличку list с полями id, title и note
3) Написать конфиг nginx (не забыть удалить дефолтный), сделать симлинку, не забыть проверить и релоаднуть конфиг

Код
```
<?php
$user = "todouser";
$password = "todopasswd";
$database = "todo";
$table = "list";

try {
  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
  echo "<h2>TODO</h2><ol>";
  foreach($db->query("SELECT * FROM $table") as $row) {
    echo "<li>" . $row['title'] . " <strong> NOTE:" . $row['note'] . "</strong>" . "</li>";
  }
  echo "</ol>";
} catch (PDOException $e) {
    print "Error! " . $e->getMessage() . "<br/>";
    die();
}
```
# Часть 4: Работа с curl
Есть сайт https://jsonplaceholder.typicode.com/. Это фейковый API для тестов и прочего экспериментального. Будем мучить его :)

1) Выполнить GET запрос на эндпоинт /users используя curl (отдаст 10 пользователей в формате json)
2) Используя curl выполнить POST запрос на эндпоинт /users, который добавит пользователя. Потребуется
- заголовок ```-H "Content-Type: application/json"```
- данные пользователя в формате json ```-d '{"name": "John", "age": 30}'```
3) Используя curl выполнить PUT запрос для изменения пользователя, которого добавил в п2 (так же потребуется заголовок и новые данные пользователя)
4) Используя curl выполнить DELETE запрос для удаления пользователя, которого добавил в п2
