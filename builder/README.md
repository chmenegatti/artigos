# Entendendo o Padrão de Projeto Builder em Go

## Introdução ao Padrão de Projeto Builder

O Padrão de Projeto Builder é um padrão de criação usado para construir objetos complexos passo a passo. Diferente de outros padrões de criação que geram objetos em uma única etapa, o padrão Builder oferece mais granularidade e controle sobre o processo de criação. Ele é particularmente útil quando um objeto requer várias etapas ou configurações antes de estar pronto para uso.
Usos Comuns do Padrão Builder

- Construção de Objetos Complexos: Ideal quando se constroem objetos que requerem múltiplas configurações ou possuem inúmeros componentes opcionais.
- Objetos Imutáveis: Útil para criar objetos imutáveis onde o objeto completo precisa ser construído antes do uso.
- Legibilidade: Melhora a legibilidade do código quando construtores ou fábricas estáticas se tornam complicados devido a muitos parâmetros.

## Prós e Contras

### Prós:

- Controle: Oferece controle preciso sobre o processo de construção.
- Separação: Separa a lógica de construção da representação, promovendo um código mais limpo e fácil de manter.
- Reusabilidade: O mesmo processo de construção pode ser usado para criar diferentes representações ou configurações do mesmo objeto.

### Contras:

- Complexidade: Pode aumentar a complexidade do código quando apenas uma construção simples é necessária.
- Overhead: Pode envolver mais classes, resultando em overhead e potencialmente mais código repetitivo.

## Implementando o Padrão Builder em Go

Abaixo está um exemplo de como o padrão Builder pode ser implementado em Go:

```go
package main

import (
    "fmt"
)

// Car representa o produto sendo construído
type Car struct {
    Brand     string
    Model     string
    Year      int
    Features  []string
}

// CarBuilder é a interface para construir um Car
type CarBuilder interface {
    SetBrand(brand string) CarBuilder
    SetModel(model string) CarBuilder
    SetYear(year int) CarBuilder
    AddFeature(feature string) CarBuilder
    Build() Car
}

// carBuilder implementa a interface CarBuilder
type carBuilder struct {
    brand    string
    model    string
    year     int
    features []string
}

func NewCarBuilder() CarBuilder {
    return &carBuilder{}
}

func (b *carBuilder) SetBrand(brand string) CarBuilder {
    b.brand = brand
    return b
}

func (b *carBuilder) SetModel(model string) CarBuilder {
    b.model = model
    return b
}

func (b *carBuilder) SetYear(year int) CarBuilder {
    b.year = year
    return b
}

func (b *carBuilder) AddFeature(feature string) CarBuilder {
    b.features = append(b.features, feature)
    return b
}

func (b *carBuilder) Build() Car {
    return Car{
        Brand:    b.brand,
        Model:    b.model,
        Year:     b.year,
        Features: b.features,
    }
}

func main() {
    car := NewCarBuilder().
        SetBrand("Toyota").
        SetModel("Corolla").
        SetYear(2023).
        AddFeature("Teto solar").
        AddFeature("Bancos de couro").
        Build()

    fmt.Printf("Carro construído: %+v\n", car)
}
´´´

### Explicação do Código

- Interfaces e Estruturas: Definimos uma interface CarBuilder que delineia os métodos necessários para definir as propriedades de um Car. A estrutura carBuilder implementa essa interface.
- Interface Fluente: Cada método no builder retorna o próprio builder (CarBuilder). Isso permite o encadeamento de métodos, facilitando uma forma limpa e legível de construir o objeto.
- Método Build: O método Build() finaliza a construção do objeto e retorna o Car totalmente construído.

## Exemplos Práticos

- Construtores de Interface do Usuário (UI): Construção de elementos de UI complexos com vários componentes opcionais.
- Objetos de Configuração: Construção de objetos de configuração onde nem todas as configurações são obrigatórias.
- Geração de Documentos: Criação de documentos estruturados como PDFs ou páginas HTML, onde os elementos são opcionais e a ordem é importante.

Através deste exemplo, vemos como o Padrão de Projeto Builder fornece uma abordagem flexível e sistemática para construir objetos complexos, tornando-se uma ferramenta valiosa no desenvolvimento de software.
