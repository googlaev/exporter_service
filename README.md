# exporter_service
exporter_service
go```

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
```

package main

import (
	"fmt"
	"os/exec"
	"regexp"
	"strings"
)

func main() {
	// Выполняем команду systemctl для получения списка активных сервисов
	cmd := exec.Command("systemctl", "list-units", "--type=service", "--state=running", "--no-pager", "--no-legend")

	// Получаем вывод команды
	output, err := cmd.Output()
	if err != nil {
		fmt.Printf("Ошибка выполнения команды: %v\n", err)
		return
	}

	// Преобразуем байты в строку
	result := string(output)

	// Разделяем результат по строкам
	lines := strings.Split(result, "\n")

	// Регулярное выражение для поиска названий служб
	re := regexp.MustCompile(`^\S+`)

	fmt.Println("Запущенные службы:")
	for _, line := range lines {
		// Используем регулярное выражение, чтобы получить только название службы
		if matches := re.FindString(line); matches != "" {
			fmt.Println(matches)
		}
	}
}
```
