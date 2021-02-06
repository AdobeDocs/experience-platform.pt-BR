---
keywords: SFTP;sftp
title: Destino da conexão SFTP
description: Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Experience Platform.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# Conexão SFTP

Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Experience Platform.

## Tipo de exportação {#export-type}

**Baseado**  em perfis - você está exportando todos os membros de um segmento, juntamente com os campos de schema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela de atributos selecionados do fluxo de trabalho [ da ativação de ](../../ui/activate-destinations.md#select-attributes)destino.

![Tipo de exportação baseado em perfil SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Destino do Connect {#connect-destination}

Consulte [Fluxo de trabalho de destinos do armazenamento da nuvem ](./workflow.md)para obter instruções sobre como se conectar aos destinos do armazenamento da nuvem, incluindo SFTP.

Para destinos SFTP, insira as seguintes informações no fluxo de trabalho de criação de destino, na etapa **Autenticação**:

* **Host**: O endereço do local do armazenamento SFTP
* **Nome de usuário**: O nome de usuário para fazer logon no local do armazenamento SFTP
* **Senha**: A senha para efetuar login no local do armazenamento SFTP

## Dados exportados {#exported-data}

Para destinos SFTP, a Platform cria um arquivo `.txt` ou `.csv` delimitado por tabulação no local do armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Destinos de e-mail Marketing e destinos do armazenamento Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) no tutorial de ativação de segmentos.