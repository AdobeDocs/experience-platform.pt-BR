---
keywords: Endereço IP, intervalo de IP, destinos de lista de permissões, incluir na lista de permissões
title: LISTA DE PERMISSÕES de endereço IP para destinos de armazenamento na nuvem
type: Documentation
description: Esta página fornece intervalos IP que você pode adicionar à lista de permissões para exportar com segurança dados do Experience Platform para o servidor SFTP, Amazon S3 ou armazenamento Azure Blob.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: c4d8ae6de2e1bbf23a25a66bde5dc88c13a13402
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Endereço IP da inclui na lista de permissões para destinos de armazenamento na nuvem {#ip-address-allow-list}

>[!IMPORTANT]
>
> * A Adobe recomenda que você marque essa página como favorito e a revisite a cada três meses para verificar os endereços IP mais recentes. O Adobe não fornece notificação de novos intervalos IP.
> * Embora o Adobe seja compatível com exportações de dados para servidores SFTP, os locais de armazenamento em nuvem recomendados para a exportação de dados são [!DNL Amazon S3] e [!DNL Azure Blob].


## Visão geral {#overview}

Lista de permissões Esta página fornece intervalos de IP que você pode adicionar ao arquivo para exportar dados com segurança do Experience Platform para o seu [Servidor SFTP](./sftp.md).

Você pode definir controles de acesso à rede por meio do firewall de rede. Ao especificar o intervalo IP apropriado, você pode permitir o tráfego para o serviço de transferência de dados.

O Adobe recomenda que você adicione os seguintes intervalos IP a um incluo na lista de permissões antes de trabalhar com conexões de destino de armazenamento na nuvem. Falha ao adicionar o intervalo IP específico da região à sua inclui na lista de permissões pode levar a erros ou ao não desempenho ao usar as conexões de destino do armazenamento em nuvem.

## Obrigatório para todos os clientes

* `52.247.108.70`

## Clientes dos EUA

* `52.252.71.64/29`

## Clientes EMEA

* `51.137.8.208/29`

## Clientes da APAC

* `20.53.201.168/29`
