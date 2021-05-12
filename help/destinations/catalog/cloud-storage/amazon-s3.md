---
keywords: Amazon S3; destino S3; s3; amazon s3
title: Conexão Amazon S3
description: Crie uma conexão de saída em tempo real com o armazenamento Amazon Web Services (AWS) S3 para exportar periodicamente arquivos de dados delimitados por tabulação ou CSV do Adobe Experience Platform para seus próprios buckets do S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 49a59e5b081243679f5d94b03a63d30df22cdc6a
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# [!DNL Amazon S3] conexão  {#s3-connection}

## Visão geral {#overview}

Crie uma conexão de saída em tempo real com seu armazenamento [!DNL Amazon Web Services] (AWS) S3 para exportar periodicamente arquivos de dados delimitados por tabulação ou CSV do Adobe Experience Platform para seus próprios buckets do S3.

## Tipo de exportação {#export-type}

**Baseado em perfil**  - você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos do fluxo de trabalho de ativação de  [destino](../../ui/activate-destinations.md#select-attributes).

![Tipo de exportação com base em perfil do Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Conectar destino {#connect-destination}

Consulte [Fluxo de trabalho de destinos de armazenamento na nuvem ](./workflow.md) para obter instruções sobre como se conectar aos destinos de armazenamento na nuvem, incluindo [!DNL Amazon S3].

Para destinos [!DNL Amazon S3], insira as seguintes informações no workflow criar destino:

* **[!DNL Amazon S3]chave de acesso e chave  [!DNL Amazon S3] secreta**: No  [!DNL Amazon S3], gere um  `access key - secret access key` par para conceder à Platform acesso à sua  [!DNL Amazon S3] conta. Saiba mais na [documentação do Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

>[!TIP]
>
>No workflow de destino de conexão, você pode criar uma pasta personalizada no armazenamento Amazon S3 por arquivo de segmento exportado. Leia [Use macros para criar uma pasta no seu local de armazenamento](./workflow.md#use-macros) para obter instruções.

## Permissões [!DNL Amazon S3] necessárias {#required-s3-permission}

Para se conectar e exportar dados para o local de armazenamento [!DNL Amazon S3] com êxito, crie um usuário do Gerenciamento de identidade e acesso (IAM) para [!DNL Platform] em [!DNL Amazon S3] e atribua permissões para as seguintes ações:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`


<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->


## Dados exportados {#exported-data}

Para destinos [!DNL Amazon S3], [!DNL Platform] cria um arquivo delimitado por tabulação `.txt` ou `.csv` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Destinos de marketing por email e destinos de armazenamento na nuvem](../../ui/activate-destinations.md#esp-and-cloud-storage) no tutorial de ativação de segmento.
