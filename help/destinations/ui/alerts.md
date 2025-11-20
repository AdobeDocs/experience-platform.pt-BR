---
keywords: Experience Platform;página inicial;tópicos populares; alertas;destinos
description: Você pode assinar alertas ao criar um fluxo de dados para receber mensagens de alerta sobre o status, o sucesso ou a falha da execução do fluxo.
title: Assinar alertas de destino em contexto
exl-id: 134144a0-cdfe-49a8-bd8b-e36a4f053de5
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 13%

---

# Assinar alertas de destino em contexto

A Adobe Experience Platform permite que você se inscreva para receber alertas baseados em eventos relacionados às atividades da Adobe Experience Platform. Os alertas reduzem ou eliminam a necessidade de pesquisar a [[!DNL Observability Insights] API](../../observability/api/overview.md) para verificar se um trabalho foi concluído, se um determinado marco em um fluxo de trabalho foi atingido ou se ocorreu algum erro.

Você pode assinar alertas ao criar um fluxo de dados para receber mensagens de alerta sobre o status, o sucesso ou a falha da execução do fluxo.

Este documento fornece etapas sobre como assinar mensagens de alertas de recebimento para seus fluxos de dados de destino.

## Introdução

Este documento requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Destinos](../home.md): integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.
* [Observabilidade](../../observability/home.md): [!DNL Observability Insights] permite monitorar as atividades do Experience Platform usando métricas estatísticas e notificações de eventos.
   * [Alertas](../../observability/alerts/overview.md): quando um determinado conjunto de condições em suas operações do Experience Platform é atingido (como um problema em potencial quando o sistema ultrapassa um limite), o Experience Platform pode enviar mensagens de alerta para qualquer usuário em sua organização que tenha assinado para eles.

## Assinar os alertas da interface {#subscribe-destination-alerts}

>[!CONTEXTUALHELP]
>id="platform_destination_alerts_subscribe"
>title="Assinar alertas de destino"
>abstract="Os alertas permitem receber notificações com base no status dos fluxos de dados de destino. É possível definir notificações de alerta para obter atualizações caso o fluxo de dados tenha sido iniciado, bem-sucedido, tenha falhado ou não tenha enviado dados para o destino."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>Você deve ativar notificações instantâneas de emails para sua conta do Experience Platform a fim de receber notificações de alerta baseadas em email para seus fluxos de dados.

Você pode habilitar alertas para seus fluxos de dados durante a etapa [!UICONTROL Configure new destination] do fluxo de trabalho [conexão de destino](connect-destination.md).

![Imagem da interface do usuário mostrando a seção de alertas de destino.](../assets/ui/alerts/destination-alerts.png)

Selecione os alertas que você deseja assinar e selecione **[!UICONTROL Next]** para revisar e concluir seu fluxo de dados.

Os alertas disponíveis para fluxos de dados de destino são descritos na tabela abaixo.

* Para destinos de streaming, somente o alerta [!DNL Activation Skipped Rate Exceeded] está disponível.
* Para destinos baseados em arquivo, todos os alertas estão disponíveis.

| Alertas | Descrição |
| --- | --- |
| Atraso na execução do fluxo de destino | Esse alerta notifica quando uma execução de fluxo de destino demora mais de 150 minutos para ativar um público-alvo. |
| Falha na execução do fluxo de destino | Este alerta notifica quando ocorre um erro ao ativar um público-alvo para um destino. |
| Êxito na execução do fluxo de destino | Este alerta notifica quando um público-alvo é ativado com êxito para um destino. |
| Início da execução do fluxo de destino | Esse alerta notifica quando uma execução de fluxo de destino começa a ativar um público-alvo. |
| Taxa de Ativação Ignorada Excedida | Este alerta notifica quando a taxa de ativação ignorada excede 1% do total de ativações. As identidades são ignoradas durante a ativação quando têm atributos ausentes ou violação de consentimento. |

## Recebimento de alertas {#receiving-alerts}

Depois que o fluxo de dados de destino for executado, você poderá receber alertas por meio da interface ou por email.

### Recebimento de alertas na interface do {#receiving-alerts-in-ui}

Os alertas são representados na interface por um ícone de notificação no cabeçalho superior da interface do usuário do Experience Platform. Selecione o ícone de notificação para ver mensagens de alerta específicas relacionadas aos fluxos de dados.

![Imagem da interface do usuário mostrando o ícone de notificação no Experience Platform](../assets/ui/alerts/notification.png)

O painel de notificações é exibido, exibindo uma lista de atualizações de status no fluxo de dados criado.

![Imagem da interface mostrando o painel de notificação](../assets/ui/alerts/alert-window.png)

Você pode passar o mouse em uma mensagem de alerta para marcá-las como lidas ou selecionar o ícone do relógio para definir lembretes futuros sobre o status do fluxo de dados.

![Imagem da interface mostrando as opções de lembrete de notificação](../assets/ui/alerts/remind-me.png)

Selecione a mensagem de alerta para ver informações específicas sobre o fluxo de dados.

![Imagem da interface mostrando como selecionar uma notificação](../assets/ui/alerts/select-alert-message.png)

A página [!UICONTROL Dataflow run details] é exibida. A metade superior da tela exibe uma visão geral do fluxo de dados, incluindo informações sobre seus atributos, a ID de execução do fluxo de dados correspondente e um resumo de erros de alto nível.

![Imagem da interface do usuário mostrando a página de detalhes da execução do fluxo de dados.](../assets/ui/alerts/dataflow-overview.png)

A metade inferior da página exibe qualquer [!UICONTROL Dataflow run errors] que tenha ocorrido durante o estágio de execução do fluxo de dados. Aqui, você pode visualizar o diagnóstico de erros ou usar a [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) para baixar o diagnóstico de erros ou o manifesto de arquivo que corresponde ao seu fluxo de dados.

![Imagem da interface do usuário mostrando a página de detalhes da execução do fluxo de dados, com destaque na seção de erros.](../assets/ui/alerts/dataflow-run-error.png)

Para obter mais informações sobre como manipular erros de fluxo de dados, consulte o manual sobre [fluxos de dados de destinos de monitoramento na interface](../../dataflows/ui/monitor-destinations.md).

### Receber alertas por email {#receiving-alerts-by-email}

Os alertas para seus fluxos de dados também são entregues a você por email. Selecione o nome do fluxo de dados no corpo do email para ver mais informações sobre o fluxo de dados.

![Captura de tela de um email de alerta](../assets/ui/alerts/email.png)

Semelhante ao alerta da interface do usuário, a página [!UICONTROL Dataflow run overview] é exibida, fornecendo uma interface para investigar quaisquer erros associados ao fluxo de dados.

![visão geral do fluxo de dados](../assets/ui/alerts/dataflow-overview.png)

## Assinar e cancelar inscrição em alertas {#subscribe-and-unsubscribe}

Você pode assinar mais alertas ou cancelar a assinatura de alertas estabelecidos para um fluxo de dados de destino existente na página de destinos [!UICONTROL Browse].

![Imagem da interface do usuário mostrando a página Navegação de Destinos](../assets/ui/alerts/destination-list.png)

Localize a conexão de destino para a qual você deseja receber alertas e selecione as reticências (`...`) para ver um menu suspenso de opções. Em seguida, selecione **[!UICONTROL Subscribe to alerts]** para modificar as configurações de alerta do fluxo de dados de destino.

![Imagem da interface mostrando as opções de destino](../assets/ui/alerts/destination-alerts-subscribe.png)

Uma janela pop-up é exibida, fornecendo uma lista de alertas de destino. Selecione os alertas que deseja assinar ou desmarque os alertas dos quais deseja cancelar a assinatura. Quando terminar, selecione **[!UICONTROL Save]**.

![Imagem da interface do usuário mostrando a página de assinaturas de alertas de destino](../assets/ui/alerts/destination-alerts-list.png)

## Próximas etapas {#next-steps}

Este documento forneceu um guia passo a passo sobre como assinar alertas em contexto para seus fluxos de dados de destino. Para obter mais informações, consulte o [guia da interface de alertas](../../observability/alerts/ui.md).
