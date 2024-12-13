> [!NOTE]  
> - для всех приложений добавить контейнер с nginx, которы будет проксировать запросы на приложение
> - переменные по типу пользователей/паролей хранить в файле .env
> - ко всем БД прикрутить healthcheck
> - данные БД должны храниться не в папке, а на docker volume

1) Запустить в docker приложение https://github.com/AnastasiyaGapochkina01/flask-redis/tree/main. Нужно самому написать простой Dockerfile и docker compose файл
2) Запустить в docker приложение https://github.com/AnastasiyaGapochkina01/front-back-app/tree/main. Dockerfile для фронта и бэка есть, надо написать docker compose файл
3) Написать скрипт, который будет собирать информацию по обоим запущенным проектам (flask-redis и front-back-app)
- ip адреса контейнеров
- id контейнеров
- имя приложения
- volumes
вывод скрипта долже перенаправляться в файл docker_projects_info в формате
```
=== project name ===
from </path/to/compose file>
<container_id> <container_ip> <volumes>
```
