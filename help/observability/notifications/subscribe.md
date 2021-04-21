---
keywords: Experience Platform, home, tópicos populares, intervalo de datas
solution: Experience Platform
title: Assinar notificações de evento do Adobe I/O
topic-legacy: developer guide
description: Este documento fornece etapas sobre como assinar notificações de evento do Adobe I/O para serviços da Adobe Experience Platform. Também são fornecidas informações de referência sobre os tipos de evento disponíveis, juntamente com links para outra documentação sobre como interpretar os dados de evento retornados para cada serviço aplicável [!DNL Platform] .
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 1%

---

# Assinar notificações do Evento do Adobe I/O

[!DNL Observability Insights] O permite assinar notificações do Adobe I/O Event relacionadas às atividades do Adobe Experience Platform. Esses eventos são enviados para um webhook configurado para facilitar a automação eficiente do monitoramento de atividades.

Este documento fornece etapas sobre como assinar notificações de evento do Adobe I/O para serviços da Adobe Experience Platform. Também são fornecidas informações de referência sobre os tipos de evento disponíveis, juntamente com links para outra documentação sobre como interpretar os dados de evento retornados para cada serviço [!DNL Platform] aplicável.

## Introdução

Este documento requer uma compreensão funcional de webhooks e como conectar um webhook de um aplicativo a outro. Consulte a [[!DNL I/O Events] documentação](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) para obter uma introdução aos webhooks.

## Criar um webhook

Para receber [!DNL I/O Event] notificações, você deve registrar um webhook especificando um URL de webhook exclusivo como parte dos detalhes de registro do evento.

Você pode configurar seu webhook usando o cliente de sua escolha. Para que um endereço de webhook temporário seja usado como parte deste tutorial, visite [Webhook.site](https://webhook.site/) e copie o URL exclusivo fornecido.

![](../images/notifications/webhook-url.png)

Durante o processo de validação inicial, [!DNL I/O Events] envia um parâmetro de consulta `challenge` em uma solicitação GET para o webhook. Você deve configurar o webhook para retornar o valor desse parâmetro na carga de resposta. Se estiver usando Webhook.site, selecione **[!DNL Edit]** no canto superior direito e digite `$request.query.challenge$` em **[!DNL Response body]** antes de selecionar **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## Crie um novo projeto no Console do desenvolvedor do Adobe

Vá para [Console do desenvolvedor do Adobe](https://www.adobe.com/go/devs_console_ui) e faça logon com sua Adobe ID. Em seguida, siga as etapas descritas no tutorial em [criar um projeto vazio](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) na documentação do Console do desenvolvedor do Adobe.

## Inscrever-se em eventos

Depois de criar um novo projeto, navegue até a tela de visão geral do projeto. Aqui, selecione **[!UICONTROL Add event]**.

![](../images/notifications/add-event-button.png)

Uma caixa de diálogo é exibida, permitindo adicionar um provedor de eventos ao seu projeto:

* Se estiver assinando notificações [!DNL Experience Platform], selecione **[!UICONTROL Platform notifications]**
* Se estiver assinando notificações [!DNL Privacy Service] do Adobe Experience Platform, selecione **[!UICONTROL Privacy Service Events]**

Depois de escolher um provedor de eventos, selecione **[!UICONTROL Next]**.

![](../images/notifications/event-provider.png)

A próxima tela exibe uma lista de tipos de eventos para assinatura. Selecione os eventos que deseja assinar e selecione **[!UICONTROL Next]**.

>[!NOTE]
>
>Se não tiver certeza sobre quais eventos assinar o serviço com o qual você está trabalhando, consulte a documentação de notificação específica do serviço:
>
>* [[!DNL Privacy Service] notificações](../../privacy-service/privacy-events.md)
>* [[!DNL Data Ingestion] notificações](../../ingestion/quality/subscribe-events.md)
>* [[!DNL Flow Service (sources)] notificações](../../sources/notifications.md)


![](../images/notifications/choose-event-subscriptions.png)

A próxima tela solicita a criação de um JSON Web Token (JWT). Você tem a opção de gerar automaticamente um par de chaves ou fazer upload de sua própria chave pública gerada no terminal.

Para os fins deste tutorial, a primeira opção é seguida. Selecione a caixa de opção para **[!UICONTROL Generate a key pair]** e selecione o botão **[!UICONTROL Generate keypair]** no canto inferior direito.

![](../images/notifications/generate-keypair.png)

Quando o par de chaves é gerado, ele é baixado automaticamente pelo navegador. Você mesmo deve armazenar esse arquivo, pois ele não é persistente no Console do desenvolvedor.

A próxima tela permite que você analise os detalhes do par de chaves recém-gerado. Selecione **[!UICONTROL Next]** para continuar.

![](../images/notifications/keypair-generated.png)

Na próxima tela, forneça um nome e uma descrição para o registro do evento na seção [!UICONTROL Event registration details] . A prática recomendada é criar um nome exclusivo e facilmente identificável para ajudar a diferenciar o registro de eventos de outros no mesmo projeto.

![](../images/notifications/registration-details.png)

Mais abaixo na mesma tela, na seção [!UICONTROL How to receive events], é possível configurar opcionalmente como receber eventos. **[!UICONTROL Webhook]** O permite fornecer um endereço personalizado do webhook para receber eventos, enquanto  **[!UICONTROL Runtime action]** permite fazer o mesmo usando o  [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Para este tutorial, selecione **[!UICONTROL Webhook]** e forneça o URL do webhook criado anteriormente. Quando terminar, selecione **[!UICONTROL Save configured events]** para concluir o registro de eventos.

![](../images/notifications/receive-events.png)

A página de detalhes para o registro de evento recém-criado é exibida, onde você pode editar sua configuração, revisar eventos recebidos, executar o rastreamento de depuração e adicionar novos provedores de evento.

![](../images/notifications/registration-complete.png)

## Próximas etapas

Ao seguir este tutorial, você registrou um webhook para receber [!DNL I/O Event] notificações para [!DNL Experience Platform] e/ou [!DNL Privacy Service]. Para obter detalhes sobre os eventos disponíveis e como interpretar as cargas de notificação para cada serviço, consulte a seguinte documentação:

* [[!DNL Privacy Service] notificações](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] notificações](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service (sources)] notificações](../../sources/notifications.md)

Consulte a [[!DNL Observability Insights] visão geral](../home.md) para obter mais informações sobre como você pode monitorar suas atividades em [!DNL Experience Platform] e [!DNL Privacy Service].
