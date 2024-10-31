### 1. Gerenciamento de Conexão de Banco de Dados (SQLite)

Esse exemplo cria uma conexão Singleton com o banco de dados SQLite, garantindo que apenas uma conexão seja usada em toda a aplicação.

```go
package main

import (
	"database/sql"
	"fmt"
	"log"
	"sync"

	_ "github.com/mattn/go-sqlite3"
)

type Database struct {
	connection *sql.DB
}

var dbInstance *Database
var dbOnce sync.Once

// Obter instância única de Database
func GetDatabaseInstance() *Database {
	dbOnce.Do(func() {
		conn, err := sql.Open("sqlite3", "./app.db")
		if err != nil {
			log.Fatal("Erro ao conectar com o banco de dados:", err)
		}
		dbInstance = &Database{connection: conn}
	})
	return dbInstance
}

func main() {
	// Utiliza a mesma conexão em diferentes partes do código
	db := GetDatabaseInstance()
	fmt.Println("Conexão de banco de dados obtida com sucesso!")
}
```

### 2. Log Centralizado

Um sistema de log Singleton centraliza a coleta de eventos e facilita a depuração, garantindo que todas as mensagens sejam registradas em um único local.

```go
package main

import (
	"fmt"
	"log"
	"os"
	"sync"
)

type Logger struct {
	file *os.File
}

var loggerInstance *Logger
var logOnce sync.Once

// Função para obter instância única do Logger
func GetLoggerInstance() *Logger {
	logOnce.Do(func() {
		file, err := os.OpenFile("app.log", os.O_APPEND|os.O_CREATE|os.O_WRONLY, 0666)
		if err != nil {
			log.Fatal("Erro ao abrir o arquivo de log:", err)
		}
		loggerInstance = &Logger{file: file}
	})
	return loggerInstance
}

// Método para escrever no log
func (l *Logger) Log(message string) {
	fmt.Fprintln(l.file, message)
}

func main() {
	logger := GetLoggerInstance()
	logger.Log("Aplicação iniciada.")
	logger.Log("Primeira operação completada com sucesso.")
	fmt.Println("Mensagens registradas no log.")
}
```

### 3. Configuração Global

Para armazenar configurações globais que precisam ser acessadas por várias partes da aplicação, uma instância Singleton facilita o acesso e mantém a consistência dos dados.

```go
package main

import (
	"fmt"
	"sync"
)

type Config struct {
	DatabaseURL  string
	Port         int
	EnableLogging bool
}

var configInstance *Config
var configOnce sync.Once

// Função para obter instância única de Config
func GetConfigInstance() *Config {
	configOnce.Do(func() {
		configInstance = &Config{
			DatabaseURL:  "localhost:5432",
			Port:         8080,
			EnableLogging: true,
		}
	})
	return configInstance
}

func main() {
	config := GetConfigInstance()
	fmt.Printf("Conectando ao banco de dados em %s, porta: %d\n", config.DatabaseURL, config.Port)
	if config.EnableLogging {
		fmt.Println("Logging está ativado.")
	}
}
```

### 4. Cache Global

Um cache Singleton pode melhorar a performance da aplicação, permitindo que dados consultados frequentemente sejam armazenados para reutilização.

```go
package main

import (
	"fmt"
	"sync"
)

type Cache struct {
	data map[string]string
}

var cacheInstance *Cache
var cacheOnce sync.Once

// Função para obter instância única de Cache
func GetCacheInstance() *Cache {
	cacheOnce.Do(func() {
		cacheInstance = &Cache{data: make(map[string]string)}
	})
	return cacheInstance
}

// Função para adicionar valor ao cache
func (c *Cache) Set(key, value string) {
	c.data[key] = value
}

// Função para recuperar valor do cache
func (c *Cache) Get(key string) string {
	return c.data[key]
}

func main() {
	cache := GetCacheInstance()
	cache.Set("user1", "Alice")
	cache.Set("user2", "Bob")

	fmt.Println("Cache recuperado para user1:", cache.Get("user1"))
	fmt.Println("Cache recuperado para user2:", cache.Get("user2"))
}
```

---

Esses exemplos demonstram como o Singleton pode ser usado para diferentes casos em Go, assegurando que recursos globais sejam consistentes e de fácil acesso. Cada exemplo aborda um caso comum onde o Singleton ajuda a melhorar a estrutura e eficiência da aplicação.