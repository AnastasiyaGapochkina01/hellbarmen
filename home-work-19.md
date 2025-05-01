Дано приложение на nodejs: https://gist.github.com/AnastasiyaGapochkina01/f1d3bd6e30e37679ead0ed158e1ba843 \
Необходимо
1) Запустить его в Docker
2) Написать ansible-роль nodejs-docker, которая будет запускать это приложение на удаленном сервере в docker
3) Написать роли
- setup-node, которая будет устанавливать nodejs сервер
- setup-mariadb, которая будет устанавливать и настраивать mariadb под проект
- setip-app, которая будет запускать приложение как systemd-unit
