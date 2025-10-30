---
keywords: extensão de encaminhamento de eventos;extensão de encaminhamento de eventos do twitter;event forwarding extension
title: Extensão de encaminhamento de eventos do Twitter
description: Essa extensão de encaminhamento de eventos do Adobe Experience Platform permite assimilar eventos no Twitter para atender às necessidades da sua empresa.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: 54c240e5-6160-4654-ac5b-6afa8d99a765
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 2%

---

# Extensão de encaminhamento de eventos da [!DNL Twitter]

[[!DNL Twitter]](https://twitter.com/i/flow/login) é uma rede social online e um serviço de rede social, no qual os usuários postam e interagem com mensagens de 280 caracteres conhecidas como tweets. Os usuários podem interagir com o Twitter usando um navegador, software de front-end móvel ou programaticamente por meio de suas [APIs](https://developer.twitter.com/en/docs/twitter-api)

A extensão [!DNL Twitter] da API de Conversões da Web [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) permite que você aproveite os dados capturados no Adobe Experience Platform Edge Network e os envie para [!DNL Twitter]. Este documento aborda os casos de uso da extensão, como instalá-la e como integrar seus recursos ao encaminhamento de eventos [regras](../../../ui/managing-resources/rules.md).

[!DNL Twitter] requer [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) para autenticação com a API [!DNL Twitter] [!DNL Web Conversions].

## Casos de uso

Essa extensão deve ser usada se você quiser usar dados da Edge Network no [!DNL Twitter] para aproveitar seus recursos de análise e direcionamento de clientes.

Por exemplo, considere uma equipe de marketing em uma organização. A equipe captura dados do evento de interação do usuário de seu site como dados do evento de seu site e os carrega em [!DNL Twitter] usando esta extensão de encaminhamento de eventos.

As equipes de marketing e análise podem aproveitar os recursos do [!DNL Twitter's] para realizar análises adicionais e direcionar esses usuários para campanhas de publicidade direcionadas.

Para obter mais informações sobre casos de uso específicos do [!DNL Twitter], consulte a documentação dos [[!DNL Twitter] casos de uso](https://developer.twitter.com/en/use-cases/build-for-businesses).

## [!DNL Twitter] pré-requisitos e medidas de proteção {#prerequisites}

Você deve ter uma conta [!DNL Twitter] válida para usar esta extensão. Vá para a [[!DNL Twitter] página de registro](https://help.twitter.com/en/using-twitter/create-twitter-account) para se registrar e criar uma conta, caso ainda não tenha uma.

Você deve configurar sua conta como uma conta de desenvolvedor do [!DNL Twitter]. Para saber como se inscrever como desenvolvedor, consulte a [[!DNL Twitter] conta de desenvolvedor](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### Medidas de proteção de API {#guardrails}

A API de Conversões da Web do [!DNL Twitter] tem um limite de taxa de 60.000 solicitações por intervalo de 15 minutos, em que cada solicitação permite 500 eventos.

### Coletar detalhes de configuração necessários {#configuration-details}

Para conectar o Experience Platform a [!DNL Twitter], as seguintes entradas são necessárias:

| Tipo de chave | Descrição |
| --- | --- |
| Chave do consumidor | &#x200B; a chave de API do aplicativo para acessar a API [!DNL Twitter]. Consulte a documentação do [!DNL Twitter] sobre [chaves e segredos da api](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) para obter orientação. |
| Segredo do consumidor | O Segredo de API permite que seu aplicativo acesse a API [!DNL Twitter]. Consulte a documentação do [!DNL Twitter] sobre [chaves e segredos da api](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) para obter orientação. |
| Segredo do token | O token secreto sem expiração do seu aplicativo, que é usado para autenticação na API [!DNL Twitter] via OAuth. Consulte a documentação do [!DNL Twitter] sobre [obtenção de tokens de acesso de uso](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) para obter orientação. |
| Token de acesso | O token de acesso sem expiração do seu aplicativo, que é usado para autenticação na API [!DNL Twitter] via OAuth. Consulte a documentação do [!DNL Twitter] sobre [obtenção de tokens de acesso de uso](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) para obter orientação. |
| ID do pixel | O Pixel do [!DNL Twitter] é uma tag de site implementada no seu site para rastrear ações ou conversões de site. Consulte a documentação do [!DNL Twitter] em [rastreamento de conversão para sites](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) para obter orientação. |

## Instalar e configurar a extensão [!DNL Twitter] {#install}

Para instalar a extensão, [crie uma propriedade de encaminhamento de eventos](../../../ui/event-forwarding/overview.md#properties) ou escolha uma propriedade existente para editar.

Selecione **[!UICONTROL Extensions]** na navegação à esquerda. Na guia **[!UICONTROL Catalog]**, selecione **[!UICONTROL Install]** no cartão da extensão [!DNL Twitter].

![Catálogo mostrando a instalação do destaque de extensão [!DNL Twitter].](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>Dependendo das suas necessidades de implementação, talvez seja necessário criar um esquema, elementos de dados e um conjunto de dados antes de configurar a extensão. Revise todas as etapas de configuração antes de começar para determinar quais entidades você precisa configurar para seu caso de uso.

Na próxima tela, insira os [valores de configuração](#configuration-details) a seguir, coletados anteriormente de [!DNL Twitter]:

* **[!UICONTROL Pixel Id]**
* **[!UICONTROL Consumer Key]**
* **[!UICONTROL Consumer Secret]**
* **[!UICONTROL Token]**
* **[!UICONTROL Token Secret]**

Quando terminar, selecione **[!UICONTROL Save]**.

Tela de configuração ![[!DNL Twitter] para a extensão [!DNL Twitter].](../../../images/extensions/server/twitter/configure.png)

## Configurar uma regra de encaminhamento de eventos {#config-rule}

Depois que todos os seus elementos de dados estiverem configurados, você poderá começar a criar regras de encaminhamento de eventos que determinam quando e como seus eventos serão enviados para [!DNL Twitter].

Crie uma nova [regra](../../../ui/managing-resources/rules.md) na propriedade de encaminhamento de eventos. Em **[!UICONTROL Actions]**, adicione uma nova ação e defina a extensão como **[!UICONTROL Twitter]**. Para enviar eventos do Edge Network para [!DNL Twitter], defina **[!UICONTROL Action Type]** como **[!UICONTROL Send Web Conversion].**

Após a seleção, controles adicionais são exibidos para configurar ainda mais o evento. Você precisa mapear as propriedades de evento [!DNL Twitter] para os elementos de dados criados anteriormente. Para obter mais informações, consulte a [[!DNL Twitter] API de Conversões da Web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![O [!DNL Twitter] está criando uma regra de evento de conversão.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL User Identification]**

| Nome do campo | Descrição | Exemplo | Obrigatório |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] Click ID] | [!DNL Twitter] ID de clique conforme analisado a partir da URL de click-through. | `26l6412g5p4iyj65a2oic2ayg2` | Obrigatório se nenhum outro identificador for adicionado. |
| [!UICONTROL Email] | Um endereço de email com hash SHA256. O texto deve estar em minúsculas e qualquer espaço à direita ou à esquerda deve ser removido antes do hash. | `eventforwarding@example.com` | Obrigatório se nenhum outro identificador for adicionado. |
| [!UICONTROL Phone] | O telefone serve como um identificador para corresponder ao evento de conversão. O número de telefone deve estar no formato E164 `[+][country code][area code][local phone number]` antes do hash. | `+911234567875` | Obrigatório se nenhum outro identificador for adicionado. |

**[!UICONTROL Conversion Data]**

| Nome do campo | Descrição | Exemplo | Obrigatório |
| --- | --- | --- | --- |
| [!UICONTROL Conversion Time] | Data e hora como cadeia de caracteres no formato ISO 8601 ou `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | 2022-02-18T01:14:00.603Z | Sim |
| [!UICONTROL Event Id] | A ID de base 36 de um evento específico. Esta ID deve corresponder a um evento pré-configurado contido em sua conta de anúncio [!DNL Twitter]. Isso é conhecido como a ID do evento correspondente no Gerenciador de eventos. | o87ne ou tw-o8z6j-o87ne (tw-pixel_id-event-id) | Sim |
| [!UICONTROL Number of Items] | O número de itens sendo comprados no evento. Deve ser um número positivo maior que 0. | 4 | Não |
| [!UICONTROL Currency] | A moeda dos itens que estão sendo comprados no evento. Isso é expresso em ISO-4217 e, se não for fornecido, o padrão será USD. | USD | Não |
| [!UICONTROL Value] | O valor do preço dos itens que estão sendo comprados no evento. | 100,00 | Não |
| [!UICONTROL Conversion ID] | Um identificador para um evento de conversão que pode ser usado para desduplicação entre conversões de Pixel da Web e API de conversão na mesma tag de evento. | 23294827 | Não |
| [!UICONTROL Description] | Uma descrição com todas as informações adicionais sobre as conversões. | Testar conversão | Não |

## Validar dados em [!DNL Twitter]

Depois que a regra de encaminhamento de eventos for criada e executada, valide se o evento enviado para a API [!DNL Twitter] é exibido conforme esperado na interface do usuário [!DNL Twitter].

Se a coleção de eventos e a integração do [!DNL Experience Platform] tiverem sido bem-sucedidas, você verá eventos no [!DNL Twitter] [!UICONTROL Events manager].

![O [!DNL Twitter] gerenciador de eventos](../../../images/extensions/server/twitter/event-manager.png)

## Próximas etapas

Este guia abordou como enviar eventos de conversão para [!DNL Twitter] usando o encaminhamento de eventos. Para obter mais informações sobre essas tecnologias subjacentes, consulte a documentação oficial:

* [[!DNL Twitter] APIs](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] API de conversão da Web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] Token de acesso do usuário](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [Rastreamento de ID e conversão de pixels](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
