---
title: LISTA DE PERMISSÕES de endereço IP para destinos de armazenamento na nuvem baseados em arquivo
type: Documentation
description: Esta página fornece intervalos IP que podem ser adicionados à lista de permissões para exportar dados com segurança do Experience Platform para destinos de armazenamento na nuvem.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 4ae7ff58d02b46f1b213bd382d3e98b3f63819e8
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 1%

---

# Endereço IP do arquivo de inclui na lista de permissões para destinos de armazenamento na nuvem baseado em arquivo {#ip-address-allow-list-cloud-storage}

>[!IMPORTANT]
>
> * A Adobe recomenda que você marque esta página como favorito e a revisite a cada três meses para verificar os endereços IP mais recentes. A Adobe não fornece notificação de novos intervalos IP.
> * Embora a Adobe ofereça suporte a exportações de dados para servidores SFTP, os locais de armazenamento na nuvem recomendados para a exportação de dados são [!DNL Amazon S3] e [!DNL Azure Blob].

## Aplicabilidade {#applicability}

As informações de intervalo IP nesta página se aplicam aos seguintes conectores de armazenamento na nuvem baseados em arquivo no catálogo de destinos:

* [[!UICONTROL Amazon S3]](./amazon-s3.md)
* [[!UICONTROL Armazenamento na nuvem do Google]](google-cloud-storage.md)
* [SFTP](./sftp.md)

>[!IMPORTANT]
>
>Os intervalos IP documentados nesta página *não* têm suporte para os seguintes destinos de armazenamento na nuvem baseados em arquivo: [!UICONTROL Azure Blob], [!UICONTROL Azure Data Lake Storage Gen2], [!UICONTROL Data Landing Zone] e servidores SFTP hospedados no Microsoft Azure.

## Visão geral {#overview}

Incluir na lista de permissões Esta página fornece intervalos IP que você pode adicionar ao arquivo para exportar dados com segurança do Experience Platform para vários destinos de armazenamento na nuvem.

Você pode definir controles de acesso à rede por meio do firewall de rede. Ao especificar o intervalo IP apropriado, você pode permitir o tráfego para o serviço de transferência de dados.

A Adobe recomenda que você adicione os seguintes intervalos IP a uma inclui na lista de permissões antes de trabalhar com conexões de destino de armazenamento na nuvem. Falha ao adicionar o intervalo IP específico da região à sua inclui na lista de permissões pode levar a erros ou ao não desempenho ao usar as conexões de destino do armazenamento em nuvem.

## Obrigatório para todos os clientes {#all-customers}

* `52.247.108.70`

## Clientes dos EUA que executam o AWS {#aws}

O intervalo IP abaixo se aplica aos clientes do Experience Platform que usam o Amazon Web Services (AWS). Consulte a [Visão geral de várias nuvens do Experience Platform](../../../landing/multi-cloud.md) para obter mais informações.

>[!NOTE]
>
>Esse intervalo IP não é compatível com clientes que executam o AWS e usam destinos baseados em arquivos para exportar dados para o Amazon S3.

* `66.117.18.0/24`

## Clientes dos EUA {#us-customers}

* `52.252.71.64/29`

## Clientes do Canadá {#canada-customers}

* `20.220.135.16/29`

## Clientes EMEA {#emea-customers}

* `51.137.8.208/29`

## Clientes do Reino Unido {#uk-customers}

* `20.26.133.96/29`

## Clientes da APAC {#apac-customers}

* `20.53.201.168/29`
