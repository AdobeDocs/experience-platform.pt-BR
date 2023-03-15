---
description: Esta página descreve como se autenticar e começar a usar o Adobe Experience Platform Destination SDK. Ele inclui instruções sobre como obter credenciais de autenticação de Adobe I/O, um nome de sandbox e a permissão de controle de acesso de criação de destino.
title: Introdução ao Destination SDK
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: 557db5b7eefdd7902895e428f7bc34e3ad8a6f58
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 4%

---

# Introdução

## Visão geral {#overview}

Esta página descreve como se autenticar e começar a usar o Adobe Experience Platform Destination SDK. Ele inclui instruções sobre como obter credenciais de autenticação de Adobe I/O, um nome de sandbox e a permissão de controle de acesso de criação de destino.

## Terminologia {#terminology}

Este guia usa conceitos específicos da plataforma, como Organização IMS e sandboxes. Consulte o [glossário Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html?lang=pt-BR) para obter as definições destes e de outros termos.

## Obter as credenciais de autenticação necessárias {#obtain-authentication-credentials}

O Destination SDK usa o [Adobe I/O](https://www.adobe.io/) gateway para autenticação. Para fazer chamadas de API para endpoints Destination SDK, você deve fornecer determinados cabeçalhos em suas chamadas de API. Trabalhe com a equipe do Adobe Exchange para configurar a autenticação para que você [Console do Adobe Developer](https://developer.adobe.com/console).

Para fazer chamadas com êxito para endpoints da API Destination SDK, siga o [Tutorial de autenticação Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html). Inicie o tutorial pelo &quot;[Gerar uma chave de API, uma ID de organização IMS e um segredo do cliente](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)&quot; etapa. A equipe do Adobe Exchange cuidará das etapas anteriores para você. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários nas chamadas de API de Destination SDK, conforme mostrado abaixo:

* `x-api-key: {API_KEY}`, também conhecida como ID do cliente
* `x-gw-ims-org-id: {ORG_ID}`, também conhecida como ID da organização
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

Todos os recursos no Experience Platform são isolados em sandboxes virtuais específicas. As solicitações para Destination SDK exigem cabeçalhos que especifiquem o nome da sandbox em que a operação ocorre:

* `x-sandbox-name: {SANDBOX_NAME}`

A equipe do Adobe Exchange fornece o nome da sandbox, que você precisa usar em chamadas para os endpoints da API Destination SDK.

## Controle de acesso baseado em função (RBAC) {#rbac}

Para usar os endpoints da API do Destination SDK descritos no [documentação de referência](./configuration-options.md), você precisará do **[!UICONTROL Criação de destino]** permissão de controle de acesso. Trabalhe com a equipe do Adobe Exchange para obter essa permissão atribuída a você no [Adobe Admin Console](https://adminconsole.adobe.com/).

![Permissão de criação de destino](./assets/destination-authoring-permission.png)

Para obter mais informações, leia os seguintes documentos sobre o Controle de acesso a Experience Platform:

* [Gerenciar permissões de um perfil de produto](/help/access-control/ui/permissions.md)
* [Permissões disponíveis para o Experience Platform](/help/access-control/home.md#permissions)
* [Documentação do Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html)

## Considerações adicionais {#additional-considerations}

* Quaisquer alterações feitas nas configurações de destino, independentemente de você criar ou editar uma configuração de destino, precisam ser revisadas e aprovadas pelo Adobe. As alterações são refletidas nos destinos somente após a revisão ser concluída.
* Somente os usuários que pertencem à mesma organização e têm acesso à sandbox podem editar a configuração de destino.

## Próximas etapas {#next-steps}

Seguindo as etapas deste artigo, você obteve credenciais de autenticação para o Adobe I/O, um nome de sandbox e a permissão de controle de acesso de criação de destino. Em seguida, você pode configurar um destino usando o Destination SDK.

* Leia os seguintes guias de configuração, dependendo do tipo de destino:

   * [Usar o Destination SDK para configurar um destino de transmissão](./configure-destination-instructions.md)
   * [Usar o Destination SDK para configurar um destino baseado em arquivo](./configure-file-based-destination-instructions.md)

* Para todas as operações, consulte a [Documentação da API de criação de destino](https://www.adobe.io/experience-platform-apis/references/destination-authoring/).
* Use o [Coleção de Postman da API de criação de destino](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json) para configurar seu destino usando os endpoints da API do Destination SDK. Para começar a usar o Postman, consulte [etapas para importar ambientes e coleções](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) e uma [guia de vídeo para criar o ambiente do Postman](https://video.tv.adobe.com/v/28832).
