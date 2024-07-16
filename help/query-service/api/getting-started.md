---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;serviço de consulta;consulta;;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Guia da API do Serviço de consulta
description: A API do Serviço de consulta permite que os desenvolvedores consultem seus dados do Adobe Experience Platform usando o SQL padrão. Siga este manual para saber como executar operações importantes usando a API.
role: Developer
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 20%

---

# [!DNL Query Service] Manual da API

Este guia do desenvolvedor fornece etapas para executar várias operações na API [!DNL Query Service] do Adobe Experience Platform.

## Introdução

Este guia requer uma compreensão funcional dos vários serviços da Adobe Experience Platform envolvidos no uso do [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Fornece a capacidade de consultar conjuntos de dados e capturar as consultas resultantes como novos conjuntos de dados em [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para usar com êxito o [!DNL Query Service] usando a API.

### Leitura de chamadas de API de amostra

Este manual fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas nesta documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs do [!DNL Experience Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Platform], conforme mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral das sandboxes](../../sandboxes/home.md).

## Exemplos de chamadas de API

Agora que você entende quais cabeçalhos usar, você está pronto para começar a fazer chamadas para a API [!DNL Query Service]. Os documentos a seguir abordam as várias chamadas de API que podem ser feitas usando a API [!DNL Query Service]. Cada chamada de exemplo inclui o formato geral da API, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.

- [Consultas](queries.md)
- [Parâmetros de conexão](connection-parameters.md)
- [Consultas programadas](scheduled-queries.md)
- [Execução para consultas programadas](runs-scheduled-queries.md)
- [Modelos de consulta](query-templates.md)
- [Consultas aceleradas](./accelerated-queries.md)
- [Assinaturas de alerta](./alert-subscriptions.md)

## Próximas etapas

Agora que você aprendeu a fazer chamadas usando a API [!DNL Query Service], poderá criar suas próprias consultas não interativas. Para obter mais informações sobre como criar consultas, leia o [Guia de Referência SQL](../sql/overview.md).
