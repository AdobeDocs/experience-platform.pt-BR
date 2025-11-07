---
title: Criar ponto de extremidade da API de público-alvo
description: Saiba como criar os metadados para um público externo usando a API.
hide: true
hidefromtoc: true
exl-id: e841a5f6-f406-4e1d-9e8a-acb861ba6587
source-git-commit: a3b82eb1efaf257723208504c90210850a44b4a4
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 7%

---

# Criar ponto de extremidade do público-alvo

O ponto de extremidade `/audiences` da POSTAGEM pode ser usado para criar os metadados de um público externo, o que permite que o público fique visível no Portal de Público. Você deve usar esse endpoint se a assimilação do público-alvo for gerenciada em um serviço separado, como a assimilação em lote.

## Introdução

>[!IMPORTANT]
>
>Os pontos de extremidade neste guia recebem o prefixo `/core/ais`, e não `/core/ups`.

Para usar as APIs do Experience Platform, você deve ter concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores de cada um dos cabeçalhos necessários nas chamadas de API do Experience Platform, conforme mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral das sandboxes](../../sandboxes/home.md).

**Formato da API**

>[!IMPORTANT]
>
>Você **deve** incluir o parâmetro de consulta `createAudienceMetaOnly=true` como parte da solicitação.

```http
POST /audiences?createAudienceMetaOnly=true
```

**Solicitação**

>[!IMPORTANT]
>
>Você **deve** incluir o cabeçalho `Accept: application/vnd.adobe.external.audiences+json; version=2` como parte da solicitação de API.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/audiences?createAudienceMetaOnly=true \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'\
 -H 'Accept: application/vnd.adobe.external.audiences+json; version=2'
 -d '{
    "name": "Sample audience name",
    "description" "A sample description for the audience.",
    "namespace": "agora",
    "originName": "Agora_Collaboration"
 }'
```

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| `name` | String | O nome do público. |
| `description` | String | Uma descrição opcional para o público-alvo. |
| `namespace` | String | O namespace do público. |
| `originName` | String | O nome da origem do público-alvo. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o público recém-criado.

```json
{
    "name": "Sample audience name",
    "audienceId": "4a815904-f2f9-4237-82fb-55605bcc2ad7"
}
```

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| `name` | String | O nome do público-alvo criado. |
| `audienceId` | String | A ID do público-alvo criado. |
