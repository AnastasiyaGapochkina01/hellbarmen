# Часть 1: BASH
1) Написать скрипт, который будет мониторить количество оперативной памяти на ВМ и делать запись раз в 5 минут в файл /var/log/ram_usage.log о текущем потреблении в формате
```
[date time] hostname total_ram used_ram
```
Cron НЕ использовать

2) Написать скрипт, который получит список пользователей и запишет его в файл all_users в формате
```
$sequence_number $username $uid $gropus
```
3) Написать скрипт, который будет получать инофрмацию о всех файлах в указанной директории (имя директории должно передавваться как аргумент) в формате
```
### => $filename <= ###
size: $size inode: $inode executable: yes/no
```
4) Написать скрипт, который будет выпуливать docker image mysql и запускать из него контейнер с БД. Значения переменных окружения для контейнера должны передаваться скрипту как аргументы
5) Написать скрипт, который будет проверять доступность заданного порта на заданном ip. Порт и ip передаются скрипту как аргумент, результат проверки должен записываться в файл check_port.log в формате
```
[date time] check port $port on host $ip is failed/success
```
Добавить запуск этого скрипта по расписанию в cron раз в 5 минут.
6) Запустить два любых проекта, которые мы запускали с помощью docker compose и написать скрипт, который будет делать бэкапы БД и данных приложений
# Часть 2: Systemd
1) Написать systemd-unit для скрипта из части 1, задача 1
2) Написать systemd-unit для запуска приложения на nodejs
```
const http = require("http");

const port = process.env.PORT || 3000; // Use environment variable for port, default to 3000

const server = http.createServer((req, res) => {
  console.log(`Request ${req.method} ${req.url}`); 
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end("Hello NodeJS!\n"); 
});

server.listen(port, () => {
  console.log(`Server started on port ${port}`);

```
3) Написать systemd-unit для запуска приложения на python
```
import time
from datetime import datetime

# Define the path to the log file
path_to_file = "/opt/myapp/timestamp.txt" 

while True:
    with open(path_to_file, "a") as f:
        f.write("Current timestamp: " + str(datetime.now()) + "\n")
    time.sleep(10)
```
4) Написать systemd-unit для запуска приложения на go
```
package main

import (
	"fmt"
	"log"
	"net/http"
	"os"
)

func main() {
	port := os.Getenv("PORT")
	if port == "" {
		port = "9010"
	}

	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, "Hello, Go!\n")
		log.Printf("Request from: %s %s\n", r.Method, r.URL.Path)
	})

	addr := "0.0.0.0:" + port
	log.Printf("Server listening on %s\n", addr)
	log.Fatal(http.ListenAndServe(addr, nil))
}
```
5) В директории /opt создать директории forking-goserver, в ней создать файлы
- main.go
```
package main

import (
	"fmt"
	"io/ioutil"
	"log"
	"os"
	"os/exec"
	"strconv"
)

func main() {
	port := os.Getenv("PORT")
	if port == "" {
		port = "3000"
	}

	// Path to the PID file
	pidFile := "/run/goserver.pid"

	// Fork the actual server process
	cmd := exec.Command("./server", port) 
	err := cmd.Start()
	if err != nil {
		log.Fatalf("Failed to start server process: %v", err)
	}
	fmt.Printf("Server process started with PID: %d\n", cmd.Process.Pid)

	// Write PID to file
	pid := cmd.Process.Pid
	pidStr := strconv.Itoa(pid)
	err = ioutil.WriteFile(pidFile, []byte(pidStr), 0644)
	if err != nil {
		log.Fatalf("Failed to write PID to file: %v", err)
	}
	fmt.Printf("PID written to %s\n", pidFile)

	os.Exit(0)
}
```
- server.go
```
package main

import (
	"fmt"
	"log"
	"net/http"
	"os"
)

func main() {
	port := os.Args[1] 
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, "Hello, Go from forked process!\n")
		log.Printf("Request from: %s %s\n", r.Method, r.URL.Path)
	})

	addr := ":" + port
	log.Printf("Server listening on %s\n", addr)
	log.Fatal(http.ListenAndServe(addr, nil))
}
```
скомпилировать исполняемые файлы
```
go build  main.go
go build -o server server.go
```
написать systemd-unit для запуска этого сервера
# Часть 3: Ansible
1) Написать роль для установки postgresql. Роль должна включать в себя таски по созданию пользователей в бд и двух баз данных для приложений
2) Написать роль для установки apache на два хоста: один из них под управлением debian, второй -- centos
3) Написать роль для установки стека prometheus+grafana+loki
4) Написать роль для установки postgres-exporter (не в docker)
5) Написать роль для установки promtail (не в docker) и подключения его к уже установленному loki для сбора логов из файла /var/log/syslog
6) Написать роль для установки node-exporter (не в docker) и подключения его к уже установленному prometheus
7) Написать роль для запуска сервера с приложением https://gitlab.com/anestesia.loc/bookstore
