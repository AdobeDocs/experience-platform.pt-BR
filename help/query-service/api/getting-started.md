---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor do Query Service
topic: query templates
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# Guia do desenvolvedor do Query Service

Este guia do desenvolvedor fornece etapas para executar várias operações na API de serviço do Query Adobe Experience Platform.

## Introdução

Este guia exige uma compreensão funcional dos vários serviços de Adobe Experience Platform envolvidos com o uso do serviço de Query.

- [Serviço](../home.md)de Query: Fornece a capacidade de query de conjuntos de dados e captura os query resultantes como novos conjuntos de dados no Experience Platform.
- [Sistema](../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
- [Caixas de proteção](../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância do Platform em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para usar o Serviço de Query com êxito usando a API.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas nesta documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas do Experience Platform.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para APIs de Experience Platform, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas à API do Platform, como mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no Experience Platform são isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs da Platform exigem um cabeçalho que especifique o nome da caixa de proteção na qual a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com caixas de proteção no Experience Platform, consulte a documentação [de visão geral das](../../sandboxes/home.md)caixas de proteção.

## Chamadas de API de exemplo

Agora que você entende quais cabeçalhos devem ser usados, você está pronto para começar a fazer chamadas para a API de serviço do Query. Os documentos a seguir percorrem várias chamadas de API que podem ser feitas usando a API de serviço de Query. Cada chamada de exemplo inclui o formato de API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

- [Queries](queries.md)
- [Parâmetros de conexão](connection-parameters.md)
- [query agendados](scheduled-queries.md)
- [É executado para query agendados](runs-scheduled-queries.md)
- [Modelos de Query](query-templates.md)

## Próximas etapas

Agora que você aprendeu a fazer chamadas usando a API de serviço de Query, é possível criar seus próprios query não interativos. Para obter mais informações sobre como criar query, leia o guia [de referência](../sql/overview.md)SQL.