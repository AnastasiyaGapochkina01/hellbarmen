1) Написать роль по установке и настройке сервера мониторинга. Все сервисы запускать с помощью docker и docker compose
- prometheus
- grafana
- alertamanger - можно без настроек
- loki
- blackbox-exporter (https://github.com/prometheus/blackbox_exporter) должен сразу мониторить твой статический сайт

графана должна сразу цеплять prometheus и loki как datasources; prometheus должен иметь в конфиге настроенные таргеты с ВМ с приложением;

2) Написать роли по установке экспортеров на ВМ с нашим приложением 
- node-exporter (НЕ в docker)
- nginx exporter (https://github.com/nginx/nginx-prometheus-exporter) - его можно в docker
- promtail (должен автоматически подклчаться к loki на сервере мониторинга и собирать логи nginx)

3) Создать дашборды для
- node-exporter
- nginx exporter
