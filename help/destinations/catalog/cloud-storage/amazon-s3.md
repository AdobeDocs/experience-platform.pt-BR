---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Destino Amazon S3
seo-title: Destino Amazon S3
description: Crie uma conexão de saída ao vivo com seu armazenamento Amazon Web Services (AWS) S3 para exportar periodicamente arquivos de dados delimitados por tabulação ou CSV da Adobe Experience Platform para seus próprios compartimentos S3.
seo-description: Crie uma conexão de saída ao vivo com seu armazenamento Amazon Web Services (AWS) S3 para exportar periodicamente arquivos de dados delimitados por tabulação ou CSV da Adobe Experience Platform para seus próprios compartimentos S3.
translation-type: tm+mt
source-git-commit: 7484e64d0d359f40ef242dfc9d2d1704018a8ed6
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# [!DNL Amazon S3] destino

## Visão geral

Crie uma conexão de saída ao vivo com seu armazenamento [!DNL Amazon Web Services] (AWS) S3 para exportar periodicamente arquivos de dados delimitados por tabulação ou CSV da Adobe Experience Platform para seus próprios compartimentos S3.

## Tipo de exportação {#export-type}

**Baseado** em perfis - você está exportando todos os membros de um segmento, juntamente com os campos de schema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela de atributos selecionados do fluxo de trabalho [da ativação de](../../ui/activate-destinations.md#select-attributes)destino.

![Tipo de exportação baseado no perfil Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Destino do Connect {#connect-destination}

Consulte Fluxo de trabalho de destinos de armazenamentos da [Cloud ](./workflow.md) para obter instruções sobre como se conectar aos destinos de armazenamentos da nuvem, incluindo [!DNL Amazon S3].

Para [!DNL Amazon S3] destinos, insira as seguintes informações no fluxo de trabalho de criação de destino:

* **[!DNL Amazon S3]chave de acesso e chave [!DNL Amazon S3] secreta**: Em [!DNL Amazon S3], gere um `access key - secret access key` par para conceder acesso CDP em tempo real à sua [!DNL Amazon S3] conta. Saiba mais na documentação [](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon Web Services.

>[!IMPORTANT]
>
>A CDP em tempo real precisa de permissões no objeto bucket no qual os arquivos de exportação serão entregues. `write`

## Dados exportados {#exported-data}

Para [!DNL Amazon S3] destinos, o CDP em tempo real cria um arquivo delimitado por tabulação `.txt` ou `.csv` no local do armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte Destinos de marketing de [email e destinos](../../ui/activate-destinations.md#esp-and-cloud-storage) de armazenamentos da Cloud no tutorial de ativação de segmentos.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`amazon-s3_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->
