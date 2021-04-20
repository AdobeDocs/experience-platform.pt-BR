---
keywords: Endereço IP, intervalo de IP, destinos de lista de permissões, lista de permissões
title: 'LISTA DE PERMISSÕES de endereço IP para destinos de armazenamento em nuvem '
type: Documentation
description: Esta página fornece intervalos IP que podem ser adicionados à lista de permissões para exportar com segurança os dados do Experience Platform para o servidor SFTP, o Amazon S3 ou o armazenamento do Azure Blob.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
translation-type: tm+mt
source-git-commit: ac62ebcc7b00a96f718a3c39725bcf21ce3d56cf
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# LISTA DE PERMISSÕES de endereço IP para destinos de armazenamento em nuvem {#ip-address-allow-list}

>[!IMPORTANT]
>
> * O Adobe recomenda marcar esta página e retorná-la a cada três meses para verificar os endereços IP mais recentes. O Adobe não fornece notificação de novos intervalos IP.
> * Embora o Adobe seja compatível com exportações de dados para servidores SFTP, os locais de armazenamento em nuvem recomendados para exportar dados são [!DNL Amazon S3] e [!DNL Azure Blob].


## Visão geral {#overview}

Esta página fornece intervalos IP que você pode adicionar à sua lista de permissões, para exportar com segurança os dados do Experience Platform para seu armazenamento [SFTP server](./sftp.md), [Amazon S3](./amazon-s3.md) ou [Azure Blob](./azure-blob.md).

Você pode definir controles de acesso à rede por meio do firewall de rede. Ao especificar o intervalo IP apropriado, é possível permitir o tráfego para o serviço de transferência de dados.

O Adobe recomenda adicionar os seguintes intervalos IP a uma lista de permissões antes de trabalhar com conexões de destino de armazenamento em nuvem. A não adição do intervalo IP específico da região à lista de permissões pode causar erros ou não desempenho ao usar as conexões de destino de armazenamento na nuvem.

## Obrigatório para todos os clientes

* `52.247.108.70`

## Clientes dos EUA

* `52.252.71.64/29`

## Clientes EMEA

* `51.137.8.208/29`

## Clientes APAC

* `20.53.201.168/29`
