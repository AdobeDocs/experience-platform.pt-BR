---
keywords: Experience Platform, home, tópicos populares, intervalo de datas
title: Assinar notificações de evento do Adobe I/O
description: Este documento fornece etapas sobre como assinar notificações de evento do Adobe I/O para serviços da Adobe Experience Platform. Também são fornecidas informações de referência sobre os tipos de evento disponíveis, juntamente com links para outra documentação sobre como interpretar os dados de evento retornados para cada [!DNL Platform] serviço.
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: 29b1942e4009770d4f9d346a760b6e78cef23969
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 4%

---

# Assinar notificações do Evento do Adobe I/O

[!DNL Observability Insights] O permite assinar notificações do Adobe I/O Event relacionadas às atividades do Adobe Experience Platform. Esses eventos são enviados para um webhook configurado para facilitar a automação eficiente do monitoramento de atividades.

Este documento fornece etapas sobre como assinar notificações de evento do Adobe I/O para serviços da Adobe Experience Platform. Também são fornecidas informações de referência sobre os tipos de evento disponíveis, juntamente com links para outra documentação sobre como interpretar os dados de evento retornados para cada [!DNL Platform] serviço.

## Introdução

Este documento requer uma compreensão funcional de webhooks e como conectar um webhook de um aplicativo a outro. Consulte a [[!DNL I/O Events] documentação](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) para uma introdução aos webhooks.

## Criar um webhook

Para receber [!DNL I/O Event] nas notificações, registre um webhook especificando um URL exclusivo do webhook como parte dos detalhes de registro do evento.

Você pode configurar seu webhook usando o cliente de sua escolha. Para um endereço temporário do webhook ser usado como parte deste tutorial, visite [Webhook.site](https://webhook.site/) e copie o URL único fornecido.

![](../images/notifications/webhook-url.png)

Durante o processo de validação inicial, [!DNL I/O Events] envia um `challenge` parâmetro de consulta em uma solicitação GET para o webhook. Você deve configurar o webhook para retornar o valor desse parâmetro na carga de resposta. Se estiver usando Webhook.site, selecione **[!DNL Edit]** no canto superior direito, digite `$request.query.challenge$` under **[!DNL Response body]** antes de selecionar **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## Crie um novo projeto no Console do desenvolvedor do Adobe

Acesse o [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e faça logon com seu Adobe ID. Em seguida, siga as etapas descritas no tutorial em [criação de um projeto vazio](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) na documentação do Console do desenvolvedor do Adobe.

## Inscrever-se em eventos

Depois de criar um novo projeto, navegue até a tela de visão geral do projeto. Aqui, selecione **[!UICONTROL Adicionar evento]**.

![](../images/notifications/add-event-button.png)

Uma caixa de diálogo é exibida, permitindo adicionar um provedor de eventos ao seu projeto:

* Se estiver assinando alertas de Experience Platform, selecione **[!UICONTROL Notificações da plataforma]**
* Se estiver assinando o Adobe Experience Platform [!DNL Privacy Service] notificações, selecione **[!UICONTROL Privacy Service Events]**

Depois de escolher um provedor de eventos, selecione **[!UICONTROL Próximo]**.

![](../images/notifications/event-provider.png)

A próxima tela exibe uma lista de tipos de eventos para assinatura. Selecione os eventos que deseja assinar e selecione **[!UICONTROL Próximo]**.

>[!NOTE]
>
>Se não tiver certeza sobre quais eventos assinar o serviço com o qual você está trabalhando, consulte a seguinte documentação:
>
>* [Notificações da plataforma](./rules.md)
>* [Notificações de Privacy Service](../../privacy-service/privacy-events.md)


![](../images/notifications/choose-event-subscriptions.png)

A próxima tela solicita a criação de um JSON Web Token (JWT). Você tem a opção de gerar automaticamente um par de chaves ou fazer upload de sua própria chave pública gerada no terminal.

Para os fins deste tutorial, a primeira opção é seguida. Selecione a caixa de opções para **[!UICONTROL Gerar um par de chaves]**, em seguida, selecione o **[!UICONTROL Gerar par de chaves]** no canto inferior direito.

![](../images/notifications/generate-keypair.png)

Quando o par de chaves é gerado, ele é baixado automaticamente pelo navegador. Você mesmo deve armazenar esse arquivo, pois ele não é persistente no Console do desenvolvedor.

A próxima tela permite que você analise os detalhes do par de chaves recém-gerado. Clique em **[!UICONTROL Avançar]** para continuar.

![](../images/notifications/keypair-generated.png)

Na próxima tela, forneça um nome e uma descrição para o registro do evento na [!UICONTROL Detalhes de registro do evento] seção. A prática recomendada é criar um nome exclusivo e facilmente identificável para ajudar a diferenciar o registro de eventos de outros no mesmo projeto.

![](../images/notifications/registration-details.png)

Mais para baixo no mesmo ecrã sob a [!UICONTROL Como receber eventos] , você pode optar por configurar como receber eventos. **[!UICONTROL Webhook]** permite que você forneça um endereço personalizado do webhook para receber eventos, enquanto **[!UICONTROL Ação de tempo de execução]** permite que você faça o mesmo usando [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Para este tutorial, selecione **[!UICONTROL Webhook]** e forneça o URL do webhook criado anteriormente. Depois de concluir, selecione **[!UICONTROL Salvar eventos configurados]** para concluir o registro do evento.

![](../images/notifications/receive-events.png)

A página de detalhes para o registro de evento recém-criado é exibida, onde você pode editar sua configuração, revisar eventos recebidos, executar o rastreamento de depuração e adicionar novos provedores de evento.

![](../images/notifications/registration-complete.png)

## Próximas etapas

Ao seguir este tutorial, você registrou um webhook para receber [!DNL I/O Event] notificações para [!DNL Experience Platform] e/ou [!DNL Privacy Service]. Para obter detalhes sobre os eventos disponíveis e como interpretar as cargas de notificação para cada serviço, consulte a seguinte documentação:

* [[!DNL Privacy Service] notificações](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] notificações](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] Notificações (fontes)](../../sources/notifications.md)

Consulte a [[!DNL Observability Insights] visão geral](../home.md) para obter mais informações sobre como monitorar suas atividades no [!DNL Experience Platform] e [!DNL Privacy Service].
