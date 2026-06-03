# Prova técnica - Analista de Qualidade (QA)

## 📋 Instruções Gerais para o(a) candidato(a)
* **Objetivo:** Avaliar sua capacidade de análise, escrita de cenários de teste, reporte de bugs e conhecimentos básicos de automação de testes.
* **Prazo de Entrega:** : 4 dias úteis
* **Formato de Entrega:** Link de um repositório público no GitHub contendo:
    1. Um arquivo `RESPOSTAS.md` com as partes conceituais e escritas.
    2. A pasta do projeto de automação com as instruções de execução no `README.md`.
* **Ferramentas Recomendadas para a Automação:** Cypress, Jest ou Selenium (fique à vontade para escolher a que tiver mais familiaridade).

> Você não precisa entregar todas as questões, faça elas conforme o seu domínio técnico. Mas saiba que quanto mais completa for a entrega, maior serão as suas chances na vaga.

## Contexto do Desafio 1
O nosso ERP possui um módulo de e-commerce e frente de caixa. Estamos lançando uma nova funcionalidade de **"Cadastro e Venda de Roupas com Grade Inteligente"**. Agora, o lojista pode cadastrar um produto (ex: *Camiseta Polo*) e definir variações de **Tamanho** (P, M, G, GG) e **Cor** (Azul, Preto), atrelando o estoque real a cada combinação. Se o estoque de uma variação zerar, o sistema deve impedir a venda dessa variação específica, mas permitir as demais.

### Questão 1: Engenharia de Testes e Análise de Cenários
Imagine que a especificação técnica diz apenas: *"O sistema deve permitir a compra de roupas escolhendo tamanho e cor, validando se há estoque disponível para a combinação selecionada."*
* **Sua tarefa:** Utilizando a linguagem Gherkins, escreva pelo menos **6 cenários de teste** fundamentais para garantir que essa funcionalidade de grade e estoque funcione corretamente no carrinho de compras.

### Questão 2: Documentação e Reporte de Bug 
Durante seus testes manuais no ambiente de homologação, você encontrou o seguinte comportamento: 
> *Ao selecionar a 'Camiseta Polo' na cor 'Preto' e tamanho 'GG', o preço unitário do produto no carrinho muda de R$ 89,90 para R$ 0,00. Se o usuário prosseguir para o checkout, ele consegue fechar a compra sem pagar pelo produto. Isso só acontece especificamente na combinação Preto + GG.*
* **Sua tarefa:** Escreva um **Reporte de Bug (Issue)** profissional para o time de desenvolvimento. O reporte deve conter: Título claro, Passos para Reproduzir, Resultado Esperado, Resultado Atual, Severidade/Prioridade e uma sugestão de qual dado/evidência seria útil anexar.

### Questão 3: Automação de Testes de Interface - E2E (Prática)
Para demonstrar seus conhecimentos em automação, crie um script básico utilizando **Cypress, Selenium ou Jest** (simulando a interface).
Como o sistema do ERP é privado, você deve automatizar um fluxo análogo em um site público de testes (sugerimos o [Sauce Demo](https://www.saucedemo.com/)).
* **Sua tarefa:** Escreva um script de automação que:
    1. Faça login com o usuário `standard_user` e senha `secret_sauce`.
    2. Adicione o produto "Sauce Labs Backpack" ao carrinho.
    3. Acesse o carrinho e valide se o produto está presente lá.

### Questão 4: Testes de API e Integração (Conceitual + Prática)
O carrinho de compras do ERP consome uma API para verificar o estoque antes de finalizar o pedido. O endpoint é: `GET /api/v1/produtos/{id}/estoque?cor={cor}&tamanho={tamanho}`.
* **Sua tarefa:**
* 1. Explique textualmente quais validações você faria nessa API (pense em Status Codes, tipos de dados e caminhos de exceção).
  2.  *(Opcional Prático/Diferencial)*: Escreva um exemplo de teste de API simples (pode ser usando `cy.request` no Cypress, `axios` no Jest ou a biblioteca de sua preferência) que valide que o endpoint retorna o Status `200 OK` e que o corpo da resposta traz um campo numérico chamado `quantidade_disponivel`. (Você pode mockar a resposta se preferir, ou apenas escrever a estrutura do código).

------------------------------------

## 🤖 Agora vamos para um novo desafio: Foco em Automação de Mensagens (WhatsApp) e Agentes de IA

**Contexto do Desafio:** Nossa plataforma permite que empresas criem **Fluxos de Mensagens Automatizados** e configurem **Agentes de IA** para atender clientes no WhatsApp. O fluxo funciona assim: O cliente manda um "Olá" -> O Agente de IA intercepta a mensagem -> Pergunta o nome e o interesse do cliente -> Salva esses dados no painel web da nossa empresa -> Encaminha o cliente para o setor correto.

### Questão 5: Estratégia de Testes para Inteligência Artificial (Conceitual)
Testar IA é diferente de testar sistemas tradicionais determinísticos, pois a IA pode responder a mesma pergunta de formas diferentes.
* **Sua tarefa:** Explique, com suas palavras, como você planejaria a estratégia de testes para garantir a qualidade desse Agente de IA. Como você testaria:
    1. O "Caminho Feliz" (o cliente responde exatamente o que a IA pede).
    2. O "Fallback" (o cliente fala algo totalmente aleatório, envia apenas um emoji ou usa palavras ofensivas).

### Questão 6: Documentação e Reporte de Bug de Integração 
Durante os testes de integração entre o WhatsApp e a nossa plataforma, você descobriu o seguinte problema:
> *Quando um cliente envia uma mensagem de texto normal, tudo funciona. Porém, se o cliente envia uma 'Mensagem de Áudio' ou uma 'Imagem', o webhook da nossa plataforma recebe o evento, não consegue tratar o formato e retorna um Erro HTTP 500, derrubando o fluxo daquele cliente, que fica travado sem receber mais nenhuma resposta do bot.*
* **Sua tarefa:** Escreva um **Reporte de Bug (Issue)** detalhado para que o desenvolvedor backend possa corrigir o problema. Lembre-se de incluir o comportamento esperado e as informações técnicas necessárias (ex: menção a logs, status code, payload).

### Questão 7: Testes de Regressão em Fluxos Dinâmicos (Conceitual)
Imagine que o time de desenvolvimento alterou o "Prompt Base" (as instruções de comportamento) da IA para deixá-la com um tom de voz mais formal e corporativo.
* **Sua tarefa:** Pensando que essa alteração pode impactar as respostas anteriores da IA, o que são **Testes de Regressão** e como você aplicaria esse conceito para garantir que essa mudança de tom de voz não quebrou as regras de negócio anteriores (como capturar o nome do cliente e salvar no banco)?
