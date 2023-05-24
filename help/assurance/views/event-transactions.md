---
title: Exibição de Transações de Evento
description: Este guia detalha informações sobre a exibição de Transações de evento no Adobe Experience Platform Assurance.
exl-id: ad97f2c1-5bbc-49e2-8378-edcb8af149a3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# Exibição de Transações de Evento

A visualização Transações de evento no Adobe Experience Platform Assurance permite validar e depurar a implementação do cliente da Rede de borda e ver os resultados da validação de upstream em tempo quase real.

## Configurar a garantia para o fluxo de trabalho da rede de borda

Depois [configurar o Assurance](../tutorials/implement-assurance.md), certifique-se de que você implementou as versões mais recentes do Assurance e das extensões de Rede de borda no aplicativo.

Para exibir os eventos, selecione no menu do lado esquerdo **[!UICONTROL Transações de Evento]** no **[!UICONTROL Adobe Experience Platform Edge]** seção.

Se você não vir essa opção, selecione **[!UICONTROL Configurar]** na parte inferior esquerda da janela, adicione o **[!UICONTROL Transações de Evento]** exibir e selecionar **[!UICONTROL Salvar]**.

## Introdução ao uso da visualização Transações de evento

Nesta seção, familiarize-se com a exibição Transação de evento e saiba como usá-la com eficiência para validação completa em workflows da Rede de borda.

### Fluxo de processamento de evento

![Exibição de transações de evento](./images/event-transactions/event-transactions-view.png)

A view Transações do Evento exibe três colunas na ordem do fluxo de processamento do evento:

- **[!UICONTROL Lado do cliente]**: essa coluna exibe os eventos processados ou recebidos no lado do cliente, acessíveis ao SDK móvel. Isso inclui os eventos que foram criados usando uma chamada de API, como `Edge.sendEvent`e os manipuladores de eventos de resposta recebidos pelo cliente do servidor da Rede de borda, se houver. Exemplos de eventos do lado do cliente:
   - O Evento de solicitação da AEP é o evento enviado por meio da extensão do Edge e contém o XDM e os dados opcionais de formato livre.
   - O identificador de evento de resposta da AEP é o identificador de evento recebido da rede de borda em resposta a um evento de solicitação da AEP. Um evento de solicitação pode receber nenhum, um ou vários identificadores de evento de resposta.
   - A resposta de erro da AEP pode ser vista em caso de erro, por exemplo, se a carga XDM não puder ser processada ou se um dos serviços upstream retornar um erro ou aviso.
- **[!UICONTROL Rede de borda]**: essa coluna exibe o evento recebido no lado do servidor pela Rede de borda por meio de uma solicitação de rede e quais dados e metadados o evento continha.
- **[!UICONTROL Upstream]**: essa coluna exibe os eventos recebidos pelos serviços upstream configurados, incluindo informações detalhadas sobre os resultados do processamento e/ou validação para o evento de entrada.
Observe que essa coluna é dinâmica e pode exibir diferentes tipos de informações, dependendo de dois fatores principais:
   - A configuração da sequência de dados e os serviços ativados nela.
   - O tipo de evento enviado para a Rede de borda.

### Eventos do Inspect

Os eventos exibidos na visualização Transações do evento fornecem informações sobre o formato e o conteúdo dos dados que estão sendo processados em cada estado, bem como detalhes relevantes sobre avisos ou erros encontrados quando os dados são processados upstream. A exibição ajuda a restringir as informações de depuração no nível de evento/solicitação e a identificar erros antecipadamente no ciclo de desenvolvimento.

#### Expandir os detalhes do evento

Para inspecionar um evento, selecione o evento desejado na exibição. Essa ação expande a **[!UICONTROL Detalhes do evento]** no lado direito da tela.
Os dados aninhados são exibidos em formato de árvore. É possível inspecionar valores de chave aninhados selecionando o **+** (mais) à esquerda do nome da chave.

![Detalhes do evento](./images/event-transactions/event-details.png)

#### Avisos ou erros do Inspect

Cada nome de evento recebe o prefixo de um ícone que indica o status de alto nível do processamento desse evento:

- Se o evento foi processado com êxito, uma marca de seleção verde será exibida.
- Se forem detectados avisos ou erros, será exibido um sinal de aviso. Selecione o evento relacionado para saber mais sobre a causa do aviso ou erro no **[!UICONTROL Detalhes do evento]** exibição.

### Definições de configuração

Você pode verificar o identificador de sequência de dados usado no momento selecionando a dica de ferramenta de informações ao lado da **[!UICONTROL Rede de borda]** cabeçalho da coluna.

![Mostrar a ID do fluxo de dados](./images/event-transactions/show-datastream-id.png)

>[!INFO]
>
>Quando vários clientes se conectam à mesma sessão do Assurance e IDs de fluxo de dados diferentes são usadas, todos eles são exibidos aqui. No entanto, isso não significa que sua implementação atual esteja usando vários fluxos de dados. Somente a ID da sequência de dados atual definida na tag (propriedade móvel) usada pelo aplicativo é usada para processar novos eventos desse cliente. Ao testar casos de uso mais complicados com diferentes configurações e vários clientes conectados, pode ser útil usar sessões do Assurance separadas para simplificar o processo de validação.
