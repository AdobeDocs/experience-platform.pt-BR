---
title: Exibição de Transações de Evento
description: Este guia detalha informações sobre a exibição Transações de evento no Adobe Experience Platform Assurance.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---


# Exibição de Transações de Evento

A exibição Transações de evento no Adobe Experience Platform Assurance permite validar e depurar a implementação do cliente da Rede de Borda e ver os resultados da validação upstream em tempo quase real.

## Configurar o Controle para o Fluxo de Trabalho da Rede de Borda

Depois [configuração de garantia](../tutorials/implement-assurance.md), certifique-se de ter implementado as versões mais recentes das extensões Assurance e Edge Network no seu aplicativo.

Para visualizar os eventos, selecione no menu à esquerda **[!UICONTROL Transações de Evento]** nos termos do **[!UICONTROL Adobe Experience Platform Edge]** seção.

Se não vir essa opção, selecione **[!UICONTROL Configurar]** na parte inferior esquerda da janela , adicione o **[!UICONTROL Transações de Evento]** exibir e selecionar **[!UICONTROL Salvar]**.

## Introdução ao uso da exibição Transações de Evento

Nesta seção, familiarize-se com a visualização Transação de evento e saiba como usá-la com eficiência para validação completa em workflows de rede de borda.

### Fluxo de processamento de evento

![Exibição de transações de evento](./images/event-transactions/event-transactions-view.png)

A exibição Transações de Evento exibe três colunas na ordem do fluxo de processamento do evento:

- **[!UICONTROL Lado do cliente]**: Essa coluna exibe os eventos processados ou recebidos no lado do cliente, acessíveis ao Mobile SDK. Isso inclui os eventos que foram criados usando uma chamada de API, como `Edge.sendEvent`e os manipuladores de evento de resposta recebidos pelo cliente do servidor da Rede de Borda, se houver. Exemplos de eventos do lado do cliente:
   - Evento de solicitação AEP é o evento enviado por meio da extensão Edge e contém os dados XDM e opcionais de forma livre.
   - O AEP Response Event Handle é o identificador de evento recebido da Edge Network em resposta a um evento de solicitação do AEP. Um evento de solicitação pode receber nenhum, um ou vários manipuladores de evento de resposta.
   - A Resposta de erro do AEP pode ser vista em caso de erro, por exemplo, se a carga XDM não pôde ser processada ou se um dos serviços upstream retornou um erro ou aviso.
- **[!UICONTROL Rede Edge]**: Essa coluna exibe o evento recebido do lado do servidor pela Rede de borda por meio de uma solicitação de rede e quais dados e metadados o evento continha.
- **[!UICONTROL Upstream]**: Essa coluna exibe os eventos recebidos pelos serviços upstream configurados, incluindo informações detalhadas sobre os resultados de processamento e/ou validação do evento de entrada.
Observe que essa coluna é dinâmica e pode exibir tipos diferentes de informações dependendo de dois fatores principais:
   - A configuração do armazenamento de dados e os serviços habilitados nela.
   - O tipo de evento enviado para a Rede de borda.

### Eventos do Inspect

Os eventos exibidos na visualização Transações de evento fornecem informações sobre o formato e o conteúdo dos dados que estão sendo processados em cada estado, bem como detalhes refinados sobre quaisquer avisos ou erros encontrados quando os dados são processados upstream. A visualização ajuda a restringir as informações de depuração no nível do evento/solicitação e identificar erros precocemente no ciclo de desenvolvimento.

#### Expanda os detalhes do evento

Para inspecionar um evento, selecione o desejado na exibição. Essa ação expande o **[!UICONTROL Detalhes do evento]** no lado direito da tela.
Os dados aninhados são exibidos em um formato de árvore. Você pode inspecionar valores-chave aninhados selecionando o **+** (mais) à esquerda do nome da chave.

![Detalhes do evento](./images/event-transactions/event-details.png)

#### Avisos ou erros do Inspect

Cada nome de evento recebe o prefixo de um ícone que indica o status de alto nível do processamento desse evento:

- Se o evento foi processado com êxito, uma marca de seleção verde é exibida.
- Se avisos ou erros tiverem sido detectados, um sinal de aviso será exibido. Selecione o evento relacionado para saber mais sobre a causa do aviso ou erro no **[!UICONTROL Detalhes do evento]** exibir.

### Configurações

Você pode verificar o identificador de conjunto de dados usado no momento selecionando a dica de ferramenta de informações ao lado do **[!UICONTROL Rede Edge]** cabeçalho da coluna.

![Mostrar a ID do armazenamento de dados](./images/event-transactions/show-datastream-id.png)

>[!INFO]
>
>Quando vários clientes se conectam à mesma sessão de Controle e IDs de armazenamento de dados diferentes são usadas, você verá todos exibidos aqui. No entanto, isso não significa que sua implementação atual está usando vários conjuntos de dados. Somente a ID do armazenamento de dados atual definida na tag (propriedade móvel) usada pelo aplicativo é usada para processar novos eventos desse cliente. Ao testar casos de uso mais complicados com configurações diferentes e vários clientes conectados, pode ser útil usar sessões de Controle separadas para simplificar o processo de validação.
