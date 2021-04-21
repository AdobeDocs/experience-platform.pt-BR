---
keywords: Experience Platform, home, tópicos populares, ingestão em lote, ingestão em lote, ingestão parcial, ingestão parcial, erro de recuperação, erro de recuperação, ingestão parcial em lote, ingestão parcial em lote, parcial, ingestão, ingestão; ingestão;
solution: Experience Platform
title: Visão geral da assimilação parcial de lote
topic-legacy: overview
description: Este documento fornece um tutorial para gerenciar a assimilação parcial de lote.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Ingestão parcial por lote

A assimilação parcial em lote é a capacidade de assimilar dados que contêm erros, até um determinado limite. Com esse recurso, os usuários podem assimilar com êxito todos os dados corretos no Adobe Experience Platform, enquanto todos os dados incorretos são armazenados em lote separadamente, juntamente com detalhes sobre o motivo pelo qual são inválidos.

Este documento fornece um tutorial para gerenciar a assimilação parcial de lote.

## Introdução

Este tutorial requer um conhecimento prático dos vários serviços da Adobe Experience Platform envolvidos com a assimilação parcial em lote. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [Ingestão](./overview.md) em lote: O método que  [!DNL Platform] assimila e armazena dados de arquivos de dados, como CSV e Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs [!DNL Platform].

### Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

## Habilite um lote para assimilação parcial de lote na API {#enable-api}

>[!NOTE]
>
>Esta seção descreve como habilitar um lote para assimilação parcial de lote usando a API. Para obter instruções sobre como usar a interface do usuário, leia a etapa [ativar um lote para assimilação parcial de lote na interface do usuário](#enable-ui).

Você pode criar um novo lote com a assimilação parcial ativada.

Para criar um novo lote, siga as etapas no [guia do desenvolvedor de assimilação de lote](./api-overview.md). Depois de atingir a etapa **[!UICONTROL Create batch]**, adicione o seguinte campo no corpo da solicitação:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `enableErrorDiagnostics` | Um sinalizador que permite que [!DNL Platform] gere mensagens de erro detalhadas sobre seu lote. |
| `partialIngestionPercentage` | A porcentagem de erros aceitáveis antes que todo o lote falhe. Portanto, neste exemplo, um máximo de 5% do lote pode ser de erros, antes que falhe. |


## Habilite um lote para a assimilação em lote parcial na interface do usuário {#enable-ui}

>[!NOTE]
>
>Esta seção descreve como habilitar um lote para a assimilação em lote parcial usando a interface do usuário do . Se você já tiver ativado um lote para assimilação parcial de lote usando a API, poderá pular para a próxima seção.

Para habilitar um lote para assimilação parcial por meio da interface [!DNL Platform], você pode criar um novo lote por meio de conexões de origem, criar um novo lote em um conjunto de dados existente ou criar um novo lote por meio do &quot;[!UICONTROL Map CSV to XDM flow]&quot;.

### Criar uma nova conexão de origem {#new-source}

Para criar uma nova conexão de origem, siga as etapas listadas no [Sources overview](../../sources/home.md). Depois de atingir a etapa **[!UICONTROL Dataflow detail]**, anote os campos **[!UICONTROL Partial ingestion]** e **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

A opção **[!UICONTROL Partial ingestion]** permite ativar ou desativar o uso de assimilação parcial de lote.

A opção **[!UICONTROL Error diagnostics]** só aparece quando o botão **[!UICONTROL Partial ingestion]** está desligado. Esse recurso permite que [!DNL Platform] gere mensagens de erro detalhadas sobre seus lotes assimilados. Se a opção **[!UICONTROL Partial ingestion]** estiver ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

O **[!UICONTROL Error threshold]** permite definir a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

### Usar um conjunto de dados existente {#existing-dataset}

Para usar um conjunto de dados existente, comece selecionando um conjunto de dados. A barra lateral à direita é preenchida com informações sobre o conjunto de dados.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

A opção **[!UICONTROL Partial ingestion]** permite ativar ou desativar o uso de assimilação parcial de lote.

A opção **[!UICONTROL Error diagnostics]** só aparece quando o botão **[!UICONTROL Partial ingestion]** está desligado. Esse recurso permite que [!DNL Platform] gere mensagens de erro detalhadas sobre seus lotes assimilados. Se a opção **[!UICONTROL Partial ingestion]** estiver ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

O **[!UICONTROL Error threshold]** permite definir a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

Agora, você pode fazer upload de dados usando o botão **Add data** e eles serão assimilados usando a assimilação parcial.

### Use o fluxo &quot;[!UICONTROL Map CSV to XDM schema]&quot; {#map-flow}

Para usar o fluxo &quot;[!UICONTROL Map CSV to XDM schema]&quot;, siga as etapas listadas no [Tutorial Mapear um arquivo CSV](../tutorials/map-a-csv-file.md). Depois de atingir a etapa **[!UICONTROL Add data]**, anote os campos **[!UICONTROL Partial ingestion]** e **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

A opção **[!UICONTROL Partial ingestion]** permite ativar ou desativar o uso de assimilação parcial de lote.

A opção **[!UICONTROL Error diagnostics]** só aparece quando o botão **[!UICONTROL Partial ingestion]** está desligado. Esse recurso permite que [!DNL Platform] gere mensagens de erro detalhadas sobre seus lotes assimilados. Se a opção **[!UICONTROL Partial ingestion]** estiver ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** permite definir a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

## Próximas etapas {#next-steps}

Este tutorial aborda como criar ou modificar um conjunto de dados para permitir a assimilação em lote parcial. Para obter mais informações sobre a ingestão em lote, leia o [guia do desenvolvedor de ingestão em lote](./api-overview.md).

Para obter informações sobre como monitorar erros de ingestão parcial, leia o [guia de diagnóstico de erro de ingestão em lote](../quality/error-diagnostics.md).
