---
title: Ponto de Extremidade de Certificado Público
description: Saiba como recuperar certificados públicos usando o ponto de extremidade /public-certificate da API de Serviço MTLS.
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: 754044621cdaf1445f809bceaa3e865261eb16f0
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 3%

---

# Endpoint de certificado público

Este guia explica como usar o endpoint de certificado público para recuperar com segurança certificados públicos para os aplicativos Adobe de sua organização. Ele inclui uma amostra de chamada de API e instruções detalhadas para ajudar os desenvolvedores a autenticar e verificar as trocas de dados.

## Introdução

Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo os cabeçalhos necessários e como ler as chamadas de exemplo da API.

## Caminhos da API {#paths}

As informações a seguir são os caminhos de API essenciais necessários para usar a API do serviço mTLS. Isso inclui o URL do gateway da plataforma, o caminho base da API e um exemplo de um caminho completo para recuperar um certificado público.

- URL DO PLATFORM Gateway: `https://platform.adobe.io/`
- Caminho base para esta API: `/data/core/mtls`
- Exemplo de um caminho completo: `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Recupere seus certificados públicos {#list}

Você pode recuperar os certificados públicos para qualquer um dos aplicativos Adobe da sua organização fazendo uma solicitação GET para o ponto de extremidade `/v1/certificate/public-certificate`.

**Formato da API**

```http
GET /v1/certificate/public-certificate
```

Os parâmetros de consulta opcionais a seguir podem ser usados ao recuperar seus certificados públicos.

| Parâmetro de consulta | Descrição | Exemplo |
| --------------- | ----------- | ------- |
| `page` | Especifica a página a partir da qual os resultados da sua solicitação serão iniciados. | `page=5` |
| `limit` | O número máximo de certificados públicos que você deseja recuperar por página. | `limit=20` |

{style="table-layout:auto"}

**Solicitação**

Um exemplo de solicitação para retornar os certificados públicos associados à sua organização é visto na seção que pode ser recolhida abaixo.

+++Exemplo de solicitação

```shell
curl -X GET https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' 
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 e lista os certificados públicos da organização.

+++Uma amostra de resposta bem-sucedida

```json
{
   "results":[
      {
         "certCommonName":"Adobe Experience Platform",
         "publicCertificate":"-----BEGIN CERTIFICATE-----\nMIIDQTCCAimgAwIBAgITBmyfACAfma......KJY5u89CjAwj\n-----END CERTIFICATE-----",
         "expiryDate":"2024-07-17T21:27:57.434Z"
      }
   ],
   "total":0,
   "count":0,
   "_links":{
      "next":{
         "href":"string",
         "templated":true
      },
      "prev":{
         "href":"string",
         "templated":true
      },
      "page":{
         "href":"string",
         "templated":true
      }
   }
}
```

| Propriedade | Descrição |
| --- | --- |
| `certCommonName` | O nome comum (CN) do certificado, que normalmente representa o nome ou a identidade do servidor ou entidade para o qual o certificado é emitido. |
| `publicCertificate` | O certificado público real em um formato de cadeia de caracteres, que é usado para autenticar e criptografar comunicações. |
| `expiryDate` | A data e a hora em que o certificado público expirará, formatadas em ISO 8601 (UTC). |

{style="table-layout:auto"}

+++

## Próximas etapas

Depois de ler este guia, você entende como recuperar seus certificados públicos usando a API do Adobe Experience Platform. Para saber mais sobre como gerenciar dados de clientes para garantir a conformidade com as regulamentações e políticas organizacionais, consulte a [visão geral sobre governança de dados](../home.md).

<!-- To test this API call, navigate to the [MTLS API reference page]() to interact with the Experience Platform API endpoints. -->

<!-- Add link after developer page is live -->
