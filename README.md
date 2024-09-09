# exporter_service
exporter_service
```

package main

import (
	"fmt"
	"os/exec"
	"strings"
)

func main() {
	// Выполняем команду systemctl для получения списка активных сервисов
	cmd := exec.Command("systemctl", "list-units", "--type=service", "--state=running")

	// Получаем вывод команды
	output, err := cmd.Output()
	if err != nil {
		fmt.Printf("Ошибка выполнения команды: %v\n", err)
		return
	}

	// Преобразуем байты в строку
	result := string(output)

	// Разделяем результат по строкам
	services := strings.Split(result, "\n")

	// Выводим список сервисов
	fmt.Println("Запущенные сервисы:")
	for _, service := range services {
		if strings.TrimSpace(service) != "" {
			fmt.Println(service)
		}
	}
}

```
