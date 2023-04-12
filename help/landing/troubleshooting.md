---
keywords: Experience Platform, home, tópicos populares, códigos de erro da API, código de erro da API, API do código de erro, API códigos de erro, erro da solicitação da API, solução de problemas da API, erro da API
solution: Experience Platform
title: Guia de solução de problemas e perguntas frequentes do Adobe Experience Platform
description: Encontre respostas para perguntas frequentes e um guia para solucionar erros comuns na Experience Platform.
landing-page-description: Encontre respostas para perguntas frequentes e um guia para solucionar erros comuns na Experience Platform.
short-description: Encontre respostas para perguntas frequentes e um guia para solucionar erros comuns na Experience Platform.
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '1877'
ht-degree: 5%

---

# [!DNL Platform] Perguntas frequentes e guia de solução de problemas

Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform, bem como um guia de solução de problemas de alto nível para erros comuns que podem ser encontrados em qualquer [!DNL Experience Platform] API. Para guias de solução de problemas em indivíduos [!DNL Platform] consulte os [diretório de solução de problemas de serviço](#service-troubleshooting-directory) abaixo.

## Perguntas frequentes {#faq}

Veja a seguir uma lista de respostas para perguntas frequentes sobre o Adobe Experience Platform.

## O que são [!DNL Experience Platform] APIs? {#what-are-experience-platform-apis}

[!DNL Experience Platform] oferece várias RESTful APIs que usam solicitações HTTP para acessar [!DNL Platform] recursos. Essas APIs de serviço expõem vários pontos de extremidade e permitem executar operações para listar (GET), pesquisar (GET), editar (PUT e/ou PATCH) e excluir recursos (DELETE). Para obter mais informações sobre endpoints e operações específicos disponíveis para cada serviço, consulte o [Documentação de referência da API](https://www.adobe.com/go/platform-api-reference-en) na Adobe I/O.

## Como formatar uma solicitação de API? {#how-do-i-format-an-api-request}

Os formatos de solicitação variam dependendo do [!DNL Platform] API que está sendo usada. A melhor maneira de aprender como estruturar suas chamadas de API é seguindo os exemplos fornecidos na documentação para o [!DNL Platform] serviço que você está usando.

Para obter mais informações sobre como formatar solicitações de API, visite o guia de introdução à API da plataforma [como ler chamadas de API de exemplo](./api-guide.md#sample-api) seção.

## Qual é minha organização IMS? {#what-is-my-ims-organization}

Uma organização IMS é uma representação Adobe de um cliente. Todas as soluções de Adobe licenciadas são integradas a esta organização de clientes. Quando uma organização IMS tem direito a [!DNL Experience Platform], ele pode atribuir acesso aos desenvolvedores. A ID organizacional IMS (`x-gw-ims-org-id`) representa a organização para a qual uma chamada de API deve ser executada e, portanto, é necessária como um cabeçalho em todas as solicitações de API. Essa ID pode ser encontrada no [Console do Adobe Developer](https://www.adobe.com/go/devs_console_ui): no **Integrações** , navegue até a guia **Visão geral** seção para qualquer integração específica encontrar a ID em **Credenciais do Cliente**. Para obter uma apresentação passo a passo de como autenticar em [!DNL Platform], consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

## Onde encontro minha chave de API? {#where-can-i-find-my-api-key}

Uma chave de API é necessária como um cabeçalho em todas as solicitações de API. Ele pode ser encontrado por meio do [Console do Adobe Developer](https://www.adobe.com/go/devs_console_ui). No console, na **Integrações** , navegue até a guia **Visão geral** seção para uma integração específica e você encontrará a chave em **Credenciais do Cliente**. Para obter uma apresentação passo a passo de como autenticar para [!DNL Platform], consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

## Como obter um token de acesso? {#how-do-i-get-an-access-token}

Os tokens de acesso são necessários no cabeçalho de Autorização de todas as chamadas de API. Eles podem ser gerados usando um `curl` , desde que você tenha acesso a uma integração para uma organização IMS. Os tokens de acesso são válidos apenas por 24 horas, depois disso um novo token deve ser gerado para continuar usando a API. Para obter detalhes sobre a geração de tokens de acesso, consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

## Como usar parâmetros de consulta? {#how-do-i-user-query-parameters}

Algumas [!DNL Platform] Os pontos de extremidade da API aceitam parâmetros de consulta para localizar informações específicas e filtrar os resultados retornados na resposta. Parâmetros de consulta são anexados a caminhos de solicitação com um ponto de interrogação (`?`), seguido por um ou mais parâmetros de consulta usando o formato `paramName=paramValue`. Ao combinar vários parâmetros em uma única chamada, você deve usar um e comercial (`&`) para separar parâmetros individuais. O exemplo a seguir demonstra como uma solicitação que usa vários parâmetros de consulta é representada na documentação.

Exemplos de parâmetros de consulta usados com frequência incluem:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Para obter informações detalhadas sobre quais parâmetros de consulta estão disponíveis para um serviço ou endpoint específico, consulte a documentação específica do serviço.

## Como indicar um campo JSON a ser atualizado em uma solicitação do PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Muitas operações do PATCH em [!DNL Platform] Uso de APIs [Ponteiro JSON](https://tools.ietf.org/html/rfc6901) strings para indicar propriedades JSON a serem atualizadas. Normalmente, elas são incluídas nas cargas de solicitação usando [Patch JSON](https://tools.ietf.org/html/rfc6902) formato. Consulte a [Guia de fundamentos da API](api-fundamentals.md) para obter informações detalhadas sobre a sintaxe necessária para essas tecnologias.

## Posso usar o Postman para fazer chamadas para [!DNL Platform] APIs? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) O é uma ferramenta útil para visualizar chamadas para APIs RESTful. O [Guia de introdução à API do Platform](api-guide.md) contém um vídeo e instruções para importar coleções do Postman. Além disso, é fornecida uma lista de coleções do Postman para cada serviço.

## Quais são os requisitos de sistema para [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Dependendo de você estar usando a interface do usuário ou a API, os seguintes requisitos de sistema se aplicam:

**Para operações baseadas na interface do usuário:**
- Um navegador da Web moderno e padrão. Enquanto a versão mais recente de [!DNL Chrome] é recomendado, versões principais atuais e anteriores de [!DNL Firefox], [!DNL Internet Explorer]e o Safari também são compatíveis.
   - Sempre que uma nova versão principal for lançada, [!DNL Platform] começa a oferecer suporte para a versão mais recente, enquanto o suporte para a terceira versão mais recente é descartado.
- Todos os navegadores devem ter cookies e JavaScript habilitado.

**Para interações de API e desenvolvedor:**
- Um ambiente de desenvolvimento para desenvolver integrações REST, streaming e Webhook.

## Erros e solução de problemas {#errors-and-troubleshooting}

Esta é uma lista de erros que você pode encontrar ao usar qualquer [!DNL Experience Platform] serviço. Para guias de solução de problemas em indivíduos [!DNL Platform] consulte os [diretório de solução de problemas de serviço](#service-troubleshooting-directory) abaixo.

## Códigos de status da API {#api-status-codes}

Os seguintes códigos de status podem ser encontrados em qualquer [!DNL Experience Platform] API. Cada uma tem várias causas, pelo que as explicações apresentadas nesta seção têm um caráter geral. Para obter mais detalhes sobre erros específicos no [!DNL Platform] serviços, consulte o [diretório de solução de problemas de serviço](#service-troubleshooting-directory) abaixo.

| Código de status | Descrição | Causas possíveis |
|--- | --- | ---|
| 400 | Solicitação inválida | A solicitação foi construída incorretamente, faltavam informações de chave e/ou continha sintaxe incorreta. |
| 401 | Falha na autenticação | A solicitação não passou uma verificação de autenticação. O token de acesso pode estar ausente ou ser inválido. Consulte a [Erros de token OAuth](#oauth-token-is-missing) para obter mais detalhes. |
| 403 | Proibido | O recurso foi encontrado, mas você não tem as credenciais corretas para exibi-lo. |
| 404 | Não encontrado | Não foi possível localizar o recurso solicitado no servidor. O recurso pode ter sido excluído ou o caminho solicitado foi inserido incorretamente. |
| 500 | Erro interno do servidor | Este é um erro do lado do servidor. Se você estiver fazendo muitas chamadas simultâneas, pode estar atingindo o limite da API e precisa filtrar os resultados. (Consulte o [!DNL Catalog Service] Subguia do guia do desenvolvedor de API em [filtragem de dados](../catalog/api/filter-data.md) para saber mais.) Aguarde um momento antes de tentar sua solicitação novamente e entre em contato com o administrador se o problema persistir. |

## Erros do cabeçalho da solicitação {#request-header-errors}

Todas as chamadas de API em [!DNL Platform] requerem cabeçalhos de solicitação específicos. Para ver quais cabeçalhos são necessários para serviços individuais, consulte o [Documentação de referência da API](https://www.adobe.com/go/platform-api-reference-en). Para localizar os valores para os cabeçalhos de autenticação necessários, consulte o [Tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Se algum desses cabeçalhos estiver ausente ou inválido ao fazer uma chamada à API, os seguintes erros podem ocorrer.

### O token OAuth está ausente {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Essa mensagem de erro é exibida quando uma mensagem de erro é exibida `Authorization` está ausente de uma solicitação de API. Certifique-se de que o cabeçalho de Autorização está incluído com um token de acesso válido antes de tentar novamente.

### O token OAuth não é válido {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Essa mensagem de erro é exibida quando o token de acesso fornecido na `Authorization` cabeçalho inválido. Verifique se o token foi inserido corretamente ou [gerar um novo token](https://www.adobe.com/go/platform-api-authentication-en) no console Adobe I/O.

### A chave de API é necessária {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Esta mensagem de erro é exibida quando um cabeçalho de chave de API (`x-api-key`) está ausente de uma solicitação de API. Certifique-se de que o cabeçalho esteja incluído com uma chave de API válida antes de tentar novamente.

### A chave de API é inválida {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Esta mensagem de erro é exibida quando o valor do cabeçalho da chave de API fornecido (`x-api-key`) é inválido. Certifique-se de ter inserido a chave corretamente antes de tentar novamente. Se você não souber sua chave de API, poderá encontrá-la no [Console Adobe I/O](https://console.adobe.io): no **Integrações** , navegue até a guia **Visão geral** seção de uma integração específica para encontrar a chave da API em **Credenciais do Cliente**.

### Cabeçalho ausente {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Esta mensagem de erro é exibida quando um cabeçalho de organização IMS (`x-gw-ims-org-id`) está ausente de uma solicitação de API. Certifique-se de que o cabeçalho esteja incluído com a ID da organização de IMS antes de tentar novamente.

### O perfil não é válido {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Essa mensagem de erro é exibida quando a integração de usuário ou Adobe I/O é exibida (identificada pela variável [token de acesso](#how-do-i-get-an-access-token) no `Authorization` ) não tem direito a fazer chamadas para [!DNL Experience Platform] As APIs para a IMS Org fornecidas no `x-gw-ims-org-id` cabeçalho. Certifique-se de ter fornecido a ID correta para sua organização IMS no cabeçalho antes de tentar novamente. Caso não saiba a ID da organização, é possível encontrá-la no [Console Adobe I/O](https://console.adobe.io): no **Integrações** , navegue até a guia **Visão geral** seção para uma integração específica encontrar a ID em **Credenciais do Cliente**.

### Erro de atualização da tag {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

Você pode receber um erro de tag se uma alteração foi feita em qualquer entidade de origem ou de destino, como fluxo, conexão, conector de origem ou conexão de destino por outro chamador de API. Devido à incompatibilidade da versão, a alteração que você está tentando fazer não seria aplicada à versão mais recente da entidade.

Para resolver isso, você precisa buscar a entidade novamente, garantir que as alterações sejam compatíveis com a nova versão da entidade e, em seguida, colocar a nova tag no `If-Match` e, por fim, faça a chamada da API .

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

Essa mensagem de erro é exibida em um dos dois casos abaixo:
- Quando um cabeçalho da Org de IMS incorreto ou malformado (`x-gw-ims-org-id`) é passada em uma solicitação de API. Certifique-se de que a ID correta da sua Organização IMS esteja incluída antes de tentar novamente.
- Quando sua conta (como representada pelas credenciais de autenticação fornecidas) não está associada a um perfil de produto para o Experience Platform. Siga as etapas em [gerando credenciais de acesso](./api-authentication.md#authentication-for-each-session) no tutorial de autenticação da API da plataforma para adicionar Plataforma à sua conta e atualizar suas credenciais de autenticação de acordo.

## Diretório de solução de problemas do serviço {#service-troubleshooting-directory}

Veja a seguir uma lista de guias de solução de problemas e a documentação de referência da API para [!DNL Experience Platform] APIs. Cada guia de solução de problemas fornece respostas para perguntas frequentes e soluções para problemas específicos de cada indivíduo [!DNL Platform] serviços. Os documentos de referência da API fornecem um guia abrangente de todos os endpoints disponíveis para cada serviço e mostram exemplos de corpos de solicitação, respostas e códigos de erro que você pode receber.

| Serviço de | Referência da API | Solução de problemas |
| --- | --- | --- |
| Controle de acesso | [API de controle de acesso](https://www.adobe.io/experience-platform-apis/references/access-control/) | [Guia de solução de problemas de controle de acesso](../access-control/troubleshooting-guide.md) |
| Ingestão de dados do Adobe Experience Platform | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [Guia de solução de problemas de assimilação em lote](../ingestion/batch-ingestion/troubleshooting.md) |
| Ingestão de dados do Adobe Experience Platform | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [Guia de solução de problemas de assimilação de streaming](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] guia de solução de problemas](../data-science-workspace/troubleshooting-guide.md) |
| Governança de dados do Adobe Experience Platform | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] guia de solução de problemas](../identity-service/troubleshooting-guide.md) |
| Serviço de query Adobe Experience Platform | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] guia de solução de problemas](../query-service/troubleshooting-guide.md) |
| Segmentação do Adobe Experience Platform | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] Perguntas frequentes e guia de solução de problemas](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] e [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] guia de solução de problemas](../profile/troubleshooting.md) |
| Sandboxes | [API de sandbox](https://www.adobe.io/experience-platform-apis/references/sandbox) | [Guia de solução de problemas de sandboxes](../sandboxes/troubleshooting-guide.md) |
