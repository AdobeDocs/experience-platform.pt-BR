---
keywords: Endereço IP, intervalo de IP, destinos de lista de permissões, incluir na lista de permissões, incluir na lista de permissões destinos de transmissão
title: INCLUI NA LISTA DE PERMISSÕES de endereço IP para destinos de transmissão
type: Documentation
description: Esta página fornece intervalos IP que você pode adicionar à lista de permissões para exportar com segurança dados do Experience Platform para o terminal da API REST HTTP, o Amazon Kinesis ou a instância do Azure Event Hubs.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: d4833821105433518ee30415fe08f281effa5616
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# INCLUI NA LISTA DE PERMISSÕES de endereço IP para destinos de transmissão {#ip-address-allowlist}

>[!IMPORTANT]
>
> * A Adobe recomenda que você marque essa página como favorito e a revisite a cada três meses para verificar os endereços IP mais recentes. O Adobe não fornece notificação de novos intervalos IP.
> * A lista de IPs documentada aqui *não* se aplicam a todos os destinos que você criar usando o [[!DNL Destination SDK]](/help/destinations/destination-sdk/overview.md).

## Visão geral {#overview}

Os intervalos IP documentados aqui se aplicam aos seguintes destinos:

* [Destino da API HTTP](./http-destination.md)
* [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)

O tráfego de saída do Experience Platform para esses destinos sempre passa pelos IPs listados nesta página.

Essa página fornece intervalos IP que podem ser adicionados à inclui na lista de permissões para exportar dados com segurança do Experience Platform para o terminal HTTP, [!DNL Amazon Kinesis]ou [!DNL Azure Event Hubs] instância. Incluir na lista de permissões Essa funcionalidade é especialmente útil se o seu ponto de extremidade HTTP estiver localizado atrás de um firewall corporativo ou se os padrões de segurança e conformidade da sua empresa exigirem uma lista de intervalos IP a serem.

Você pode definir controles de acesso à rede por meio do firewall de rede. Ao especificar o intervalo IP apropriado, você pode permitir o tráfego para o serviço de transferência de dados.

A Adobe recomenda que você adicione os seguintes intervalos IP a uma inclui na lista de permissões antes de trabalhar com os destinos mencionados acima nesta página. Se você não adicionar um intervalo IP específico da região ao seu incluo na lista de permissões, poderá causar erros ou problemas de desempenho ao usar esses destinos de transmissão.

## VA7: clientes dos EUA e das Américas {#us-americas}

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
`20.22.83.112`

## NLD2: clientes EMEA {#emea}

`40.74.4.160/28`
`40.74.6.128/28`
`40.74.7.128/28`
`40.74.4.176/28`
`51.144.184.248/29`
`40.74.7.208/28`
`52.142.236.87`
`20.50.23.153`
`20.101.246.9`
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
`20.101.233.128`

## AUS5: clientes da APAC {#apac}

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
`20.53.206.128`
`20.227.35.177`

## CAN2: Clientes do Canadá {#can}

`20.104.46.128/28`
`20.104.46.160/28`
`20.104.46.64/28`
`20.104.46.80/28`
`20.116.145.94`
`20.116.147.168`
`20.200.70.192/28`
`20.200.70.208/28`
`20.200.70.224/28`
`20.200.70.240/28`
`20.200.71.0/28`
`20.200.71.112/28`
`20.200.71.128/28`
`20.200.71.144/28`
`20.200.71.16/28`
`20.200.71.160/28`
`20.200.71.176/28`
`20.200.71.32/28`
`20.200.71.48/28`
`20.200.71.64/28`
`20.200.71.80/28`
`20.200.71.96/28`
`20.200.93.180`
`20.200.94.116`
`20.200.94.83`
