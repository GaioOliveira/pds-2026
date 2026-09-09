# Estudo de Caso Integrado: App "IFBank" (Módulo Pix)

**Objetivo de Aprendizagem:** 
Integrar os conhecimentos de Elicitação de Requisitos (Casos de Uso), Comportamento (Sequência) e Estrutura (Classes) na modelagem de um aplicativo financeiro.

---

### 🏦 O Cenário

O **IFBank** é um banco digital que está redesenhando o seu aplicativo. A diretoria pediu que a sua equipe de análise modele a principal funcionalidade do sistema: a **Área do Pix**. 

O aplicativo deve permitir que o cliente consulte seu saldo, cadastre suas chaves Pix e, o mais importante, realize transferências via Pix. 

Para realizar um Pix, o sistema tem algumas regras de negócio estritas:
1. O cliente já deve estar logado no aplicativo.
2. O sistema deve validar se a chave Pix de destino existe (simular uma comunicação com o sistema central do Banco Central - BACEN).
3. O cliente deve ter saldo suficiente na conta.
4. Ao finalizar, o valor deve ser debitado da conta do cliente, uma transação deve ser salva no extrato e um comprovante deve ser gerado na tela.

Sua missão é criar um material como um "Dossiê de Análise" deste módulo passando por três etapas.

---

### 📝 Etapa 1: O Levantamento (Casos de Uso)

Antes de pensar em código, precisamos mapear as funcionalidades e o roteiro exato de uso.

**A. Diagrama de Casos de Uso:**
Desenhe um diagrama que inclua:
* **Atores:** O `Cliente` e o `Sistema BACEN` .
* **Casos de Uso principais:** `Consultar Saldo`, `Cadastrar Chave Pix`, `Realizar Pix` e `Autenticar Usuário`.
* **Relacionamento:** Lembre-se de usar `<<include>>` onde for conveniente.

**B. Descrição Textual:**
Faça a descrição textual detalhada **apenas** do caso de uso **"Realizar Pix"**. 
* Defina as *Pré-condições* (ex: ter saldo, estar logado).
* Escreva o *Fluxo Principal* passo a passo (Cliente digita chave -> Sistema busca dados -> Cliente digita valor...).
* Crie pelo menos **dois Fluxos de Exceção** (Ex: [FE-01] Saldo Insuficiente; [FE-02] Chave Pix Inválida).

---

### 📝 Etapa 2: A Interação (Diagrama de Sequência)

Agora, vamos focar no comportamento interno. Como os objetos do sistema "conversam" para fazer o Pix acontecer?

Desenhe o Diagrama de Sequência para o **Fluxo Principal** do caso de uso "Realizar Pix".
* **Objetos sugeridos:** `:TelaPix`, `:ControladorPix`, `:Conta` e o próprio ator `:Cliente`. Você também pode representar o `:SistemaBACEN` recebendo uma mensagem de validação.
* **O Fluxo:** Mostre as chamadas de método. Exemplo: A tela pede para o controlador validar a chave; o controlador pede para a conta verificar o saldo (`verificarSaldo(valor)`); se tudo der certo, o controlador pede para a conta `debitar(valor)`.
* **Dica:** Use um bloco `alt / else` (condição) para mostrar o que acontece se o saldo for aprovado vs. reprovado.

---

### 📝 Etapa 3: A Estrutura (Diagrama de Classes)

Com base nos passos e ações que você definiu nas Etapas 1 e 2, construa a "estrutura" desse sistema bancário.

Desenhe o Diagrama de Classes focando no núcleo do sistema:
* **Classes obrigatórias:** `Cliente`, `Conta`, `Transacao`, `ChavePix`.
* **Atributos:** Pense nas informações cruciais. A Conta tem `saldo`, `numero`, `agencia`. A Transação tem `valor`, `data`, `tipo`. Lembre-se de usar o **encapsulamento** (atributos privados `-`). A classe `ChavePIX` pode ter:  tipo (é CPF, CNPJ, E-mail, Telefone ou Aleatória, poderia ser um Enum),
valor: a string em si (ex: "joao@email.com"), dataCadastro (quando foi registrada), status (está ativa, inativa).
* **Métodos:** Traga as ações que você usou no Diagrama de Sequência para cá. A classe `Conta` precisará de métodos públicos (`+`) como `debitar(valor)` e `creditar(valor)`.
* **Relacionamentos:** Conecte as classes com as associações corretas e suas **multiplicidades**. (Ex: Um Cliente tem quantas Contas? 1 ou muitas? Uma Conta tem quantas Transações no extrato?).

---

### 📝 Entregas

Ao final, sua equipe deve entregar um documento contendo:
1. Imagem do Diagrama de Casos de Uso.
2. Texto com a Descrição do "Realizar Pix".
3. Imagem do Diagrama de Sequência do Pix.
4. Imagem do Diagrama de Classes.
