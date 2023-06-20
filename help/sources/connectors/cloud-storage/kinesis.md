---
title: Visão geral do Conector de origem do Amazon Kinesis
description: Saiba como conectar o Amazon Kinesis ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] origem

>[!IMPORTANT]
>
>A variável [!DNL Amazon Kinesis] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem, como o AWS, [!DNL Google Cloud Platform], e [!DNL Azure]. Você pode trazer seus dados desses sistemas para [!DNL Platform].

As fontes de armazenamento na nuvem podem trazer seus próprios dados para [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Origens. [!DNL Platform] permite trazer dados do [!DNL Amazon Kinesis] em tempo real.

>[!NOTE]
>
>O fator de escala para [!DNL Kinesis] deve ser aumentado se você precisar assimilar dados de alto volume. Atualmente, o volume máximo de dados que você pode trazer de seu [!DNL Kinesis] para a Platform é de 4000 registros por segundo. Para aumentar e assimilar dados de volume maior, entre em contato com o representante da Adobe.

## Pré-requisitos

A seção a seguir fornece mais informações sobre a configuração de pré-requisitos necessária antes que você possa criar um [!DNL Kinesis] conexão de origem.

### Configurar política de acesso

A [!DNL Kinesis] o fluxo requer as seguintes permissões para criar uma conexão de origem:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Essas permissões são organizadas por meio da variável [!DNL Kinesis] e são verificados pela Platform depois de inserir suas credenciais e selecionar o fluxo de dados.

O exemplo abaixo exibe os direitos de acesso mínimos necessários para criar uma [!DNL Kinesis] conexão de origem.

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

Para obter mais informações sobre o controle de acesso para [!DNL Kinesis] fluxos de dados, consulte o seguinte [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Configurar tipo de iterador

[!DNL Kinesis] O suporta os seguintes tipos de iterador para permitir que você especifique a ordem de leitura dos seus dados:

| Tipo de iterador | Descrição |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Os dados são lidos a partir de uma posição identificada por um número de sequência específico. |
| `AFTER_SEQUENCE_NUMBER` | Os dados são lidos, começando após a posição identificada por um número de sequência específico. |
| `AT_TIMESTAMP` | Os dados são lidos a partir de uma posição identificada por um carimbo de data e hora específico. |
| `TRIM_HORIZON` | Os dados são lidos a partir do registro de dados mais antigo. |
| `LATEST` | Os dados são lidos a partir do registro de dados mais recente. |

A [!DNL Kinesis] A origem da interface do usuário só oferece suporte no momento `TRIM_HORIZON`, enquanto a API oferece suporte a `TRIM_HORIZON` e `LATEST` como modos para obter dados. O valor padrão do iterador que a Platform usa para o [!DNL Kinesis] a origem é `TRIM_HORIZON`.

Para obter mais informações sobre tipos de iteradores, consulte o seguinte [[!DNL Kinesis] documento](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Conectar [!DNL Amazon Kinesis] para [!DNL Platform]

A documentação abaixo fornece informações sobre como se conectar [!DNL Amazon Kinesis] para [!DNL Platform] uso de APIs ou da interface do usuário:

### Uso de APIs

- [Criar uma conexão de origem do Amazon Kinesis usando a API do Serviço de fluxo](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Coletar dados de transmissão usando a API de Serviço de Fluxo](../../tutorials/api/collect/streaming.md)

### Uso da interface

- [Criar uma conexão de origem do Amazon Kinesis na interface](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configurar um fluxo de dados para uma conexão de armazenamento em nuvem na interface](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
