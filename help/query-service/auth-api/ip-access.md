---
keywords: Experience Platform; segurança; ip-access; QS-Auth; guia de API; serviço de consulta; intervalos de IP
title: Ponto de Extremidade de Acesso IP
description: Saiba como gerenciar intervalos IP para acesso à sandbox no Serviço de consulta usando o ponto de extremidade da API de acesso IP.
role: Developer
source-git-commit: 23e5260133f0f16ac30d14346c227a21f251b7e1
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 3%

---

# Ponto de extremidade de acesso IP

Para proteger o acesso a dados em uma sandbox do Serviço de consulta especificada, use o ponto de extremidade de Acesso a IP para gerenciar intervalos de IP permitidos. Você pode usar essa API para buscar, configurar ou excluir intervalos de IPs associados à ID da sua organização.

Você pode executar as seguintes ações com a API de acesso IP:

- **Buscar todos os intervalos IP**
- **Definir novos intervalos IP**
- **Excluir intervalos IP existentes**

Este documento aborda as solicitações e respostas que você pode fazer e receber do ponto de extremidade `/security/ip-access`.

>[!NOTE]
>
>Você deve ter um token de usuário para chamar essa API. Consulte o [guia de introdução](./getting-started.md) para obter informações sobre como adquirir os valores necessários para cada um dos cabeçalhos.

## Buscar todos os intervalos IP {#fetch-all-ip-ranges}

Recupere uma lista de todos os intervalos IP configurados para sua sandbox. Se nenhum intervalo IP for definido, todos os IPs serão permitidos por padrão, e a resposta retornará uma lista vazia em `allowedIpRanges`.

**Formato da API**

```http
GET /security/ip-access
```

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista dos intervalos IP permitidos da sandbox.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "101.10.1.1"}
  ]
}
```

A tabela a seguir fornece uma descrição e um exemplo das propriedades do schema de resposta:

| Propriedade | Descrição | Exemplo |
|------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------|
| `imsOrg` | ID da organização para a sandbox. | `{ORG_ID}` |
| `sandboxName` | Nome da sandbox à qual se aplicam restrições de IP. | `prod` |
| `channel` | O modo de acesso para restrições de IP. Atualmente, o único valor aceito é `data_distiller`. Esse valor significa que as restrições de IP são aplicadas às conexões PSQL ou JDBC. | `data_distiller` |
| `allowedIpRanges` | Lista de IPs permitidos no formato CIDR ou IP fixo. Cada entrada pode incluir uma descrição opcional. | `[{"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"}]` |

>[!NOTE]
>
>O campo `allowedIpRanges` pode incluir dois tipos de especificações de IP:<br><ul><li>**CIDR**: notação CIDR padrão (por exemplo, `"136.23.110.0/23"`) para definir intervalos IP.</li><li>**IPs Corrigidos**: IPs Simples para permissões de acesso individuais (por exemplo, `"101.10.1.1"`).</li></ul>

## Definir novos intervalos de IP

Substitua os intervalos IP existentes definindo uma nova lista para a sandbox. Esta operação requer uma lista completa de intervalos IP, incluindo todos que permanecem inalterados.

**Formato da API**

```http
PUT /security/ip-access
```

**Solicitação**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "ipRanges": [
       {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
       {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
       {"ipRange": "101.10.1.1"},
       {"ipRange": "163.77.30.9", "description": "Test server IP"}
     ]
   }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes dos intervalos IP recém-configurados.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```

## Excluir intervalos de IP {#delete-ip-ranges}

Remova todos os intervalos IP configurados para a sandbox. Essa ação exclui os intervalos IP e retorna a lista IP excluída.

>[!NOTE]
>
>A operação de exclusão se aplica à ID da organização (`imsOrg`) e afeta todos os intervalos IP configurados para a sandbox.

**Formato da API**

```http
DELETE /security/ip-access
```

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes dos intervalos IP excluídos.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "deletedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```

