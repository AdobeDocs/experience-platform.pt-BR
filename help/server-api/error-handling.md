---
title: Tratamento de erros
description: Saiba mais sobre os possíveis erros que você pode encontrar ao executar solicitações de API para a API do servidor da rede de borda do Adobe Experience Platform.
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 3%

---

# Tratamento de erros

## Visão geral {#overview}

Os erros de API na API do servidor da rede de borda da Adobe Experience Platform podem ter várias causas, internas (rede de borda em si) ou externas (relacionadas a entrada, configuração ou upstream).

## Tipos de erro {#error-types}

| Erro | Tipo | Descrição | Código de status |
| --- | --- | --- | --- |
| `RequestProcessingError` | Interno | Erro de uso geral emitido pela Adobe Experience Platform Edge Network em circunstâncias inesperadas. | `500` |
| `InputError` | Externo | Inclui erros causados por entrada malformada, bem como erros de validação de entidade. | `4xx` |
| `ConfigurationError` | Externo | Erros de configuração do lado do servidor. | `422` |
| `UpstreamError` | Externo | Erros de comunicação com serviços upstream. | `207 Multi-Status` |

## Severidade

Os erros da API do servidor também podem ser divididos por gravidade:

* **Erros fatais** interromperá o pipeline de expedição.
* **Erros não fatais** O poderia sinalizar um processamento parcial, permitindo que o processamento de solicitações continuasse.
   * Quando presente, o código de status geral da solicitação será alterado para `207 Multi-Status`.

| Erro | Tipo | Observações |
| --- | --- | --- |
| `RequestProcessingError` | Fatal | Pode ocorrer a qualquer momento durante o processamento da solicitação. |
| `InputError` | Fatal | Ocorre ao aceitar a solicitação, antes de despachá-la upstream. |
| `ConfigurationError` | Fatal | Ocorre ao aceitar a solicitação, antes de despachá-la upstream. |
| `UpstreamError` | Não Fatal | Erros de comunicação com serviços upstream. |

### Erros fatais {#fatal-errors}

Erros fatais interrompem o processamento de solicitações e fazem com que um status de resposta não 2xx seja retornado. Confira o [tipos de erro](#error-types) para ver o código de status esperado, correspondente a cada tipo de erro.

Os erros serão acompanhados por um corpo de resposta contendo um objeto de erro. Nesse caso, o corpo da resposta contém um detalhe do problema, conforme definido por [RFC 7807 Detalhes do problema para APIs HTTP](https://tools.ietf.org/html/rfc7807).

O tipo de conteúdo retornado é o `application/problem+json` tipo de mídia. Quando presente, essa resposta contém detalhes legíveis por máquina relacionados ao erro. Os detalhes do problema incluem um tipo de URI.

Todos os objetos com erro têm um `type`, `status`, `title`, `detail` e `report` para que o cliente da API possa informar qual é o problema.

| Propriedade | Tipo | Descrição |
| -------- | ------ | ----------- |
| `type` | String | Uma referência de URI (RFC3986) que identifica o tipo de problema, seguindo o formato `https://ns.adobe.com/aep/errors/<ERROR-CODE>`. |
| `status` | Número | O código do status HTTP gerado pelo servidor para esta ocorrência do problema. |
| `title` | String | Um resumo curto e em formato legível por humanos do tipo de problema. |
| `detail` | String | Uma descrição curta e legível do tipo de problema. |
| `report` | Objeto | Um mapa de propriedades adicionais que ajudam na depuração, como a ID da solicitação ou a ID da organização. Em alguns casos, ela pode conter dados específicos para o erro em questão, como uma lista de erros de validação. |

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

Os erros não fatais podem ser ainda divididos em:

* Erros: problemas que ocorreram ao processar a solicitação, mas não fizeram com que toda a solicitação fosse rejeitada (por exemplo, uma falha de upstream não crítica).
* Avisos: mensagens de serviços upstream que poderiam sinalizar que ocorreu um processamento parcial da solicitação.

Ao encontrar erros não fatais (excluindo avisos), a variável [!DNL Server API] mudará o status da resposta para `207 Multi-Status`.

Por outro lado, os avisos são na sua maioria informativos, uma vez que representam geralmente uma condição potencialmente transitória, que não afetou totalmente o pedido. Um exemplo aqui é uma leitura parcial de perfil no mecanismo de segmentação, nesse caso, a precisão é afetada em algum grau, mas a funcionalidade ainda é fornecida.

Os erros não fatais são representados na variável _Detalhes do problema_ mas são incorporados diretamente na resposta padrão do gateway do Edge, que é do tipo `application/json`.

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
| `4xx Bad Request` | Mais `4xx` erros, como 400, 403, 404, não devem ser repetidos em nome do cliente, exceto por `429`. Esses são erros do cliente e não terão êxito. O cliente deve corrigir o erro antes de tentar novamente a solicitação. |
| `429 Too Many Requests` | `429` O código de resposta HTTP indica que a Rede de borda da Adobe Experience Platform ou um serviço upstream está limitando a taxa de solicitações. Nesse caso, o chamador deve respeitar a variável `Retry-After` cabeçalho de resposta. Qualquer resposta que flua de volta deve ter o código de resposta HTTP com um código de erro específico de domínio. |
| `500 Internal Server Error` | `500` os erros são genéricos, erros &quot;catch-all&quot;. `500` os erros não devem ser repetidos, exceto por `502` e `503`. Os intermediários devem `500` e pode responder com uma mensagem/código de erro genérico ou uma mensagem/código de erro mais específico do domínio. |
| `502 Bad Gateway` | Indica que a Rede de Borda da Adobe Experience Platform recebeu uma resposta inválida dos servidores upstream. Isso pode ocorrer devido a problemas de rede entre servidores. O problema de rede temporário pode ser resolvido e, portanto, uma nova tentativa pode resolver o problema. Portanto, os destinatários de `502` erros podem repetir a solicitação depois de algum tempo. |
| `503 Service Unavailable` | Este código de erro indica que o serviço está temporariamente indisponível. Isso pode ocorrer durante os períodos de manutenção. Destinatários de `503` podem repetir a solicitação, mas devem respeitar as `Retry-After` cabeçalho. |
| `504 Gateway Timeout` | Indica que a solicitação da Rede de borda da Adobe Experience Platform para os servidores upstream atingiu o tempo limite. Isso pode ocorrer devido a problemas de rede entre servidores, problemas de DNS ou outros problemas de rede. Os problemas temporários da rede podem ser resolvidos depois de algum tempo e uma nova tentativa pode resolver o problema. |
