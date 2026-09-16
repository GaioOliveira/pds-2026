# Atividade: Da Modelagem à Implementação em Java
## Sistema de Vendas da Cantina Escolar

---

## 1. Enunciado do Problema

A cantina de uma escola deseja informatizar o processo de venda de lanches e bebidas. Atualmente, os pedidos são anotados em papel e os cálculos são feitos manualmente, o que gera filas longas no intervalo e erros frequentes nos valores.

O novo sistema deve permitir que:

- Os **clientes** possam consultar o cardápio, escolher produtos, informar quantidades, fechar o pedido e realizar o pagamento.
- Os **atendentes** possam registrar a venda, receber o pagamento e emitir um comprovante simples.
- O **gerente** possa cadastrar produtos, alterar preços, atualizar estoques e consultar vendas realizadas.

### Regras de Negócio

1. Cada **Produto** possui:
   - código (identificador único);
   - nome;
   - categoria (ex.: lanche, bebida, doce);
   - preço unitário;
   - quantidade em estoque.

2. Um **Pedido** pode conter um ou mais itens.

3. Cada **ItemDoPedido** registra:
   - produto escolhido;
   - quantidade solicitada;
   - subtotal (preço unitário × quantidade).

4. O sistema deve calcular o **valor total** do pedido somando os subtotais dos itens.

5. O **Pagamento** pode ser realizado em:
   - dinheiro;
   - PIX;
   - cartão de crédito ou débito.
   Ele representa a etapa em que um pedido recebe uma forma de quitação financeira. Não é responsável por calcular o valor do pedido: essa é a responsabilidade de Pedido. Sua responsabilidade é registrar como o cliente pagou, quanto pagou e se o pagamento é suficiente para encerrar a compra.



6. Um pedido só pode ser **finalizado** se:
   - tiver pelo menos um item;
   - todos os produtos tiverem estoque suficiente;
   - o valor pago for suficiente para cobrir o total.

7. Um produto **não pode ser vendido** se estiver sem estoque.

8. O sistema deve registrar **data e hora** de cada venda.

9. O gerente pode:
   - cadastrar novos produtos;
   - alterar preços;
   - atualizar estoques (entrada ou saída);
   - remover produtos do cardápio (quando não forem mais comercializados).

#### Situação de Exemplo para Facilitar a Compreensão do Processo ####

- O pedido tem duas coxinhas de R$ 6,50 e um suco de R$ 5,00.
- A classe `Pedido` calcula o total: R$ 18,00.
- O cliente informa que pagará em dinheiro e entrega R$ 20,00.
- A classe `Pagamento` guarda o tipo `DINHEIRO` e o valor `20,00`.
- O sistema verifica se R$ 20,00 é suficiente para R$ 18,00.
- Como é suficiente, a classe `Pagamento` calcula o troco: R$ 2,00.




---

## 2. Tarefas 

### Tarefa 1 – Casos de Uso

A partir do enunciado:

1. Identifique os **atores** do sistema.
2. Liste os **casos de uso** principais.
3. Descreva **textualmente** pelo menos dois casos de uso, incluindo:
   - objetivo;
   - atores envolvidos;
   - fluxo principal (passo a passo);
   - pelo menos um fluxo alternativo ou exceção.


### Tarefa 2 – Diagrama de Classes

Com base nos casos de uso e nas regras de negócio, elabore o **diagrama de classes** do sistema, contendo:

1. As **classes** identificadas;
2. Os **atributos** de cada classe (com tipo, se possível);
3. Os **métodos** principais de cada classe;
4. Os **relacionamentos** entre as classes, indicando:
   - tipo (associação, agregação, composição, generalização);
   - multiplicidade (1, 0..1, 1..*, etc);
   - papéis (quando fizer sentido).

Entregue o diagrama em formato digital (ex.: draw.io, Lucidchart, PlantUML, Mermaid).

### Tarefa 3 – Implementação em Java

Implemente em Java o núcleo do sistema, contendo **pelo menos** as seguintes classes:

- `Produto`
- `ItemPedido`
- `Pedido`
- `Pagamento`

Requisitos mínimos:

1. Cada classe deve ter:
   - atributos privados;
   - construtor;
   - métodos getters e setters quando necessário;
   - métodos de comportamento coerentes com o diagrama.

2. A classe `Pedido` deve:
   - armazenar uma lista de `ItemPedido`;
   - possuir método para adicionar item;
   - possuir método para calcular o total do pedido.

3. A classe `ItemPedido` deve:
   - armazenar referência a um `Produto`;
   - armazenar quantidade;
   - calcular subtotal.

4. A classe `Pagamento` deve:
   - armazenar tipo de pagamento;
   - armazenar valor pago;
   - possuir método para validar se o pagamento é suficiente.

5. Crie uma classe `Main` (ou `TesteSistema`) com um método `main` que:
   - cadastre alguns produtos;
   - simule a criação de um pedido;
   - adicione itens ao pedido;
   - realize um pagamento;
   - imprima no console um resumo da venda.

---

## 3. Critérios de Avaliação

### Casos de Uso (3 pontos)
- Identificação correta dos atores (0,5)
- Lista coerente de casos de uso (0,5)
- Descrição clara de pelo menos dois casos de uso (1,0)
- Inclusão de fluxos alternativos ou exceções (1,0)

### Diagrama de Classes (4 pontos)
- Classes adequadas ao problema (1,0)
- Atributos e métodos coerentes (1,0)
- Relacionamentos corretos e bem indicados (1,5)
- Legibilidade e organização do diagrama (0,5)

### Implementação em Java (3 pontos)
- Estrutura correta das classes (1,0)
- Lógica de cálculo de totais e subtotais (1,0)
- Funcionamento do teste no `main` (1,0)

---

## 4. Prazo e Entrega

- **Prazo:** 23/09/2026
- **Entrega:** repositório individual do GitHub em pasta com o nome GradedIndividualTask

---

**Observação:** Este é um exercício de modelagem e programação. Não é necessário implementar interface gráfica, banco de dados ou persistência (caso alguém já possua esse conhecimento). Foque na qualidade da modelagem e na coerência entre requisitos, diagrama e código.

`Have fun with it!`
