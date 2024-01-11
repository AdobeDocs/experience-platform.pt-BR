---
title: Endereço IP lista de permissões destinos SFTP
type: Documentation
description: Esta página fornece intervalos IP que podem ser adicionados à lista de permissões para exportar dados com segurança do Experience Platform para o servidor SFTP.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 52186e03ba2a9d8b105d01ebfcd9be7666bfb6ff
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Endereço IP relacionado à inclui na lista de permissões para destinos SFTP {#ip-address-allow-list-sftp}

>[!IMPORTANT]
>
> * A Adobe recomenda que você marque essa página como favorito e a revisite a cada três meses para verificar os endereços IP mais recentes. O Adobe não fornece notificação de novos intervalos IP.
> * Embora o Adobe seja compatível com exportações de dados para servidores SFTP, os locais de armazenamento em nuvem recomendados para a exportação de dados são [!DNL Amazon S3] e [!DNL Azure Blob].

## Visão geral {#overview}

Incluir na lista de permissões Esta página fornece intervalos de IP que você pode adicionar ao arquivo para exportar dados com segurança do Experience Platform para o seu [Servidor SFTP](./sftp.md).

Você pode definir controles de acesso à rede por meio do firewall de rede. Ao especificar o intervalo IP apropriado, você pode permitir o tráfego para o serviço de transferência de dados.

O Adobe recomenda que você adicione os seguintes intervalos IP a um incluo na lista de permissões antes de trabalhar com conexões de destino de armazenamento na nuvem. Falha ao adicionar o intervalo IP específico da região à sua inclui na lista de permissões pode levar a erros ou ao não desempenho ao usar as conexões de destino do armazenamento em nuvem.

## Obrigatório para todos os clientes

* `52.247.108.70`

## Clientes dos EUA

* `52.252.71.64/29`

## Clientes do Canadá

* `20.220.135.16/29`

## Clientes EMEA

* `51.137.8.208/29`

## Clientes do Reino Unido

* `20.26.133.96/29`

## Clientes da APAC

* `20.53.201.168/29`
