---
keywords: Amazon S3; destino S3; s3; amazon s3
title: Conexão Amazon S3
description: Crie uma conexão de saída em tempo real com o armazenamento Amazon Web Services (AWS) S3 para exportar periodicamente arquivos de dados CSV do Adobe Experience Platform para seus próprios buckets do S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 691e3181e05a24b6bb0ebbe8e0f797a2b4c572d2
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# [!DNL Amazon S3] conexão {#s3-connection}

## Visão geral {#overview}

Crie uma conexão de saída ao vivo para o [!DNL Amazon Web Services] (AWS) Armazenamento S3 para exportar periodicamente arquivos de dados CSV do Adobe Experience Platform para seus próprios buckets do S3.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Em lote]** | Destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Tipo de exportação com base em perfil do Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Nome do bucket"
>abstract="Deve ter entre 3 e 63 caracteres. Deve começar e terminar com uma letra ou número. Deve conter somente letras minúsculas, números ou hífens ( - ). Não deve ser formatado como um endereço IP (por exemplo, 192.100.1.1)."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Caminho da pasta"
>abstract="Deve conter somente caracteres A-Z, a-z, 0-9 e pode incluir os seguintes caracteres especiais: `/!-_.'()"^[]+$%.*"`. Para criar uma pasta por arquivo de segmento, insira a macro /%SEGMENT_NAME% ou /%SEGMENT_ID% ou /%SEGMENT_NAME%/%SEGMENT_ID% no campo de texto. Macros só podem ser inseridas no final do caminho da pasta. Visualize exemplos de macro na documentação."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#use-macros" text="Use macros para criar uma pasta no seu local de armazenamento"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Chave pública RSA"
>abstract="Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Sua chave pública deve ser escrita como uma sequência de caracteres codificada em Base64."

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
