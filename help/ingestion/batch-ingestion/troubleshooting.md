---
keywords: Experience Platform;página inicial;tópicos populares;dados assimilados;solução de problemas;perguntas frequentes;Assimilação;Assimilação em lote;assimilação em lote;
solution: Experience Platform
title: Guia de solução de problemas de assimilação em lote
description: Esta documentação ajudará a responder às perguntas frequentes sobre as APIs de assimilação de dados em lote do Adobe Experience Platform.
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 1%

---

# Guia de solução de problemas de assimilação em lote

Esta documentação ajudará a responder perguntas frequentes sobre as APIs do Adobe Experience Platform [!DNL Batch Data Ingestion].

## Chamadas de API em lote

### Os lotes estão ativos imediatamente após receber um HTTP 200 OK da API CompleteBatch?

A resposta `200 OK` da API significa que o lote foi aceito para processamento - ele não estará ativo até passar para seu estado final, como Ativo ou Falha.

### É seguro repetir a chamada à API CompleteBatch após a falha?

Sim - é seguro tentar novamente a chamada da API. Apesar da falha, é possível que a operação tenha sido bem-sucedida e o lote tenha sido aceito com êxito. No entanto, espera-se que os clientes tenham mecanismos de repetição em caso de falha da API e, na verdade, são incentivados a tentar novamente. Se a operação for bem-sucedida, a API retornará com êxito, mesmo após uma nova tentativa.

### Quando a API de upload de arquivo grande deve ser usada?

O tamanho de arquivo recomendado para usar a API de Upload de arquivo grande é 256 MB ou maior. Mais informações sobre como usar a API de Carregamento de Arquivo Grande podem ser encontradas [aqui](./api-overview.md#ingest-large-parquet-files).

### Por que a chamada da API Large File Complete falha?

Se partes de um arquivo grande estiverem sobrepostas ou ausentes, o servidor responderá com uma solicitação HTTP 400 incorreta. Isso pode ocorrer porque é possível carregar partes sobrepostas, já que as validações de intervalo são feitas no momento da conclusão do arquivo, quando as partes do arquivo são unidas.

## Suporte para assimilação

### Quais são os formatos de assimilação compatíveis?

Atualmente, o Parquet e o JSON são compatíveis. O CSV é compatível com base no legado — embora os dados sejam promovidos para verificações principais e preliminares sejam feitas, nenhum recurso moderno, como conversão, particionamento ou validação de linha é compatível.

### Onde o formato de entrada de lote deve ser especificado?

O formato de entrada deve ser especificado no momento da criação do lote dentro da carga. Um exemplo de como especificar o formato de entrada de lote pode ser visto abaixo:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### Por que os dados carregados não aparecem no conjunto de dados?

Para que os dados apareçam no conjunto de dados, o lote deve ser marcado como concluído. Todos os arquivos que você deseja assimilar devem ser carregados antes de marcar o lote como concluído. Um exemplo de marcação de um lote como concluído pode ser visto abaixo:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Como o JSON multilinha é assimilado?

Para assimilar JSON multilinha, o sinalizador `isMultiLineJson` precisa ser definido no momento da criação do lote. Um exemplo disso pode ser visto abaixo:

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
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

Para JSON de várias linhas, um objeto pode ocupar várias linhas, enquanto todos os objetos são envolvidos em uma matriz JSON. Por exemplo:

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

### A assimilação de CSV é compatível?

A assimilação de CSV só é compatível com esquemas simples. Atualmente, a assimilação de dados hierárquicos em CSV não é suportada.

Para obter todos os recursos de assimilação de dados, é necessário usar os formatos JSON ou Parquet.

### Que tipos de validação são executados nos dados?

Há três níveis de validação executados nos dados:

- Esquema - A assimilação em lote garante que o esquema dos dados assimilados corresponda ao esquema do conjunto de dados.
- Tipo de dados - A assimilação em lote garante que o tipo de cada campo assimilado corresponda ao tipo definido no esquema do conjunto de dados.
- Restrições - A assimilação em lote garante que as restrições, como &quot;Obrigatório&quot;, &quot;enum&quot; e &quot;format&quot;, sejam definidas corretamente na definição do esquema.

### Como um lote já assimilado pode ser substituído?

Um lote já assimilado pode ser substituído usando o recurso Repetição de lote. Mais informações sobre a Repetição em Lote podem ser encontradas [aqui](./api-overview.md#replay-a-batch).

### Como a assimilação em lote é monitorada?

Depois que um lote tiver sido sinalizado para a promoção de lotes, o progresso da assimilação de lotes poderá ser monitorado com a seguinte solicitação:

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
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
        "imsOrg":"{ORG_ID}",
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

## Estados em lote

### Quais são os possíveis estados de lote?

Um lote pode, em seu ciclo de vida, passar pelos seguintes estados:

| Status | Dados gravados no Principal | Descrição |
| ------ | ---------------------- | ----------- |
| Abandonado | | O cliente falhou ao concluir o lote no período de tempo esperado. |
| Anulado | | O cliente chamou explicitamente, por meio das [!DNL Batch Data Ingestion] APIs, uma operação de anulação para o lote especificado. Quando um lote está no estado Carregado, ele não pode ser anulado. |
| Ativo/sucesso | x | O lote foi promovido com sucesso de estágio para mestre e agora está disponível para consumo downstream. **Observação:** Ativo e Êxito são usados alternadamente. |
| Arquivado | | O lote foi arquivado no armazenamento frio. |
| Com falha/Falha | | Um estado terminal que resulta de uma configuração incorreta e/ou de dados incorretos. Um erro acionável é registrado junto com o lote para permitir que os clientes corrijam e reenviem os dados. **Observação:** Falha e Falha são usadas alternadamente. |
| Inativo | x | O lote foi promovido com sucesso, mas foi revertido ou expirou. O lote não estará mais disponível para consumo downstream, mas os dados subjacentes permanecerão no Principal até que ele tenha sido retido, arquivado ou excluído de alguma outra forma. |
| Carregando | | No momento, o cliente está gravando dados para o lote. O lote **não** está pronto para promoção, neste momento. |
| Carregado | | O cliente concluiu a gravação de dados para o lote. O lote está pronto para promoção. |
| Retido | | Os dados foram removidos do Principal e em um arquivo designado no Adobe Data Lake. |
| Armazenamento temporário | | O cliente sinalizou com êxito o lote para promoção e os dados estão sendo preparados para consumo downstream. |
| Repetindo | | O cliente sinalizou o lote para promoção, mas devido a um erro, o lote está sendo repetido por um serviço de Monitoramento de Lote. Esse estado pode ser usado para informar aos clientes que pode haver um atraso na assimilação dos dados. |
| Paralisado | | O cliente sinalizou o lote para promoção, mas depois de `n` tentativas por um serviço de Monitoramento de Lote, a promoção do lote foi interrompida. |

### O que significa &quot;Preparo&quot; para lotes?

Quando um lote está em &quot;Preparo&quot;, significa que ele foi sinalizado com êxito para promoção e que os dados estão sendo preparados para consumo downstream.

### O que significa quando um lote está &quot;Repetindo&quot;?

Quando um lote está em &quot;Tentando novamente&quot;, significa que a assimilação de dados do lote foi temporariamente interrompida devido a problemas intermitentes. Quando isso acontece, não é necessária a intervenção do cliente.

### O que significa quando um lote é &quot;Paralisado&quot;?

Quando um lote está &quot;Interrompido&quot;, significa que [!DNL Data Ingestion Services] está tendo dificuldade para assimilar o lote e todas as tentativas foram esgotadas.

### O que significa se um lote ainda estiver &quot;Carregando&quot;?

Quando um lote está em &quot;Carregando&quot;, significa que a API CompleteBatch não foi chamada para promover o lote.

### Há alguma maneira de saber se um lote foi assimilado com êxito?

Sim, assim que o status do lote for &quot;Ativo&quot;, o lote foi assimilado com sucesso. Para saber o status do lote, siga as etapas detalhadas [anteriormente](#how-is-batch-ingestion-monitored).

### O que acontece depois que um lote falha? {#what-if-a-batch-fails}

Quando um lote falha, o processo é interrompido e retorna um status `Failure`. O motivo da falha pode ser identificado na seção `errors` da carga. Exemplos de erros podem ser vistos abaixo:

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

Depois que os erros forem corrigidos, o lote poderá ser recarregado.

## Suporte a lote

### Como os lotes devem ser excluídos?

Em vez de excluir diretamente de [!DNL Catalog], os lotes devem ser removidos usando qualquer um dos métodos fornecidos abaixo:

1. Se o lote estiver em andamento, ele deverá ser anulado.
2. Se o lote for dominado com êxito, ele deverá ser revertido.

### Quais métricas em nível de lote estão disponíveis?

As seguintes métricas em nível de lote estão disponíveis para lotes no estado Ativo/Sucesso:

| Métrica | Descrição |
| ------ | ----------- |
| inputByteSize | O número total de bytes preparados para processamento por [!DNL Data Ingestion Services]. |
| inputRecordSize | O número total de linhas preparadas para [!DNL Data Ingestion Services] serem processadas. |
| outputByteSize | O número total de bytes gerados por [!DNL Data Ingestion Services] para [!DNL Data Lake]. |
| outputRecordSize | O número total de linhas geradas por [!DNL Data Ingestion Services] para [!DNL Data Lake]. |
| partitionCount | O número total de partições gravadas em [!DNL Data Lake]. |

### Por que as métricas não estão disponíveis em alguns lotes?

Há dois motivos pelos quais as métricas podem não estar disponíveis em seu lote:

1. O lote nunca chegou com êxito ao estado Ativo/bem-sucedido.
2. O lote foi promovido usando um caminho de promoção herdado, como assimilação de CSV.

### O que significam os diferentes códigos de status?

| Código de status | Descrição |
| ----------- | ----------- |
| 106 | O arquivo de conjunto de dados está vazio. |
| 118 | O arquivo CSV contém uma linha de cabeçalho vazia. |
| 200 | O lote foi aceito para processamento e passará para um estado final, como Ativo ou Falha. Depois de enviado, o lote pode ser monitorado usando o endpoint `GetBatch`. |
| 400 | Solicitação inválida. Retornado se houver partes ausentes ou sobrepostas em um lote. |

`[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files`
