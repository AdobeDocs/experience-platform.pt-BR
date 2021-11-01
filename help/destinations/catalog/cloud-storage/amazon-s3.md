---
keywords: Amazon S3; destino S3; s3; amazon s3
title: Conexão Amazon S3
description: Crie uma conexão de saída em tempo real com o armazenamento Amazon Web Services (AWS) S3 para exportar periodicamente arquivos de dados CSV do Adobe Experience Platform para seus próprios buckets do S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# [!DNL Amazon S3] conexão {#s3-connection}

## Visão geral {#overview}

Crie uma conexão de saída ao vivo para o [!DNL Amazon Web Services] (AWS) Armazenamento S3 para exportar periodicamente arquivos de dados CSV do Adobe Experience Platform para seus próprios buckets do S3.

## Tipo de exportação {#export-type}

**Baseado em perfil** - estiver exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos do [fluxo de trabalho de ativação de destino](../../ui/activate-segment-streaming-destinations.md#mapping).

![Tipo de exportação com base em perfil do Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!DNL Amazon S3]chave de acesso** e **[!DNL Amazon S3]chave secreta**: Em [!DNL Amazon S3]gerar um `access key - secret access key` par para conceder acesso à plataforma [!DNL Amazon S3] conta. Saiba mais na [Documentação do Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Nome]**: insira um nome que ajudará a identificar esse destino.
* **[!UICONTROL Descrição]**: insira uma descrição deste destino.
* **[!UICONTROL Nome do bucket]**: digite o nome do [!DNL Amazon S3] bucket a ser usado por este destino.
* **[!UICONTROL Caminho da pasta]**: insira o caminho para a pasta de destino que hospedará os arquivos exportados.

Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Sua chave pública deve ser escrita como uma [!DNL Base64] sequência de caracteres codificada.

>[!TIP]
>
>No workflow de destino de conexão, você pode criar uma pasta personalizada no armazenamento Amazon S3 por arquivo de segmento exportado. Ler [Use macros para criar uma pasta no seu local de armazenamento](overview.md#use-macros) para obter instruções.

### Obrigatório [!DNL Amazon S3] permissões {#required-s3-permission}

Para se conectar e exportar dados com êxito para seu [!DNL Amazon S3] local de armazenamento, criar um usuário do Gerenciamento de identidade e acesso (IAM) para [!DNL Platform] em [!DNL Amazon S3] e atribuir permissões para as seguintes ações:

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

## Ativar segmentos para este destino {#activate}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Dados exportados {#exported-data}

Para [!DNL Amazon S3] destinos, [!DNL Platform] cria um `.csv` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) no tutorial de ativação de segmento.
