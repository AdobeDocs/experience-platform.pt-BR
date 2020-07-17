---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor do Serviço de segmentação
topic: developer guide
translation-type: tm+mt
source-git-commit: c0eacfba2feea66803e63ed55ad9d0a97e9ae47c
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

O Serviço de segmentação de Adobe Experience Platform permite que você crie segmentos e gere audiências no Adobe Experience Platform a partir de seus [!DNL Real-time Customer Profile] dados.

O guia do desenvolvedor requer uma compreensão funcional dos vários serviços de Experience Platform envolvidos com o uso [!DNL Segmentation Service].

- [!DNL Segmentation](../home.md): Permite criar segmentos de audiência a partir de dados de Perfil do cliente em tempo real.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
- [!DNL Real-time Customer Profile](../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
- [Caixas de proteção](../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância do Platform em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para trabalhar com a [!DNL Segmentation] API.

## Lendo chamadas de exemplo da API

A documentação da [!DNL Segmentation Service] API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas do Experience Platform.

## Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído o tutorial [de](../../tutorials/authentication.md) autenticação para fazer chamadas com êxito para pontos de extremidade da Platform. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em chamadas de API de Experience Platform, como mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção na qual a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com caixas de proteção em [!DNL Experience Platform], consulte a documentação [de visão geral das](../../sandboxes/home.md)caixas de proteção.

<!-- ## Estimates

Estimates provides statistical information for a segment definition, such as projected audience size and confidence interval. You can use the `/estimate` endpoint to view an estimate of a segment definition. 

For more information on using this endpoint, please read the [estimates developer guide](./estimates.md). 

## Export jobs

Export jobs are asynchronous processes that are used to persist audience segment members to datasets. You can use the `/export/jobs` endpoint to retrieve all export jobs, create a new export job, retrieve details of a specific export job, or cancel a specific export job.

For more information on using this endpoint, please read the [export jobs developer guide](./export-jobs.md).

## Previews

Previews provide a paginated list of qualifying profiles for a segment definition, allowing you to compare the results against what you expect. You can use the `/preview` endpoint to create a new preview job, look up results of a specific preview job, or delete a specific preview job.

For more information on using this endpoint, please read the [previews developer guide](./previews.md).

## PQL conversions

Profile Query Language (PQL) conversions allows you to convert your formatting between `pql/text` and `pql/json`. You can do this by using the `/segment/conversion` endpoint.

For more information on using this endpoint, please read the [PQL conversions developer guide](./pql-conversions.md).

## Schedules

Schedules are a tool that can be used to automatically run export jobs once a day. You can use the `/config/schedules` endpoint to retrieve a list of schedules, create a new schedule, retrieve details of a specific schedule, update a specific schedule, or delete a specific schedule. 

For more information on using this endpoint, please read the [schedules developer guide](./schedules.md). -->

## Definições de segmento

As definições de segmentos definem quais perfis farão parte de quais segmentos de audiência. Você pode usar o `/segment/definitions` endpoint para recuperar uma lista de definições de segmento, criar uma nova definição de segmento, recuperar detalhes de uma definição de segmento específica, excluir uma definição de segmento específica ou substituir detalhes de uma definição de segmento específica.

Para obter mais informações sobre como usar esse terminal, leia o guia [do desenvolvedor de definições de](./segment-definitions.md)segmento.

## Trabalhos de segmento

O processo de trabalhos de segmento estabelecia definições de segmento anteriormente para gerar um segmento de audiência. Você pode usar o `/segment/jobs` endpoint para recuperar uma lista de trabalhos de segmento, criar um novo trabalho de segmento, recuperar detalhes de um trabalho de segmento específico ou excluir um trabalho de segmento específico.

Para obter mais informações sobre como usar esse terminal, leia o guia [do desenvolvedor de trabalhos de](./segment-jobs.md)segmento.

## Pesquisa de segmento

A pesquisa por segmento é usada para pesquisar e indexar campos configuráveis contidos em várias fontes de dados e retorná-los em tempo quase real. Para começar a trabalhar com a pesquisa de segmentos, consulte o guia do desenvolvedor de [pesquisa](segment-search.md)

## Próximas etapas

Para fazer chamadas usando a [!DNL Segmentation Service] API, selecione um dos guias de ponto de extremidade disponíveis usando a navegação esquerda ou dentro da visão geral do guia do [desenvolvedor](./overview.md)