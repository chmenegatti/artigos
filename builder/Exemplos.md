## Aqui estão exemplos práticos em Go baseados nos usos comuns que mencionei anteriormente para o padrão de projeto Builder:

### 1. Construtores de Interface do Usuário (UI)

Imagine que estamos construindo um painel de controle com diversos componentes opcionais:


```go
package main
import (
    "fmt"
)
// Dashboard represents a complex UI element
type Dashboard struct {
    Header  string
    Sidebar bool
    Footer  bool
    Widgets []string
}
// DashboardBuilder is the builder interface for Dashboard
type DashboardBuilder interface {
    SetHeader(header string) DashboardBuilder
    EnableSidebar() DashboardBuilder
    EnableFooter() DashboardBuilder
    AddWidget(widget string) DashboardBuilder
    Build() Dashboard
}
// dashboardBuilder implements the DashboardBuilder
type dashboardBuilder struct {
    header  string
    sidebar bool
    footer  bool
    widgets []string
}
func NewDashboardBuilder() DashboardBuilder {
    return &dashboardBuilder{}
}
func (b *dashboardBuilder) SetHeader(header string) DashboardBuilder {
    b.header = header
    return b
}
func (b *dashboardBuilder) EnableSidebar() DashboardBuilder {
    b.sidebar = true
    return b
}
func (b *dashboardBuilder) EnableFooter() DashboardBuilder {
    b.footer = true
    return b
}
func (b *dashboardBuilder) AddWidget(widget string) DashboardBuilder {
    b.widgets = append(b.widgets, widget)
    return b
}
func (b *dashboardBuilder) Build() Dashboard {
    return Dashboard{
        Header:  b.header,
        Sidebar: b.sidebar,
        Footer:  b.footer,
        Widgets: b.widgets,
    }
}
func main() {
    dashboard := NewDashboardBuilder().
        SetHeader("Admin Dashboard").
        EnableSidebar().
        AddWidget("Chart").
        AddWidget("Activity Feed").
        Build()
fmt.Printf("Dashboard created: %+v\n", dashboard)

}
```

### 2. Objetos de Configuração

Aqui é um exemplo de como usar um Builder para criar um objeto de configuração:

```go
package main

import (
    "fmt"
)

// Config represents a configuration object
type Config struct {
    Host         string
    Port         int
    EnableTLS    bool
    MaxRetries   int
    RetryTimeout int
}

// ConfigBuilder is the builder interface for Config
type ConfigBuilder interface {
    SetHost(host string) ConfigBuilder
    SetPort(port int) ConfigBuilder
    EnableTLS() ConfigBuilder
    SetMaxRetries(retries int) ConfigBuilder
    SetRetryTimeout(timeout int) ConfigBuilder
    Build() Config
}

// configBuilder implements the ConfigBuilder
type configBuilder struct {
    host         string
    port         int
    enableTLS    bool
    maxRetries   int
    retryTimeout int
}

func NewConfigBuilder() ConfigBuilder {
    return &configBuilder{}
}

func (b *configBuilder) SetHost(host string) ConfigBuilder {
    b.host = host
    return b
}

func (b *configBuilder) SetPort(port int) ConfigBuilder {
    b.port = port
    return b
}

func (b *configBuilder) EnableTLS() ConfigBuilder {
    b.enableTLS = true
    return b
}

func (b *configBuilder) SetMaxRetries(retries int) ConfigBuilder {
    b.maxRetries = retries
    return b
}

func (b *configBuilder) SetRetryTimeout(timeout int) ConfigBuilder {
    b.retryTimeout = timeout
    return b
}

func (b *configBuilder) Build() Config {
    return Config{
        Host:         b.host,
        Port:         b.port,
        EnableTLS:    b.enableTLS,
        MaxRetries:   b.maxRetries,
        RetryTimeout: b.retryTimeout,
    }
}

func main() {
    config := NewConfigBuilder().
        SetHost("localhost").
        SetPort(8080).
        EnableTLS().
        SetMaxRetries(5).
        SetRetryTimeout(30).
        Build()

    fmt.Printf("Config created: %+v\n", config)
}

```

3. Geração de Documentos
Um exemplo de Builder para criar um documento simples com seções e parágrafos:

```go

package main

import (
    "fmt"
    "strings"
)

// Document represents a structured document
type Document struct {
    Title    string
    Sections []Section
}

type Section struct {
    Heading string
    Content string
}

// DocumentBuilder is the builder interface for Document
type DocumentBuilder interface {
    SetTitle(title string) DocumentBuilder
    AddSection(heading, content string) DocumentBuilder
    Build() Document
}

// documentBuilder implements the DocumentBuilder
type documentBuilder struct {
    title    string
    sections []Section
}

func NewDocumentBuilder() DocumentBuilder {
    return &documentBuilder{}
}

func (b *documentBuilder) SetTitle(title string) DocumentBuilder {
    b.title = title
    return b
}

func (b *documentBuilder) AddSection(heading, content string) DocumentBuilder {
    b.sections = append(b.sections, Section{Heading: heading, Content: content})
    return b
}

func (b *documentBuilder) Build() Document {
    return Document{
        Title:    b.title,
        Sections: b.sections,
    }
}

func (doc Document) String() string {
    var sb strings.Builder
    sb.WriteString("Title: " + doc.Title + "\n")
    for _, section := range doc.Sections {
        sb.WriteString("\n" + section.Heading + "\n")
        sb.WriteString(section.Content + "\n")
    }
    return sb.String()
}

func main() {
    document := NewDocumentBuilder().
        SetTitle("Project Report").
        AddSection("Introduction", "This document provides an overview of the project...").
        AddSection("Conclusion", "The project was successful...").
        Build()

    fmt.Println(document)
}

```

Esses exemplos ilustram como o padrão Builder pode ser aplicado em diversos cenários práticos, permitindo a construção de objetos complexos de forma clara e organizada.
