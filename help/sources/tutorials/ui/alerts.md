---
keywords: Experience Platform;página inicial;tópicos populares; alertas
description: Você pode assinar alertas ao criar um fluxo de dados para receber mensagens de alerta sobre o status, o sucesso ou a falha da execução do fluxo.
title: Assinar alertas de contexto na interface do usuário
exl-id: 5d51edaa-ecba-4ac0-8d3c-49010466b9a5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 7%

---

# Assinar alertas para fluxos de dados de fontes na interface

O Adobe Experience Platform permite assinar alertas baseados em eventos relacionados a atividades do Adobe Experience Platform. Os alertas reduzem ou eliminam a necessidade de sondar a [[!DNL Observability Insights] API](../../../observability/api/overview.md) para verificar se um trabalho foi concluído, se um determinado marco em um fluxo de trabalho foi atingido ou se ocorreram erros.

Você pode assinar alertas ao criar um fluxo de dados para receber mensagens de alerta sobre o status, o sucesso ou a falha da execução do fluxo.

Este documento fornece etapas sobre como assinar mensagens de alertas de recebimento para seus fluxos de dados de origens.

## Introdução

Este documento requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Observabilidade](../../../observability/home.md): [!DNL Observability Insights] permite monitorar as atividades do Experience Platform usando métricas estatísticas e notificações de eventos.
   * [Alertas](../../../observability/alerts/overview.md): quando um determinado conjunto de condições em suas operações do Experience Platform é atingido (como um problema em potencial quando o sistema ultrapassa um limite), o Experience Platform pode enviar mensagens de alerta para qualquer usuário em sua organização que tenha assinado para eles.

## Assinar os alertas da interface {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="Assinar alertas de origens"
>abstract="Os alertas permitem receber notificações com base no status dos fluxos de dados de cada origem. É possível definir notificações de alerta para obter atualizações caso o fluxo de dados tenha sido iniciado, bem-sucedido, tenha falhado ou não tenha assimilado dados."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>Você deve ativar notificações instantâneas de emails para sua conta do Experience Platform a fim de receber notificações de alerta baseadas em email para seus fluxos de dados.

Você pode habilitar alertas para seus fluxos de dados durante a etapa [!UICONTROL detalhes do fluxo de dados] do fluxo de trabalho de fontes no espaço de trabalho de fontes.

![detalhes do fluxo de dados](../../images/tutorials/alerts/dataflow-detail.png)

Os alertas disponíveis para fluxos de dados de origens são:

>[!NOTE]
>
>Atualmente, os alertas não oferecem suporte para fontes de transmissão. Você só pode assinar notificações de alerta para origens de lote.

| Alertas | Descrição |
| --- | --- |
| Início da execução do fluxo de fontes | Esse alerta envia uma mensagem quando o fluxo de dados de origem é iniciado. |
| Êxito na execução do fluxo de fontes | Esse alerta envia uma mensagem quando os dados da sua fonte são assimilados com êxito na Experience Platform. |
| Falha na execução do fluxo de fontes | Esse alerta envia uma mensagem se ocorrer um erro no fluxo de dados. |

Selecione os alertas que você deseja assinar e selecione **[!UICONTROL Avançar]** para revisar e concluir seu fluxo de dados.

![selecionar-alertas](../../images/tutorials/alerts/select-alerts.png)

Consulte os guias a seguir para obter etapas detalhadas sobre como criar um fluxo de dados de origens na interface do usuário:

* [Advertising](./dataflow/advertising.md)
* [Armazenamento na nuvem](./dataflow/batch/cloud-storage.md)
* [CRM](./dataflow/crm.md)
* [Banco de dados](./dataflow/databases.md)
* [Comércio eletrônico](./dataflow/ecommerce.md)
* [Arquivos locais](./create/local-system/local-file-upload.md)
* [Automação de marketing](./dataflow/marketing-automation.md)
* [Pagamentos](./dataflow/payments.md)
* [Protocolos](./dataflow/protocols.md)

## Receber alertas

Depois que o fluxo de dados for executado, você poderá receber alertas por meio da interface do usuário ou por email.

### Na interface

Os alertas são representados na interface por um ícone de notificação no cabeçalho superior da interface do usuário do Experience Platform. Selecione o ícone de notificação para ver mensagens de alerta específicas relacionadas aos fluxos de dados.

![notificação](../../images/tutorials/alerts/notification.png)

O painel de notificações é exibido, exibindo uma lista de atualizações de status no fluxo de dados criado.

![janela-alerta](../../images/tutorials/alerts/alert-window.png)

Você pode passar o mouse em uma mensagem de alerta para marcá-las como lidas ou selecionar o ícone do relógio para definir lembretes futuros sobre o status do fluxo de dados.

![lembrete](../../images/tutorials/alerts/remind-me.png)

Selecione a mensagem de alerta para ver informações específicas sobre o fluxo de dados.

![selecionar-mensagem-alerta](../../images/tutorials/alerts/select-alert-message.png)

A página [!UICONTROL Visão geral da execução do fluxo de dados] é exibida. A metade superior da tela exibe uma visão geral do fluxo de dados, incluindo informações sobre seus atributos, a ID de execução do fluxo de dados correspondente e um resumo de erros de alto nível.

![visão geral do fluxo de dados](../../images/tutorials/alerts/dataflow-overview.png)

A metade inferior da página exibe [!UICONTROL erros de execução do fluxo de dados] ocorridos durante o estágio de execução do fluxo de dados. Aqui, você pode visualizar o diagnóstico de erros ou usar a [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) para baixar o diagnóstico de erros ou o manifesto de arquivo que corresponde ao seu fluxo de dados.

![erros de execução de fluxo de dados](../../images/tutorials/alerts/dataflow-run-error.png)

Para obter mais informações sobre como manipular erros de fluxo de dados, consulte o manual sobre [monitoramento de fluxos de dados de fontes na interface](../../../dataflows/ui/monitor-sources.md).

### Por email

Os alertas para seus fluxos de dados também são entregues a você por email. Selecione o nome do fluxo de dados no corpo do email para ver mais informações sobre o fluxo de dados.

![email](../../images/tutorials/alerts/email.png)

Semelhante ao alerta da interface do usuário, a página [!UICONTROL Visão geral da execução do fluxo de dados] é exibida, fornecendo uma interface para investigar quaisquer erros associados ao seu fluxo de dados.

![visão geral do fluxo de dados](../../images/tutorials/alerts/dataflow-overview.png)

## Assinar e cancelar inscrição em alertas

Você pode assinar mais alertas ou cancelar a assinatura de alertas estabelecidos para um fluxo de dados existente na página [!UICONTROL Fluxos de Dados]. Localize o fluxo de dados criado na lista e selecione as reticências (`...`) para ver um menu suspenso de opções. Em seguida, selecione **[!UICONTROL Assinar alertas]** para modificar as configurações de alerta do seu fluxo de dados.

![opções](../../images/tutorials/alerts/options.png)

Uma janela pop-up é exibida, fornecendo uma lista de fontes e alertas. Selecione os alertas que deseja assinar ou desmarque os alertas dos quais deseja cancelar a assinatura. Quando terminar, selecione **[!UICONTROL Salvar]**.

![salvar](../../images/tutorials/alerts/save.png)

## Próximas etapas

Este documento forneceu um guia passo a passo sobre como assinar alertas em contexto para seus fluxos de dados de fontes. Para obter mais informações, consulte o [guia da interface de alertas](../../../observability/alerts/ui.md).