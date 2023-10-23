---
keywords: Endereço IP, intervalo IP, lista de permissões, incluir na lista de permissões
title: INCLUI NA LISTA DE PERMISSÕES de endereço IP para o serviço de consulta
description: Esta página fornece intervalos IP que podem ser adicionados à lista de permissões.
source-git-commit: 89d04a98e983b5dc9f353a831cdbe21c7c7aaf36
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 2%

---

# INCLUIR NA LISTA DE PERMISSÕES endereço IP {#ip-address-allow-list}

>[!IMPORTANT]
>
> * A Adobe recomenda que você marque essa página como favorito e a revisite a cada três meses para verificar os endereços IP mais recentes. O Adobe não fornece notificação de novos intervalos IP.
> * Embora o Adobe seja compatível com exportações de dados para servidores SFTP, os locais de armazenamento em nuvem recomendados para a exportação de dados são [!DNL Amazon S3] e [!DNL Azure Blob].

## Visão geral {#overview}

Incluir na lista de permissões Essa página fornece endereços IP que você pode adicionar ao arquivo para exportar dados com segurança do Experience Platform para o seu [Servidor SFTP](../destinations/catalog/cloud-storage/sftp.md).

Você pode definir controles de acesso à rede por meio do firewall de rede. Ao especificar o intervalo IP apropriado, você pode permitir o tráfego para o serviço de transferência de dados.

O Adobe recomenda que você adicione os seguintes intervalos de IP a um incluo na lista de permissões, dependendo da sua região. Se você não adicionar um intervalo IP específico da região ao seu incluo na lista de permissões, poderá ocorrer erros ou problemas de desempenho.

## VA7: clientes dos EUA e das Américas {#us-americas}

* 52.138.119.167

## NLD2: clientes EMEA {#emea}

* 51.124.70.4

## AUS5: clientes da APAC {#apac}

* 20.193.36.37

## CAN2: Clientes canadenses {#can2}

* 20.104.5.248
