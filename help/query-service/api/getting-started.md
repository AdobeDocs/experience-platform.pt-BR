---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, query
solution: Experience Platform
title: Guia da API do Serviço de query
topic-legacy: query templates
description: A API do Serviço de query permite que desenvolvedores consultem seus dados do Adobe Experience Platform usando o SQL padrão. Siga este manual para saber como executar operações importantes usando a API.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 6%

---

# [!DNL Query Service] Manual da API

Este guia do desenvolvedor fornece etapas para executar várias operações no Adobe Experience Platform [!DNL Query Service] API.

## Introdução

Este guia requer uma compreensão funcional dos vários serviços da Adobe Experience Platform envolvidos no uso do [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Fornece a capacidade de consultar conjuntos de dados e capturar as consultas resultantes como novos conjuntos de dados em [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para usar com sucesso [!DNL Query Service] usando a API .

### Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas nesta documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Experience Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Platform] Chamadas de API, conforme mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com sandboxes no [!DNL Experience Platform], consulte o [documentação de visão geral das sandboxes](../../sandboxes/home.md).

## Exemplos de chamadas de API

Agora que você entende quais cabeçalhos devem ser usados, você está pronto para começar a fazer chamadas para o [!DNL Query Service] API. Os seguintes documentos percorrem as várias chamadas de API que você pode fazer usando o [!DNL Query Service] API. Cada chamada de exemplo inclui o formato da API geral, uma solicitação de amostra que mostra os cabeçalhos necessários e uma resposta de amostra.

- [Consultas](queries.md)
- [Parâmetros de conexão](connection-parameters.md)
- [Consultas agendadas](scheduled-queries.md)
- [É executado para consultas agendadas](runs-scheduled-queries.md)
- [Templates de query](query-templates.md)

## Próximas etapas

Agora que você aprendeu a fazer chamadas usando o [!DNL Query Service] Você pode criar suas próprias consultas não interativas. Para obter mais informações sobre como criar consultas, leia o [Guia de referência SQL](../sql/overview.md).
