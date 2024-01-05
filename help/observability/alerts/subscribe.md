---
keywords: Experience Platform;página inicial;tópicos populares;intervalo de datas
title: Assinar notificações de eventos Adobe I/O
description: Este documento fornece etapas sobre como assinar notificações de eventos Adobe I/O para serviços da Adobe Experience Platform. Também são fornecidas informações de referência sobre os tipos de evento disponíveis, juntamente com links para documentação adicional sobre como interpretar os dados retornados do evento para cada tipo aplicável [!DNL Platform] serviço.
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: 49f4cf07d2f002e45e27dffac4fd0049446bc68f
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 2%

---

# Assinar notificações de eventos Adobe I/O

[!DNL Observability Insights] permite assinar notificações de eventos Adobe I/O relacionadas às atividades do Adobe Experience Platform. Esses eventos são enviados para um webhook configurado para facilitar a automação eficiente do monitoramento de atividades.

Este documento fornece etapas sobre como assinar notificações de eventos Adobe I/O para serviços da Adobe Experience Platform. Também são fornecidas informações de referência sobre os tipos de evento disponíveis, juntamente com links para documentação adicional sobre como interpretar os dados retornados do evento para cada tipo aplicável [!DNL Platform] serviço.

## Introdução

Este documento requer uma compreensão funcional de webhooks e como conectar um webhook de um aplicativo a outro. Consulte a [[!DNL I/O Events] documentação](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) para obter uma introdução aos webhooks.

## Criar um webhook

Para receber [!DNL I/O Event] notificações, você deve registrar um webhook especificando um URL de webhook exclusivo como parte dos detalhes de registro do evento.

Você pode configurar o webhook usando o cliente de sua escolha. Para obter um endereço de webhook temporário para usar como parte deste tutorial, visite [Webhook.site](https://webhook.site/) e copie o URL exclusivo fornecido.

![](../images/notifications/webhook-url.png)

Durante o processo de validação inicial, [!DNL I/O Events] envia um `challenge` parâmetro de consulta em uma solicitação do GET para o webhook. Você deve configurar seu webhook para retornar o valor desse parâmetro na carga de resposta. Se estiver usando o Webhook.site, selecione **[!DNL Edit]** no canto superior direito, digite `$request.query.challenge$` em **[!DNL Response body]** antes de selecionar **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## Criar um novo projeto no Console do Adobe Developer

Acesse o [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e faça logon com seu Adobe ID. Em seguida, siga as etapas descritas no tutorial em [criação de um projeto vazio](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) na documentação do Console do Adobe Developer.

## Assinar eventos

>[OBSERVAÇÃO!]
>
>A notificação de assimilação de dados será descontinuada da assinatura de E/S de Adobe. Em vez disso, você deve usar o **Informações de execução do fluxo de fontes** Evento de E/S.

Depois de criar um novo projeto, acesse a tela de visão geral do projeto. Aqui, selecione **[!UICONTROL Adicionar evento]**.

![](../images/notifications/add-event-button.png)

Uma caixa de diálogo é exibida, permitindo adicionar um provedor de eventos ao projeto:

* Se estiver assinando alertas de Experience Platform, selecione **[!UICONTROL Notificações da plataforma]**
* Se você estiver assinando o Adobe Experience Platform [!DNL Privacy Service] notificações, selecione **[!UICONTROL Eventos Privacy Service]**

Depois de escolher um provedor de eventos, selecione **[!UICONTROL Próxima]**.

![](../images/notifications/event-provider.png)

A próxima tela exibe uma lista de tipos de evento para se inscrever. Selecione os eventos que deseja assinar e selecione **[!UICONTROL Próxima]**.

>[!NOTE]
>
>Se não tiver certeza de quais eventos você deve assinar para o serviço com o qual está trabalhando, consulte a seguinte documentação:
>
>* [Notificações da plataforma](./rules.md)
>* [Notificações Privacy Service](../../privacy-service/privacy-events.md)

![](../images/notifications/choose-event-subscriptions.png)

A próxima tela solicita que você crie um JSON Web Token (JWT). Você tem a opção de gerar automaticamente um par de chaves ou fazer upload de sua própria chave pública gerada no terminal.

Para os fins deste tutorial, a primeira opção é seguida. Selecione a caixa de opção para **[!UICONTROL Gerar um par de chaves]**, em seguida, selecione a **[!UICONTROL Gerar par de chaves]** no canto inferior direito.

![](../images/notifications/generate-keypair.png)

Quando o par de chaves é gerado, ele é baixado automaticamente pelo navegador. Você mesmo deve armazenar esse arquivo, pois ele não é mantido no Console do desenvolvedor.

A próxima tela permite revisar os detalhes do par de chaves recém-gerado. Clique em **[!UICONTROL Avançar]** para continuar.

![](../images/notifications/keypair-generated.png)

Na próxima tela, forneça um nome e uma descrição para o registro do evento na [!UICONTROL Detalhes de inscrição no evento] seção. A prática recomendada é criar um nome exclusivo e de fácil identificação para ajudar a diferenciar esse registro de evento dos outros no mesmo projeto.

![](../images/notifications/registration-details.png)

Mais abaixo na mesma tela, sob o [!UICONTROL Como receber eventos] é possível configurar opcionalmente como receber eventos. **[!UICONTROL Webhook]** permite fornecer um endereço de webhook personalizado para receber eventos, enquanto **[!UICONTROL Ação em tempo de execução]** permite fazer o mesmo usando [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Para este tutorial, selecione **[!UICONTROL Webhook]** e forneça o URL do webhook criado anteriormente. Quando terminar, selecione **[!UICONTROL Salvar eventos configurados]** para concluir o registro do evento.

![](../images/notifications/receive-events.png)

A página de detalhes do registro de evento recém-criado é exibida, onde você pode editar sua configuração, revisar eventos recebidos, executar o rastreamento de depuração e adicionar novos provedores de eventos.

![](../images/notifications/registration-complete.png)

## Próximas etapas

Ao seguir este tutorial, você registrou um webhook para receber [!DNL I/O Event] notificações para [!DNL Experience Platform] e/ou [!DNL Privacy Service]. Para obter detalhes sobre eventos disponíveis e como interpretar cargas de notificação para cada serviço, consulte a seguinte documentação:

* [Notificações do [!DNL Privacy Service]](../../privacy-service/privacy-events.md)
* [Notificações do [!DNL Data Ingestion]](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] (fontes) notificações](../../sources/notifications.md)

Consulte a [[!DNL Observability Insights] visão geral](../home.md) para obter mais informações sobre como monitorar suas atividades no [!DNL Experience Platform] e [!DNL Privacy Service].
