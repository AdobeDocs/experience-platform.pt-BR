---
keywords: Experience Platform;início;tópicos populares;códigos de erro de API;código de erro de API;código de erro API;códigos de erro API;erro de solicitação de API;solução de problemas de API;erro de API
solution: Experience Platform
title: Perguntas frequentes sobre o Adobe Experience Platform e Guia de solução de problemas
description: Encontre respostas para perguntas frequentes e um guia para solucionar erros comuns na Experience Platform.
landing-page-description: Encontre respostas para perguntas frequentes e um guia para solucionar erros comuns na Experience Platform.
short-description: Encontre respostas para perguntas frequentes e um guia para solucionar erros comuns na Experience Platform.
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 5%

---

# [!DNL Platform] Guia de perguntas frequentes e solução de problemas

Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform, bem como um guia de solução de problemas de alto nível para erros comuns que podem ser encontrados em qualquer [!DNL Experience Platform] API. Para obter guias de solução de problemas em [!DNL Platform] serviços, consulte a [diretório de solução de problemas de serviço](#service-troubleshooting-directory) abaixo.

## Perguntas frequentes {#faq}

Veja a seguir uma lista de respostas para perguntas frequentes sobre o Adobe Experience Platform.

## O que são [!DNL Experience Platform] APIs? {#what-are-experience-platform-apis}

[!DNL Experience Platform] O oferece várias APIs RESTful que usam solicitações HTTP para acessar [!DNL Platform] recursos. Cada uma dessas APIs de serviço expõe vários endpoints e permite executar operações para listar (GET), pesquisar (GET), editar (PUT e/ou PATCH) e excluir (DELETE) recursos. Para obter mais informações sobre endpoints e operações específicos disponíveis para cada serviço, consulte [Documentação de referência da API](https://www.adobe.com/go/platform-api-reference-en) no Adobe I/O.

## Como formatar uma solicitação de API? {#how-do-i-format-an-api-request}

Os formatos de solicitação variam dependendo da [!DNL Platform] API em uso. A melhor maneira de saber como estruturar suas chamadas de API é seguindo os exemplos fornecidos na documentação para a API específica [!DNL Platform] serviço que você está usando.

Para obter mais informações sobre como formatar solicitações de API, consulte o guia de introdução à API da plataforma [leitura de chamadas de API de amostra](./api-guide.md#sample-api) seção.

## Qual é minha organização? {#what-is-my-ims-organization}

Uma organização é uma representação Adobe de um cliente. Todas as soluções de Adobe licenciadas são integradas a esta organização do cliente. Quando uma organização tem direito a [!DNL Experience Platform], ele pode atribuir acesso aos desenvolvedores. A ID da organização (`x-gw-ims-org-id`) representa a organização para a qual uma chamada de API deve ser executada e, portanto, é necessária como um cabeçalho em todas as solicitações de API. Essa ID pode ser encontrada por meio da variável [Console do Adobe Developer](https://www.adobe.com/go/devs_console_ui): no **Integrações** , navegue até o **Visão geral** para qualquer integração específica para encontrar a ID em **Credenciais do cliente**. Para obter uma apresentação passo a passo de como autenticar no [!DNL Platform], consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

## Onde encontro minha chave de API? {#where-can-i-find-my-api-key}

Uma chave de API é necessária como cabeçalho em todas as solicitações de API. Ele pode ser encontrado por meio da [Console do Adobe Developer](https://www.adobe.com/go/devs_console_ui). No console, no **Integrações** , navegue até o **Visão geral** para uma integração específica e você encontrará a chave em **Credenciais do cliente**. Para obter uma apresentação passo a passo de como realizar a autenticação no [!DNL Platform], consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

## Como obter um token de acesso? {#how-do-i-get-an-access-token}

Os tokens de acesso são necessários no cabeçalho de Autorização de todas as chamadas de API. Elas podem ser geradas usando um comando CURL, desde que você tenha acesso a uma integração para uma organização. Os tokens de acesso são válidos somente por 24 horas, após as quais um novo token deve ser gerado para continuar usando a API. Para obter detalhes sobre a geração de tokens de acesso, consulte a [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

## Como usar parâmetros de consulta? {#how-do-i-user-query-parameters}

Alguns [!DNL Platform] Os endpoints da API aceitam parâmetros de consulta para localizar informações específicas e filtrar os resultados retornados na resposta. Os parâmetros de consulta são anexados a caminhos de solicitação com um ponto de interrogação (`?`), seguido por um ou mais parâmetros de consulta usando o formato `paramName=paramValue`. Ao combinar vários parâmetros em uma única chamada do, você deve usar um E comercial (`&`) para separar parâmetros individuais. O exemplo a seguir demonstra como uma solicitação que usa vários parâmetros de consulta é representada na documentação.

Exemplos de parâmetros de consulta comumente usados incluem:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Para obter informações detalhadas sobre quais parâmetros de consulta estão disponíveis para um serviço ou endpoint específico, consulte a documentação específica do serviço.

## Como indicar um campo JSON para atualizar em uma solicitação PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Muitas operações de PATCH em [!DNL Platform] Uso de APIs [Ponteiro JSON](https://tools.ietf.org/html/rfc6901) cadeias de caracteres para indicar as propriedades JSON que serão atualizadas. Normalmente, são incluídas em cargas de solicitação usando [Patch JSON](https://tools.ietf.org/html/rfc6902) formato. Consulte a [Guia de fundamentos de API](api-fundamentals.md) para obter informações detalhadas sobre a sintaxe necessária para essas tecnologias.

## Posso usar o Postman para fazer chamadas para [!DNL Platform] APIs? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) O é uma ferramenta útil para visualizar chamadas para APIs RESTful. A variável [Guia de introdução à API da plataforma](api-guide.md) contém um vídeo e instruções para importar coleções do Postman. Além disso, é fornecida uma lista de coleções do Postman para cada serviço.

## Quais são os requisitos de sistema do [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Dependendo de você estar usando a interface do usuário ou a API, os seguintes requisitos de sistema se aplicam:

**Para operações baseadas em interface do usuário:**
- Um navegador da Web moderno e padrão. Embora a versão mais recente do [!DNL Chrome] O é recomendado para as versões principais atuais e anteriores do [!DNL Firefox], [!DNL Internet Explorer], e Safari também são compatíveis.
   - Cada vez que uma nova versão principal é lançada, [!DNL Platform] O começa a oferecer suporte à versão mais recente, enquanto o suporte à terceira versão mais recente é descartado.
- Todos os navegadores devem ter cookies e JavaScript ativados.

**Para API e interações do desenvolvedor:**
- Um ambiente de desenvolvimento para desenvolver integrações REST, streaming e Webhook.

## Erros e solução de problemas {#errors-and-troubleshooting}

Veja a seguir uma lista de erros que você pode encontrar ao usar qualquer [!DNL Experience Platform] serviço. Para obter guias de solução de problemas em [!DNL Platform] serviços, consulte a [diretório de solução de problemas de serviço](#service-troubleshooting-directory) abaixo.

## Códigos de status da API {#api-status-codes}

Os seguintes códigos de status podem ser encontrados em qualquer [!DNL Experience Platform] API. Cada um tem uma variedade de causas, portanto, as explicações fornecidas nesta seção são de natureza geral. Para obter mais detalhes sobre erros específicos em [!DNL Platform] serviços, consulte a [diretório de solução de problemas de serviço](#service-troubleshooting-directory) abaixo.

| Código de status | Descrição | Possíveis causas |
|--- | --- | ---|
| 400 | Solicitação inválida | A solicitação foi construída incorretamente, informações de chave ausentes e/ou continha sintaxe incorreta. |
| 401 | Falha na autenticação | A solicitação não passou em uma verificação de autenticação. Seu token de acesso pode estar ausente ou ser inválido. Consulte a [Erros de token OAuth](#oauth-token-is-missing) abaixo para obter mais detalhes. |
| 403 | Proibido | O recurso foi encontrado, mas você não tem as credenciais corretas para exibi-lo. <br> Uma causa provável desse erro é que você pode não ter o necessário [permissões de controle de acesso](/help/access-control/home.md) para acessar ou editar o recurso. Ler como [obter as permissões de controle de acesso baseadas em atributos necessárias](/help/landing/api-authentication.md#get-abac-permissions) para usar APIs da plataforma. </p> |
| 404 | Não encontrado | O recurso solicitado não foi encontrado no servidor. O recurso pode ter sido excluído ou o caminho solicitado foi inserido incorretamente. |
| 500 | Erro interno do servidor | Esse é um erro do lado do servidor. Se você estiver fazendo muitas chamadas simultâneas, talvez esteja atingindo o limite da API e precise filtrar seus resultados. (Consulte a [!DNL Catalog Service] Subguia do guia do desenvolvedor de API em [filtragem de dados](../catalog/api/filter-data.md) para saber mais.) Aguarde um momento antes de tentar sua solicitação novamente e entre em contato com o administrador se o problema persistir. |

## Erros no cabeçalho da solicitação {#request-header-errors}

Todas as chamadas de API em [!DNL Platform] exigem cabeçalhos de solicitação específicos. Para ver quais cabeçalhos são necessários para serviços individuais, consulte [Documentação de referência da API](https://www.adobe.com/go/platform-api-reference-en). Para localizar os valores dos cabeçalhos de autenticação necessários, consulte [Tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Se qualquer um desses cabeçalhos estiver ausente ou for inválido ao fazer uma chamada de API, os seguintes erros poderão ocorrer.

### Token OAuth ausente {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Essa mensagem de erro é exibida quando uma `Authorization` O cabeçalho do está ausente em uma solicitação de API. Verifique se o cabeçalho de Autorização está incluído com um token de acesso válido antes de tentar novamente.

### O token OAuth é inválido {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Esta mensagem de erro é exibida quando o token de acesso fornecido no `Authorization` cabeçalho inválido. Verifique se o token foi inserido corretamente ou [gerar um novo token](https://www.adobe.com/go/platform-api-authentication-en) no Console do Adobe I/O.

### A chave de API é obrigatória {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Essa mensagem de erro é exibida quando um cabeçalho de chave de API (`x-api-key`) está ausente em uma solicitação de API. Verifique se o cabeçalho está incluído com uma chave de API válida antes de tentar novamente.

### A chave de API é inválida {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Essa mensagem de erro é exibida quando o valor do cabeçalho da chave de API fornecido (`x-api-key`) é inválido. Verifique se você inseriu a chave corretamente antes de tentar novamente. Se você não souber sua chave de API, poderá encontrá-la no [Console Adobe I/O](https://console.adobe.io): no **Integrações** , navegue até o **Visão geral** para obter uma integração específica e encontrar a chave de API em **Credenciais do cliente**.

### Cabeçalho ausente {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Essa mensagem de erro é exibida quando um cabeçalho de organização (`x-gw-ims-org-id`) está ausente em uma solicitação de API. Verifique se o cabeçalho está incluído com a ID da organização antes de tentar novamente.

### O perfil não é válido {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Essa mensagem de erro é exibida quando o usuário ou a integração de Adobe I/O (identificada pela variável [token de acesso](#how-do-i-get-an-access-token) no `Authorization` cabeçalho) não está autorizado a fazer chamadas para [!DNL Experience Platform] APIs para a organização fornecidas no `x-gw-ims-org-id` cabeçalho. Verifique se você forneceu a ID correta para a organização no cabeçalho antes de tentar novamente. Caso não saiba a ID da organização, é possível encontrá-la na [Console Adobe I/O](https://console.adobe.io): no **Integrações** , navegue até o **Visão geral** para obter uma integração específica para encontrar a ID em **Credenciais do cliente**.

### Erro ao atualizar tag {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

Você pode receber um erro de etag se uma alteração tiver sido feita em qualquer entidade de origem ou destino, como fluxo, conexão, conector de origem ou conexão de destino, por outro chamador de API. Devido à incompatibilidade de versões, a alteração que você está tentando fazer não seria aplicada à versão mais recente da entidade.

Para resolver isso, você precisa buscar a entidade novamente, verifique se suas alterações são compatíveis com a nova versão da entidade e coloque a nova tag no `If-Match` e, por fim, faça a chamada à API.

### Tipo de conteúdo válido não especificado {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Esta mensagem de erro é exibida quando uma solicitação POST, PUT ou PATCH tem uma solicitação inválida ou ausente `Content-Type` cabeçalho. Certifique-se de que o cabeçalho esteja incluído na solicitação e que seu valor esteja `application/json`.

### Região do usuário ausente {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

Essa mensagem de erro é exibida em qualquer um dos casos abaixo:
- Quando um cabeçalho de ID de organização incorreto ou malformado (`x-gw-ims-org-id`) é transmitido em uma solicitação de API. Verifique se a ID correta da organização foi incluída antes de tentar novamente.
- Quando sua conta (conforme representada pelas credenciais de autenticação fornecidas) não está associada a um perfil de produto para o Experience Platform. Siga as etapas em [geração de credenciais de acesso](./api-authentication.md#authentication-for-each-session) no tutorial de autenticação da API da plataforma para adicionar a Platform à sua conta e atualizar suas credenciais de autenticação de acordo.

## Diretório de solução de problemas de serviço {#service-troubleshooting-directory}

Veja a seguir uma lista de guias de solução de problemas e a documentação de referência da API para [!DNL Experience Platform] APIs. Cada guia de solução de problemas fornece respostas a perguntas frequentes e soluções para problemas específicos de cada indivíduo [!DNL Platform] serviços. Os documentos de referência da API fornecem um guia abrangente para todos os endpoints disponíveis para cada serviço e mostram exemplos de corpos de solicitação, respostas e códigos de erro que você pode receber.

| Serviço de | Referência da API | Solução de problemas |
| --- | --- | --- |
| Controle de acesso | [API de controle de acesso](https://www.adobe.io/experience-platform-apis/references/access-control/) | [Guia de solução de problemas de controle de acesso](../access-control/troubleshooting-guide.md) |
| Assimilação de dados Adobe Experience Platform | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [Guia de solução de problemas de assimilação em lote](../ingestion/batch-ingestion/troubleshooting.md) |
| Assimilação de dados Adobe Experience Platform | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [Guia de solução de problemas de assimilação de streaming](../ingestion/streaming-ingestion/troubleshooting.md) |
| Espaço de trabalho de ciência de dados da Adobe Experience Platform | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] guia de solução de problemas](../data-science-workspace/troubleshooting-guide.md) |
| Governança de dados do Adobe Experience Platform | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] guia de solução de problemas](../identity-service/troubleshooting-guide.md) |
| Serviço de consulta Adobe Experience Platform | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] guia de solução de problemas](../query-service/troubleshooting-guide.md) |
| Segmentação do Adobe Experience Platform | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] Guia de perguntas frequentes e solução de problemas](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] e [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] guia de solução de problemas](../profile/troubleshooting.md) |
| Sandboxes | [API de sandbox](https://www.adobe.io/experience-platform-apis/references/sandbox) | [Guia de solução de problemas de sandboxes](../sandboxes/troubleshooting-guide.md) |
