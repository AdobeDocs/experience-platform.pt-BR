---
keywords: Amazon Kinesis;destino cinesis;cinesis
title: (Beta) Conexão Amazon Kinesis
description: Crie uma conexão de saída em tempo real com o armazenamento do Amazon Kinesis para fazer o stream de dados do Adobe Experience Platform.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: c62117de27b150f072731c910bb0593ce1fca082
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 1%

---

# (Beta) [!DNL Amazon Kinesis] conexão

## Visão geral {#overview}

>[!IMPORTANT]
>
>O [!DNL Amazon Kinesis] no Platform está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

O [!DNL Kinesis Data Streams] serviço por [!DNL Amazon Web Services] O permite coletar e processar grandes fluxos de registros de dados em tempo real.

Você pode criar uma conexão de saída em tempo real com o [!DNL Amazon Kinesis] armazenamento para fazer o stream de dados do Adobe Experience Platform.

* Para obter mais informações sobre [!DNL Amazon Kinesis], consulte o [Documentação do Amazon](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Para conectar-se a [!DNL Amazon Kinesis] programaticamente, consulte o [Tutorial da API de destinos de transmissão](../../api/streaming-destinations.md).
* Para conectar-se a [!DNL Amazon Kinesis] usando a interface do usuário da Platform, consulte as seções abaixo.

![Amazon Kinesis na interface do usuário](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Casos de uso {#use-cases}

Ao usar destinos de transmissão, como [!DNL Amazon Kinesis], você pode alimentar facilmente eventos de segmentação de alto valor e atributos de perfil associados nos sistemas de sua escolha.

Por exemplo, um prospecto baixou um white-paper que os qualifica em um segmento de &quot;alta propensão à conversão&quot;. Mapeando o segmento em que o prospecto entra na [!DNL Amazon Kinesis] , você receberia esse evento em [!DNL Amazon Kinesis]. Lá, você pode empregar uma abordagem faça você mesmo e descrever a lógica de negócios sobre o evento, pois acha que funcionaria melhor com os sistemas de TI de sua empresa.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Endereço IP lista de permissões {#ip-address-allowlist}

Para atender aos requisitos de segurança e conformidade dos clientes, o Experience Platform fornece uma lista de IPs estáticos que você pode lista de permissões a [!DNL Amazon Kinesis] destino. Consulte [LISTA DE PERMISSÕES de endereço IP para destinos de transmissão](/help/destinations/catalog/streaming/ip-address-allow-list.md) para obter a lista completa de IPs a serem lista de permissões.

## Obrigatório [!DNL Amazon Kinesis] permissões {#required-kinesis-permission}

Para se conectar e exportar dados com êxito para seu [!DNL Amazon Kinesis] fluxos, o Experience Platform precisa de permissões para as seguintes ações:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Essas permissões são organizadas por meio do [!DNL Kinesis] e são marcados pela Platform depois de configurar o destino do Kinesis na interface do usuário da plataforma.

O exemplo abaixo exibe os direitos mínimos de acesso necessários para exportar dados com êxito para um [!DNL Kinesis] destino.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
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
| `kinesis:ListStreams` | Uma ação que lista seus fluxos de dados do Amazon Kinesis. |
| `kinesis:PutRecord` | Uma ação que grava um único registro de dados em um fluxo de dados do Kinesis. |
| `kinesis:PutRecords` | Uma ação que grava vários registros de dados em um fluxo de dados do Kinesis em uma única chamada. |

Para obter mais informações sobre como controlar o acesso para [!DNL Kinesis] fluxos de dados, leia o seguinte [[!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmentnames"
>title="Incluir nomes de segmentos"
>abstract="Alterne se deseja que a exportação de dados inclua os nomes dos segmentos que você está exportando. Visualize a documentação de um exemplo de exportação de dados com esta opção selecionada."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmenttimestamps"
>title="Incluir carimbos de data e hora do segmento"
>abstract="Alterne se deseja que a exportação de dados inclua o carimbo de data e hora UNIX quando os segmentos foram criados e atualizados, bem como o carimbo de data e hora UNIX quando os segmentos foram mapeados para o destino para ativação. Visualize a documentação de um exemplo de exportação de dados com esta opção selecionada."

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!DNL Amazon Web Services]chave de acesso e chave secreta**: Em [!DNL Amazon Web Services]gerar um `access key - secret access key` par para conceder acesso à plataforma [!DNL Amazon Kinesis] conta. Saiba mais na [Documentação do Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **região**: Indicar qual [!DNL Amazon Web Services] região para a qual transmitir dados.
* **Nome**: Forneça um nome para a conexão com o [!DNL Amazon Kinesis]
* **Descrição**: Forneça uma descrição para a conexão com o [!DNL Amazon Kinesis].
* **fluxo**: Forneça o nome de um fluxo de dados existente em seu [!DNL Amazon Kinesis] conta. A Platform exportará dados para esse fluxo.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Ativar segmentos para este destino {#activate}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil de fluxo](../../ui/activate-streaming-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Comportamento de exportação de perfil {#profile-export-behavior}

O Experience Platform otimiza o comportamento de exportação do perfil para seu [!DNL Amazon Kinesis] , para exportar somente dados para seu destino quando ocorrerem atualizações relevantes de um perfil após a qualificação de segmento ou outros eventos significativos. Os perfis são exportados para o seu destino nas seguintes situações:

* A atualização de perfil foi determinada por uma alteração na associação de segmento para pelo menos um dos segmentos mapeados para o destino. Por exemplo, o perfil se qualificou para um dos segmentos mapeados para o destino ou saiu de um dos segmentos mapeados para o destino.
* A atualização do perfil foi determinada por uma alteração no [mapa de identidade](/help/xdm/field-groups/profile/identitymap.md). Por exemplo, um perfil que já se qualificou para um dos segmentos mapeados para o destino foi adicionado a uma nova identidade no atributo do mapa de identidade.
* A atualização do perfil foi determinada por uma alteração nos atributos para pelo menos um dos atributos mapeados para o destino. Por exemplo, um dos atributos mapeados para o destino na etapa de mapeamento é adicionado a um perfil.

Em todos os casos descritos acima, somente os perfis onde as atualizações relevantes ocorreram são exportados para o seu destino. Por exemplo, se um segmento mapeado para o fluxo de destino tiver cem membros e cinco novos perfis se qualificarem para o segmento, a exportação para o seu destino será incremental e incluirá apenas os cinco novos perfis.

Observe que todos os atributos mapeados são exportados para um perfil, independentemente de onde as alterações se encontrem. Portanto, no exemplo acima, todos os atributos mapeados para esses cinco novos perfis serão exportados mesmo se os atributos em si não tiverem sido alterados.

### O que determina uma exportação de dados e o que está incluído na exportação {#what-determines-export-what-is-included}

Com relação aos dados exportados para um determinado perfil, é importante entender os dois conceitos diferentes de *o que determina a exportação de dados para o [!DNL Amazon Kinesis] destino* e *que dados estão incluídos na exportação*.

| O que determina uma exportação de destino | O que está incluído na exportação de destino |
|---------|----------|
| <ul><li>Atributos e segmentos mapeados servem como a dica para uma exportação de destino. Isso significa que, se qualquer segmento mapeado alterar estados (de nulo para realizado ou de realizado/existente para existente) ou se qualquer atributo mapeado for atualizado, uma exportação de destino será iniciada.</li><li>Como as identidades não podem ser mapeadas para [!DNL Amazon Kinesis] destinos, as alterações em qualquer identidade em um determinado perfil também determinam exportações de destino.</li><li>Uma alteração para um atributo é definida como qualquer atualização no atributo, independentemente de ser ou não o mesmo valor. Isso significa que uma substituição em um atributo é considerada uma alteração mesmo que o valor em si não tenha sido alterado.</li></ul> | <ul><li>Todos os segmentos (com o status de associação mais recente), independentemente de estarem ou não mapeados no fluxo de dados, são incluídos na variável `segmentMembership` objeto.</li><li>Todas as identidades na `identityMap` também são incluídos (no momento, o Experience Platform não suporta mapeamento de identidade na [!DNL Amazon Kinesis] destino).</li><li>Somente os atributos mapeados são incluídos na exportação de destino.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Por exemplo, considere esse fluxo de dados como um [!DNL Amazon Kinesis] destino onde três segmentos são selecionados no fluxo de dados e quatro atributos são mapeados para o destino.

![Fluxo de dados de destino do Amazon Kinesis](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Uma exportação de perfil para o destino pode ser determinada por um perfil que se qualifica para ou sai de um dos *três segmentos mapeados*. No entanto, na exportação de dados, no `segmentMembership` objeto (consulte [Dados exportados](#exported-data) seção abaixo), outros segmentos não mapeados podem aparecer, se esse perfil específico for membro deles. Se um perfil se qualificar para o segmento Cliente com Carros coreanos, mas também for membro do filme &quot;Voltar ao futuro&quot; assistido e dos segmentos de fãs de ficção científica, esses dois outros segmentos também estarão presentes `segmentMembership` objeto da exportação de dados, mesmo que não estejam mapeados no fluxo de dados.

Do ponto de vista dos atributos do perfil, qualquer alteração nos quatro atributos mapeados acima determinará uma exportação de destino e qualquer um dos quatro atributos mapeados presentes no perfil estará presente na exportação de dados.

## Dados exportados {#exported-data}

Seu exportado [!DNL Experience Platform] os dados chegam ao seu [!DNL Amazon Kinesis] destino no formato JSON. Por exemplo, a exportação abaixo contém um perfil que se qualificou para um determinado segmento, é um membro de outros dois segmentos e saiu de outro segmento. A exportação também inclui o atributo de perfil nome, sobrenome, data de nascimento e endereço de email pessoal. As identidades desse perfil são ECID e email.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
      }
   }
},
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

>[!MORELIKETHIS]
>
>* [Conecte-se ao Amazon Kinesis e ative dados usando a API do Serviço de Fluxo](../../api/streaming-destinations.md)
>* [Destino de Hubs de Eventos do Azure](./azure-event-hubs.md)
>* [Tipos e categorias de destino](../../destination-types.md)

