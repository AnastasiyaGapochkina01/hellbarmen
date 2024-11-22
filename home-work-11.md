> [!NOTE]  
> - для всех добавить контейнер с nginx, которы будет проксировать запросы на приложение
> - переменные по типу пользователей/паролей хранить в файле .env
> - ко всем БД прикрутить healthcheck
> - данные БД должны храниться не в папке, а на docker volume
> - для всех запущенных контейнеров с самим движком выяснить ip адреса

1) С помощью docker-compose запустить opencart (образ можно взять готовый отсюда https://hub.docker.com/r/bitnami/opencart/)
2) С помощью docker-compose запустить drupal (https://hub.docker.com/_/drupal)
3) С помощью docker-compose запустить laravel (образ можно взять готовый отсюда https://hub.docker.com/r/bitnami/laravel)
4) С помощью docker-compose запустить graylog
5) Написать bash-скрипт для создания бэкапов баз из контейнеров
