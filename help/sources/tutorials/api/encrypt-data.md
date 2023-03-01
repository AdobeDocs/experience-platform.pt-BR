---
title: Assimilação de dados criptografados
description: O Adobe Experience Platform permite assimilar arquivos criptografados por meio de fontes em lote de armazenamento na nuvem.
hide: true
hidefromtoc: true
source-git-commit: a1babf70a7a4e20f3e535741c95ac927597c9f48
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 2%

---

# Assimilação de dados criptografados

O Adobe Experience Platform permite assimilar arquivos criptografados por meio de fontes em lote de armazenamento na nuvem. Com a assimilação de dados criptografados, você pode aproveitar os mecanismos assimétricos de criptografia para transferir com segurança os dados em lote para o Experience Platform. Atualmente, os mecanismos de criptografia assimétrica compatíveis são PGP e GPG.

O processo de assimilação de dados criptografados é o seguinte:

1. [Criar um par de chaves de criptografia usando APIs Experience Platform](#create-encryption-key-pair). O par de chaves de criptografia consiste em uma chave privada e uma chave pública. Depois de criada, você pode copiar ou baixar a chave pública, juntamente com a ID da chave pública e o Tempo de expiração correspondentes. Durante esse processo, a chave privada será armazenada pelo Experience Platform em um cofre seguro. **NOTA:** A chave pública na resposta é codificada na Base64 e deve ser descriptografada antes do uso.
2. Use a chave pública para criptografar o arquivo de dados que você deseja assimilar.
3. Coloque o arquivo criptografado no armazenamento na nuvem.
4. Quando o arquivo criptografado estiver pronto, [crie uma conexão de origem e um fluxo de dados para sua fonte de armazenamento em nuvem](#create-a-dataflow-for-encrypted-data). Durante a etapa de criação do fluxo, você deve fornecer uma `encryption` e inclua a ID da chave pública.
5. Experience Platform recupera a chave privada do cofre seguro para descriptografar os dados no momento da assimilação.

>[!IMPORTANT]
>
>O tamanho máximo de um único arquivo criptografado é de 100 MB. Por exemplo, você pode assimilar dados de 2 GB em uma única execução de fluxo de dados. No entanto, qualquer arquivo individual nesses dados não pode exceder 100 MB.

Este documento fornece etapas sobre como gerar um par de chaves de criptografia para criptografar seus dados e assimilar esses dados criptografados no Experience Platform usando fontes de armazenamento na nuvem.

## Introdução

Este tutorial requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
   * [Fontes de armazenamento na nuvem](../api/collect/cloud-storage.md): crie um fluxo de dados para trazer dados em lote da fonte de armazenamento na nuvem para o Experience Platform.
* [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../landing/api-guide.md).

## Criar par de chaves de criptografia {#create-encryption-key-pair}

A primeira etapa na assimilação de dados criptografados no Experience Platform é criar seu par de chaves de criptografia fazendo uma solicitação POST para o `/encryption/keys` endpoint do [!DNL Connectors] API.

**Formato da API**

```http
POST /data/foundation/connectors/encryption/keys
```

**Solicitação**

A solicitação a seguir gera um par de chaves de criptografia usando o algoritmo de criptografia PGP.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| Parâmetro | Descrição |
| --- | --- |
| `encryptionAlgorithm` | O tipo de algoritmo de criptografia que você está usando. Os tipos de criptografia compatíveis são `PGP` e `GPG`. |
| `params.passPhrase` | A senha fornece uma camada adicional de proteção para suas chaves de criptografia. Após a criação, o Experience Platform armazena a senha em um cofre seguro diferente da chave pública. Você deve fornecer uma sequência de caracteres não vazia como senha. |

**Resposta**

Uma resposta bem-sucedida retorna a chave pública codificada na Base64, a ID da chave pública e o tempo de expiração das chaves. O tempo de expiração é automaticamente definido como 180 dias após a data de geração da chave. A hora de expiração não pode ser configurada no momento.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

## Conecte sua fonte de armazenamento em nuvem ao Experience Platform usando o [!DNL Flow Service] API

Depois de recuperar o par de chaves de criptografia, você pode continuar e criar uma conexão de origem para sua fonte de armazenamento na nuvem e trazer seus dados criptografados para a Platform.

Primeiro, você deve criar uma conexão base para autenticar sua origem na Platform. Para criar uma conexão base e autenticar sua origem, selecione a origem que deseja usar na lista abaixo:

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Armazenamento Azure Data Lake Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Armazenamento de arquivos do Azure](../api/create/cloud-storage/azure-file-storage.md)
* [Zona de aterrissagem de dados](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Armazenamento em nuvem Google](../api/create/cloud-storage/google.md)
* [Armazenamento de objetos de oracle](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

Depois de criar uma conexão básica, siga as etapas descritas no tutorial para [criando uma conexão de origem para uma origem de armazenamento na nuvem](../api/collect/cloud-storage.md) para criar uma conexão de origem, de destino e de mapeamento.

## Criar um fluxo de dados para dados criptografados {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>Você deve ter o seguinte para criar um fluxo de dados para assimilação de dados criptografados:
>* [ID da chave pública](#create-encryption-key-pair)
>* [ID da conexão de origem](../api/collect/cloud-storage.md#source)
>* [ID da conexão de destino](../api/collect/cloud-storage.md#target)
>* [ID do mapeamento](../api/collect/cloud-storage.md#mapping)


Para criar um fluxo de dados, faça uma solicitação POST ao `/flows` endpoint do [!DNL Flow Service] API. Para assimilar dados criptografados, é necessário adicionar um `encryption` para a `transformations` propriedade e incluir a `publicKeyId` criado em uma etapa anterior.

**Formato da API**

```http
POST /flows
```

**Solicitação**

A solicitação a seguir cria um fluxo de dados para assimilar dados criptografados de uma fonte de armazenamento na nuvem.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data",
    "description": "ACME Customer Data (Encrypted)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| Propriedade | Descrição |
| --- | --- |
| `flowSpec.id` | A ID de especificação do fluxo que corresponde às fontes de armazenamento na nuvem. |
| `sourceConnectionIds` | A ID da conexão de origem. Essa ID representa a transferência de dados da origem para a Platform. |
| `targetConnectionIds` | A ID da conexão de destino. Essa ID representa onde os dados são colocados depois de trazidos para a Platform. |
| `transformations[x].params.mappingId` | A ID do mapeamento. |
| `transformations.name` | Ao assimilar arquivos criptografados, você deve fornecer `Encryption` como parâmetro de transformações adicional para o fluxo de dados. |
| `transformations[x].params.publicKeyId` | A ID da chave pública que você criou. Essa ID é metade do par de chaves de criptografia usado para criptografar os dados de armazenamento na nuvem. |
| `scheduleParams.startTime` | A hora de início do fluxo de dados em época. |
| `scheduleParams.frequency` | A frequência com que o fluxo de dados coletará dados. Os valores aceitáveis incluem: `once`, `minute`, `hour`, `day`ou `week`. |
| `scheduleParams.interval` | O intervalo designa o período entre duas execuções de fluxo consecutivas. O valor do intervalo deve ser um inteiro diferente de zero. O intervalo não é necessário quando a frequência está definida como `once` e deve ser maior ou igual a `15` para outros valores de frequência. |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado para seus dados criptografados.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou um par de chaves de criptografia para seus dados de armazenamento na nuvem e um fluxo de dados para assimilar seus dados criptografados usando o [!DNL Flow Service API]. Para obter atualizações de status sobre a integridade, os erros e as métricas do fluxo de dados, leia o guia na [monitoramento do fluxo de dados usando o [!DNL Flow Service] API](./monitor.md).