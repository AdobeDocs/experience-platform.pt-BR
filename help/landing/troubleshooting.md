---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia de solução de problemas e perguntas frequentes do Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: 9eeddfaf3e704d66b81f983afcdf5ef3c45c6075
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 2%

---


# [!DNL Platform] Perguntas frequentes e guia de solução de problemas

Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform, bem como um guia de solução de problemas de alto nível para erros comuns que podem ser encontrados em qualquer [!DNL Experience Platform] API. Para obter guias de solução de problemas em [!DNL Platform] serviços individuais, consulte o diretório [de solução de problemas de](#service-troubleshooting-directory) serviço abaixo.

## Perguntas frequentes {#faq}

Veja a seguir uma lista de respostas para perguntas frequentes sobre o Adobe Experience Platform.

## O que são [!DNL Experience Platform] APIs? {#what-are-experience-platform-apis}

[!DNL Experience Platform] oferta várias RESTful APIs que usam solicitações HTTP para acessar [!DNL Platform] recursos. Essas APIs de serviço expõem vários pontos de extremidade e permitem que você execute operações para recursos de lista (GET), pesquisa (GET), edição (PUT e/ou PATCH) e exclusão (DELETE). Para obter mais informações sobre endpoints e operações específicos disponíveis para cada serviço, consulte a documentação [de Referência da](https://www.adobe.io/apis/experienceplatform/home/api-reference.html) API em E/S da Adobe.

## Como formatar uma solicitação de API? {#how-do-i-format-an-api-request}

Os formatos de solicitação variam dependendo da [!DNL Platform] API que está sendo usada. A melhor maneira de aprender como estruturar suas chamadas de API é seguindo os exemplos fornecidos na documentação do [!DNL Platform] serviço específico que você está usando.

### Lendo chamadas de exemplo da API

A documentação para [!DNL Experience Platform] mostra exemplos de chamadas de API de duas maneiras diferentes. Primeiro, a chamada é apresentada em seu formato **de** API, uma representação de modelo mostrando somente a operação (GET, POST, PUT, PATCH, DELETE) e o ponto de extremidade que está sendo usado (por exemplo, `/global/classes`). Alguns modelos também mostram a localização das variáveis para ajudar a ilustrar como uma chamada deve ser formulada, como `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

As chamadas são então mostradas como comandos cURL em uma **solicitação**, o que inclui os cabeçalhos necessários e o &quot;caminho base&quot; completo necessário para interagir com a API com êxito. O caminho base deve ser pré-aberto para todos os pontos finais. Por exemplo, o `/global/classes` endpoint mencionado é `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Você verá o formato da API/padrão de solicitação em toda a documentação e deverá usar o caminho completo mostrado no exemplo de Solicitação ao fazer suas próprias chamadas para APIs da Platform.

### Exemplo de solicitação de API

A seguir, há um exemplo de solicitação de API que demonstra o formato que você encontrará na documentação.

**Formato da API**

O formato da API mostra a operação (GET) e o ponto de extremidade que está sendo usado. As variáveis são indicadas por chaves (nesse caso, `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Solicitação**

Neste exemplo de solicitação, as variáveis do formato de API recebem valores reais no caminho da solicitação. Todos os cabeçalhos obrigatórios também são mostrados, assim como exemplos de valores de cabeçalho ou variáveis nas quais informações confidenciais (como tokens de segurança e IDs de acesso) devem ser incluídas.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta ilustra o que você esperaria receber após uma chamada bem-sucedida para a API, com base na solicitação que foi enviada. Ocasionalmente, a resposta fica truncada para o espaço, o que significa que você pode ver mais informações ou informações adicionais para aquelas exibidas na amostra.

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

Para obter mais informações sobre endpoints específicos nas APIs da Platform, incluindo cabeçalhos obrigatórios e corpos de solicitação, consulte a documentação [de Referência da](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)API.

## Qual é a minha organização IMS? {#what-is-my-ims-organization}

Uma organização IMS é uma representação da Adobe de um cliente. Todas as soluções licenciadas da Adobe são integradas a essa organização de clientes. Quando uma organização IMS tem direito a [!DNL Experience Platform], ela pode atribuir acesso a desenvolvedores. A ID de organização IMS (`x-gw-ims-org-id`) representa a organização para a qual uma chamada de API deve ser executada e, portanto, é necessária como um cabeçalho em todas as solicitações de API. Essa ID pode ser encontrada no [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui): na guia **Integrações** , navegue até a seção **Visão geral** de qualquer integração específica para localizar a ID em Credenciais **do** cliente. Para obter uma apresentação passo a passo sobre como autenticar em [!DNL Platform], consulte o tutorial [de](../tutorials/authentication.md)autenticação.

## Onde posso encontrar minha chave de API? {#where-can-i-find-my-api-key}

Uma chave de API é necessária como um cabeçalho em todas as solicitações de API. Ele pode ser encontrado por meio do [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). No console, na guia **Integrações** , navegue até a seção **Visão geral** de uma integração específica e você encontrará a chave em Credenciais **** do cliente. Para obter uma apresentação passo a passo sobre como autenticar em [!DNL Platform], consulte o tutorial [de](../tutorials/authentication.md)autenticação.

## Como faço para obter um token de acesso? {#how-do-i-get-an-access-token}

Tokens de acesso são necessários no cabeçalho de autorização de todas as chamadas de API. Eles podem ser gerados usando um `curl` comando, desde que você tenha acesso a uma integração para uma organização IMS. Os Tokens de acesso só são válidos por 24 horas, após o que um novo token deve ser gerado para continuar usando a API. Para obter detalhes sobre a geração de tokens de acesso, consulte o tutorial [de](../tutorials/authentication.md)autenticação.

## Como usar parâmetros de query? {#how-do-i-user-query-parameters}

Alguns pontos de extremidade [!DNL Platform] da API aceitam parâmetros de query para localizar informações específicas e filtrar os resultados retornados na resposta. Os parâmetros de Query são anexados a caminhos de solicitação com um símbolo de ponto de interrogação (`?`), seguido por um ou mais parâmetros de query usando o formato `paramName=paramValue`. Ao combinar vários parâmetros em uma única chamada, você deve usar um E comercial (`&`) para separar os parâmetros individuais. O exemplo a seguir demonstra como uma solicitação que usa vários parâmetros de query é representada na documentação.

Exemplos de parâmetros de query usados com frequência incluem:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Para obter informações detalhadas sobre quais parâmetros de query estão disponíveis para um serviço ou terminal específico, consulte a documentação específica do serviço.

## Como indicar um campo JSON para atualizar em uma solicitação PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Muitas operações PATCH em [!DNL Platform] APIs usam strings de ponteiro [JSON](https://tools.ietf.org/html/rfc6901) para indicar propriedades JSON a serem atualizadas. Normalmente, eles são incluídos nas cargas de solicitação usando o formato Patch [](https://tools.ietf.org/html/rfc6902) JSON. Consulte o guia [de fundamentos da](api-fundamentals.md) API para obter informações detalhadas sobre a sintaxe necessária para essas tecnologias.

## Posso usar o Postman para fazer chamadas para [!DNL Platform] APIs? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[O Postman](https://www.postman.com/) é uma ferramenta útil para visualizar chamadas para RESTful APIs. Esta publicação [](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) Média descreve como você pode configurar o Postman para executar automaticamente a autenticação e usá-la para consumir [!DNL Experience Platform] APIs.

## Quais são os requisitos do sistema para [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Dependendo de se você estiver usando a interface do usuário ou a API, os seguintes requisitos de sistema se aplicam:

**Para operações baseadas na interface do usuário:**
- Um navegador da Web moderno e padrão. Embora a versão mais recente do [!DNL Chrome] seja recomendada, as principais versões atuais e anteriores do [!DNL Firefox], [!DNL Internet Explorer]e do Safari também são suportadas.
   - Cada vez que uma nova versão principal é lançada, [!DNL Platform] os start que suportam a versão mais recente são descartados enquanto o suporte para a terceira versão mais recente é descartado.
- Todos os navegadores devem ter cookies e JavaScript ativado.

**Para interações de API e desenvolvedor:**
- Um ambiente de desenvolvimento para desenvolver integrações REST, streaming e Webhook.

## Erros e solução de problemas {#errors-and-troubleshooting}

A seguir está uma lista de erros que podem ocorrer ao usar qualquer [!DNL Experience Platform] serviço. Para obter guias de solução de problemas em [!DNL Platform] serviços individuais, consulte o diretório [de solução de problemas de](#service-troubleshooting-directory) serviço abaixo.

## Códigos de status da API {#api-status-codes}

Os seguintes códigos de status podem ser encontrados em qualquer [!DNL Experience Platform] API. Cada uma tem várias causas, pelo que as explicações apresentadas nesta seção são de natureza geral. Para obter mais detalhes sobre erros específicos em [!DNL Platform] serviços individuais, consulte o diretório [de solução de problemas de](#service-troubleshooting-directory) serviço abaixo.

| Código de status | Descrição | Causas possíveis |
--- | --- | ---
| 400 | Solicitação incorreta | A solicitação foi construída incorretamente, faltavam informações importantes e/ou continha sintaxe incorreta. |
| 401 | Falha na autenticação | A solicitação não passou em uma verificação de autenticação. Seu token de acesso pode estar ausente ou ser inválido. Consulte a seção [OAuth token errors](#oauth-token-is-missing) abaixo para obter mais detalhes. |
| 403 | Proibido | O recurso foi encontrado, mas você não tem as credenciais certas para visualização-lo. |
| 404 | Não encontrado | Não foi possível localizar o recurso solicitado no servidor. O recurso pode ter sido excluído ou o caminho solicitado foi inserido incorretamente. |
| 500 | Erro interno do servidor | Este é um erro do lado do servidor. Se você estiver fazendo muitas chamadas simultâneas, pode estar atingindo o limite da API e precisar filtrar seus resultados. (Consulte o subguia do guia do desenvolvedor da [!DNL Catalog Service] API sobre [filtragem de dados](../catalog/api/filter-data.md) para saber mais.) Aguarde um momento antes de tentar novamente sua solicitação e entre em contato com o administrador se o problema persistir. |

## Erros de cabeçalho de solicitação {#request-header-errors}

Todas as chamadas de API em [!DNL Platform] exigem cabeçalhos de solicitação específicos. Para ver quais cabeçalhos são necessários para serviços individuais, consulte a documentação [de Referência da](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)API. Para localizar os valores dos cabeçalhos de autenticação necessários, consulte o tutorial [](../tutorials/authentication.md)Autenticação. Se algum desses cabeçalhos estiver ausente ou for inválido ao fazer uma chamada de API, os seguintes erros podem ocorrer.

### O token OAuth está ausente {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Esta mensagem de erro é exibida quando um `Authorization` cabeçalho está ausente de uma solicitação de API. Certifique-se de que o cabeçalho de Autorização esteja incluído com um token de acesso válido antes de tentar novamente.

### O token OAuth não é válido

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Esta mensagem de erro é exibida quando o token de acesso fornecido no cabeçalho não é válido. `Authorization` Verifique se o token foi inserido corretamente ou [gere um novo token](../tutorials/authentication.md) no Console de E/S da Adobe.

### A chave da API é obrigatória

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Esta mensagem de erro é exibida quando um cabeçalho de chave da API (`x-api-key`) está ausente de uma solicitação de API. Certifique-se de que o cabeçalho esteja incluído com uma chave de API válida antes de tentar novamente.

### A chave da API é inválida

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Esta mensagem de erro é exibida quando o valor do cabeçalho da chave da API (`x-api-key`) fornecido é inválido. Verifique se você inseriu a chave corretamente antes de tentar novamente. Se você não souber sua chave de API, poderá encontrá-la no Console [de E/S da](https://console.adobe.io)Adobe: na guia **Integrações** , navegue até a seção **Visão geral** de uma integração específica para localizar a chave da API em Credenciais **do** cliente.


### Cabeçalho ausente

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Esta mensagem de erro é exibida quando um cabeçalho organizacional IMS (`x-gw-ims-org-id`) está ausente de uma solicitação de API. Certifique-se de que o cabeçalho esteja incluído na ID da organização IMS antes de tentar novamente.

### Perfil inválido

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Essa mensagem de erro é exibida quando a integração de E/S do usuário ou Adobe (identificada pelo [token de acesso](#how-do-i-get-an-access-token) no cabeçalho `Authorization` ) não tem direito a fazer chamadas para [!DNL Experience Platform] APIs para a Organização IMS fornecida no `x-gw-ims-org-id` cabeçalho. Verifique se você forneceu a ID correta para sua organização IMS no cabeçalho antes de tentar novamente. Se você não souber a ID da organização, poderá encontrá-la no Console [de E/S da](https://console.adobe.io)Adobe: na guia **Integrações** , navegue até a seção **Visão geral** de uma integração específica para localizar a ID em Credenciais **do** cliente.

### Tipo de conteúdo válido não especificado

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Esta mensagem de erro é exibida quando uma solicitação POST, PUT ou PATCH tem um cabeçalho inválido ou ausente `Content-Type` . Certifique-se de que o cabeçalho esteja incluído na solicitação e que seu valor esteja `application/json`.


## Diretório de solução de problemas de serviço {#service-troubleshooting-directory}

A seguir está uma lista de guias de solução de problemas e documentação de referência da API para [!DNL Experience Platform] APIs. Cada guia de solução de problemas fornece respostas a perguntas frequentes e soluções para problemas específicos a [!DNL Platform] serviços individuais. Os documentos de referência da API fornecem um guia abrangente para todos os pontos de extremidade disponíveis para cada serviço e mostram exemplos de corpos de solicitação, respostas e códigos de erro que você pode receber.

| Serviço de | Referência da API | Solução de problemas |
--- | --- | ---
| Controle de acesso | [API do Controle de acesso](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Guia de solução de problemas do Controle de acesso](../access-control/troubleshooting-guide.md) |
| Catálogo | [API de Serviço de Catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| Ingestão de dados (lote) | [API de ingestão de dados](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guia de solução de problemas de ingestão em lote](../ingestion/batch-ingestion/troubleshooting.md) |
| Ingestão de dados (Streaming) | [API de ingestão de dados](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guia de solução de problemas de ingestão de streaming](../ingestion/streaming-ingestion/troubleshooting.md) |
| Área de trabalho da ciência de dados | [API de aprendizado de máquina do Sensei](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [Guia de solução de problemas da Data Science Workspace](../data-science-workspace/troubleshooting-guide.md) |
| Rotulação e aplicação de uso de dados (DULE) | [API de serviço de política DULE](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Modelo de dados de experiência (XDM) | [API de registro do Schema](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [Perguntas frequentes do sistema XDM e guia de solução de problemas](../xdm/troubleshooting-guide.md) |
| Serviço de identidade | [API do Serviço de Identidade](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [Guia de solução de problemas do Serviço de identidade](../identity-service/troubleshooting-guide.md) |
| Serviço de Query | [API de serviço de Query](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [Guia de solução de problemas do Serviço de Query](../query-service/troubleshooting-guide.md) |
| Perfil do cliente em tempo real | [API de Perfil do cliente em tempo real](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [Guia de solução de problemas do Perfil](../profile/troubleshooting.md) |
| Sandboxes | [API do Sandbox](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Guia de solução de problemas de caixas de proteção](../sandboxes/troubleshooting-guide.md) |
| Segmentação | [API de segmentação](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |