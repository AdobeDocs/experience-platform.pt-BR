---
description: Esta página descreve como se autenticar e começar a usar o Adobe Experience Platform Destination SDK. Ele inclui instruções sobre como obter credenciais de autenticação da Adobe I/O, um nome de sandbox e a permissão de controle de acesso para criação de destino.
title: Introdução ao Destination SDK
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---

# Introdução

## Visão geral {#overview}

Esta página descreve como se autenticar e começar a usar o Adobe Experience Platform Destination SDK. Ele inclui instruções sobre como obter credenciais de autenticação da Adobe I/O, um nome de sandbox e a permissão de controle de acesso para criação de destino.

## Terminologia {#terminology}

Este guia usa conceitos específicos da Experience Platform, como organização e sandboxes. Consulte o [glossário do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html?lang=pt-BR) para obter as definições desses termos. Consulte o [glossário do Destination SDK](/help/destinations/destination-sdk/glossary.md) para obter os termos relacionados diretamente a esta funcionalidade.

## Obter as credenciais de autenticação necessárias {#obtain-authentication-credentials}

O Destination SDK usa o gateway [Adobe I/O](https://www.adobe.io/) para autenticação. Para fazer chamadas de API para endpoints do Destination SDK, você deve fornecer determinados cabeçalhos nas chamadas de API. Trabalhe com a equipe da Adobe Exchange para configurar a autenticação para você no [Adobe Developer Console](https://developer.adobe.com/console).

Para fazer chamadas com êxito para pontos de extremidade de API do Destination SDK, siga o [tutorial de autenticação do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=pt-BR). Inicie o tutorial da etapa &quot;[Gerar uma chave de API, ID da organização e segredo do cliente](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=pt-BR#api-ims-secret)&quot;. A equipe do Adobe Exchange cuidará das etapas anteriores para você. Concluir o tutorial de autenticação fornece os valores de cada um dos cabeçalhos necessários nas chamadas de API do Destination SDK, conforme mostrado abaixo:

* `x-api-key: {API_KEY}`, também conhecido como ID do cliente
* `x-gw-ims-org-id: {ORG_ID}`, também conhecido como ID da organização
* `Authorization: Bearer {ACCESS_TOKEN}`. O token de acesso tem um tempo de expiração de 24 horas, expresso em milissegundos, portanto, você terá que atualizá-lo. Para atualizar o token de acesso, repita as etapas descritas no tutorial de autenticação.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {ORG_ID}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## Propriedade de destino e sandboxes {#destination-ownership}

Todos os recursos no Experience Platform são isolados em sandboxes virtuais específicas. As solicitações para o Destination SDK exigem cabeçalhos que especifiquem o nome da sandbox em que a operação ocorre:

* `x-sandbox-name: {SANDBOX_NAME}`

A equipe do Adobe Exchange fornece o nome da sandbox, que você precisa usar em chamadas para os endpoints da API do Destination SDK.

## Controle de acesso baseado em função (RBAC) {#rbac}

Para usar os pontos de extremidade da API do Destination SDK descritos na [documentação de referência](functionality/configuration-options.md), você precisa da permissão de controle de acesso **[!UICONTROL Criação de Destino]**. Trabalhe com a equipe da Adobe Exchange para obter esta permissão atribuída a você no [Adobe Admin Console](https://adminconsole.adobe.com/).

![Permissão de criação do destino](./assets/destination-authoring-permission.png)

Para obter mais informações, leia os seguintes documentos de Controle de acesso do Experience Platform:

* [Gerenciar permissões de um perfil de produto](/help/access-control/ui/permissions.md)
* [Permissões disponíveis para o Experience Platform](/help/access-control/home.md#permissions)
* [Documentação do Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html)

## Considerações adicionais {#additional-considerations}

* Para destinos públicos/de produção, todas as alterações feitas nas configurações de destino, independentemente de você criar ou editar uma configuração de destino, precisam ser revisadas e aprovadas pela Adobe. As alterações são refletidas nos destinos somente após a revisão ser concluída. Isso não se aplica a destinos privados que só estão disponíveis para você.
* Somente os usuários que pertencem à mesma organização e têm acesso à sandbox podem editar a configuração de destino.

## Próximas etapas {#next-steps}

Seguindo as etapas deste artigo, você obteve credenciais de autenticação para o Adobe I/O, um nome de sandbox e a permissão de controle de acesso de criação de destino. Em seguida, você pode configurar um destino usando o Destination SDK.

* Leia os seguintes guias de configuração, dependendo do tipo de destino:

   * [Usar o Destination SDK para configurar um destino de transmissão](guides/configure-destination-instructions.md)
   * [Usar o Destination SDK para configurar um destino baseado em arquivo](guides/configure-file-based-destination-instructions.md)

* Para todas as operações, consulte a [documentação da API de criação de destino](https://www.adobe.io/experience-platform-apis/references/destination-authoring/).
* Use a [coleção Postman da API de Criação de Destino](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json) para configurar seu destino usando os pontos de extremidade da API do Destination SDK. Para começar a usar o Postman, consulte as [etapas para importar ambientes e coleções](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) e o [guia de vídeo para criar o ambiente do Postman](https://video.tv.adobe.com/v/28832).
