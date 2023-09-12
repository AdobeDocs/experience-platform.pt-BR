---
title: Assimilação de dados criptografados
description: Saiba como assimilar arquivos criptografados por meio de fontes de lote de armazenamento na nuvem usando a API.
hide: true
hidefromtoc: true
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: cd8844121fef79205d57fa979ca8630fc1b1ece4
workflow-type: tm+mt
source-wordcount: '1473'
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
>O tamanho máximo de um único arquivo criptografado é de 1 GB. Por exemplo, você pode assimilar dados de 2 GBs em uma única execução de fluxo de dados. No entanto, qualquer arquivo individual nesses dados não pode exceder 1 GB.

Este documento fornece etapas sobre como gerar um par de chaves de criptografia para criptografar seus dados e assimilar esses dados criptografados no Experience Platform usando fontes de armazenamento na nuvem.

## Introdução

Este tutorial requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
   * [Fontes de armazenamento na nuvem](../api/collect/cloud-storage.md): crie um fluxo de dados para trazer dados em lote da fonte de armazenamento na nuvem para o Experience Platform.
* [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../landing/api-guide.md).

### Extensões de arquivo compatíveis com arquivos criptografados

A lista de extensões de arquivo compatíveis com arquivos criptografados é a seguinte:

* .csv
* .tsv
* .json
* .parquet
* .csv.gpg
* .tsv.gpg
* .json.gpg
* .parquet.gpg
* .csv.pgp
* .tsv.pgp
* .json.pgp
* .parquet.pgp
* .gpg
* .pgp

>[!NOTE]
>
>A assimilação de arquivos criptografados em fontes do Adobe Experience Platform suporta o openPGP e não qualquer versão proprietária específica do PGP.

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

| Propriedade | Descrição |
| --- | --- |
| `publicKey` | A chave pública é usada para criptografar os dados no armazenamento na nuvem. Essa chave corresponde à chave privada que também foi criada durante essa etapa. No entanto, a chave privada vai imediatamente para Experience Platform. |
| `publicKeyId` | A ID da chave pública é usada para criar um fluxo de dados e assimilar os dados criptografados do armazenamento na nuvem no Experience Platform. |
| `expiryTime` | O tempo de expiração define a data de expiração do par de chaves de criptografia. Essa data é definida automaticamente para 180 dias após a data de geração da chave e é exibida no formato de carimbo de data e hora unix. |

+++(Opcional) Criar par de chaves de verificação de assinatura para dados assinados

### Criar par de chaves gerenciado pelo cliente

Opcionalmente, é possível criar um par de chaves de verificação de assinatura para assinar e assimilar os dados criptografados.

Durante esse estágio, você deve gerar sua própria combinação de chave privada e chave pública e usar sua chave privada para assinar seus dados criptografados. Em seguida, você deve codificar sua chave pública em Base64 e, em seguida, compartilhá-la no Experience Platform para que a Platform verifique sua assinatura.

### Compartilhar sua chave pública no Experience Platform

Para compartilhar sua chave pública, faça uma solicitação POST para o `/customer-keys` ao fornecer seu algoritmo de criptografia e sua chave pública codificada na Base64.

**Formato da API**

```http
POST /data/foundation/connectors/encryption/customer-keys
```

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": {{ENCRYPTION_ALGORITHM}},       
      "publicKey": {{BASE_64_ENCODED_PUBLIC_KEY}}
    }'
```

| Parâmetro | Descrição |
| --- | --- |
| `encryptionAlgorithm` | O tipo de algoritmo de criptografia que você está usando. Os tipos de criptografia compatíveis são `PGP` e `GPG`. |
| `publicKey` | A chave pública que corresponde às chaves gerenciadas pelo cliente usadas para assinar o criptografado. Essa chave deve ser codificada na Base64. |

**Resposta**

```json
{    
  "publicKeyId": "e31ae895-7896-469a-8e06-eb9207ddf1c2" 
} 
```

| Propriedade | Descrição |
| --- | --- |
| `publicKeyId` | Essa ID de chave pública é retornada em resposta ao compartilhamento da chave gerenciada pelo cliente com o Experience Platform. Você pode fornecer essa ID de chave pública como a ID de chave de verificação de assinatura ao criar um fluxo de dados para dados assinados e criptografados. |

+++

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
>
>* [ID da chave pública](#create-encryption-key-pair)
>* [ID da conexão de origem](../api/collect/cloud-storage.md#source)
>* [ID da conexão de destino](../api/collect/cloud-storage.md#target)
>* [ID de mapeamento](../api/collect/cloud-storage.md#mapping)

Para criar um fluxo de dados, faça uma solicitação POST ao `/flows` endpoint do [!DNL Flow Service] API. Para assimilar dados criptografados, é necessário adicionar um `encryption` para a `transformations` propriedade e incluir a `publicKeyId` criado em uma etapa anterior.

**Formato da API**

```http
POST /flows
```

**Solicitação**

>[!BEGINTABS]

>[!TAB Criar um fluxo de dados para assimilação de dados criptografados]

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


>[!TAB Criar um fluxo de dados para assimilar dados criptografados e assinados]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data (with Sign Verification)",
    "description": "ACME Customer Data (with Sign Verification)",
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
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17",
                "signVerificationKeyId":"e31ae895-7896-469a-8e06-eb9207ddf1c2"
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
| `params.signVerificationKeyId` | A ID da chave de verificação de sinal é a mesma que a ID da chave pública que foi recuperada após compartilhar sua chave pública codificada em Base64 com o Experience Platform. |

>[!ENDTABS]

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado para seus dados criptografados.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```


>[!BEGINSHADEBOX]

**Restrições à assimilação recorrente**

A assimilação de dados criptografados não oferece suporte à assimilação de pastas recorrentes ou de vários níveis nas fontes. Todos os arquivos criptografados devem estar contidos em uma única pasta. Também não há suporte para curingas com várias pastas em um único caminho de origem.

Veja a seguir um exemplo de estrutura de pastas com suporte, em que o caminho de origem é `/ACME-customers/*.csv.gpg`.

Nesse cenário, os arquivos em negrito são assimilados no Experience Platform.

* Clientes ACME
   * **Arquivo1.csv.gpg**
   * File2.json.gpg
   * **Arquivo3.csv.gpg**
   * File4.json
   * **Arquivo5.csv.gpg**

Veja a seguir um exemplo de uma estrutura de pastas não compatível, na qual o caminho de origem é `/ACME-customers/*`.

Nesse cenário, a execução do fluxo falhará e retornará uma mensagem de erro indicando que os dados não podem ser copiados da origem.

* Clientes ACME
   * File1.csv.gpg
   * File2.json.gpg
   * Subfolder1
      * File3.csv.gpg
      * File4.json.gpg
      * File5.csv.gpg
* Fidelização por ACME
   * File6.csv.gpg

>[!ENDSHADEBOX]

## Próximas etapas

Seguindo este tutorial, você criou um par de chaves de criptografia para seus dados de armazenamento na nuvem e um fluxo de dados para assimilar seus dados criptografados usando o [!DNL Flow Service API]. Para obter atualizações de status sobre a integridade, os erros e as métricas do fluxo de dados, leia o guia na [monitoramento do fluxo de dados usando o [!DNL Flow Service] API](./monitor.md).