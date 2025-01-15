1) Написать плейбук для проверки доступности целевых хостов с выводом только ответа сервера (pong)
2) Написать плейбук для получения информации о целевых хостах с помощью фактов
- ip-адрес
- операционная система
- fqdn
- модель процессора
3) Написать плейбук по предварительной настройке целевых хостов:
- установить bash-completion, git, curl, wget, ca-certificates, gnupg2, apt-transport-https, software-properties-common, zsh
- добавить пользователя admin с uid 5000, правами sudo и случайно сгенерированным паролем (можно сделать вывод пароля при прокатке чтобы потом проверить) и оболочкой zsh
- добавить в /opt директорию facts и в нее файл с именем, которое совпадает с именем хоста и содержимым
```
hostname: <имя хоста>
ip: <ip адрес>
role: <переменная role, указанная при прокатке>
```
4) Написать скрипт, который будет проверять свободное место на диске и написать плейбук по добавлению его на сервер и запуску с помощью cron
5) Написать плейбук, который 
- установит на хост golang
- создаст в директории /opt директорию server и положит туда код
```
package main

import (
	"fmt"
	"os"
	"net/http"
)

var AppVersion = "1.0.0"

func funcHandler(w http.ResponseWriter, r *http.Request) {
	w.Write([]byte("Hello from DevOps in practice cource, app version is"+AppVersion))
}

func main() {
	Port := os.Getenv("PORT")
	if Port == "" {
		Port = "3000"
	}
	fmt.Print("\nApp version", AppVersion, "running on", Port)
	mux := http.NewServeMux()
	mux.HandleFunc("/", funcHandler)
	http.ListenAndServe(":"+Port, mux)
}
```
- соберет из кода исполняемый файл
```
CGO_ENABLED=0 GO111MODULE=off GOOS=linux go build -o server main.go
```
- запустит server как systemd сервис
- выполнит проверку сервера с помощью curl
