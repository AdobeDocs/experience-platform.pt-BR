---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, query
solution: Experience Platform
title: Guia da API do Serviço de query
topic-legacy: query templates
description: A API do Serviço de query permite que desenvolvedores consultem seus dados do Adobe Experience Platform usando o SQL padrão. Siga este guia para saber como executar operações principais usando a API.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---

# [!DNL Query Service] Guia da API

Este guia do desenvolvedor fornece etapas para executar várias operações na API [!DNL Query Service] do Adobe Experience Platform.

## Introdução

Este guia requer uma compreensão funcional dos vários serviços da Adobe Experience Platform envolvidos com o uso de [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Fornece a capacidade de consultar conjuntos de dados e capturar as consultas resultantes como novos conjuntos de dados no  [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para usar [!DNL Query Service] com êxito usando a API.

### Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas nesta documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Experience Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Platform], conforme mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral das sandboxes](../../sandboxes/home.md).

## Exemplos de chamadas de API

Agora que você sabe quais cabeçalhos usar, está pronto para começar a fazer chamadas para a API [!DNL Query Service]. Os seguintes documentos percorrem as várias chamadas de API que você pode fazer usando a API [!DNL Query Service]. Cada chamada de exemplo inclui o formato da API geral, uma solicitação de amostra que mostra os cabeçalhos necessários e uma resposta de amostra.

- [Queries](queries.md)
- [Parâmetros de conexão](connection-parameters.md)
- [Consultas agendadas](scheduled-queries.md)
- [É executado para consultas agendadas](runs-scheduled-queries.md)
- [Templates de query](query-templates.md)

## Próximas etapas

Agora que você aprendeu a fazer chamadas usando a API [!DNL Query Service], é possível criar suas próprias consultas não interativas. Para obter mais informações sobre como criar consultas, leia o [Guia de Referência SQL](../sql/overview.md).
