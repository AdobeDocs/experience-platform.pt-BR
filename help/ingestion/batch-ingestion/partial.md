---
keywords: Experience Platform;página inicial;tópicos populares;assimilação em lote;Assimilação em lote;assimilação parcial;Assimilação parcial;Recuperar erro;recuperar erro;Assimilação parcial em lote;Assimilação parcial em lote;assimilação;Assimilação;
solution: Experience Platform
title: Visão geral da assimilação parcial de lotes
description: Este documento fornece um tutorial para gerenciar a assimilação parcial de lotes.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: bc72f77b1b4a48126be9b49c5c663ff11e9054ea
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 9%

---

# Assimilação parcial de lote

A assimilação parcial de lotes é a capacidade de assimilar dados que contêm erros até um determinado limite. Com esse recurso, os usuários podem assimilar todos os dados corretos na Adobe Experience Platform com sucesso, enquanto todos os dados incorretos são armazenados em lote separadamente, juntamente com detalhes sobre o motivo da invalidade.

Este documento fornece um tutorial para gerenciar a assimilação parcial de lotes.

## Introdução

Este tutorial requer um conhecimento prático dos vários serviços da Adobe Experience Platform envolvidos com a assimilação parcial de lotes. Antes de iniciar este tutorial, revise a documentação dos seguintes serviços:

- [Assimilação em lote](./overview.md): o método que [!DNL Experience Platform] assimila e armazena dados de arquivos de dados, como CSV e Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs do [!DNL Experience Platform].

### Leitura de chamadas de API de amostra

Este manual fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas da [!DNL Experience Platform].

### Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para APIs da [!DNL Experience Platform], você deve concluir primeiro o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

## Ativar um lote para assimilação parcial de lotes na API {#enable-api}

>[!NOTE]
>
>Esta seção descreve como ativar um lote para assimilação parcial de lotes usando a API. Para obter instruções sobre como usar a interface, leia o [habilitar um lote para assimilação parcial de lotes na etapa da interface](#enable-ui).

Você pode criar um novo lote com a assimilação parcial ativada.

Para criar um novo lote, siga as etapas no [guia do desenvolvedor de assimilação em lote](./api-overview.md). Ao atingir a etapa **[!UICONTROL Create batch]**, adicione o seguinte campo no corpo da solicitação:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `enableErrorDiagnostics` | Um sinalizador que permite que o [!DNL Experience Platform] gere mensagens de erro detalhadas sobre o lote. |
| `partialIngestionPercent` | A porcentagem de erros aceitáveis antes que todo o lote falhe. Portanto, neste exemplo, no máximo 5% do lote podem ser erros, antes que falhe. |


## Ativar um lote para assimilação parcial de lotes na interface do usuário {#enable-ui}

>[!NOTE]
>
>Esta seção descreve como ativar um lote para assimilação parcial de lotes usando a interface do. Se você já tiver ativado um lote para assimilação parcial de lotes usando a API do, poderá pular para a próxima seção.

Para habilitar um lote para assimilação parcial por meio da interface do usuário do [!DNL Experience Platform], você pode criar um novo lote por meio de conexões de origem, criar um novo lote em um conjunto de dados existente ou criar um novo lote por meio do &quot;[!UICONTROL Map CSV to XDM flow]&quot;.

### Criar uma nova conexão de origem {#new-source}

Para criar uma nova conexão de origem, siga as etapas listadas na [Visão geral das fontes](../../sources/home.md). Depois de atingir a etapa **[!UICONTROL Dataflow detail]**, anote os campos **[!UICONTROL Partial ingestion]** e **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

O botão **[!UICONTROL Partial ingestion]** permite habilitar ou desabilitar o uso de assimilação parcial de lotes.

A opção de alternância **[!UICONTROL Error diagnostics]** aparece somente quando a opção de alternância **[!UICONTROL Partial ingestion]** está desativada. Este recurso permite que o [!DNL Experience Platform] gere mensagens de erro detalhadas sobre os lotes assimilados. Se a opção **[!UICONTROL Partial ingestion]** estiver ativada, o diagnóstico de erro aprimorado será aplicado automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

O **[!UICONTROL Error threshold]** permite definir a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

### Usar um conjunto de dados existente {#existing-dataset}

Para usar um conjunto de dados existente, comece selecionando um conjunto de dados. A barra lateral à direita é preenchida com informações sobre o conjunto de dados.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

O botão **[!UICONTROL Partial ingestion]** permite habilitar ou desabilitar o uso de assimilação parcial de lotes.

A opção de alternância **[!UICONTROL Error diagnostics]** aparece somente quando a opção de alternância **[!UICONTROL Partial ingestion]** está desativada. Este recurso permite que o [!DNL Experience Platform] gere mensagens de erro detalhadas sobre os lotes assimilados. Se a opção **[!UICONTROL Partial ingestion]** estiver ativada, o diagnóstico de erro aprimorado será aplicado automaticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

O **[!UICONTROL Error threshold]** permite definir a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

Agora é possível carregar dados usando o botão **Adicionar dados**, que será assimilado usando a assimilação parcial.

### Usar o fluxo &quot;[!UICONTROL Map CSV to XDM schema]&quot; {#map-flow}

Para usar o fluxo &quot;[!UICONTROL Map CSV to XDM schema]&quot;, siga as etapas listadas no [Tutorial de Mapear um arquivo CSV](../tutorials/map-csv/overview.md). Depois de atingir a etapa **[!UICONTROL Add data]**, anote os campos **[!UICONTROL Partial ingestion]** e **[!UICONTROL Error diagnostics]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

O botão **[!UICONTROL Partial ingestion]** permite habilitar ou desabilitar o uso de assimilação parcial de lotes.

A opção de alternância **[!UICONTROL Error diagnostics]** aparece somente quando a opção de alternância **[!UICONTROL Partial ingestion]** está desativada. Este recurso permite que o [!DNL Experience Platform] gere mensagens de erro detalhadas sobre os lotes assimilados. Se a opção **[!UICONTROL Partial ingestion]** estiver ativada, o diagnóstico de erro aprimorado será aplicado automaticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** permite definir a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

## Habilitar assimilação parcial e diagnóstico de erro para um fluxo de dados existente

Se um fluxo de dados no Experience Platform foi criado sem ativar a assimilação parcial ou o diagnóstico de erro, você ainda poderá ativar esses recursos sem recriar o fluxo. Ao habilitar a assimilação parcial e o diagnóstico de erro robusto, você pode melhorar muito a confiabilidade e a facilidade de solução de problemas em seus fluxos de trabalho de assimilação de dados. Leia as seções abaixo para saber como habilitar a assimilação parcial e o diagnóstico de erros para um fluxo de dados existente usando a API [!DNL Flow Service].

Por padrão, os fluxos de dados podem não ter assimilação parcial ou diagnóstico de erro ativado. Esses recursos são úteis para identificar e isolar problemas durante a assimilação de dados. Usando a API [!DNL Flow Service], você pode recuperar a configuração de fluxo de dados atual e aplicar as alterações necessárias usando uma solicitação PATCH.

Siga as etapas abaixo para ativar a assimilação parcial e o diagnóstico de erro para um fluxo de dados existente.

### Recuperar detalhes do fluxo

Para recuperar as configurações de fluxo de dados, faça uma solicitação GET para o ponto de extremidade `/flows/{FLOW_ID}` e forneça a ID do fluxo de dados. Para obter mais informações sobre como recuperar detalhes do fluxo de dados, consulte o guia [Atualizar fluxos de dados usando a [!DNL Flow Service] API](../../sources/tutorials/api/update-dataflows.md).

Não deixe de salvar o valor do campo `etag` retornado na resposta. Isso é necessário para que a solicitação de atualização garanta a consistência da versão.

### Atualizar configuração de fluxo

Em seguida, faça uma solicitação PATCH para o ponto de extremidade `/flows/` e forneça a ID do fluxo de dados para o qual você deseja habilitar a assimilação parcial e o diagnóstico de erros.

>[!IMPORTANT]
>
>- Inclua o valor `etag` salvo anteriormente no cabeçalho da solicitação usando a chave If-Match.
>- Você pode modificar o valor `partialIngestionPercent` para atender às suas necessidades específicas.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
        {
            "op": "add",
            "path": "/options",
            "value": {
                "partialIngestionPercent": "10"
            }
        },
        {
            "op": "add",
            "path": "/options/errorDiagnosticsEnabled",
            "value": true
        }
    ]'
```

**Resposta**

Uma resposta bem-sucedida retorna o `id` do fluxo de dados e um `etag` atualizado.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

### Verificar a atualização

Depois que a PATCH for concluída, faça uma solicitação do GET e recupere o fluxo de dados para verificar se as alterações foram concluídas com êxito.

**Formato da API**

```http
GET /flows/{FLOW_ID}
```

**Solicitação**

A solicitação a seguir recupera informações atualizadas sobre a ID de fluxo.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do fluxo de dados, confirmando que a assimilação parcial e o diagnóstico de erro agora estão habilitados na seção `options`.

```json
"options": {
    "partialIngestionPercent": 10,
    "errorDiagnosticsEnabled": true
}
```

## Próximas etapas {#next-steps}

Este tutorial abordou como criar ou modificar um conjunto de dados para permitir a assimilação parcial de lotes. Para obter mais informações sobre a assimilação em lote, leia o [guia do desenvolvedor de assimilação em lote](./api-overview.md).

Para obter informações sobre o monitoramento de erros de assimilação parcial, leia o [guia de diagnóstico de erros de assimilação em lote](../quality/error-diagnostics.md).
