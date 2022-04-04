---
title: Tratamento de erros
description: Saiba mais sobre os possíveis erros que você pode encontrar ao executar solicitações de API para a API do servidor de rede de borda do Adobe Experience Platform.
seo-description: Learn about the possible errors you might encounter when performing API requests to the Adobe Experience Platform Edge Network Server API.
keywords: erro; código; manuseio; borda; rede; gateway; api
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 3%

---

# Tratamento de erros

## Visão geral {#overview}

Os erros de API na API do Servidor de Rede de Borda do Adobe Experience Platform podem ter várias causas, internas (própria Rede de Borda) ou externas (entrada, configuração ou relacionadas a upstream).

## Tipos de erro {#error-types}

| Erro | Tipo | Descrição | Código de status |
| --- | --- | --- | --- |
| `RequestProcessingError` | Interno | Erro de propósito geral emitido pela Rede de borda do Adobe Experience Platform em circunstâncias inesperadas. | `500` |
| `InputError` | Externo | Inclui erros causados por entrada malformada, bem como erros de validação de entidade. | `4xx` |
| `ConfigurationError` | Externo | Erros de configuração do lado do servidor. | `422` |
| `UpstreamError` | Externo | Erros de comunicação com serviços upstream. | `207 Multi-Status` |

## Gravidade

Os erros da API do servidor também podem ser divididos por gravidade:

* **Erros fatais** interromperá o pipeline de despacho.
* **Erros não fatais** O pode sinalizar um processamento parcial, permitindo que o processamento da solicitação continue.
   * Quando presente, o código de status geral da solicitação será alterado para `207 Multi-Status`.

| Erro | Tipo | Observações |
| --- | --- | --- |
| `RequestProcessingError` | Fatal | Pode ocorrer em qualquer ponto durante o processamento da solicitação. |
| `InputError` | Fatal | Ocorre ao aceitar a solicitação, antes de enviá-la para upstream. |
| `ConfigurationError` | Fatal | Ocorre ao aceitar a solicitação, antes de enviá-la para upstream. |
| `UpstreamError` | Não fatal | Erros de comunicação com serviços upstream. |

### Erros fatais {#fatal-errors}

Erros fatais interrompem o processamento da solicitação e fazem com que um status de resposta não 2xx seja retornado. Confira o [tipos de erro](#error-types) para ver o código de status esperado, correspondente a cada tipo de erro.

Os erros serão acompanhados por um corpo de resposta contendo um objeto de erro. Nesse caso, o corpo da resposta contém um detalhe do problema, conforme definido por [Detalhes do problema RFC 7807 para APIs HTTP](https://tools.ietf.org/html/rfc7807).

O tipo de conteúdo retornado é a variável `application/problem+json` tipo de mídia. Quando presente, essa resposta contém detalhes legíveis por máquina relacionados ao erro. Os detalhes do problema incluem um tipo de URI.

Todos os objetos de erro têm uma `type`, `status`, `title`, `detail` e `report` propriedades da mensagem para que o cliente da API possa saber qual é o problema.

| Propriedade | Tipo | Descrição |
| -------- | ------ | ----------- |
| `type` | String | Uma referência de URI (RFC3986) que identifica o tipo de problema, seguindo o formato `https://ns.adobe.com/aep/errors/<ERROR-CODE>`. |
| `status` | Número | O código de status HTTP gerado pelo servidor para essa ocorrência do problema. |
| `title` | String | Um resumo breve e legível por humanos do tipo de problema. |
| `detail` | String | Uma breve descrição legível por humanos do tipo de problema. |
| `report` | Objeto | Um mapa de propriedades adicionais que auxilia na depuração, como a ID da solicitação ou a ID da organização. Em alguns casos, pode conter dados específicos para o erro em questão, como uma lista de erros de validação. |

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0104-422",
   "status":422,
   "title":"Unprocessable entity",
   "detail":"Invalid request (report attached). Please check your input and try again.",
   "report":{
      "errors":[
         "Allowed Adobe version is 1.0 for standard 'Adobe' at index 0",
         "Allowed IAB version is 2.0 for standard 'IAB TCF' at index 1",
         "IAB consent string value must not be empty for standard 'IAB TCF' at index 1"
      ],
      "requestId":"0f8821e5-ed1a-4301-b445-5f336fb50ee8",
      "orgId":"53A16ACB5CC1D3760A495C99@AdobeOrg"
   }
}
```

### Erros não fatais {#non-fatal-errors}

Os erros não fatais podem ser divididos em:

* Erros: Problemas que ocorreram ao processar a solicitação, mas não fizeram com que toda a solicitação fosse rejeitada (por exemplo, uma falha não crítica de upstream).
* Avisos: Mensagens de serviços upstream que poderiam sinalizar que ocorreu um processamento parcial da solicitação.

Ao encontrar erros não fatais (excluindo avisos), a variável [!DNL Server API] alterará o status da resposta para `207 Multi-Status`.

Os avisos, por outro lado, são na sua maioria informativos, uma vez que geralmente representam uma condição potencialmente transitória, que não afetou totalmente a solicitação. Um exemplo aqui é um perfil parcial lido no mecanismo de segmentação, nesse caso a precisão é afetada até certo ponto, mas a funcionalidade ainda é oferecida.

Erros não fatais são representados na variável _Detalhes do problema_ , mas são incorporados diretamente na resposta padrão do gateway do Edge, que é do tipo `application/json`.

```json
{
  "requestId": "72eaa048-207e-4dde-bf16-0cb2b21336d5",
  "handle": [
  ],
  "errors": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0201-503",
      "status": 503,
      "title": "The 'com.adobe.experience.platform.ode' service is temporarily unable to serve this request. Please try again later."
    }
  ],
  "warnings": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0204-200",
      "status": 200,
      "title": "A warning occurred while calling the 'com.adobe.audiencemanager' service for this request.",
      "report": {
        "cause": {
          "message": "Cannot read related customer for device id: ...",
          "code": 202
        }
      }
    }
  ]
}
```

## Manuseio `4xx` e `5xx` Respostas


| Código de erro | Descrição |
|---|---|
| `4xx Bad Request` | Mais `4xx` erros, como 400, 403, 404, não devem ser repetidos em nome do cliente, exceto por `429`. Esses são erros de cliente e não terão êxito. O cliente deve corrigir o erro antes de tentar novamente a solicitação. |
| `429 Too Many Requests` | `429` O código de resposta HTTP indica que a rede de borda da Adobe Experience Platform ou um serviço upstream está limitando a taxa de solicitações. Nesse caso, o chamador deve respeitar o `Retry-After` cabeçalho de resposta. Qualquer resposta que retorne deve ter o código de resposta HTTP com um código de erro específico de domínio. |
| `500 Internal Server Error` | `500` são erros genéricos e catch-all . `500` os erros não devem ser repetidos, exceto para `502` e `503`. Os intermediários devem responder com uma `500` e pode responder com um código/mensagem de erro genérico ou um código/mensagem de erro mais específico do domínio. |
| `502 Bad Gateway` | Indica que a Rede de Borda da Adobe Experience Platform recebeu uma resposta inválida de servidores upstream. Isso pode ocorrer devido a problemas de rede entre servidores. O problema temporário de rede pode ser resolvido e, portanto, uma nova tentativa pode resolver o problema, de modo que os recipients do `502` erros podem repetir a solicitação após algum tempo. |
| `503 Service Unavailable` | Este código de erro indica que o serviço está temporariamente indisponível. Isso pode acontecer durante os períodos de manutenção. Recipients de `503` erros podem repetir a solicitação, mas devem respeitar a variável `Retry-After` cabeçalho. |
| `504 Gateway Timeout` | Indica que a solicitação da Rede de borda da Adobe Experience Platform para os servidores de upstream atingiu o tempo limite. Isso pode ocorrer devido a problemas de rede entre servidores, problemas de DNS ou outros problemas de rede. Os problemas temporários de rede podem ser resolvidos após algum tempo e uma nova tentativa pode resolver o problema. |
