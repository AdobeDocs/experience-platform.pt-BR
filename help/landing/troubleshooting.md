---
keywords: Experience Platform;página inicial;tópicos populares;códigos de erro de API;código de erro de API;código de erro API;códigos de erro API;erro de solicitação de API;solução de problemas de API;erro de API
solution: Experience Platform
title: Perguntas frequentes sobre o Adobe Experience Platform e Guia de solução de problemas
description: Encontre respostas para perguntas frequentes e um guia para solucionar erros comuns na Adobe Experience Platform.
landing-page-description: Encontre respostas para perguntas frequentes e um guia para solucionar erros comuns na Adobe Experience Platform.
short-description: Encontre respostas para perguntas frequentes e um guia para solucionar erros comuns na Experience Platform.
type: Documentation
role: Developer
feature: API, Audiences, Data Ingestion, Datasets, Destinations, Privacy, Queries, Schemas, Sandboxes, Sources
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 4%

---

# Guia de solução de problemas e perguntas frequentes do [!DNL Experience Platform]

Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform, bem como um guia de solução de problemas de alto nível para erros comuns que podem ser encontrados em qualquer API do [!DNL Experience Platform]. Para obter guias de solução de problemas sobre serviços [!DNL Experience Platform] individuais, consulte o [diretório de solução de problemas de serviço](#service-troubleshooting-directory) abaixo.

## Perguntas frequentes {#faq}

Veja a seguir uma lista de respostas para perguntas frequentes sobre o Adobe Experience Platform.

## O que são [!DNL Experience Platform] APIs? {#what-are-experience-platform-apis}

[!DNL Experience Platform] oferece várias APIs RESTful que usam solicitações HTTP para acessar recursos [!DNL Experience Platform]. Cada uma dessas APIs de serviço expõe vários endpoints e permite executar operações para listar (GET), pesquisar (GET), editar (PUT e/ou PATCH) e excluir (DELETE) recursos. Para obter mais informações sobre endpoints e operações específicos disponíveis para cada serviço, consulte a [documentação de Referência da API](https://www.adobe.com/go/platform-api-reference-en) no Adobe I/O.

## Como formatar uma solicitação de API? {#how-do-i-format-an-api-request}

Os formatos de solicitação variam dependendo da API [!DNL Experience Platform] que está sendo usada. A melhor maneira de saber como estruturar suas chamadas de API é seguindo os exemplos fornecidos na documentação do serviço [!DNL Experience Platform] específico que você está usando.

Para obter mais informações sobre como formatar solicitações de API, consulte a seção Guia de introdução à API do Experience Platform [lendo chamadas de API de exemplo](./api-guide.md#sample-api).

## Qual é minha organização? {#what-is-my-ims-organization}

Uma organização é uma representação da Adobe de um cliente. Todas as soluções licenciadas da Adobe são integradas a essa organização do cliente. Quando uma organização tem direito a [!DNL Experience Platform], ela pode atribuir acesso aos desenvolvedores. A ID de organização (`x-gw-ims-org-id`) representa a organização para a qual uma chamada de API deve ser executada e, portanto, é necessária como um cabeçalho em todas as solicitações de API. Esta ID pode ser encontrada por meio da [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui): na guia **Integrações**, navegue até a seção **Visão geral** de qualquer integração específica para encontrar a ID em **Credenciais de Cliente**. Para obter uma apresentação passo a passo de como autenticar no [!DNL Experience Platform], consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

## Onde encontro minha chave de API? {#where-can-i-find-my-api-key}

Uma chave de API é necessária como cabeçalho em todas as solicitações de API. Ele pode ser encontrado por meio da [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). No console, na guia **Integrações**, navegue até a seção **Visão geral** de uma integração específica e você encontrará a chave em **Credenciais do Cliente**. Para obter uma apresentação passo a passo de como autenticar no [!DNL Experience Platform], consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

## Como obter um token de acesso? {#how-do-i-get-an-access-token}

Os tokens de acesso são necessários no cabeçalho de Autorização de todas as chamadas de API. Elas podem ser geradas usando um comando CURL, desde que você tenha acesso a uma integração para uma organização. Os tokens de acesso são válidos somente por 24 horas, após as quais um novo token deve ser gerado para continuar usando a API. Para obter detalhes sobre a geração de tokens de acesso, consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

## Como usar parâmetros de consulta? {#how-do-i-user-query-parameters}

Alguns pontos de extremidade de API [!DNL Experience Platform] aceitam parâmetros de consulta para localizar informações específicas e filtrar os resultados retornados na resposta. Os parâmetros de consulta são anexados a caminhos de solicitação com um símbolo de ponto de interrogação (`?`), seguido por um ou mais parâmetros de consulta usando o formato `paramName=paramValue`. Ao combinar vários parâmetros em uma única chamada, você deve usar um E comercial (`&`) para separar parâmetros individuais. O exemplo a seguir demonstra como uma solicitação que usa vários parâmetros de consulta é representada na documentação.

Exemplos de parâmetros de consulta comumente usados incluem:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Para obter informações detalhadas sobre quais parâmetros de consulta estão disponíveis para um serviço ou endpoint específico, consulte a documentação específica do serviço.

## Como indicar um campo JSON para atualizar em uma solicitação PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Muitas operações do PATCH nas APIs [!DNL Experience Platform] usam cadeias de caracteres [JSON Pointer](https://tools.ietf.org/html/rfc6901) para indicar propriedades JSON a serem atualizadas. Normalmente, eles são incluídos em cargas de solicitação usando o formato [Patch JSON](https://tools.ietf.org/html/rfc6902). Consulte o [guia de fundamentos de API](api-fundamentals.md) para obter informações detalhadas sobre a sintaxe necessária para essas tecnologias.

## Posso usar o Postman para fazer chamadas para APIs do [!DNL Experience Platform]? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

O [Postman](https://www.postman.com/) é uma ferramenta útil para visualizar chamadas para APIs RESTful. O [guia de introdução à API do Experience Platform](api-guide.md) contém um vídeo e instruções para importar coleções do Postman. Além disso, é fornecida uma lista de coleções do Postman para cada serviço.

## Quais são os requisitos de sistema para o [!DNL Experience Platform]? {#what-are-the-system-requirements-for-platform}

Dependendo de você estar usando a interface do usuário ou a API, os seguintes requisitos de sistema se aplicam:

**Para operações baseadas na interface do usuário:**

- Um navegador da Web moderno e padrão. Embora a versão mais recente do [!DNL Chrome] seja recomendada, versões principais atuais e anteriores do [!DNL Firefox], [!DNL Internet Explorer] e Safari também são compatíveis.

   - Cada vez que uma nova versão principal é lançada, o [!DNL Experience Platform] começa a oferecer suporte à versão mais recente enquanto o suporte à terceira versão mais recente é descartado.

- Todos os navegadores devem ter os cookies e o JavaScript ativados.

**Para API e interações de desenvolvedor:**

- Um ambiente de desenvolvimento para desenvolver integrações REST, streaming e Webhook.

## Erros e solução de problemas {#errors-and-troubleshooting}

Esta é uma lista de erros que você pode encontrar ao usar qualquer serviço [!DNL Experience Platform]. Para obter guias de solução de problemas sobre serviços [!DNL Experience Platform] individuais, consulte o [diretório de solução de problemas de serviço](#service-troubleshooting-directory) abaixo.

## Códigos de status da API {#api-status-codes}

Os códigos de status a seguir podem ser encontrados em qualquer API [!DNL Experience Platform]. Cada um tem uma variedade de causas, portanto, as explicações fornecidas nesta seção são de natureza geral. Para obter mais detalhes sobre erros específicos em serviços individuais [!DNL Experience Platform], consulte o [diretório de solução de problemas de serviço](#service-troubleshooting-directory) abaixo.

| Código de status | Descrição | Possíveis causas |
|--- | --- | ---|
| 400 | Solicitação inválida | A solicitação foi construída incorretamente, informações de chave ausentes e/ou continha sintaxe incorreta. |
| 401 | Falha na autenticação | A solicitação não passou em uma verificação de autenticação. Seu token de acesso pode estar ausente ou ser inválido. Consulte a seção [Erros de token OAuth](#oauth-token-is-missing) abaixo para obter mais detalhes. |
| 403 | Proibido | O recurso foi encontrado, mas você não tem as credenciais corretas para exibi-lo. <br> Uma causa provável desse erro é que talvez você não tenha as [permissões de controle de acesso](/help/access-control/home.md) necessárias para acessar ou editar o recurso. Leia como [obter as permissões de controle de acesso baseadas em atributos](/help/landing/api-authentication.md#get-abac-permissions) necessárias para usar as APIs do Experience Platform. </p> |
| 404 | Não encontrado | O recurso solicitado não foi encontrado no servidor. O recurso pode ter sido excluído ou o caminho solicitado foi inserido incorretamente. |
| 500 | Erro interno do servidor | Esse é um erro do lado do servidor. Se você estiver fazendo muitas chamadas simultâneas, talvez esteja atingindo o limite da API e precise filtrar seus resultados. (Consulte o subguia do guia do desenvolvedor da API [!DNL Catalog Service] em [filtrando dados](../catalog/api/filter-data.md) para saber mais.) Aguarde um momento antes de tentar sua solicitação novamente e entre em contato com o administrador se o problema persistir. |

## Erros no cabeçalho da solicitação {#request-header-errors}

Todas as chamadas de API em [!DNL Experience Platform] exigem cabeçalhos de solicitação específicos. Para ver quais cabeçalhos são necessários para serviços individuais, consulte a [documentação de Referência da API](https://www.adobe.com/go/platform-api-reference-en). Para localizar os valores dos cabeçalhos de autenticação necessários, consulte o [Tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Se qualquer um desses cabeçalhos estiver ausente ou for inválido ao fazer uma chamada de API, os seguintes erros poderão ocorrer.

### Token OAuth ausente {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Esta mensagem de erro é exibida quando um cabeçalho `Authorization` está ausente em uma solicitação de API. Verifique se o cabeçalho de Autorização está incluído com um token de acesso válido antes de tentar novamente.

### O token OAuth é inválido {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Esta mensagem de erro é exibida quando o token de acesso fornecido no cabeçalho `Authorization` não é válido. Verifique se o token foi inserido corretamente ou [gere um novo token](https://www.adobe.com/go/platform-api-authentication-en) no Console do Adobe I/O.

### A chave de API é obrigatória {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Esta mensagem de erro é exibida quando um cabeçalho de chave de API (`x-api-key`) está ausente em uma solicitação de API. Verifique se o cabeçalho está incluído com uma chave de API válida antes de tentar novamente.

### A chave de API é inválida {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Esta mensagem de erro é exibida quando o valor do cabeçalho da chave de API fornecido (`x-api-key`) é inválido. Verifique se você inseriu a chave corretamente antes de tentar novamente. Se você não souber sua chave de API, poderá encontrá-la no [Console do Adobe I/O](https://console.adobe.io): na guia **Integrações**, navegue até a seção **Visão geral** de uma integração específica para encontrar a chave de API em **Credenciais do cliente**.

### Cabeçalho ausente {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Esta mensagem de erro é exibida quando um cabeçalho de organização (`x-gw-ims-org-id`) está ausente em uma solicitação de API. Verifique se o cabeçalho está incluído com a ID da organização antes de tentar novamente.

### O perfil não é válido {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Esta mensagem de erro é exibida quando o usuário ou a integração do Adobe I/O (identificada pelo [token de acesso](#how-do-i-get-an-access-token) no cabeçalho `Authorization`) não tem direito a fazer chamadas para APIs [!DNL Experience Platform] para a organização fornecida no cabeçalho `x-gw-ims-org-id`. Verifique se você forneceu a ID correta para a organização no cabeçalho antes de tentar novamente. Caso não saiba a ID da organização, é possível encontrá-la no [Console do Adobe I/O](https://console.adobe.io): na guia **Integrações**, navegue até a seção **Visão geral** de uma integração específica para encontrar a ID em **Credenciais do cliente**.

### Erro ao atualizar tag {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

Você pode receber um erro de etag se uma alteração tiver sido feita em qualquer entidade de origem ou destino, como fluxo, conexão, conector de origem ou conexão de destino, por outro chamador de API. Devido à incompatibilidade de versões, a alteração que você está tentando fazer não seria aplicada à versão mais recente da entidade.

Para resolver isso, você precisa buscar a entidade novamente, verificar se suas alterações são compatíveis com a nova versão da entidade, colocar a nova tag no cabeçalho `If-Match` e finalmente fazer a chamada de API.

### Tipo de conteúdo válido não especificado {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Esta mensagem de erro é exibida quando uma solicitação POST, PUT ou PATCH tem um cabeçalho `Content-Type` inválido ou ausente. Verifique se o cabeçalho está incluído na solicitação e se seu valor é `application/json`.

### Região do usuário ausente {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

Essa mensagem de erro é exibida em qualquer um dos casos abaixo:

- Quando um cabeçalho de ID de organização incorreto ou malformado (`x-gw-ims-org-id`) é transmitido em uma solicitação de API. Verifique se a ID correta da organização foi incluída antes de tentar novamente.
- Quando sua conta (conforme representada pelas credenciais de autenticação fornecidas) não está associada a um perfil de produto do Experience Platform. Siga as etapas em [gerar credenciais de acesso](./api-authentication.md#authentication-for-each-session) no tutorial de autenticação da API do Experience Platform para adicionar o Experience Platform à sua conta e atualizar suas credenciais de autenticação adequadamente.

## Diretório de solução de problemas de serviço {#service-troubleshooting-directory}

Veja a seguir uma lista de guias de solução de problemas e a documentação de referência da API para as APIs [!DNL Experience Platform]. Cada guia de solução de problemas fornece respostas a perguntas frequentes e soluções para problemas específicos de serviços individuais do [!DNL Experience Platform]. Os documentos de referência da API fornecem um guia abrangente para todos os endpoints disponíveis para cada serviço e mostram exemplos de corpos de solicitação, respostas e códigos de erro que você pode receber.

| Serviço | Referência da API | Resolução de problemas |
| --- | --- | --- |
| Controle de acesso | [API de controle de acesso](https://www.adobe.io/experience-platform-apis/references/access-control/) | [Guia de solução de problemas de controle de acesso](../access-control/troubleshooting-guide.md) |
| Assimilação de dados Adobe Experience Platform | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [Guia de solução de problemas de assimilação em lote](../ingestion/batch-ingestion/troubleshooting.md) |
| Assimilação de dados Adobe Experience Platform | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [Guia de solução de problemas de assimilação de streaming](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) | [[!DNL Data Science Workspace] guia de solução de problemas](../data-science-workspace/troubleshooting-guide.md) |
| Governança de dados do Adobe Experience Platform | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Serviço de identidade da Adobe Experience Platform | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] guia de solução de problemas](../identity-service/troubleshooting-guide.md) |
| Serviço de consulta Adobe Experience Platform | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] guia de solução de problemas](../query-service/troubleshooting-guide.md) |
| Segmentação do Adobe Experience Platform | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] Perguntas frequentes e guia de solução de problemas](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] e [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] guia de solução de problemas](../profile/troubleshooting.md) |
| Sandboxes | [API de sandbox](https://www.adobe.io/experience-platform-apis/references/sandbox) | [Guia de solução de problemas de sandboxes](../sandboxes/troubleshooting-guide.md) |
