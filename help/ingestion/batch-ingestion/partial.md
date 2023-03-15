---
keywords: Experience Platform;página inicial;tópicos populares;assimilação em lote;Assimilação em lote;assimilação parcial;Assimilação parcial;Recuperar erro;recuperar erro;Assimilação parcial em lote;Assimilação parcial em lote;assimilação;Assimilação;
solution: Experience Platform
title: Visão geral da assimilação parcial de lotes
description: Este documento fornece um tutorial para gerenciar a assimilação parcial de lotes.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# Assimilação parcial de lote

A assimilação parcial de lotes é a capacidade de assimilar dados que contêm erros até um determinado limite. Com esse recurso, os usuários podem assimilar todos os dados corretos na Adobe Experience Platform com sucesso, enquanto todos os dados incorretos são armazenados em lote separadamente, juntamente com detalhes sobre o motivo da invalidade.

Este documento fornece um tutorial para gerenciar a assimilação parcial de lotes.

## Introdução

Este tutorial requer um conhecimento prático dos vários serviços da Adobe Experience Platform envolvidos com a assimilação parcial de lotes. Antes de iniciar este tutorial, revise a documentação dos seguintes serviços:

- [Assimilação em lote](./overview.md): o método que [!DNL Platform] A assimila e armazena dados de arquivos de dados, como CSV e Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para o [!DNL Platform] APIs.

### Leitura de chamadas de API de amostra

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para [!DNL Platform] APIs, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos os [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

## Ativar um lote para assimilação parcial de lotes na API {#enable-api}

>[!NOTE]
>
>Esta seção descreve como ativar um lote para assimilação parcial de lotes usando a API. Para obter instruções sobre como usar a interface do usuário, leia o [habilitar um lote para assimilação parcial de lotes na interface do usuário](#enable-ui) etapa.

Você pode criar um novo lote com a assimilação parcial ativada.

Para criar um novo lote, siga as etapas da seção [guia do desenvolvedor de assimilação em lote](./api-overview.md). Depois de alcançar o **[!UICONTROL Criar lote]** adicione o seguinte campo no corpo da solicitação:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `enableErrorDiagnostics` | Um sinalizador que permite [!DNL Platform] para gerar mensagens de erro detalhadas sobre o lote. |
| `partialIngestionPercent` | A porcentagem de erros aceitáveis antes que todo o lote falhe. Portanto, neste exemplo, no máximo 5% do lote podem ser erros, antes que falhe. |


## Ativar um lote para assimilação parcial de lotes na interface do usuário {#enable-ui}

>[!NOTE]
>
>Esta seção descreve como ativar um lote para assimilação parcial de lotes usando a interface do. Se você já tiver ativado um lote para assimilação parcial de lotes usando a API do, poderá pular para a próxima seção.

Para ativar um lote para assimilação parcial por meio da [!DNL Platform] Na interface do usuário, você pode criar um novo lote por meio de conexões de origem, criar um novo lote em um conjunto de dados existente ou criar um novo lote por meio da &quot;[!UICONTROL Mapear CSV para fluxo XDM]&quot;.

### Criar uma nova conexão de origem {#new-source}

Para criar uma nova conexão de origem, siga as etapas listadas no [Visão geral das fontes](../../sources/home.md). Depois de alcançar o **[!UICONTROL Detalhes do fluxo de dados]** etapa, tome nota da **[!UICONTROL Assimilação parcial]** e **[!UICONTROL Diagnóstico de erro]** campos.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

A variável **[!UICONTROL Assimilação parcial]** ativar/desativar permite ativar ou desativar o uso de assimilação parcial de lotes.

A variável **[!UICONTROL Diagnóstico de erro]** alternar só aparece quando a variável **[!UICONTROL Assimilação parcial]** está desativado. Esse recurso permite [!DNL Platform] para gerar mensagens de erro detalhadas sobre os lotes assimilados. Se a variável **[!UICONTROL Assimilação parcial]** for ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

A variável **[!UICONTROL Limite de erro]** permite que você defina a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

### Usar um conjunto de dados existente {#existing-dataset}

Para usar um conjunto de dados existente, comece selecionando um conjunto de dados. A barra lateral à direita é preenchida com informações sobre o conjunto de dados.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

A variável **[!UICONTROL Assimilação parcial]** ativar/desativar permite ativar ou desativar o uso de assimilação parcial de lotes.

A variável **[!UICONTROL Diagnóstico de erro]** alternar só aparece quando a variável **[!UICONTROL Assimilação parcial]** está desativado. Esse recurso permite [!DNL Platform] para gerar mensagens de erro detalhadas sobre os lotes assimilados. Se a variável **[!UICONTROL Assimilação parcial]** for ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

A variável **[!UICONTROL Limite de erro]** permite que você defina a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

Agora, é possível fazer upload de dados usando o **Adicionar dados** e será assimilado usando a assimilação parcial.

### Use o &quot;[!UICONTROL Mapear CSV para esquema XDM]Fluxo &quot; {#map-flow}

Para usar o &quot;[!UICONTROL Mapear CSV para esquema XDM]&quot;, siga as etapas listadas no [Mapear um tutorial de arquivo CSV](../tutorials/map-csv/overview.md). Depois de alcançar o **[!UICONTROL Adicionar dados]** etapa, tome nota da **[!UICONTROL Assimilação parcial]** e **[!UICONTROL Diagnóstico de erro]** campos.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

A variável **[!UICONTROL Assimilação parcial]** ativar/desativar permite ativar ou desativar o uso de assimilação parcial de lotes.

A variável **[!UICONTROL Diagnóstico de erro]** alternar só aparece quando a variável **[!UICONTROL Assimilação parcial]** está desativado. Esse recurso permite [!DNL Platform] para gerar mensagens de erro detalhadas sobre os lotes assimilados. Se a variável **[!UICONTROL Assimilação parcial]** for ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Limite de erro]** permite que você defina a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

## Próximas etapas {#next-steps}

Este tutorial abordou como criar ou modificar um conjunto de dados para permitir a assimilação parcial de lotes. Para obter mais informações sobre assimilação em lote, leia a [guia do desenvolvedor de assimilação em lote](./api-overview.md).

Para obter informações sobre o monitoramento de erros de assimilação parcial, leia o [guia de diagnóstico de erro de assimilação em lote](../quality/error-diagnostics.md).
