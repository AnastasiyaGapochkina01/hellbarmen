# Часть 1
1) Установить nginx, если он еще не установлен
2) Посмотреть статус демона nginx
3) Остановить nginx
4) Запустить nginx
5) Убрать nginx из автозагрузки
6) Вернуть nginx в автозагрузку
7) "Замаскировать" nginx, попробовать перезапустить/остановить/запустить nginx; снять с nginx "маскировку"

# Часть 2
1) Установить на ВМ php
2) В директории /opt создать папку rot13
3) В директории /opt/rot13 создать файл с именем rot13-server.php с кодом
```
<?php
$sock = socket_create(AF_INET, SOCK_DGRAM, SOL_UDP);
socket_bind($sock, '0.0.0.0', 10000);
for (;;) {
  socket_recvfrom($sock, $message, 1024, 0, $ip, $port);
  $reply = str_rot13($message);
  socket_sendto($sock, $reply, strlen($reply), 0, $ip, $port);
}
```
4) Запустить сервер командой php rot13-server.php и проверить что сервер работает: выполнить nc -u 127.0.0.1 10000 и ввести Hello World
5) Написать юнит-файл для запуска rot13-server.php как сервиса

# Часть 3
1) Установить redis ([install-redis-on-linux](https://redis.io/docs/latest/operate/oss_and_stack/install/install-redis/install-redis-on-linux/)) - ссылка доступна под VPN
2) Посмотреть статус демона redis
3) Запустить второй экземпляр демона redis, написав systemd unit
