---
keywords: Amazon S3;destino S3;s3;amazon s3
title: Conexão Amazon S3
description: Crie uma conexão de saída ao vivo com seu armazenamento Amazon Web Services (AWS) S3 para exportar periodicamente arquivos de dados delimitados por tabulação ou CSV da Adobe Experience Platform para seus próprios compartimentos S3.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# [!DNL Amazon S3] conexão  {#s3-connection}

Crie uma conexão de saída ao vivo com seu [!DNL Amazon Web Services] (AWS) armazenamento S3 para exportar periodicamente arquivos de dados delimitados por tabulação ou CSV da Adobe Experience Platform para seus próprios compartimentos S3.

## Tipo de exportação {#export-type}

**Baseado**  em perfis - você está exportando todos os membros de um segmento, juntamente com os campos de schema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela de atributos selecionados do fluxo de trabalho [ da ativação de ](../../ui/activate-destinations.md#select-attributes)destino.

![Tipo de exportação baseado no perfil Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Destino do Connect {#connect-destination}

Consulte [Fluxo de trabalho de destinos do armazenamento da nuvem ](./workflow.md) para obter instruções sobre como se conectar aos destinos do armazenamento da nuvem, incluindo [!DNL Amazon S3].

Para destinos [!DNL Amazon S3], insira as seguintes informações no fluxo de trabalho de criação de destino:

* **[!DNL Amazon S3]chave de acesso e chave [!DNL Amazon S3]** secreta: Em  [!DNL Amazon S3], gere um  `access key - secret access key` par para conceder acesso à Plataforma à sua  [!DNL Amazon S3] conta. Saiba mais na [documentação do Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

>[!IMPORTANT]
>
>A plataforma precisa de `write` permissões no objeto bucket onde os arquivos de exportação serão entregues.

## Dados exportados {#exported-data}

Para destinos [!DNL Amazon S3], a plataforma cria um arquivo `.txt` ou `.csv` delimitado por tabulação no local do armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Destinos de e-mail Marketing e destinos do armazenamento Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) no tutorial de ativação de segmentos.
