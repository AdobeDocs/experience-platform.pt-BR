---
keywords: SFTP; sftp
title: Conexão SFTP
description: Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Conexão SFTP

## Visão geral {#overview}

Crie uma conexão de saída ao vivo com seu servidor SFTP para exportar periodicamente arquivos de dados delimitados do Adobe Experience Platform.

>[!IMPORTANT]
>
> Embora o Adobe seja compatível com exportações de dados para servidores SFTP, os locais de armazenamento em nuvem recomendados para exportar dados são [!DNL Amazon S3] e [!DNL Azure Blob].

## Tipo de exportação {#export-type}

**Baseado em perfil**  - você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos do fluxo de trabalho de ativação de  [destino](../../ui/activate-destinations.md#select-attributes).

![Tipo de exportação com base em perfil SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Conectar destino {#connect-destination}

Consulte o [Fluxo de trabalho de destinos de armazenamento na nuvem ](./workflow.md) para obter instruções sobre como se conectar aos destinos de armazenamento na nuvem, incluindo SFTP.

Para destinos SFTP, insira as seguintes informações no workflow criar destino , na etapa **Authentication** :

* **Host**: O endereço do local de armazenamento SFTP
* **Nome de usuário**: O nome de usuário para fazer logon no local de armazenamento SFTP
* **Senha**: A senha para fazer logon no local de armazenamento SFTP

## Dados exportados {#exported-data}

Para destinos SFTP, a Platform cria um arquivo `.txt` ou `.csv` delimitado por tabulação no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [Destinos de marketing por email e destinos de armazenamento na nuvem](../../ui/activate-destinations.md#esp-and-cloud-storage) no tutorial de ativação de segmento.

## LISTA DE PERMISSÕES de endereço IP

Consulte [lista de permissões de endereço IP para destinos de armazenamento em nuvem](./ip-address-allow-list.md) se precisar adicionar IPs Adobe a uma lista de permissões.