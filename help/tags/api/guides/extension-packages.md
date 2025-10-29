---
title: Compartilhamento de pacotes de extensão privados na API do Reator
description: Saiba como autorizar outras empresas a compartilhar pacotes de extensão privados na API do Reator.
exl-id: 3300a630-6d22-46e1-8b1b-b5d12a3ea44c
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 3%

---

# Compartilhamento de pacotes de extensão privados

>[!NOTE]
>
>Os usuários com a permissão `develop_extensions` na organização do proprietário do pacote de extensão podem criar, listar e excluir autorizações de uso do pacote de extensão para esse pacote de extensão. Os usuários em uma organização autorizada que possuem a permissão `manage_properties` só podem listar as autorizações de uso do pacote de extensão para sua organização e atualizar seu estado para `accepted` se quiserem usar esse pacote de extensão, ou para `rejected` se não quiserem usá-lo.

Os proprietários de pacotes de extensão podem conceder permissão para que outras empresas utilizem suas versões privadas por meio da API do Reator. Uma licença de uso para um pacote de extensão é concedida a cada empresa aprovada, e essa autorização é válida para todas as versões privadas atuais e futuras do pacote.

Este guia fornece uma visão geral de alto nível sobre como configurar autorizações de uso de pacotes de extensão. Para obter orientações mais detalhadas sobre como gerenciar autorizações na API do Reator, incluindo o exemplo JSON da estrutura de uma autorização, consulte o [manual do ponto de extremidade de autorização de uso do pacote de extensão](../endpoints/extension-package-usage-authorizations.md).

## Criar uma autorização {#create-authorization}

Para criar uma nova autorização, você deve ter o direito `develop_extensions`. O exemplo a seguir demonstra como criar uma autorização de uso de pacote de extensão para um pacote de extensão usando o `authorized_org_id` da empresa que você deseja autorizar.

**Formato da API**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parâmetro | Descrição |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | O `ID` do pacote de extensão para o qual você deseja criar uma autorização. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir cria uma nova autorização de pacote de extensão para a empresa especificada.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| Propriedade | Descrição |
| --- | --- |
| `attributes.authorized_org_id` | O `ID` da organização que você deseja autorizar. |

{style="table-layout:auto"}

O estado inicial da autorização está no estágio `pending_approval`. Antes de usar o pacote de extensão, a empresa deve aprovar a autorização. Os usuários da empresa podem navegar pelo pacote de extensão privado enquanto a autorização estiver pendente de aprovação, mas não podem instalá-lo e não podem encontrá-lo no catálogo de extensões.

## Aprovar uma autorização {#approve-authorization}

Para aprovar uma autorização, você deve ter os direitos de `manage_properties`. Como empresa autorizada, será necessário enviar uma solicitação PATCH para a autorização de uso do pacote de extensão, incluindo o `ID` da autorização e definir o estado definido como `approved`.

**Formato da API**

```http
PATCH //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | O `ID` da autorização que você deseja aprovar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação do PATCH a seguir define o `state` de uma autorização como `approved`.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "state": "approved"
            },
            "id": ":extension_package_usage_authorization_id",
            "type": "extension_package_usage_authorizations"
        }
      }
```

Depois que a autorização for aprovada como a empresa autorizada, você poderá instalar o pacote de extensão em suas propriedades.

>[!NOTE]
>
>Se a autorização for rejeitada, a empresa autorizada não poderá usar o pacote de extensão.

## Excluir uma autorização {#delete-authorization}

Como proprietário de um pacote de extensão, você pode revogar a autorização a qualquer momento excluindo a autorização de uso do pacote de extensão. Isso impedirá que a empresa autorizada exiba versões privadas do pacote de extensão no catálogo e o instale em suas propriedades. No entanto, as versões privadas já instaladas continuarão a funcionar conforme esperado após a exclusão.

**Formato da API**

```http
DELETE //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | O `ID` da autorização que você deseja excluir. |

{style="table-layout:auto"}

**Solicitação**

A solicitação do DELETE a seguir remove os privilégios de autorização de uma empresa.

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
```
