---
title: Analytics Events 2.0 no Assurance
description: Este guia explica como usar o Adobe Analytics e o Analytics Edge View com o Adobe Experience Platform Assurance.
badgeBeta: label="Beta" type="Informative"
source-git-commit: f707554ea89731fbd3f013d6065fde27ba7fa811
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 19%

---

# Analytics Events 2.0 no Assurance

O Analytics Events 2.0 fornece uma visualização mais avançada dos eventos do SDK para os usuários que depuram e validam a implementação do Adobe Analytics. A exibição mostra eventos enviados para o Adobe Analytics do [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/solution/adobe-analytics/) bem como a [SDK da rede de borda da Adobe Experience Platform](https://developer.adobe.com/client-sdks/edge/edge-network/). A visualização também apresenta um painel de detalhes, que fornece contexto sobre como o evento foi processado pelo SDK do cliente, bem como pelos serviços upstream depois que ele deixou o dispositivo.

## Introdução

Para usar essa visualização, conclua as seguintes etapas:

1. [Configurar o Adobe Experience Platform Assurance](../tutorials/implement-assurance.md).
2. [Criar e conectar-se a uma sessão do Assurance](../tutorials/using-assurance.md).
3. Na interface do usuário do Assurance, no painel de navegação esquerdo **Início** menu exibir, selecione **Analytics Events 2.0 (Beta)**. Se você não vir essa opção, selecione **Configurar** na parte inferior esquerda da janela, adicione o **Analytics Events 2.0 (Beta)** e selecione **Salvar**.

## Exibição de eventos do Analytics

Use a Exibição de evento do Analytics se estiver usando a **Adobe Analytics** extensão móvel. Essa visualização permite que você visualize facilmente os Eventos do Analytics enviados de seu cliente conectado, incluindo Rastrear ação, Rastrear estado e Eventos do ciclo de vida. Ao selecionar um dos eventos do Analytics na tabela, os detalhes de como o evento foi processado podem ser exibidos no painel direito.

![Uma imagem que demonstra diferentes componentes na visualização de eventos do Analytics.](./images/adobe-analytics-edge/analytics-events.png)

### Status pós-processado

Depois que o SDK fizer uma solicitação de rede com o Adobe Analytics, o status informará se o Assurance conseguiu recuperar as informações de pós-processamento da solicitação do Adobe Analytics. A exibição Eventos do Analytics deve permanecer ativa enquanto o status de pós-processamento estiver em operação após a solicitação ser acionada.

Observe que para recuperar informações de pós-processamento, o usuário conectado precisa ter acesso ao conjunto de relatórios correspondente.

| Status | Descrição |
| :----- | :---------- |
| `Queued` | A solicitação de rede está buscando as informações de pós-processamento. |
| `Processed` | A solicitação de rede foi bem-sucedida e as informações de pós-processamento foram recebidas. |
| `Delayed` | O número máximo de tentativas de solicitações para buscar as informações de pós-processamento foi excedido. |
| `Error` | Um erro causou a falha na solicitação de rede. Mais detalhes sobre o erro são exibidos na exibição dos detalhes do evento. |
| `Unauthorized` | O usuário não tem acesso ao conjunto de relatórios do Adobe Analytics. |
| `Unavailable` | A solicitação do Adobe Analytics não tem um evento `AnalyticsResponse` correspondente. |
| `No Debug Flag` | A versão atual do Adobe Analytics ou do Assurance SDK pode não ser compatível com o recurso de depuração do Analytics. Para obter mais informações, leia o [Manual de solução de problemas](../troubleshooting.md). |
| `Expired` | O evento `AnalyticsTrack` ou `LifecycleStart` tem mais de 24 horas. |

### Exibição dos detalhes do evento

Para um evento de rastreamento do Analytics, a exibição detalhada contém as seguintes partes:

- Um evento de solicitação do Analytics do SDK de origem.
- Metadados e dados de contexto da solicitação, como ID do conjunto de relatórios, versões de extensão do SDK e dados de contexto.
- Informações pós-processadas sobre o evento do Analytics que contêm o mapeamento de revars, evars e props.

### Validação da visualização do Analytics

A visualização de validação permite visualizar facilmente os resultados nos scripts de validação relacionados ao Analytics. Os erros exibidos pelos validadores podem conter links para onde devem ser corrigidos ou exibir eventos que estão em um estado de erro.

![Uma imagem que mostra a guia validadores na exibição do Analytics.](./images/adobe-analytics-edge/analytics-validation-view.png)

## Exibição de borda do Analytics

Use a exibição de Borda do Analytics se estiver usando **Rede de borda** ou **Edge Bridge** extensões móveis. Para habilitar essa exibição, selecione o botão &quot;Borda do Analytics (Beta)&quot; na parte superior direita para exibir os eventos do Analytics enviados pela rede de borda na sessão atual. Isso inclui todos os eventos que foram acionados pela extensão do ciclo de vida, solicitações do Edge e/ou eventos do Edge Bridge com base em Rastrear ação e Rastrear estado.

![Uma imagem que mostra a alternância usada para alternar entre a Exibição do Analytics e a Exibição de borda do Analytics.](./images/adobe-analytics-edge/analytics-view-toggle.png)

A visualização Analytics Edge contém informações sobre solicitações de Edge relacionadas ao Analytics e métodos de ciclo de vida despachados pelo cliente. Ao escolher um evento na lista, o painel direito exibe os eventos que foram processados pelo SDK do cliente, bem como pelo serviço upstream depois que eles saíram do dispositivo, para que você possa visualizar facilmente a cadeia de eventos que resultou de uma chamada.

![Uma imagem que demonstra diferentes componentes na Exibição de borda do Analytics.](./images/adobe-analytics-edge/edge-analytics-events.png)

### Validação de borda do Analytics

A exibição de validação do Analytics Edge permite visualizar facilmente os resultados nos scripts de validação relacionados ao Analytics Edge. Os erros exibidos pelos validadores podem conter links para onde devem ser corrigidos ou exibir eventos que estão em um estado de erro.

![Uma imagem que mostra a guia validadores na exibição de Borda do Analytics.](./images/adobe-analytics-edge/edge-analytics-validation-view.png)
