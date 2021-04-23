---
keywords: Experience Platform, home, tópicos populares, Amazon Kinesis, amazon cinesis, Kinesis, cinesis
solution: Experience Platform
title: Visão geral do Amazon Kinesis Source Connector
topic-legacy: overview
description: Saiba como conectar o Amazon Kinesis ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
translation-type: tm+mt
source-git-commit: af11bc966889be54fc27e02f3eee321519cef88f
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] conector

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform] e [!DNL Azure]. Você pode trazer seus dados desses sistemas para [!DNL Platform].

As fontes de armazenamento em nuvem podem trazer seus próprios dados para [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Fontes . [!DNL Platform] O permite trazer dados do  [!DNL Amazon Kinesis] em tempo real.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Pré-requisitos

A seção a seguir fornece mais informações sobre a configuração de pré-requisito necessária antes que você possa criar uma conexão de origem [!DNL Kinesis].

### Configurar política de acesso

Um fluxo [!DNL Kinesis] requer as seguintes permissões para criar uma conexão de origem:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Essas permissões são organizadas por meio do console [!DNL Kinesis] e são verificadas pela Platform depois de inserir suas credenciais e selecionar seu fluxo de dados.

O exemplo abaixo exibe os direitos mínimos de acesso necessários para criar uma conexão de origem [!DNL Kinesis].

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
| `kinesis:GetRecords` | Uma ação necessária para obter registros de um deslocamento ou ID de compartilhamento específico. |
| `kinesis:DescribeStream` | Uma ação que retorna informações sobre o fluxo, incluindo o mapa compartilhado, necessário para gerar uma ID compartilhada. |
| `kinesis:ListStreams` | Uma ação necessária para listar os fluxos disponíveis que você pode selecionar na interface do usuário. |

Para obter mais informações sobre como controlar o acesso para [!DNL Kinesis] fluxos de dados, consulte o seguinte [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Configurar tipo de iterador

[!DNL Kinesis] O suporta os seguintes tipos de iterador para permitir que você especifique a ordem de leitura dos dados:

| Tipo de iterador | Descrição |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Os dados são lidos a partir de uma posição identificada por um número de sequência específico. |
| `AFTER_SEQUENCE_NUMBER` | Os dados são lidos começando após a posição identificada por um número de sequência específico. |
| `AT_TIMESTAMP` | Os dados são lidos a partir de uma posição identificada por um carimbo de data e hora específico. |
| `TRIM_HORIZON` | Os dados são lidos a partir do registro de dados mais antigo. |
| `LATEST` | Os dados são lidos a partir do registro de dados mais recente. |

No momento, uma fonte de interface [!DNL Kinesis] suporta apenas `TRIM_HORIZON`, enquanto a API suporta `TRIM_HORIZON` e `LATEST` como modos para obter dados. O valor padrão do iterador que a Platform usa para a origem [!DNL Kinesis] é `TRIM_HORIZON`.

Para obter mais informações sobre tipos de iterador, consulte o seguinte [[!DNL Kinesis] document](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Conecte [!DNL Amazon Kinesis] a [!DNL Platform]

A documentação abaixo fornece informações sobre como se conectar [!DNL Amazon Kinesis] a [!DNL Platform] usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão de origem do Amazon Kinesis usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Coletar dados de fluxo usando a API do Serviço de fluxo](../../tutorials/api/collect/streaming.md)

### Uso da interface do usuário

- [Criar uma conexão de origem do Amazon Kinesis na interface do usuário](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configurar um fluxo de dados para uma conexão de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
