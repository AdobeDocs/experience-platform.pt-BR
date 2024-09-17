---
keywords: Endereço IP, intervalo IP, lista de permissões, inclui na lista de permissões, Serviço de consulta, acesso à rede
title: INCLUI NA LISTA DE PERMISSÕES de endereço IP para o serviço de consulta
description: Esta página fornece intervalos IP atualizados que você pode adicionar ao incluo na lista de permissões para obter acesso seguro ao Serviço de consulta.
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: 029d0ad63460a71770e5ba3cd75a29cb04c0cb9c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# INCLUIR NA LISTA DE PERMISSÕES endereço IP {#ip-address-allow-list}

>[!IMPORTANT]
>
> * A Adobe recomenda que você marque essa página como favorito e a revisite a cada três meses para verificar os endereços IP mais recentes. O Adobe não fornece notificação de novos intervalos IP.
> * Embora o Adobe ofereça suporte a exportações de dados para servidores SFTP, os locais de armazenamento na nuvem recomendados para exportar dados são [!DNL Amazon S3] e [!DNL Azure Blob].
> * A partir de 15 de outubro de 2024, novos intervalos IP substituíram os existentes. Certifique-se de que os IPs antigos e novos sejam adicionados ao seu incluo na lista de permissões antes dessa data para evitar qualquer interrupção no serviço.

## Visão geral {#overview}

Incluir na lista de permissões Esta página fornece endereços IP que você pode adicionar ao seu arquivo para exportar com segurança dados do Experience Platform para seu [servidor SFTP](../destinations/catalog/cloud-storage/sftp.md).

Você pode definir controles de acesso à rede por meio do firewall de rede. Ao especificar o intervalo IP apropriado, você pode permitir o tráfego para o serviço de transferência de dados.

Como parte das melhorias contínuas, o Adobe atualizou os intervalos IP usados para acesso de rede ao Serviço de consulta em 15 de outubro de 2024. Os endereços IP existentes serão descontinuados e novos endereços IP ocuparão seu lugar. É crucial adicionar os intervalos de IP antigos e novos ao incluo na lista de permissões durante o período de transição para garantir serviço ininterrupto.

A Adobe recomenda adicionar os seguintes intervalos IP específicos da região a um incluo na lista de permissões, dependendo da sua região. Falha ao adicionar intervalos IP específicos da região ao incluo na lista de permissões pode levar a erros ou ao não desempenho.

## VA7: clientes dos EUA e das Américas {#us-americas}

**IP Antigo:** 20.14.241.153\
**Novo IP:** 4.152.211.251

## NLD2: clientes EMEA {#emea}

**IP Antigo:** 20.101.233.128\
**Novo IP:** 108.141.12.47

## AUS5: clientes da APAC {#apac}

**IP Antigo:** 20.248.220.69\
**Novo IP:** 40.82.220.111

## CAN2: Clientes canadenses {#can2}

**IP Antigo:** 4.172.1.139\
**Novo IP:** 4.172.28.20

## GBR9: Clientes do Reino Unido {#gbr9}

**IP Antigo:** 20.108.200.9\
**Novo IP:** 20.254.80.141

