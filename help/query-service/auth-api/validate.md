---
keywords: Experience Platform; segurança; acesso a ip; validação; guia de API; serviço de consulta; verificação de IP
title: Endpoint de validação de IP
description: Saiba como validar o acesso IP para sandboxes no Serviço de consulta usando o endpoint da API de validação de IP.
role: Developer
source-git-commit: ad1b6d8449a2a3ca9c8422e70769d12e33d8e255
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 1%

---

# Endpoint de validação de IP

Use o ponto de extremidade da API de validação de IP para verificar se um endereço IP especificado tem permissão para acessar uma sandbox designada no Serviço de consulta. Essa verificação confirma se as restrições de acesso se aplicam ou se um endereço IP tem permissão para acessar dados em uma sandbox.

## Validar IP para acesso à sandbox {#validate-ip-for-sandbox-access}

Use o ponto de extremidade de Validação de IP para verificar se um determinado endereço IP tem permissão para acessar dados da sandbox especificada. Se nenhuma restrição de IP for configurada para a sandbox, todos os endereços IP serão permitidos por padrão. Se houver restrições de IP ou CIDR existentes, essa API verificará se o endereço IP especificado corresponde a algum intervalo configurado.

>[!NOTE]
>
>Você pode acessar este ponto de extremidade com **tokens de usuário** ou **tokens de serviço**. Não são necessários requisitos de função específicos.

**Formato da API**

```http
POST /security/validate/ip-access
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/security/validate/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
       "ipAddress": "197.2.0.2"
     }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com um booliano que indica se o IP é permitido.

>[!NOTE]
>
>O campo `isAllowed` na resposta retorna `true` se o IP fornecido tiver permissão para acessar a sandbox e `false` se não tiver. Essa API oferece suporte à validação dinâmica do acesso e à garantia de conformidade de segurança para ambientes de sandbox.

```json
{
"isAllowed": true
}
```
