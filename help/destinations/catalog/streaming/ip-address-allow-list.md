---
keywords: Endereço IP, intervalo de IP, destinos de lista de permissões,  lista de permissões, lista de permissões destinos de transmissão
title: 'LISTA DE PERMISSÕES de endereço IP para destinos de transmissão '
type: Documentation
description: Esta página fornece intervalos IP que podem ser adicionados à lista de permissões para exportar com segurança dados do Experience Platform para o terminal HTTP REST API.
source-git-commit: 508435ebe7ba762d204408118703fa6469616118
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# Endereço IP lista de permissões para destinos de transmissão {#ip-address-allowlist}

>[!IMPORTANT]
>
> * O Adobe recomenda marcar esta página e retorná-la a cada três meses para verificar os endereços IP mais recentes. O Adobe não fornece notificação de novos intervalos IP.
> * A lista de IPs documentada aqui *não* aplique-se a todos os destinos que você criar usando [[!DNL Destination SDK]](/help/destinations/destination-sdk/overview.md).


## Visão geral {#overview}

Os intervalos IP documentados aqui se aplicam aos seguintes destinos:

* [Destino da API HTTP](./http-destination.md)
* [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)

O tráfego de saída do Experience Platform para esses destinos sempre passa pelos IPs listados nesta página.

Esta página fornece intervalos IP que podem ser adicionados à sua  de lista de permissões, para exportar com segurança dados do Experience Platform para o terminal HTTP, [!DNL Amazon Kinesis]ou [!DNL Azure Event Hubs] instância. Essa funcionalidade é especialmente útil se o terminal HTTP estiver localizado atrás de um firewall corporativo ou se os padrões de segurança e conformidade de sua empresa exigirem uma lista de intervalos IP a serem incluir na lista de permissões.

Você pode definir controles de acesso à rede por meio do firewall de rede. Ao especificar o intervalo IP apropriado, é possível permitir o tráfego para o serviço de transferência de dados.

O Adobe recomenda adicionar os seguintes intervalos IP a uma antes de trabalhar com os destinos mencionados acima nesta página. A não adição do intervalo IP específico da região à sua lista de permissões pode causar erros ou não desempenho ao usar esses destinos de transmissão.

## VA7: Clientes dos EUA e das Américas {#us-americas}

`20.186.185.239`
`40.70.154.136/29`
`52.254.106.160/28`
`52.254.106.176/28`
`52.254.105.192/28`
`20.186.185.181`
`52.254.107.64/28`
`52.254.107.80/28`
`52.254.106.144/28`
`52.254.106.0/28`
`52.254.107.16/28`
`52.254.107.32/28`
`52.254.106.224/28`
`20.186.185.227`
`52.254.106.192/28`
`52.254.107.128/28`
`52.254.106.208/28`
`52.254.106.240/28`
`52.254.107.0/28`
`52.254.107.144/28`

## NLD2: Clientes EMEA {#emea}

`40.74.4.160/28`
`40.74.6.128/28`
`40.74.7.128/28`
`40.74.4.176/28`
`51.144.184.248/29`
`40.74.7.208/28`
`52.142.236.87`
`20.50.23.153`
`40.74.4.144/28`
`40.74.7.160/28`
`40.74.3.176/28`
`40.74.6.144/28`
`40.74.6.80/28`
`40.74.5.128/28`
`40.74.7.144/28`
`40.74.7.176/28`
`40.74.6.96/28`
`40.74.6.112/28`
`51.105.144.1`
`40.74.7.192/28`
`51.105.144.81`
`51.124.70.4`

## AUS5: Clientes APAC {#apac}

`20.43.104.80/28`
`20.43.104.16/28`
`20.43.104.128/28`
`20.40.188.166`
`20.40.191.224/28`
`20.43.104.176/28`
`20.43.104.0/28`
`20.43.105.0/28`
`20.43.105.48/28`
`20.40.191.240/28`
`20.43.104.192/28`
`20.40.188.227`
`20.40.188.194`
`20.43.104.144/28`
`20.43.104.160/28`
`20.43.104.96/28`
`20.43.105.32/28`
`20.43.104.112/28`
`20.43.105.16/28`
`20.43.104.48/28`
`20.40.191.96/28`
`20.43.104.32/28`
`20.43.104.64/28`