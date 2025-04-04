---
title: Visão geral do Amazon Kinesis Source Connector
description: Saiba como conectar o Amazon Kinesis ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] origem

>[!IMPORTANT]
>
>- A origem [!DNL Amazon Kinesis] está disponível no catálogo de origens para usuários que compraram o Real-Time CDP Ultimate.
>
>- Agora você pode usar a origem [!DNL Amazon Kinesis] ao executar o Adobe Experience Platform no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../landing/multi-cloud.md).


O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem, como AWS, [!DNL Google Cloud Platform] e [!DNL Azure]. Você pode trazer seus dados desses sistemas para o [!DNL Experience Platform].

As fontes de armazenamento na nuvem podem trazer seus próprios dados para o [!DNL Experience Platform] sem precisar baixar, formatar ou carregar. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Origens. [!DNL Experience Platform] permite trazer dados de [!DNL Amazon Kinesis] em tempo real.

>[!NOTE]
>
>O fator de escala para [!DNL Kinesis] deve ser aumentado se você precisar assimilar dados de alto volume. Atualmente, o volume máximo de dados que você pode trazer da sua conta do [!DNL Kinesis] para a Experience Platform é de 4.000 registros por segundo. Para aumentar e assimilar dados de volume maior, entre em contato com o representante da Adobe.

## Pré-requisitos

A seção a seguir fornece mais informações sobre a configuração de pré-requisito necessária para que você possa criar uma conexão de origem [!DNL Kinesis].

### Configurar política de acesso

Um fluxo [!DNL Kinesis] requer as seguintes permissões para criar uma conexão de origem:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Essas permissões são organizadas por meio do console [!DNL Kinesis] e são verificadas pela Experience Platform depois que você insere suas credenciais e seleciona seu fluxo de dados.

O exemplo abaixo exibe os direitos de acesso mínimos necessários para criar uma conexão de origem [!DNL Kinesis].

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:GetShardIterator",
                "kinesis:GetRecords",
                "kinesis:DescribeStream",
                "kinesis:ListStreams"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `kinesis:GetShardIterator` | Uma ação necessária para percorrer registros. |
| `kinesis:GetRecords` | Uma ação necessária para obter registros de um deslocamento específico ou ID compartilhada. |
| `kinesis:DescribeStream` | Uma ação que retorna informações sobre o fluxo, incluindo o mapa de fragmentos, que é necessário para gerar uma ID de fragmentos. |
| `kinesis:ListStreams` | Uma ação necessária para listar os fluxos disponíveis que você pode selecionar na interface do usuário. |

Para obter mais informações sobre como controlar o acesso a [!DNL Kinesis] fluxos de dados, consulte o seguinte [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Configurar tipo de iterador

[!DNL Kinesis] oferece suporte aos seguintes tipos de iterador para permitir que você especifique a ordem de leitura dos seus dados:

| Tipo de iterador | Descrição |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Os dados são lidos a partir de uma posição identificada por um número de sequência específico. |
| `AFTER_SEQUENCE_NUMBER` | Os dados são lidos, começando após a posição identificada por um número de sequência específico. |
| `AT_TIMESTAMP` | Os dados são lidos a partir de uma posição identificada por um carimbo de data e hora específico. |
| `TRIM_HORIZON` | Os dados são lidos a partir do registro de dados mais antigo. |
| `LATEST` | Os dados são lidos a partir do registro de dados mais recente. |

Atualmente, uma origem de interface do usuário [!DNL Kinesis] dá suporte apenas a `TRIM_HORIZON`, enquanto a API dá suporte a `TRIM_HORIZON` e `LATEST` como modos de obtenção de dados. O valor de iterador padrão que o Experience Platform usa para a origem [!DNL Kinesis] é `TRIM_HORIZON`.

Para obter mais informações sobre tipos de iterador, consulte o seguinte [[!DNL Kinesis] documento](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Conectar [!DNL Amazon Kinesis] a [!DNL Experience Platform]

A documentação abaixo fornece informações sobre como conectar o [!DNL Amazon Kinesis] ao [!DNL Experience Platform] usando APIs ou a interface do usuário:

### Uso de APIs

- [Crie uma conexão de origem Amazon Kinesis usando a API do Serviço de fluxo](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Coletar dados de transmissão usando a API de Serviço de Fluxo](../../tutorials/api/collect/streaming.md)

### Uso da interface

- [Criar uma conexão de origem Amazon Kinesis na interface](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configurar um fluxo de dados para uma conexão de armazenamento em nuvem na interface](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
