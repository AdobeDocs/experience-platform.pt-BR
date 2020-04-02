---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor do Serviço de segmentação
topic: developer guide
translation-type: tm+mt
source-git-commit: 38762fa57188ed018c4347c07765f3d09daef2e6

---


# Guia do desenvolvedor do Serviço de segmentação

A segmentação permite que você construa segmentos e gere audiências na Adobe Experience Platform a partir dos dados do Perfil do cliente em tempo real.

## Introdução

Este guia exige uma compreensão de trabalho dos vários serviços da plataforma Adobe Experience envolvidos com o uso da segmentação.

- [Segmentação](../home.md): Permite criar segmentos de audiência a partir de dados de Perfil do cliente em tempo real.
- [Sistema](../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
- [Perfil](../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
- [Caixas de proteção](../../sandboxes/home.md): A plataforma Experience fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para usar a segmentação com êxito usando a API.

### Lendo chamadas de exemplo da API

A documentação da API do Serviço de segmentação fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas da plataforma Experience.

### Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído o tutorial [de](../../tutorials/authentication.md) autenticação para fazer chamadas com êxito para os pontos de extremidade da plataforma. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em chamadas à API da plataforma Experience, conforme mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos da plataforma Experience são isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção na qual a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>**Observação:** Para obter mais informações sobre como trabalhar com caixas de proteção na Experience Platform, consulte a documentação [de visão geral das](../../sandboxes/home.md)caixas de proteção.

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

For more information on using this endpoint, please read the [schedules developer guide](./schedules.md).

## Segment definitions

Segment definitions define which profiles will be part of which audience segments. You can use the `/segment/definitions` endpoint to retrieve a list of segment definitions, create a new segment definition, retrieve details of a specific segment definition, delete a specific segment definition, or overwrite details of a specific segment definition.

For more information on using this endpoint, please read the [segment definitions developer guide](./segment-definitions.md). -->

## Trabalhos de segmento

O processo de trabalhos de segmento estabelecia definições de segmento anteriormente para gerar um segmento de audiência. Você pode usar o `/segment/jobs` endpoint para recuperar uma lista de trabalhos de segmento, criar um novo trabalho de segmento, recuperar detalhes de um trabalho de segmento específico ou excluir um trabalho de segmento específico.

Para obter mais informações sobre como usar esse terminal, leia o guia [do desenvolvedor de trabalhos de](./segment-jobs.md)segmento.

## Próximas etapas

Para começar a fazer chamadas usando a API de segmentação, selecione um dos subguias para saber como usar pontos de extremidade específicos relacionados à segmentação. Para saber mais sobre como trabalhar com segmentos usando a interface do usuário da plataforma, consulte o guia [do usuário de](../ui/overview.md)Segmentação.