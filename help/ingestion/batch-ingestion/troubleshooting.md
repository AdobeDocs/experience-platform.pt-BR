---
keywords: Experience Platform;home;popular topics;ingested data
solution: Experience Platform
title: Guia de solução de problemas de ingestão em lote Adobe Experience Platform
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 9766cadee83e81bacc2abe6b13342ac95aae19a9
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 1%

---


# Guia de solução de problemas de ingestão em lote

Esta documentação ajudará a responder a perguntas frequentes sobre [!DNL Batch Data Ingestion] APIs da Adobe Experience Platform.

## Chamadas de API em lote

### Os lotes estão imediatamente ativos após receber um HTTP 200 OK da API CompleteBatch?

A `200 OK` resposta da API significa que o lote foi aceito para processamento - não está ativo até que ele seja transição para seu estado final, como Ativo ou Falha.

### É seguro repetir a chamada CompleteBatch da API depois que ela falhar?

Sim - é seguro repetir a chamada da API. Apesar do fracasso, é possível que a operação tenha realmente êxito e o lote tenha sido aceite com êxito. No entanto, espera-se que os clientes tenham mecanismos de repetição em caso de falha da API e, na verdade, sejam encorajados a tentar novamente. Se a operação realmente tiver êxito, a API retornará com sucesso, mesmo depois de tentar novamente.

### Quando a API de Upload de Arquivo Grande deve ser usada?

O tamanho de arquivo recomendado para usar a API de Upload de Arquivo Grande é de 256 MB ou maior. Mais informações sobre como usar a API de carregamento de arquivo grande podem ser encontradas [aqui](./api-overview.md#ingest-large-parquet-files).

### Por que a chamada API Large File Complete está falhando?

Se partes de um arquivo grande forem encontradas sobrepostas ou ausentes, o servidor responderá com uma solicitação HTTP 400 incorreta. Isso pode ocorrer porque é possível fazer upload de partes sobrepostas, já que as validações de intervalo são feitas no momento da conclusão do arquivo, quando os blocos do arquivo são agrupados.

## Suporte a ingestão

### Quais são os formatos de assimilação compatíveis?

Atualmente, o Parquet e o JSON são suportados. O CSV é suportado em uma base herdada - enquanto os dados serão promovidos para verificações principais e preliminares, nenhum recurso moderno, como conversão, particionamento ou validação de linha será suportado.

### Onde deve ser especificado o formato de entrada do lote?

O formato de entrada deve ser especificado na hora de criação do lote dentro da carga. Um exemplo de como especificar o formato de entrada em lote pode ser visto abaixo:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### Por que os dados carregados não aparecem no conjunto de dados?

Para que os dados sejam exibidos no conjunto de dados, o lote deve ser marcado como concluído. Todos os arquivos que você deseja assimilar devem ser carregados antes de marcar o lote como concluído. Um exemplo de marcação de um lote como concluído pode ser visto abaixo:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Como o JSON de várias linhas é ingerido?

Para assimilar JSON de várias linhas, o sinalizador `isMultiLineJson` precisa ser definido no momento da criação do lote. Um exemplo disso pode ser visto abaixo:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
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

Por padrão, [!DNL Batch Data Ingestion] usa JSON de linha única.

### A ingestão de CSV é suportada?

A ingestão de CSV só é suportada para schemas simples. Atualmente, não há suporte para a assimilação de dados hierárquicos em CSV.

Para obter todos os recursos de ingestão de dados, é necessário usar formatos JSON ou Parquet.

### Que tipos de validação são executados nos dados?

Há três níveis de validação executados nos dados:

- Schema - A ingestão em lote garante que o schema dos dados ingeridos corresponda ao schema do conjunto de dados.
- Tipo de dados - A ingestão em lote garante que o tipo para cada campo ingerido corresponda ao tipo definido no schema do conjunto de dados.
- Restrições - A ingestão em lote garante que as restrições, como &quot;Obrigatório&quot;, &quot;enumerado&quot; e &quot;formato&quot;, sejam adequadamente definidas na definição do schema.

### Como substituir um lote já ingerido?

Um lote já ingerido pode ser substituído usando o recurso Repetição em lote. Mais informações sobre a Repetição em lote podem ser encontradas [aqui](./api-overview.md#replay-a-batch).

### Como é monitorizada a ingestão em lote?

Depois que um lote é sinalizado para promoção em lote, o progresso da ingestão em lote pode ser monitorado com a seguinte solicitação:

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
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

## Estados de lote

### Quais são os possíveis estados de lote?

Um lote pode, em seu ciclo de vida, passar pelos seguintes estados:

| Status | Dados escritos para Principal | Descrição |
| ------ | ---------------------- | ----------- |
| Abandonado |  | O cliente não conseguiu concluir o lote no período de tempo esperado. |
| Abortado |  | O cliente chamou explicitamente, por meio das [!DNL Batch Data Ingestion] APIs, uma operação de anulação para o lote especificado. Quando um lote está no estado Carregado, o lote não pode ser abortado. |
| Ativo/Sucesso | x | O lote foi promovido com sucesso do estágio para o principal e agora está disponível para consumo a jusante. **Observação:** Ativo e bem-sucedido são usados alternadamente. |
| Arquivado |  | O lote foi arquivado em armazenamento frio. |
| Falha/falha |  | Um estado de terminal que resulta de uma configuração incorreta e/ou de dados inválidos. Um erro acionável é registrado, juntamente com o lote, para permitir que os clientes corrijam e reenviem os dados. **Observação:** Falha e Falha são usadas alternadamente. |
| Inativo | x | O lote foi promovido com êxito, mas foi revertido ou expirou. O lote não estará mais disponível para consumo downstream, mas os dados subjacentes permanecerão Principais até que tenham sido retidos, arquivados ou excluídos de outra forma. |
| Carregando |  | O cliente está gravando dados para o lote no momento. O lote **não** está pronto para promoção nesse momento. |
| Carregado |  | O cliente concluiu a gravação de dados para o lote. O lote está pronto para promoção. |
| Retenção |  | Os dados foram retirados do Principal e em um arquivo designado no Adobe Data Lake. |
| Armazenamento temporário |  | O cliente assinou com êxito o lote para promoção, e os dados estão sendo preparados para consumo a jusante. |
| Tentando novamente |  | O cliente assinou o lote para promoção, mas devido a um erro, o lote está sendo tentado novamente por um serviço de Monitoramento em lote. Esse estado pode ser usado para informar aos clientes que pode haver um atraso na assimilação dos dados. |
| Parado |  | O cliente assinou o lote para promoção, mas após `n` tentativas por um serviço de Monitoramento em lote, a promoção em lote parou. |

### O que significa &quot;armazenamento temporário&quot; para lotes?

Quando um lote está em &quot;Preparação&quot;, isso significa que o lote foi sinalizado com êxito para promoção e que os dados estão sendo preparados para consumo a jusante.

### O que significa quando um lote é &quot;Tentando novamente&quot;?

Quando um lote está em &quot;Tentando novamente&quot;, isso significa que a ingestão de dados do lote foi interrompida temporariamente devido a problemas intermitentes. Quando isso acontece, não requer intervenção do cliente.

### O que significa quando um lote está &quot;parado&quot;?

Quando um lote está em &quot;Parado&quot;, isso significa que [!DNL Data Ingestion Services] há dificuldade em ingerir o lote e todas as tentativas estão esgotadas.

### O que significa se um lote ainda estiver &quot;Carregando&quot;?

Quando um lote está em &quot;Carregamento&quot;, isso significa que a API CompleteBatch não foi chamada para promover o lote.

### Existe alguma forma de saber se um lote foi ingerido com êxito?

Quando o status do lote for &quot;Ativo&quot;, o lote será ingerido com êxito. Para descobrir o status do lote, siga as etapas detalhadas [anteriormente](#how-is-batch-ingestion-monitored).

### O que acontece depois de um lote falhar?

Quando um lote falha, o motivo da falha pode ser identificado na `errors` seção da carga. Exemplos de erros podem ser vistos abaixo:

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

Em vez de eliminar diretamente do [!DNL Catalog], os lotes devem ser removidos utilizando um dos métodos abaixo indicados:

1. Se o lote estiver em andamento, o lote deve ser abortado.
2. Se o lote for dominado com êxito, o lote deve ser revertido.

### Quais métricas em nível de lote estão disponíveis?

As seguintes métricas em nível de lote estão disponíveis para lotes no estado Ativo/Sucesso:

| Métrica | Descrição |
| ------ | ----------- |
| inputByteSize | O número total de bytes preparados para [!DNL Data Ingestion Services] processamento. |
| inputRecordSize | O número total de linhas preparadas para [!DNL Data Ingestion Services] processamento. |
| outputByteSize | O número total de bytes gerados por [!DNL Data Ingestion Services] até [!DNL Data Lake]. |
| outputRecordSize | O número total de linhas distribuídas por [!DNL Data Ingestion Services] até [!DNL Data Lake]. |
| partitionCount | O número total de partições gravadas em [!DNL Data Lake]. |

### Por que as métricas não estão disponíveis em alguns lotes?

Há dois motivos para as métricas não estarem disponíveis no lote:

1. O lote nunca chegou ao estado Ativo/Sucesso.
2. O lote foi promovido usando um caminho de promoção herdado, como a ingestão de CSV.

### O que significam os diferentes códigos de status?

| Código de status | Descrição |
| ----------- | ----------- |
| 106 | O arquivo de conjunto de dados está vazio. |
| 118 | O arquivo CSV contém uma linha de cabeçalho vazia. |
| 200 | O lote foi aceito para processamento e será transição para um estado final, como Ativo ou Falha. Depois de submetido, o lote pode ser monitorizado usando o `GetBatch` endpoint. |
| 400 | Solicitação inválida. Retornado se houver partes ausentes ou sobrepostas em um lote. |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
