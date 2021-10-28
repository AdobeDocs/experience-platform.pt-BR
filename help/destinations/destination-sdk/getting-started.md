---
description: Esta página descreve como autenticar e começar a usar o Adobe Experience Platform Destination SDK. Ele inclui instruções sobre como obter credenciais de autenticação do Adobe I/O, um nome de sandbox e a permissão de controle de acesso de criação de destino.
title: Introdução ao SDK de destino
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: 0bd57e226155ee68758466146b5d873dc4fdca29
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 2%

---

# Introdução

## Visão geral {#overview}

Esta página descreve como autenticar e começar a usar o Adobe Experience Platform Destination SDK. Ele inclui instruções sobre como obter credenciais de autenticação do Adobe I/O, um nome de sandbox e a permissão de controle de acesso de criação de destino.

## Terminologia {#terminology}

Este guia usa conceitos específicos da plataforma, como Organização IMS e sandboxes. Consulte o [Glossário de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html) para as definições destes e outros termos.

## Obter credenciais de autenticação necessárias {#obtain-authentication-credentials}

O SDK de destino usa o [Adobe I/O](https://www.adobe.io/) gateway para autenticação. Para fazer chamadas de API para endpoints do SDK de destino, você deve fornecer determinados cabeçalhos em suas chamadas de API. Trabalhe com a equipe do Adobe Exchange para configurar a autenticação para você no [Console do desenvolvedor do Adobe](http://console.adobe.io/).

Para fazer chamadas com êxito para endpoints da API do SDK de destino, siga o [Tutorial de autenticação de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html). Inicie o tutorial a partir do &quot;[Gerar uma chave de API, ID de organização IMS e segredo do cliente](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)&quot;. A equipe do Adobe Exchange lidará com as etapas anteriores para você. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em chamadas de API do SDK de destino, conforme mostrado abaixo:

* `x-api-key: {API_KEY}`também chamada de ID do cliente
* `x-gw-ims-org-id: {IMS_ORG}`também conhecida como ID da organização
* `Authorization: Bearer {ACCESS_TOKEN}`. O token de acesso tem um tempo de expiração de 24 horas, expresso em milissegundos, portanto, será necessário atualizá-lo. Para atualizar o token de acesso, repita as etapas descritas no tutorial de autenticação.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {IMS_ORG}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## Propriedade de destino e sandboxes {#destination-ownership}

Todos os recursos no Experience Platform são isolados para sandboxes virtuais específicas. As solicitações para o SDK de destino exigem cabeçalhos que especificam o nome da sandbox em que a operação ocorre:

* `x-sandbox-name: {SANDBOX_NAME}`

A equipe do Adobe Exchange fornece o nome da sandbox, que deve ser usado em chamadas para os pontos de extremidade da API do SDK de destino.

## Controle de acesso baseado em funções (RBAC) {#rbac}

Para usar os endpoints da API do SDK de destino descritos na seção [documentação de referência](./configuration-options.md), você precisa do **[!UICONTROL Criação de destinos]** permissão de controle de acesso. Trabalhe com a equipe do Adobe Exchange para obter essa permissão atribuída a você em [Adobe Admin Console](https://adminconsole.adobe.com/).

![Permissão de criação de destino](./assets/destination-authoring-permission.png)

Para obter mais informações, leia os seguintes documentos de Controle de Acesso ao Experience Platform:

* [Gerenciar permissões para um perfil de produto](/help/access-control/ui/permissions.md)
* [Permissões disponíveis para o Experience Platform](/help/access-control/home.md#permissions)
* [Documentação do Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html)

## Considerações adicionais {#additional-considerations}

* Quaisquer alterações feitas nas configurações de destino, sejam você criar ou editar uma configuração de destino, precisam ser revisadas e aprovadas pelo Adobe. Suas alterações são refletidas em seus destinos somente após a revisão ser feita.
* Somente os usuários que pertencem à mesma organização e têm acesso à sandbox podem editar a configuração de destino.

## Próximas etapas {#next-steps}

Seguindo as etapas deste artigo, você obteve credenciais de autenticação para o Adobe I/O, um nome de sandbox e a permissão de controle de acesso de criação de destino. Em seguida, você pode configurar um destino usando o SDK de destino.
* Ler [Use o SDK de destino para configurar seu destino](./configure-destination-instructions.md) para as próximas etapas.
* Para todas as operações, consulte a [Documentação da API de criação de destino](https://www.adobe.io/experience-platform-apis/references/destination-authoring/).
