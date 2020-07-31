---
title: Destino SFTP
seo-title: Destino SFTP
description: Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Experience Platform.
seo-description: Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Experience Platform.
translation-type: tm+mt
source-git-commit: 098dd31be4d6ee6971cd87bcbfe0f686e34918e1
workflow-type: tm+mt
source-wordcount: '170'
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

Para [!SFTP] destinos, o CDP Adobe em tempo real cria um arquivo delimitado por tabulação `.txt` ou `.csv` no local do armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte Destinos de marketing de [email e destinos](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) de armazenamentos da Cloud no tutorial de ativação de segmentos.