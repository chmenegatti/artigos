# Design Patterns em Golang

Este repositório contém uma coleção de artigos e exemplos práticos sobre Design Patterns implementados em Golang. Cada padrão está em sua própria pasta, contendo um README com explicações detalhadas e exemplos de código.

## Padrões Disponíveis

### Padrões Criacionais

- [Singleton](./singleton/README.md): Garante que uma classe tenha apenas uma instância e fornece um ponto global de acesso a ela.

- [Builder](./builder/README.md): Separa a construção de um objeto complexo da sua representação, permitindo o mesmo processo de construção criar diferentes representações. 

- [Factory Method](./factory-method/README.md): Define uma interface para criar um objeto, mas permite que as subclasses decidam qual classe instanciar. (breve)

- [Abstract Factory](./abstract-factory/README.md): Fornece uma interface para criar famílias de objetos relacionados ou dependentes sem especificar suas classes concretas. (breve)

- [Prototype](./prototype/README.md): Especifica os tipos de objetos a serem criados usando uma instância prototípica e cria novos objetos copiando este protótipo.(breve)

### Padrões Estruturais

- [Adapter](./adapter/README.md): Permite que interfaces incompatíveis trabalhem juntas. (breve)

- [Bridge](./bridge/README.md): Separa uma abstração da sua implementação para que as duas possam variar independentemente. (breve)

- [Composite](./composite/README.md): Compõe objetos em estruturas de árvore para representar hierarquias parte-todo. (breve)

- [Decorator](./decorator/README.md): Adiciona responsabilidades adicionais a um objeto dinamicamente. (breve)

- [Facade](./facade/README.md): Fornece uma interface unificada para um conjunto de interfaces em um subsistema. (breve)

### Padrões Comportamentais

- [Observer](./observer/README.md): Define uma dependência um-para-muitos entre objetos para que quando um objeto mude de estado, todos os seus dependentes sejam notificados e atualizados automaticamente. (breve)

- [Strategy](./strategy/README.md): Define uma família de algoritmos, encapsula cada um deles e os torna intercambiáveis. (breve)

- [Command](./command/README.md): Encapsula uma solicitação como um objeto, permitindo parametrizar clientes com diferentes solicitações, enfileirar ou registrar solicitações e suportar operações que podem ser desfeitas. (breve)

- [State](./state/README.md): Permite que um objeto altere seu comportamento quando seu estado interno muda. (breve)

- [Chain of Responsibility](./chain-of-responsibility/README.md): Passa a solicitação ao longo de uma cadeia de manipuladores. Ao receber uma solicitação, cada manipulador decide processar a solicitação ou passá-la para o próximo manipulador na cadeia. (breve)

## Como Usar

Cada pasta contém um README.md com uma explicação detalhada do padrão, suas características, vantagens, desvantagens e exemplos de implementação em Golang. Para explorar um padrão específico, basta clicar no link correspondente acima.

## Contribuindo

Contribuições são bem-vindas! Se você tem um exemplo de Design Pattern em Golang que gostaria de adicionar, ou se encontrou um erro em um dos exemplos existentes, sinta-se à vontade para abrir uma issue ou enviar um pull request.

## Licença

Este projeto está licenciado sob a licença MIT - veja o arquivo [LICENSE.md](LICENSE.md) para detalhes.
