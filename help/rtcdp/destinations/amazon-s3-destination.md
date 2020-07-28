---
title: Destino Amazon S3
seo-title: Destino Amazon S3
description: Crie uma conexão de saída ao vivo com seu armazenamento Amazon Web Services (AWS) S3 para exportar periodicamente arquivos de dados delimitados por tabulação ou CSV do Adobe Experience Platform para seus próprios compartimentos S3.
seo-description: Crie uma conexão de saída ao vivo com seu armazenamento Amazon Web Services (AWS) S3 para exportar periodicamente arquivos de dados delimitados por tabulação ou CSV do Adobe Experience Platform para seus próprios compartimentos S3.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# [!DNL Amazon S3] destino

## Visão geral

Crie uma conexão de saída ao vivo com seu armazenamento [!DNL Amazon Web Services] (AWS) S3 para exportar periodicamente arquivos de dados delimitados por tabulação ou CSV do Adobe Experience Platform para seus próprios compartimentos S3.

## Destino do Connect {#connect-destination}

Consulte Fluxo de trabalho de destinos do armazenamento [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)para obter instruções sobre como se conectar aos destinos do armazenamento na nuvem, incluindo [!DNL Amazon S3].

Para [!DNL Amazon S3] destinos, insira as seguintes informações no fluxo de trabalho de criação de destino:

* **[!DNL Amazon S3]chave de acesso e chave[!DNL Amazon S3]secreta **: Em[!DNL Amazon S3], gere uma chave de acesso - par de chaves de acesso secreto para conceder acesso CDP Adobe em tempo real à sua[!DNL Amazon S3]conta.



>[!IMPORTANT]
>
>A CDP em tempo real do Adobe precisa de `write` permissões no objeto bucket onde os arquivos de exportação serão entregues.
