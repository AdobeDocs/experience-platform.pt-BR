---
title: Destino do Amazon S3
seo-title: Destino do Amazon S3
description: Crie uma conexão de saída ao vivo com seu armazenamento Amazon Web Services (AWS) S3 para exportar periodicamente arquivos de dados delimitados por tabulação ou CSV da Adobe Experience Platform para seus próprios compartimentos S3.
seo-description: Crie uma conexão de saída ao vivo com seu armazenamento Amazon Web Services (AWS) S3 para exportar periodicamente arquivos de dados delimitados por tabulação ou CSV da Adobe Experience Platform para seus próprios compartimentos S3.
translation-type: tm+mt
source-git-commit: f3c6c27b7ad07ada0df18aabe0e8503253b38342

---


# Destino do Amazon S3

## Visão geral

Crie uma conexão de saída ao vivo com seu armazenamento Amazon Web Services (AWS) S3 para exportar periodicamente arquivos de dados delimitados por tabulação ou CSV da Adobe Experience Platform para seus próprios compartimentos S3.

## Destino do Connect {#connect-destination}

Consulte Fluxo de trabalho de destinos de armazenamento da [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)para obter instruções sobre como se conectar aos destinos de armazenamento da nuvem, incluindo o Amazon S3.

Para destinos do Amazon S3, insira as seguintes informações no fluxo de trabalho de criação de destino:

* **Chave de acesso Amazon S3 e chave** secreta Amazon S3: No Amazon S3, gere uma chave de acesso - par de chaves de acesso secreto para conceder acesso CDP em tempo real da Adobe à sua conta Amazon S3.



>[!IMPORTANT]
>
>O Adobe Real-time CDP precisa de permissões no objeto bucket onde os arquivos de exportação serão entregues. `write`
