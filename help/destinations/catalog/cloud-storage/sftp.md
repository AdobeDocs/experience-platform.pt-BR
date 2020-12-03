---
keywords: SFTP;sftp
title: Destino SFTP
seo-title: Destino SFTP
description: Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Experience Platform.
seo-description: Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Experience Platform.
translation-type: tm+mt
source-git-commit: 7484e64d0d359f40ef242dfc9d2d1704018a8ed6
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Destino SFTP

## Visão geral

Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Experience Platform.

## Tipo de exportação {#export-type}

**Baseado** em perfis - você está exportando todos os membros de um segmento, juntamente com os campos de schema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela de atributos selecionados do fluxo de trabalho [da ativação de](../../ui/activate-destinations.md#select-attributes)destino.

![Tipo de exportação baseado em perfil SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Destino do Connect {#connect-destination}

Consulte Fluxo de trabalho de destinos do armazenamento [Cloud ](./workflow.md)para obter instruções sobre como se conectar aos destinos do armazenamento na nuvem, incluindo SFTP.

Para destinos SFTP, insira as seguintes informações no fluxo de trabalho de criação de destino, na etapa **Autenticação** :

* **Host**: O endereço do local do armazenamento SFTP
* **Nome de usuário**: O nome de usuário para fazer logon no local do armazenamento SFTP
* **Senha**: A senha para efetuar login no local do armazenamento SFTP

## Dados exportados {#exported-data}

Para destinos SFTP, o CDP em tempo real cria um arquivo delimitado por tabulação `.txt` ou `.csv` no local do armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte Destinos de marketing de [email e destinos](../../ui/activate-destinations.md#esp-and-cloud-storage) de armazenamentos da Cloud no tutorial de ativação de segmentos.