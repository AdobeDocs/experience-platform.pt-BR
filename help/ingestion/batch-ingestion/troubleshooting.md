---
keywords: Experience Platform; home; tópicos populares; dados assimilados; solução de problemas; perguntas frequentes; Assimilação; Assimilação em lote; ingestão em lote;
solution: Experience Platform
title: Guia de solução de problemas de assimilação em lote
topic-legacy: troubleshooting
description: Essa documentação ajudará a responder às perguntas frequentes sobre as APIs de assimilação de dados em lote do Adobe Experience Platform.
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 1%

---

# Guia de solução de problemas de assimilação em lote

Esta documentação ajudará a responder perguntas frequentes sobre o Adobe Experience Platform [!DNL Batch Data Ingestion] APIs.

## Chamadas de API em lote

### Os lotes estão ativos imediatamente após receber um HTTP 200 OK da API CompleteBatch?

O `200 OK` resposta da API significa que o lote foi aceito para processamento; ele não está ativo até ser transferido para seu estado final, como Ativo ou Falha.

### É seguro repetir a chamada da API CompleteBatch após uma falha?

Sim - é seguro repetir a chamada da API. Apesar do fracasso, é possível que a operação tenha sido efetivamente bem sucedida e o lote tenha sido aceite com êxito. No entanto, espera-se que os clientes tenham mecanismos de repetição em caso de falha da API e, na verdade, são incentivados a tentar novamente. Se a operação realmente tiver êxito, a API retornará o sucesso, mesmo após tentar novamente.

### Quando a API de upload de arquivo grande deve ser usada?

O tamanho de arquivo recomendado para usar a API de upload de arquivo grande é de 256 MB ou maior. Encontre mais informações sobre como usar a API de upload de arquivo grande [here](./api-overview.md#ingest-large-parquet-files).

### Por que a chamada da API Large File Complete está falhando?

Se partes de um arquivo grande forem encontradas sobrepostas ou ausentes, o servidor responderá com uma Solicitação HTTP 400 inválida. Isso pode ocorrer porque é possível fazer upload de partes sobrepostas, já que as validações de intervalo são feitas no momento da conclusão do arquivo, quando os blocos de arquivo são agrupados.

## Suporte a assimilação

### Quais são os formatos de assimilação compatíveis?

Atualmente, o Parquet e o JSON são compatíveis. O CSV é compatível com base em legado, enquanto os dados serão promovidos para verificações principais e preliminares, nenhum recurso moderno, como conversão, particionamento ou validação de linha será suportado.

### Onde deve ser especificado o formato de entrada do lote?

O formato de entrada deve ser especificado no momento da criação do lote dentro da carga útil. Um exemplo de como especificar o formato de entrada de lote pode ser visto abaixo:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### Por que os dados carregados não estão aparecendo no conjunto de dados?

Para que os dados apareçam no conjunto de dados, o lote deve ser marcado como concluído. Todos os arquivos que você deseja assimilar devem ser carregados antes de marcar o lote como concluído. Um exemplo de marcação de um lote como concluído pode ser visto abaixo:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Como o JSON de várias linhas é assimilado?

Para assimilar JSON de várias linhas, a variável `isMultiLineJson` O sinalizador precisa ser definido no momento da criação do lote. Um exemplo disso pode ser visto abaixo:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### Qual é a diferença entre linhas JSON (JSON de linha única) e JSON de várias linhas?

Para linhas JSON, há um objeto JSON por linha. Por exemplo:

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

Para JSON de várias linhas, um objeto pode ocupar várias linhas, enquanto todos os objetos são vinculados em uma matriz JSON. Por exemplo:

```json
[
    {"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}},
    {"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}},
    {
        "string": "string3",
        "int": 3,
        "array": [
            3,
            6,
            9
        ],
        "dict": {
            "key": "value3",
            "extra_key": "extra_value3"
        }
    }
]
```

Por padrão, [!DNL Batch Data Ingestion] O usa JSON de linha única.

### A assimilação de CSV é compatível?

A assimilação de CSV só é compatível com esquemas simples. Atualmente, a assimilação de dados hierárquicos em CSV não é compatível.

Para obter todos os recursos de assimilação de dados, os formatos JSON ou Parquet precisam ser usados.

### Quais tipos de validação são executados nos dados?

Há três níveis de validação executados nos dados:

- Schema - Assimilação em lote garante que o esquema do dos dados assimilados corresponda ao esquema do conjunto de dados.
- Tipo de dados - A assimilação em lote garante que o tipo de cada campo assimilado corresponda ao tipo definido no esquema do conjunto de dados.
- Restrições - A assimilação em lote garante que as restrições, como &quot;Obrigatório&quot;, &quot;enum&quot; e &quot;formato&quot; sejam adequadamente definidas na definição do schema.

### Como substituir um lote já ingerido?

Um lote já assimilado pode ser substituído usando o recurso Reprodução em lote. Mais informações sobre a Reprodução em lote podem ser encontradas [here](./api-overview.md#replay-a-batch).

### Como é monitorizada a ingestão de lote?

Depois que um lote for sinalizado para promoção em lote, o progresso da assimilação em lote poderá ser monitorado com a seguinte solicitação:

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Com essa solicitação, você receberá uma resposta semelhante a esta:

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{IMS_ORG}",
        "created":1494349962314,
        "createdClient":"{API_KEY}",
        "createdUser":"{USER_ID}",
        "updatedUser":"{USER_ID}",
        "completed":1494349963467,
        "externalId":"{EXTERNAL_ID}",
        "status":"staging",
        "errors":[],
    }
}
```

## Estados do lote

### Quais são os possíveis estados em lote?

Um lote pode, em seu ciclo de vida, passar pelos seguintes estados:

| Status | Dados gravados no Principal | Descrição |
| ------ | ---------------------- | ----------- |
| Abandonado |  | O cliente não conseguiu concluir o lote no período de tempo esperado. |
| Abortado |  | O cliente chamou explicitamente, por meio da [!DNL Batch Data Ingestion] APIs, uma operação de anulação para o lote especificado. Quando um lote está no estado Carregado, o lote não pode ser anulado. |
| Ativo/Sucesso | x | O lote foi promovido com sucesso de estágio para principal e agora está disponível para consumo downstream. **Observação:** Ative e Success são usados alternadamente. |
| Arquivado |  | O lote foi arquivado no frigorífico. |
| Falha/Falha |  | Um estado de terminal que resulta de uma configuração incorreta e/ou dados incorretos. Um erro acionável é registrado, juntamente com o lote, para permitir que os clientes corrijam e reenviem os dados. **Observação:** Falha e Falha são usadas alternadamente. |
| Inativo | x | O lote foi promovido com êxito, mas foi revertido ou expirou. O lote não estará mais disponível para consumo downstream, mas os dados subjacentes permanecerão Principais até que tenham sido retidos, arquivados ou excluídos de outra forma. |
| Carregamento |  | No momento, o cliente está gravando dados para o lote. O lote é **not** pronto para promoção, neste momento. |
| Carregado |  | O cliente concluiu a gravação de dados para o lote. O lote está pronto para promoção. |
| Mantido |  | Os dados foram retirados do Principal e em um arquivo designado no Adobe Data Lake. |
| Armazenamento temporário |  | O cliente assinou com êxito o lote para promoção e os dados estão sendo preparados para consumo downstream. |
| Tentando novamente |  | O cliente sinalizou o lote para promoção, mas devido a um erro, o lote está sendo repetido por um serviço de Monitoramento de Lote. Esse estado pode ser usado para informar aos clientes que pode haver um atraso na assimilação dos dados. |
| Paralisado |  | O cliente assinou o lote para promoção, mas depois `n` novas tentativas por um serviço de Monitoramento em Lote, a promoção em lote foi paralisada. |

### O que significa &quot;Preparo&quot; para lotes?

Quando um lote está em &quot;Preparo&quot;, significa que o lote foi sinalizado com êxito para promoção e que os dados estão sendo preparados para consumo downstream.

### O que significa quando um lote está &quot;Tentando novamente&quot;?

Quando um lote está em &quot;Tentando novamente&quot;, significa que a assimilação de dados do lote foi temporariamente interrompida devido a problemas intermitentes. Quando isso acontece, não requer a intervenção do cliente.

### O que significa quando um lote está &quot;Paralisado&quot;?

Quando um lote está em &quot;Stalled&quot; (Paralisado), significa que [!DNL Data Ingestion Services] O está enfrentando dificuldades para assimilar o lote e todas as tentativas foram esgotadas.

### O que significa se um lote ainda estiver &quot;Carregando&quot;?

Quando um lote está em &quot;Carregamento&quot;, significa que a API CompleteBatch não foi chamada para promover o lote.

### Existe uma maneira de saber se um lote foi assimilado com êxito?

Quando o status do lote for &quot;Ativo&quot;, o lote será assimilado com êxito. Para descobrir o status do lote, siga as etapas detalhadas [before](#how-is-batch-ingestion-monitored).

### O que acontece depois que um lote falha?

Quando um lote falha, o motivo da falha pode ser identificado na variável `errors` da carga. Exemplos de erros podem ser vistos abaixo:

```json
    "errors":[
        {
            "code":"106",
            "description":"Dataset file is empty. Please upload file with data.",
            "rows":[]
        },
        {
            "code":"118",
            "description":"CSV file contains empty header row.",
            "rows":[]
        }
    ]
```

Depois que os erros forem corrigidos, o lote poderá ser carregado novamente.

## Suporte em lote

### Como os lotes devem ser excluídos?

Em vez de excluir diretamente de [!DNL Catalog], os lotes devem ser removidos usando qualquer um dos métodos fornecidos abaixo:

1. Se o lote estiver em andamento, o lote deve ser abortado.
2. Se o lote for dominado com êxito, o lote deve ser revertido.

### Quais métricas em nível de lote estão disponíveis?

As seguintes métricas em nível de lote estão disponíveis para lotes no estado Ativo/Sucesso:

| Métrica | Descrição |
| ------ | ----------- |
| inputByteSize | O número total de bytes preparados para [!DNL Data Ingestion Services] para processar. |
| inputRecordSize | O número total de linhas preparadas para [!DNL Data Ingestion Services] para processar. |
| outputByteSize | O número total de bytes enviados por [!DNL Data Ingestion Services] para [!DNL Data Lake]. |
| outputRecordSize | O número total de linhas geradas por [!DNL Data Ingestion Services] para [!DNL Data Lake]. |
| partitionCount | O número total de partições gravadas em [!DNL Data Lake]. |

### Por que as métricas não estão disponíveis em alguns lotes?

Existem dois motivos pelos quais as métricas podem não estar disponíveis em seu lote:

1. O lote nunca chegou ao estado Ativo/Sucesso.
2. O lote foi promovido usando um caminho de promoção herdado, como a assimilação de CSV.

### O que significam os diferentes códigos de status?

| Código de status | Descrição |
| ----------- | ----------- |
| 106 | O arquivo do conjunto de dados está vazio. |
| 118 | O arquivo CSV contém uma linha de cabeçalho vazia. |
| 200 | O lote foi aceito para processamento e será transferido para um estado final, como Ativo ou Falha. Uma vez submetido, o lote pode ser monitorizado utilizando o método `GetBatch` endpoint . |
| 400 | Solicitação inválida. Retornado se houver partes ausentes ou sobrepostas em um lote. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
