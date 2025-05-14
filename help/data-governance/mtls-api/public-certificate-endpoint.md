---
title: Ponto de Extremidade de Certificado Público
description: Saiba como recuperar certificados públicos usando o ponto de extremidade /public-certificate da API de Serviço MTLS.
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: d74353e70e992150c031397009d0c8add3df5e7b
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 2%

---

# Endpoint de certificado público

>[!NOTE]
>
>O Adobe não oferece mais suporte ao download estático de certificados mTLS públicos. Use essa API para recuperar certificados válidos para suas integrações. A recuperação automatizada agora é necessária para evitar interrupções do serviço.

Este guia explica como usar o endpoint de certificado público para recuperar com segurança certificados públicos para os aplicativos Adobe de sua organização. Ele inclui uma amostra de chamada de API e instruções detalhadas para ajudar os desenvolvedores a autenticar e verificar as trocas de dados.

## Introdução

Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter detalhes importantes sobre os cabeçalhos necessários e como interpretar chamadas de API de exemplo.

## Caminhos da API {#paths}

As informações a seguir são os caminhos de API essenciais necessários para usar a API do serviço mTLS. Isso inclui o URL do gateway da plataforma, o caminho base da API e um exemplo de um caminho completo para recuperar um certificado público.

- URL DO PLATFORM Gateway: `https://platform.adobe.io/`
- Caminho base para esta API: `/data/core/mtls`
- Exemplo de um caminho completo: `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Recupere seus certificados públicos {#list}

Faça uma solicitação do GET ao ponto de extremidade `/v1/certificate/public-certificate` para recuperar os certificados públicos para qualquer um dos aplicativos Adobe de sua organização.

**Formato da API**

```http
GET /v1/certificate/public-certificate
```

Os parâmetros de consulta opcionais a seguir podem ser usados ao recuperar seus certificados públicos.

| Parâmetros de consulta | Descrição | Exemplo |
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

## Automação do ciclo de vida do certificado {#certificate-lifecycle-automation}

A Adobe automatiza o ciclo de vida de certificados mTLS públicos para garantir a continuidade e reduzir as interrupções do serviço.

- Os certificados são reemitidos 60 dias antes da expiração.
- Os certificados são revogados 30 dias antes da expiração.

>[!NOTE]
>
>Essas linhas do tempo serão encurtadas ao longo do tempo em alinhamento com as [diretrizes do Fórum CA/B](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days), que visam reduzir a duração dos certificados para no máximo 47 dias.

Você deve atualizar suas integrações para oferecer suporte à recuperação automatizada por meio da API. Não se baseie em downloads manuais de certificados ou cópias estáticas, pois podem resultar em certificados expirados ou revogados.

## Próximas etapas

Depois de recuperar os certificados públicos usando a API, atualize as integrações para chamar regularmente este endpoint antes que os certificados expirem. Para testar esta chamada interativamente, visite a [página de referência da API do MTLS](https://developer.adobe.com/experience-platform-apis/references/mtls-service/). Adobe Experience Platform Para obter orientação mais ampla sobre integrações baseadas em certificados, consulte a [Visão geral sobre criptografia de dados](../../landing/governance-privacy-security/encryption.md) ou a [Visão geral sobre governança de dados](../home.md).
