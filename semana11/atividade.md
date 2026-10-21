## Atividade Prática: Modelagem de Ciclo de Vida (Diagrama de Estados)

**Contexto do Problema: O Bug do "IFDelivery"**

A startup "IFDelivery" está crescendo rápido, mas a equipe de suporte tem recebido dezenas de reclamações diárias relatando bugs bizarros no aplicativo. Os clientes relatam que:
* Pedidos estão sendo cancelados *depois* de já estarem na mochila do motoboy.
* O sistema está tentando enviar novos pedidos para motoboys que já estão no meio de uma entrega.
* Restaurantes estão começando a preparar pedidos que ainda não tiveram o pagamento aprovado no cartão.

**O Diagnóstico:** O sistema perdeu o controle sobre "em que fase" as coisas estão. A equipe de desenvolvimento pediu a ajuda de vocês (Analistas de Sistemas) para mapear o ciclo de vida exato das duas principais entidades do sistema para que eles possam travar essas ações indevidas no código.

---

### 🎯 Sua Missão

Sua equipe deve analisar as regras de negócio abaixo e construir **dois Diagramas de Estados** distintos: um para o objeto `Pedido` e outro para o objeto `Entregador`.

#### Parte 1: O Ciclo de Vida do Objeto `Pedido`
Leia o roteiro abaixo e identifique os estados e os eventos (gatilhos) que mudam o estado do pedido.

1. Quando o cliente finaliza o carrinho, o pedido nasce no estado **Aguardando Pagamento**.
2. Se o cliente solicitar o cancelamento aqui, ele vai para o estado final **Cancelado**.
3. Quando o evento `processarPagamento()` ocorre com a guarda `[aprovado]`, ele avança para **Aguardando Restaurante**. (Se a guarda for `[recusado]`, ele vai para Cancelado).
4. O restaurante recebe o alerta. Quando aciona `aceitarPedido()`, o status muda para **Em Preparo**. *(Atenção: A partir daqui, o cliente não pode mais cancelar o pedido pelo app!)*
5. Quando o cozinheiro aciona `finalizarPreparo()`, o pedido fica **Pronto para Coleta**.
6. O motoboy chega e aciona `biparPacote()`, mudando o pedido para **Em Rota**.
7. Ao chegar na casa do cliente, o motoboy aciona `confirmarEntrega()`, levando o pedido ao seu estado final: **Entregue**.

*-> Crie o Diagrama de Estados para a classe `Pedido`.*

#### Parte 2: O Ciclo de Vida do Objeto `Entregador`
O entregador tem um ciclo de vida diferente, que se repete em loop de forma paralela aos pedidos.

1. Quando o motoboy abre o app, ele está **Offline** (Estado Inicial).
2. Ao apertar o botão `ficarOnline()`, ele muda para o estado **Disponível**.
3. Enquanto está Disponível, o sistema pode enviar uma notificação. Se ele acionar `aceitarCorrida()`, seu estado muda para **A Caminho do Restaurante**.
4. Ao chegar no local, ele aperta `confirmarChegada()` e seu estado muda para **Aguardando Pacote**.
5. Quando o restaurante entrega o pacote, ele aciona `iniciarRota()` e muda para **Realizando Entrega**.
6. Ao entregar na casa do cliente, ele aperta `finalizarEntrega()`. Neste momento, ele não "morre" (não é estado final), ele volta automaticamente para o estado **Disponível**, pronto para uma nova corrida.
7. O estado final só ocorre se, estando no estado Disponível, ele acionar `ficarOffline()`.

*-> Crie o Diagrama de Estados para a classe `Entregador`.*

---

### 💡 Dicas do Professor para a Modelagem:
* Lembrem-se das bolinhas pretas: Todo diagrama precisa de um **Estado Inicial** (bolinha preenchida) e um **Estado Final** (bolinha preenchida com um círculo em volta).
* **Estado não é ação!** "Entregando" ou "Em Rota" são bons nomes de estados. "Entregar Pacote" é uma ação (o evento que vai na seta).
* Verifiquem a lógica do Entregador: percebam que o ciclo de vida dele tem um **loop** de repetição, enquanto o do pedido é linear até "morrer" (ser entregue).
