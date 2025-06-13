Собрать комплексный дашборд для приложения:
1) Процент успешных запросов за последние 5 минут
2) Запросы по статус-кодам за 5 минут
3) 95-й перцентиль задержки
4) Количество 5xx ошибок в минуту
5) Ошибки при записи логов в БД
6) Доступность главного эндпоинта (/)
7) Активные подключения к PostgreSQL

Потребуется доработка приложения и инфры:
1) К [метрикам](https://gitlab.com/devops201206/metrics_app/-/blob/main/app.py?ref_type=heads#L15) добавить 
```
DB_ERROR_COUNT = Counter('flask_log_errors_total', 'Database log insert errors')
```

2) В [функции `log_request`](https://gitlab.com/devops201206/metrics_app/-/blob/main/app.py?ref_type=heads#L67)
```
except Exception as e:
    DB_ERROR_COUNT.inc()
```

3) Добавить эндпоинт /healthcheck
```
@app.route('/health')
def health():
    try:
        conn = get_db_connection()
        conn.close()
        return 'OK', 200
    except Exception:
        return 'Database Error', 500
```

4) Добавить postgres-exporter к compose приложения
