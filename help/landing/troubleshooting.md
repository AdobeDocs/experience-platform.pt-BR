---
keywords: Experience Platform, home, tópicos populares, códigos de erro da API, código de erro da API, API do código de erro, API códigos de erro, erro da solicitação da API, solução de problemas da API, erro da API
solution: Experience Platform
title: Guia de solução de problemas e perguntas frequentes do Adobe Experience Platform
description: Encontre respostas para perguntas frequentes e um guia para solucionar erros comuns na Experience Platform.
landing-page-description: Encontre respostas para perguntas frequentes e um guia para solucionar erros comuns na Experience Platform.
topic-legacy: getting started
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 4%

---

# [!DNL Platform] Perguntas frequentes e guia de solução de problemas

Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform, bem como um guia de solução de problemas de alto nível para erros comuns que podem ser encontrados em qualquer API [!DNL Experience Platform]. Para obter guias de solução de problemas em serviços individuais [!DNL Platform], consulte o [diretório de solução de problemas de serviço](#service-troubleshooting-directory) abaixo.

## Perguntas frequentes {#faq}

Veja a seguir uma lista de respostas para perguntas frequentes sobre o Adobe Experience Platform.

## O que são APIs [!DNL Experience Platform]? {#what-are-experience-platform-apis}

[!DNL Experience Platform] O oferece várias RESTful APIs que usam solicitações HTTP para acessar  [!DNL Platform] recursos. Essas APIs de serviço expõem vários pontos de extremidade e permitem executar operações para listar (GET), pesquisar (GET), editar (PUT e/ou PATCH) e excluir recursos (DELETE). Para obter mais informações sobre endpoints e operações específicos disponíveis para cada serviço, consulte a [documentação de Referência da API](http://www.adobe.com/go/platform-api-reference-en) no Adobe I/O.

## Como formatar uma solicitação de API? {#how-do-i-format-an-api-request}

Os formatos de solicitação variam, dependendo da API [!DNL Platform] que está sendo usada. A melhor maneira de aprender como estruturar suas chamadas de API é seguindo os exemplos fornecidos na documentação do serviço específico [!DNL Platform] que você está usando.

Para obter mais informações sobre como formatar solicitações de API, visite o guia de introdução da API de plataforma [lendo chamadas de API de exemplo](./api-guide.md#sample-api) seção.

## Qual é minha organização IMS? {#what-is-my-ims-organization}

Uma organização IMS é uma representação Adobe de um cliente. Todas as soluções de Adobe licenciadas são integradas a esta organização de clientes. Quando uma organização IMS tem direito a [!DNL Experience Platform], ela pode atribuir acesso aos desenvolvedores. A ID organizacional IMS (`x-gw-ims-org-id`) representa a organização para a qual uma chamada de API deve ser executada e, portanto, é necessária como um cabeçalho em todas as solicitações de API. Essa ID pode ser encontrada no [Console do desenvolvedor do Adobe](https://www.adobe.com/go/devs_console_ui): na guia **Integrations**, navegue até a seção **Overview** de qualquer integração específica para encontrar a ID em **Client Credentials**. Para obter uma apresentação passo a passo de como autenticar em [!DNL Platform], consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

## Onde encontro minha chave de API? {#where-can-i-find-my-api-key}

Uma chave de API é necessária como um cabeçalho em todas as solicitações de API. Ele pode ser encontrado por meio do [Console do Desenvolvedor do Adobe](https://www.adobe.com/go/devs_console_ui). No console, na guia **Integrations**, navegue até a seção **Overview** de uma integração específica e você encontrará a chave em **Client Credentials**. Para obter uma apresentação passo a passo de como autenticar para [!DNL Platform], consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

## Como obter um token de acesso? {#how-do-i-get-an-access-token}

Os tokens de acesso são necessários no cabeçalho de Autorização de todas as chamadas de API. Eles podem ser gerados usando um comando `curl`, desde que você tenha acesso a uma integração para uma organização IMS. Os tokens de acesso são válidos apenas por 24 horas, depois disso um novo token deve ser gerado para continuar usando a API. Para obter detalhes sobre a geração de tokens de acesso, consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en).

## Como usar parâmetros de consulta? {#how-do-i-user-query-parameters}

Alguns endpoints da API [!DNL Platform] aceitam parâmetros de consulta para localizar informações específicas e filtrar os resultados retornados na resposta. Parâmetros de consulta são anexados a caminhos de solicitação com um símbolo de ponto de interrogação (`?`), seguidos por um ou mais parâmetros de consulta usando o formato `paramName=paramValue`. Ao combinar vários parâmetros em uma única chamada, você deve usar um E comercial (`&`) para separar parâmetros individuais. O exemplo a seguir demonstra como uma solicitação que usa vários parâmetros de consulta é representada na documentação.

Exemplos de parâmetros de consulta usados com frequência incluem:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Para obter informações detalhadas sobre quais parâmetros de consulta estão disponíveis para um serviço ou endpoint específico, consulte a documentação específica do serviço.

## Como indicar um campo JSON a ser atualizado em uma solicitação do PATCH? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Muitas operações de PATCH nas APIs [!DNL Platform] usam [Ponteiro JSON](https://tools.ietf.org/html/rfc6901) strings para indicar propriedades JSON a serem atualizadas. Normalmente, eles são incluídos nas cargas de solicitação usando o formato [JSON Patch](https://tools.ietf.org/html/rfc6902). Consulte o [Guia de fundamentos da API](api-fundamentals.md) para obter informações detalhadas sobre a sintaxe necessária para essas tecnologias.

## Posso usar o Postman para fazer chamadas para [!DNL Platform] APIs? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[](https://www.postman.com/) O Postmanis é uma ferramenta útil para visualizar chamadas para APIs RESTful. O [Guia de introdução à API da plataforma](api-guide.md) contém um vídeo e instruções para importar coleções de Postman. Além disso, uma lista de coleções Postman para cada serviço é fornecida.

## Quais são os requisitos do sistema para [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Dependendo de você estar usando a interface do usuário ou a API, os seguintes requisitos de sistema se aplicam:

**Para operações baseadas na interface do usuário:**
- Um navegador da Web moderno e padrão. Embora a versão mais recente de [!DNL Chrome] seja recomendada, as versões principais atuais e anteriores de [!DNL Firefox], [!DNL Internet Explorer] e Safari também são compatíveis.
   - Cada vez que uma nova versão principal é lançada, [!DNL Platform] começa a oferecer suporte para a versão mais recente, enquanto o suporte para a terceira versão mais recente é descartado.
- Todos os navegadores devem ter cookies e JavaScript habilitado.

**Para interações de API e desenvolvedor:**
- Um ambiente de desenvolvimento para desenvolver integrações REST, streaming e Webhook.

## Erros e solução de problemas {#errors-and-troubleshooting}

Esta é uma lista de erros que você pode encontrar ao usar qualquer serviço [!DNL Experience Platform]. Para obter guias de solução de problemas em serviços individuais [!DNL Platform], consulte o [diretório de solução de problemas de serviço](#service-troubleshooting-directory) abaixo.

## Códigos de status da API {#api-status-codes}

Os seguintes códigos de status podem ser encontrados em qualquer API [!DNL Experience Platform]. Cada uma tem várias causas, pelo que as explicações apresentadas nesta seção têm um caráter geral. Para obter mais detalhes sobre erros específicos em serviços individuais [!DNL Platform], consulte o [diretório de solução de problemas de serviço](#service-troubleshooting-directory) abaixo.

| Código de status | Descrição | Causas possíveis |
|--- | --- | ---|
| 400 | Solicitação inválida | A solicitação foi construída incorretamente, faltavam informações de chave e/ou continha sintaxe incorreta. |
| 401° | Falha na autenticação | A solicitação não passou uma verificação de autenticação. O token de acesso pode estar ausente ou ser inválido. Consulte a seção [OAuth token errors](#oauth-token-is-missing) abaixo para obter mais detalhes. |
| 403 | Proibido | O recurso foi encontrado, mas você não tem as credenciais corretas para exibi-lo. |
| 404 | Não encontrado | Não foi possível localizar o recurso solicitado no servidor. O recurso pode ter sido excluído ou o caminho solicitado foi inserido incorretamente. |
| 500 | Erro interno do servidor | Este é um erro do lado do servidor. Se você estiver fazendo muitas chamadas simultâneas, pode estar atingindo o limite da API e precisa filtrar os resultados. (Consulte o subguia [!DNL Catalog Service] do guia do desenvolvedor de API em [filtrar dados](../catalog/api/filter-data.md) para saber mais.) Aguarde um momento antes de tentar sua solicitação novamente e entre em contato com o administrador se o problema persistir. |

## Erros de cabeçalho da solicitação {#request-header-errors}

Todas as chamadas de API em [!DNL Platform] exigem cabeçalhos de solicitação específicos. Para ver quais cabeçalhos são necessários para serviços individuais, consulte a [documentação de Referência da API](http://www.adobe.com/go/platform-api-reference-en). Para localizar os valores para os cabeçalhos de autenticação necessários, consulte o [Tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Se algum desses cabeçalhos estiver ausente ou inválido ao fazer uma chamada à API, os seguintes erros podem ocorrer.

### O token OAuth está ausente {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Essa mensagem de erro é exibida quando um cabeçalho `Authorization` está ausente de uma solicitação de API. Certifique-se de que o cabeçalho de Autorização está incluído com um token de acesso válido antes de tentar novamente.

### O token OAuth não é válido

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Essa mensagem de erro é exibida quando o token de acesso fornecido no cabeçalho `Authorization` não é válido. Certifique-se de que o token foi inserido corretamente ou [gere um novo token](https://www.adobe.com/go/platform-api-authentication-en) no Console Adobe I/O.

### A chave de API é necessária

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Essa mensagem de erro é exibida quando um cabeçalho de chave de API (`x-api-key`) está ausente em uma solicitação de API. Certifique-se de que o cabeçalho esteja incluído com uma chave de API válida antes de tentar novamente.

### A chave de API é inválida

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Esta mensagem de erro é exibida quando o valor do cabeçalho da chave de API fornecido (`x-api-key`) é inválido. Certifique-se de ter inserido a chave corretamente antes de tentar novamente. Se não souber sua chave de API, poderá encontrá-la no [Console do Adobe I/O](https://console.adobe.io): na guia **Integrations**, navegue até a seção **Overview** de uma integração específica para encontrar a chave da API em **Client Credentials**.


### Cabeçalho ausente

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Essa mensagem de erro é exibida quando um cabeçalho de organização IMS (`x-gw-ims-org-id`) está ausente em uma solicitação de API. Certifique-se de que o cabeçalho esteja incluído com a ID da organização de IMS antes de tentar novamente.

### O perfil não é válido

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Essa mensagem de erro é exibida quando a integração do usuário ou Adobe I/O (identificada pelo [token de acesso](#how-do-i-get-an-access-token) no cabeçalho `Authorization`) não tem direito a fazer chamadas para [!DNL Experience Platform] APIs para a Organização IMS fornecida no cabeçalho `x-gw-ims-org-id`. Certifique-se de ter fornecido a ID correta para sua organização IMS no cabeçalho antes de tentar novamente. Se você não souber a ID da organização, poderá encontrá-la no [Console do Adobe I/O](https://console.adobe.io): na guia **Integrations**, navegue até a seção **Overview** de uma integração específica para encontrar a ID em **Client Credentials**.

### Tipo de conteúdo válido não especificado

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Esta mensagem de erro é exibida quando uma solicitação POST, PUT ou PATCH tem um cabeçalho `Content-Type` inválido ou ausente. Certifique-se de que o cabeçalho esteja incluído na solicitação e que seu valor seja `application/json`.


## Diretório de solução de problemas de serviço {#service-troubleshooting-directory}

Veja a seguir uma lista de guias de solução de problemas e a documentação de referência da API para APIs [!DNL Experience Platform]. Cada guia de solução de problemas fornece respostas a perguntas frequentes e soluções para problemas específicos a serviços individuais [!DNL Platform]. Os documentos de referência da API fornecem um guia abrangente de todos os endpoints disponíveis para cada serviço e mostram exemplos de corpos de solicitação, respostas e códigos de erro que você pode receber.

| Serviço de | Referência da API | Solução de problemas |
| --- | --- | --- |
| Controle de acesso | [API de controle de acesso](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Guia de solução de problemas de controle de acesso](../access-control/troubleshooting-guide.md) |
| Ingestão de dados do Adobe Experience Platform | [[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guia de solução de problemas de assimilação em lote ](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[Guia de solução de problemas de assimilação de streaming](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] guia de solução de problemas](../data-science-workspace/troubleshooting-guide.md) |
| Governança de dados do Adobe Experience Platform | [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] guia de solução de problemas](../identity-service/troubleshooting-guide.md) |
| Serviço de query Adobe Experience Platform | [[!DNL Query Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [[!DNL Query Service] guia de solução de problemas](../query-service/troubleshooting-guide.md) |
| Segmentação do Adobe Experience Platform | [[!DNL Segmentation API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] Perguntas frequentes e guia de solução de problemas](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] e [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [[!DNL Profile] guia de solução de problemas](../profile/troubleshooting.md) |
| Sandboxes | [API de sandbox](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Guia de solução de problemas de sandboxes](../sandboxes/troubleshooting-guide.md) |
