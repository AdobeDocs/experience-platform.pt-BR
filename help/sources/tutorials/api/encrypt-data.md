---
title: Ingestão de dados criptografados
description: O Adobe Experience Platform permite assimilar arquivos criptografados por meio de fontes de lote de armazenamento em nuvem.
hide: true
hidefromtoc: true
source-git-commit: 526c9665843efaeb0e98423dc424a4193434f583
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 2%

---

# Assimilação de dados criptografados

O Adobe Experience Platform permite assimilar arquivos criptografados por meio de fontes de lote de armazenamento em nuvem. Com a assimilação de dados criptografados, você pode utilizar mecanismos de criptografia assimétricos para transferir com segurança dados em lote para o Experience Platform. Atualmente, os mecanismos de criptografia assimétrica compatíveis são PGP e GPG.

O processo de assimilação de dados criptografados é o seguinte:

1. [Criar um par de chaves de criptografia usando APIs do Experience Platform](#create-encryption-key-pair). O par de chaves de criptografia consiste em uma chave privada e uma chave pública. Depois de criada, é possível copiar ou baixar a chave pública, juntamente com a ID da chave pública correspondente e o Tempo de expiração. Durante esse processo, a chave privada será armazenada pelo Experience Platform em um cofre seguro.
2. Use a chave pública para criptografar o arquivo de dados que deseja assimilar.
3. Coloque o arquivo criptografado no armazenamento na nuvem.
4. Quando o arquivo criptografado estiver pronto, [criar uma conexão de origem e um fluxo de dados para a origem de armazenamento na nuvem](#create-a-dataflow-for-encrypted-data). Durante a etapa de criação do fluxo, é necessário fornecer um `encryption` e incluir a ID da chave pública.
5. O Experience Platform recupera a chave privada do cofre seguro para descriptografar os dados no momento da assimilação.

Este documento fornece etapas sobre como gerar um par de chaves de criptografia para criptografar seus dados e assimilar esses dados criptografados para o Experience Platform usando fontes de armazenamento em nuvem.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
   * [Fontes de armazenamento na nuvem](../api/collect/cloud-storage.md): Crie um fluxo de dados para trazer dados em lote da fonte de armazenamento em nuvem para o Experience Platform.
* [Sandboxes](../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../landing/api-guide.md).

## Criar par de chaves de criptografia {#create-encryption-key-pair}

A primeira etapa para assimilar dados criptografados no Experience Platform é criar seu par de chaves de criptografia fazendo uma solicitação de POST para o `/encryption/keys` endpoint da variável [!DNL Connectors] API.

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
| `params.passPhrase` | A senha fornece uma camada adicional de proteção para suas chaves de criptografia. Após a criação, o Experience Platform armazena a senha em um cofre seguro diferente da chave pública. Você deve fornecer uma string que não esteja vazia como senha. |

**Resposta**

Uma resposta bem-sucedida retorna sua chave pública, ID da chave pública e o tempo de expiração das chaves. O tempo de expiração é automaticamente definido como 180 dias após a data de geração da chave. No momento, a expiração não é configurável.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

## Conecte sua fonte de armazenamento em nuvem ao Experience Platform usando o [!DNL Flow Service] API

Depois de recuperar o par de chaves de criptografia, você pode continuar e criar uma conexão de origem para a fonte de armazenamento na nuvem e trazer seus dados criptografados para a Platform.

Primeiro, você deve criar uma conexão básica para autenticar sua fonte em relação à Plataforma. Para criar uma conexão básica e autenticar sua fonte, selecione a fonte que deseja usar na lista abaixo:

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Gen2 do Armazenamento Azure Data Lake](../api/create/cloud-storage/adls-gen2.md)
* [Armazenamento de Arquivos do Azure](../api/create/cloud-storage/azure-file-storage.md)
* [Zona de aterrissagem de dados](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Armazenamento em nuvem Google](../api/create/cloud-storage/google.md)
* [Armazenamento de objetos de oracle](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

Depois de criar uma conexão base, você deve seguir as etapas descritas no tutorial para [criação de uma conexão de origem para uma fonte de armazenamento em nuvem](../api/collect/cloud-storage.md) para criar uma conexão de origem, uma conexão de destino e um mapeamento.

## Criar um fluxo de dados para dados criptografados {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>Você deve ter o seguinte, para criar um fluxo de dados para a assimilação de dados criptografados:
>* [ID da chave pública](#create-encryption-key-pair)
>* [ID de conexão de origem](../api/collect/cloud-storage.md#source)
>* [ID de conexão do Target](../api/collect/cloud-storage.md#target)
>* [ID de mapeamento](../api/collect/cloud-storage.md#mapping)


Para criar um fluxo de dados, faça uma solicitação de POST para a função `/flows` endpoint da variável [!DNL Flow Service] API. Para assimilar dados criptografados, é necessário adicionar um `encryption` para `transformations` e inclua o `publicKeyId` que foi criado em uma etapa anterior.

**Formato da API**

```http
POST /flows
```

**Solicitação**

A solicitação a seguir cria um fluxo de dados para assimilar dados criptografados para uma fonte de armazenamento na nuvem.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Customer Data",
      "description: "ACME encrypted data ingestion",
      "flowSpec": {
          "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "26b53912-1005-49f0-b539-12100559f0e2"
      ],
      "targetConnectionIds": [
        "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                  "mappingVersion": 0
              }
          },
          {
              "name": "Encryption",
              "params": {
                  "publicKeyId": 512e686e-543e-4354-bcba-e1403ddcc532
          }
  }
      ],
      "scheduleParams": {
          "startTime": "1597784298",
          "frequency": "once"
      }
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `flowSpec.id` | A ID de especificação de fluxo que corresponde às fontes de armazenamento em nuvem. |
| `sourceConnectionIds` | A ID da conexão de origem. Essa ID representa a transferência de dados da origem para a plataforma. |
| `targetConnectionIds` | A ID de conexão do target. Essa ID representa o local para onde os dados chegam quando são trazidos para a Platform. |
| `transformations[x].params.mappingId` | A ID de mapeamento. |
| `transformations.name` | Ao assimilar arquivos criptografados, você deve fornecer `Encryption` como um parâmetro de transformações adicional para o fluxo de dados. |
| `transformations[x].params.publicKeyId` | A ID da chave pública que você criou. Essa ID é metade do par de chaves de criptografia usado para criptografar seus dados de armazenamento na nuvem. |
| `scheduleParams.startTime` | A hora de início do fluxo de dados em época. |
| `scheduleParams.frequency` | A frequência com que o fluxo de dados coletará dados. Os valores aceitáveis incluem: `once`, `minute`, `hour`, `day`ou `week`. |
| `scheduleParams.interval` | O intervalo designa o período entre duas execuções consecutivas de fluxo. O valor do intervalo deve ser um número inteiro diferente de zero. O intervalo não é necessário quando a frequência é definida como `once` e deve ser maior que ou igual a `15` para outros valores de frequência. |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado para seus dados criptografados.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um par de chaves de criptografia para seus dados de armazenamento em nuvem e um fluxo de dados para assimilar seus dados criptografados usando o [!DNL Flow Service API]. Para obter atualizações de status sobre a integridade, erros e métricas do seu fluxo de dados, leia o guia sobre [monitorar seu fluxo de dados usando o [!DNL Flow Service] API](./monitor.md).