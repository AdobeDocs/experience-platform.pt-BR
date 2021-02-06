---
keywords: Experience Platform;home;popular topics;ingestão em lote;ingestão parcial;ingestão parcial;Erro de recuperação;erro de recuperação;ingestão em lote parcial;ingestão em lote parcial;parcial;ingestão;ingestão;ingestão;ingestão;ingestão;ingestão;
solution: Experience Platform
title: Visão Geral da Ingestão de Lote Parcial
topic: overview
description: Este documento fornece um tutorial para gerenciar a ingestão parcial em lote.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---


# Ingestão parcial em lote

A ingestão parcial em lote é a capacidade de assimilar dados que contenham erros, até um certo limite. Com esse recurso, os usuários podem assimilar com êxito todos os seus dados corretos no Adobe Experience Platform enquanto todos os dados incorretos são armazenados separadamente em lote, juntamente com detalhes sobre o motivo pelo qual são inválidos.

Este documento fornece um tutorial para gerenciar a ingestão parcial em lote.

## Introdução

Este tutorial requer um conhecimento prático dos vários serviços da Adobe Experience Platform envolvidos com a ingestão parcial de lote. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [Ingestão](./overview.md) em lote: O método que  [!DNL Platform] ingere e armazena dados de arquivos de dados, como CSV e Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para [!DNL Platform] APIs.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

## Habilitar um lote para ingestão parcial em lote na API {#enable-api}

>[!NOTE]
>
>Esta seção descreve como ativar um lote para ingestão parcial em lote usando a API. Para obter instruções sobre como usar a interface do usuário, leia a etapa [ativar um lote para a ingestão parcial em lote na etapa UI](#enable-ui).

Você pode criar um novo lote com a ingestão parcial ativada.

Para criar um novo lote, siga as etapas no [guia do desenvolvedor de ingestão em lote](./api-overview.md). Depois de atingir a etapa **[!UICONTROL Criar lote]**, adicione o seguinte campo no corpo da solicitação:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `enableErrorDiagnostics` | Um sinalizador que permite que [!DNL Platform] gere mensagens de erro detalhadas sobre o lote. |
| `partialIngestionPercentage` | A porcentagem de erros aceitáveis antes que todo o lote falhe. Assim, neste exemplo, um máximo de 5% do lote pode ser de erros, antes que falhe. |


## Ative um lote para a ingestão parcial em lote na interface do usuário {#enable-ui}

>[!NOTE]
>
>Esta seção descreve como ativar um lote para ingestão parcial em lote usando a interface do usuário. Se você já tiver ativado um lote para a ingestão parcial por lote usando a API, poderá pular para a próxima seção.

Para habilitar um lote para ingestão parcial por meio da interface do usuário [!DNL Platform], você pode criar um novo lote por meio de conexões de origem, criar um novo lote em um conjunto de dados existente ou criar um novo lote por meio do &quot;[!UICONTROL Mapear CSV para o fluxo XDM]&quot;.

### Criar uma nova conexão de origem {#new-source}

Para criar uma nova conexão de origem, siga as etapas listadas em [Visão geral das Fontes](../../sources/home.md). Depois de atingir a etapa **[!UICONTROL Detalhe do Fluxo de Dados]**, anote os campos **[!UICONTROL Inclusão parcial]** e **[!UICONTROL Diagnóstico de Erro]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

A alternância **[!UICONTROL ingestão parcial]** permite ativar ou desativar a utilização da ingestão parcial em lote.

A alternância **[!UICONTROL Diagnóstico de erro]** só aparece quando a alternância **[!UICONTROL ingestão parcial]** está desativada. Este recurso permite que [!DNL Platform] gere mensagens de erro detalhadas sobre os lotes ingeridos. Se a alternância **[!UICONTROL ingestão parcial]** estiver ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

O **[!UICONTROL Limite de erro]** permite definir a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

### Usar um conjunto de dados existente {#existing-dataset}

Para usar um conjunto de dados existente, selecione um start selecionando um conjunto de dados. A barra lateral à direita é preenchida com informações sobre o conjunto de dados.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

A alternância **[!UICONTROL ingestão parcial]** permite ativar ou desativar a utilização da ingestão parcial em lote.

A alternância **[!UICONTROL Diagnóstico de erro]** só aparece quando a alternância **[!UICONTROL ingestão parcial]** está desativada. Este recurso permite que [!DNL Platform] gere mensagens de erro detalhadas sobre os lotes ingeridos. Se a alternância **[!UICONTROL ingestão parcial]** estiver ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

O **[!UICONTROL Limite de erro]** permite definir a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

Agora, você pode fazer upload de dados usando o botão **Adicionar dados**, e eles serão ingeridos usando a ingestão parcial.

### Use o fluxo &quot;[!UICONTROL Mapear CSV para schema XDM]&quot; {#map-flow}

Para usar o fluxo &quot;[!UICONTROL Mapear CSV para o schema XDM]&quot;, siga as etapas listadas em [Mapear um arquivo CSV tutorial](../tutorials/map-a-csv-file.md). Depois de atingir a etapa **[!UICONTROL Adicionar dados]**, anote os campos **[!UICONTROL Inclusão parcial]** e **[!UICONTROL Diagnóstico de erro]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

A alternância **[!UICONTROL ingestão parcial]** permite ativar ou desativar a utilização da ingestão parcial em lote.

A alternância **[!UICONTROL Diagnóstico de erro]** só aparece quando a alternância **[!UICONTROL ingestão parcial]** está desativada. Este recurso permite que [!DNL Platform] gere mensagens de erro detalhadas sobre os lotes ingeridos. Se a alternância **[!UICONTROL ingestão parcial]** estiver ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL O limite de erros]** permite definir a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

## Próximas etapas {#next-steps}

Este tutorial aborda como criar ou modificar um conjunto de dados para permitir a ingestão parcial em lote. Para mais informações sobre a ingestão em lote, leia o [guia do desenvolvedor de ingestão em lote](./api-overview.md).

Para obter informações sobre como monitorar erros de ingestão parcial, leia o [guia de diagnóstico de erro de ingestão em lote](../quality/error-diagnostics.md).
