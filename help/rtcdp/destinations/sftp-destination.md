---
keywords: SFTP;sftp
title: Destino SFTP
seo-title: Destino SFTP
description: Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Experience Platform.
seo-description: Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Experience Platform.
translation-type: tm+mt
source-git-commit: cbd748c1881c61f5e636567d94b68f2cf7302fa5
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# Destino SFTP

## Visão geral

Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Experience Platform.

Para exportar dados, execute as seguintes etapas:

## Destino do Connect {#connect-destination}

Consulte Fluxo de trabalho de destinos do armazenamento [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)para obter instruções sobre como se conectar aos destinos do armazenamento na nuvem, incluindo SFTP.

Para destinos SFTP, insira as seguintes informações no fluxo de trabalho de criação de destino, na etapa **Autenticação** :

* **Host**: o endereço do local do armazenamento SFTP
* **Nome de usuário**: o nome de usuário para fazer logon no local do armazenamento SFTP
* **Senha**: a senha para efetuar login no local do armazenamento SFTP

## Dados exportados {#exported-data}

Para destinos SFTP, o Adobe Real-time CDP cria um arquivo delimitado por tabulação `.txt` ou `.csv` no local do armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte Destinos de marketing de [email e destinos](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) de armazenamentos da Cloud no tutorial de ativação de segmentos.