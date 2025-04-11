Имеется проект https://github.com/AnastasiyaGapochkina01/nuxt - это код для генерации статического сайта. Для сборки используются команды
```
npm ci --cache .npm --prefer-offline
npm run generate
```
результатом являетсяя папка .output/public со статичными файлами сайта.\
Необходимо написать роли для
1) установки nginx. Роль должна 
- устанавливать nginx не из стандартных репозиториев, а из репы nginx (https://nginx.org/en/linux_packages.html#Debian)
- удалять дефолтный конфиг vhost`а
- генерировать новый vhost из шаблона, который будет раздавать статику из папки /var/www/nuxt-static/current
- изменять в nginx.conf количество воркеров с auto на 4
2) сборки и доставки статического кода:
- собирать статику
- копировать файлы статики на удаленный хост в папку /var/www/nuxt-static/release-$(timestamp)
- создавать (переключать) симлинк /var/www/nuxt-static/current -> /var/www/nuxt-static/release-$(timestamp)

**bash возможны вариант реализации**
```
#!/bin/bash
timestamp=$(date +%s)
git clone /var/www/nuxt-static/release-${timestamp}
# run build command in /var/www/nuxt-static/release-${timestamp}
ln -sfn /var/www/nuxt-static/release-${timestamp} /var/www/nuxt-static/current 
```
