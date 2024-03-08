---
keywords: extensão de encaminhamento de eventos;twitter;extensão de encaminhamento de eventos do twitter
title: Extensão de encaminhamento de eventos do Twitter
description: Essa extensão de encaminhamento de eventos do Adobe Experience Platform permite assimilar eventos no Twitter para atender aos requisitos da sua empresa.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: 54c240e5-6160-4654-ac5b-6afa8d99a765
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 3%

---

# Extensão de encaminhamento de eventos da [!DNL Twitter]

[[!DNL Twitter]](https://twitter.com/i/flow/login) O é um serviço de redes sociais online, no qual os usuários postam e interagem com mensagens de 280 caracteres conhecidas como tweets. Os usuários podem interagir com o Twitter usando um navegador, software de front-end móvel ou programaticamente por meio de seu [APIs](https://developer.twitter.com/en/docs/twitter-api)

A variável [!DNL Twitter] API de conversões da Web [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) permite que você aproveite os dados capturados na Rede de borda da Adobe Experience Platform e os envie para [!DNL Twitter]. Este documento aborda os casos de uso da extensão, como instalá-la e como integrar seus recursos ao encaminhamento de eventos [regras](../../../ui/managing-resources/rules.md).

[!DNL Twitter] exige [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) para autenticação com o [!DNL Twitter] [!DNL Web Conversions] API.

## Casos de uso

Essa extensão deve ser usada se você quiser usar dados da Rede de borda no [!DNL Twitter] para aproveitar os recursos de análise e direcionamento do cliente.

Por exemplo, considere uma equipe de marketing em uma organização. A equipe captura dados do evento de interação do usuário de seu site como dados do evento de seu site e os carrega em [!DNL Twitter] usar esta extensão de encaminhamento de eventos.

As equipes de marketing e análise podem aproveitar [!DNL Twitter's] recursos para realizar análises adicionais e direcionar esses usuários para campanhas de anúncio direcionadas.

Para obter mais informações sobre casos de uso específicos do [!DNL Twitter], consulte o [[!DNL Twitter] casos de uso](https://developer.twitter.com/en/use-cases/build-for-businesses) documentação.

## [!DNL Twitter] pré-requisitos e medidas de proteção {#prerequisites}

Você deve ter um válido [!DNL Twitter] para usar essa extensão. Vá para a [[!DNL Twitter] página de registro](https://help.twitter.com/en/using-twitter/create-twitter-account) para registrar e criar uma conta se ainda não tiver uma.

Você deve configurar sua conta como um [!DNL Twitter] conta de desenvolvedor. Para saber como se inscrever como desenvolvedor, consulte o [[!DNL Twitter] conta do desenvolvedor](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### Medidas de proteção de API {#guardrails}

A variável [!DNL Twitter] A API de conversões da Web tem um limite de taxa de 60.000 solicitações por intervalo de 15 minutos, em que cada solicitação permite 500 eventos.

### Coletar detalhes de configuração necessários {#configuration-details}

Para conectar o Experience Platform a [!DNL Twitter], as seguintes entradas são necessárias:

| Tipo de chave | Descrição |
| --- | --- |
| Chave do consumidor | &#x200B; A chave de API do aplicativo para acessar o [!DNL Twitter] API. Consulte a [!DNL Twitter] documentação sobre [chaves e segredos da api](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) para obter orientação. | |
| Segredo do consumidor | O segredo da API permite que o aplicativo acesse o [!DNL Twitter] API. Consulte a [!DNL Twitter] documentação sobre [chaves e segredos da api](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) para obter orientação. |
| Segredo do token | O token secreto sem expiração do seu aplicativo, que é usado para autenticação na [!DNL Twitter] API via OAuth. Consulte a [!DNL Twitter] documentação sobre [obtenção de tokens de acesso de uso](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) para obter orientação. |
| Token de acesso | O token de acesso sem expiração do seu aplicativo, que é usado para autenticação na [!DNL Twitter] API via OAuth. Consulte a [!DNL Twitter] documentação sobre [obtenção de tokens de acesso de uso](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) para obter orientação. |
| ID do pixel | A variável [!DNL Twitter] Pixel é uma tag do site implementada no site para rastrear ações ou conversões do site. Consulte a [!DNL Twitter] documentação sobre [rastreamento de conversão para sites](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) para obter orientação. |

## Instale e configure o [!DNL Twitter] extensão {#install}

Para instalar a extensão, [criar uma propriedade de encaminhamento de eventos](../../../ui/event-forwarding/overview.md#properties) ou escolha uma propriedade existente para editar.

Selecionar **[!UICONTROL Extensões]** no painel de navegação esquerdo. No **[!UICONTROL Catálogo]** selecione **[!UICONTROL Instalar]** no cartão para o [!DNL Twitter] extensão.

![Catálogo que mostra o [!DNL Twitter] realce da extensão instalar.](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>Dependendo das suas necessidades de implementação, talvez seja necessário criar um esquema, elementos de dados e um conjunto de dados antes de configurar a extensão. Revise todas as etapas de configuração antes de começar para determinar quais entidades você precisa configurar para seu caso de uso.

Na tela seguinte, insira [valores de configuração](#configuration-details) que você coletou anteriormente [!DNL Twitter]:

* **[!UICONTROL ID do pixel]**
* **[!UICONTROL Chave do consumidor]**
* **[!UICONTROL Segredo do consumidor]**
* **[!UICONTROL Token]**
* **[!UICONTROL Segredo do token]**

Quando terminar, selecione **[!UICONTROL Salvar]**.

![[!DNL Twitter] tela de configuração para o [!DNL Twitter] extensão.](../../../images/extensions/server/twitter/configure.png)

## Configurar uma regra de encaminhamento de eventos {#config-rule}

Depois que todos os elementos de dados forem configurados, você poderá começar a criar regras de encaminhamento de eventos que determinam quando e como seus eventos serão enviados para o [!DNL Twitter].

Criar um novo [regra](../../../ui/managing-resources/rules.md) na propriedade de encaminhamento de eventos. Em **[!UICONTROL Ações]**, adicione uma nova ação e defina a extensão para **[!UICONTROL Twitter]**. Para enviar eventos da Rede de borda para o [!DNL Twitter], defina o **[!UICONTROL Tipo de ação]** para **[!UICONTROL Enviar conversão da Web].**

Após a seleção, controles adicionais são exibidos para configurar ainda mais o evento. Você precisa mapear o [!DNL Twitter] para os elementos de dados criados anteriormente. Para obter mais informações, consulte [[!DNL Twitter] API de conversões da Web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![A variável [!DNL Twitter] criação de uma regra de evento de conversão.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL Identificação do usuário]**

| Nome do campo | Descrição | Exemplo | Obrigatório |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] ID do clique] | [!DNL Twitter] ID do clique conforme analisado no URL de click-through. | 26l6412g5p4iyj65a2oic2ayg2 | Obrigatório se nenhum outro identificador for adicionado. |
| [!UICONTROL Email] | Um endereço de email com hash SHA256. O texto deve estar em minúsculas e qualquer espaço à direita ou à esquerda deve ser removido antes do hash. | eventforwarding@example.com | Obrigatório se nenhum outro identificador for adicionado. |
| [!UICONTROL Telefone] | O telefone serve como um identificador para corresponder ao evento de conversão. O número de telefone deve estar no formato E164 [+][código do país][código de área][local phone number] antes do hash. | +911234567875 | Obrigatório se nenhum outro identificador for adicionado. |

**[!UICONTROL Dados de conversão]**

| Nome do campo | Descrição | Exemplo | Obrigatório |
| --- | --- | --- | --- |
| [!UICONTROL Tempo de conversão] | Data e hora como string em ISO 8601 ou em `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. | 2022-02-18T01:14:00,603Z | Sim |
| [!UICONTROL ID do evento] | A ID de base 36 de um evento específico. Essa ID deve corresponder a um evento pré-configurado contido em seu [!DNL Twitter] conta de publicidade. Isso é conhecido como a ID do evento correspondente no Gerenciador de eventos. | o87ne ou tw-o8z6j-o87ne (tw-pixel_id-event-id) | Sim |
| [!UICONTROL Número de itens] | O número de itens sendo comprados no evento. Deve ser um número positivo maior que 0. | 4 | Não |
| [!UICONTROL Moeda] | A moeda dos itens que estão sendo comprados no evento. Isso é expresso em ISO-4217 e, se não for fornecido, o padrão será USD. | USD | Não |
| [!UICONTROL Valor] | O valor do preço dos itens que estão sendo comprados no evento. | 100,00 | Não |
| [!UICONTROL ID de conversão] | Um identificador para um evento de conversão que pode ser usado para desduplicação entre conversões de Pixel da Web e API de conversão na mesma tag de evento. | 23294827 | Não |
| [!UICONTROL Descrição] | Uma descrição com todas as informações adicionais sobre as conversões. | Testar conversão | Não |

## Validar dados no [!DNL Twitter]

Depois que a regra de encaminhamento de eventos tiver sido criada e executada, valide se o evento enviado para o [!DNL Twitter] A API é exibida conforme esperado no [!DNL Twitter] IU.

Se a coleção de eventos e a [!DNL Experience Platform] integração foram bem-sucedidas, você verá eventos no [!DNL Twitter] [!UICONTROL Gerenciador de eventos].

![A variável [!DNL Twitter] gerenciador de eventos](../../../images/extensions/server/twitter/event-manager.png)

## Próximas etapas

Este guia abordou como enviar eventos de conversão para o [!DNL Twitter] usando o encaminhamento de eventos. Para obter mais informações sobre essas tecnologias subjacentes, consulte a documentação oficial:

* [[!DNL Twitter] APIs](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] API de conversão da Web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] Token de acesso do usuário](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [Rastreamento de ID de pixel e conversão](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
