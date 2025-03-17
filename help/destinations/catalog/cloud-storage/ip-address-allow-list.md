---
title: LISTA DE PERMISSÕES de endereço IP para destinos de armazenamento na nuvem baseados em arquivo
type: Documentation
description: Esta página fornece intervalos IP que podem ser adicionados à lista de permissões para exportar dados com segurança do Experience Platform para destinos de armazenamento na nuvem.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: ee4c42a2298c588590b1535524ed8f3dfe13b603
workflow-type: tm+mt
source-wordcount: '249'
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
>Os intervalos IP documentados nesta página *não* têm suporte para os seguintes destinos de armazenamento na nuvem baseados em arquivo: [!UICONTROL Azure Blob], [!UICONTROL Azure Data Lake Storage Gen2] e [!UICONTROL Data Landing Zone].

## Visão geral {#overview}

Incluir na lista de permissões Esta página fornece intervalos IP que você pode adicionar ao arquivo para exportar dados com segurança do Experience Platform para vários destinos de armazenamento na nuvem.

Você pode definir controles de acesso à rede por meio do firewall de rede. Ao especificar o intervalo IP apropriado, você pode permitir o tráfego para o serviço de transferência de dados.

A Adobe recomenda que você adicione os seguintes intervalos IP a uma inclui na lista de permissões antes de trabalhar com conexões de destino de armazenamento na nuvem. Falha ao adicionar o intervalo IP específico da região à sua inclui na lista de permissões pode levar a erros ou ao não desempenho ao usar as conexões de destino do armazenamento em nuvem.

## Obrigatório para todos os clientes {#all-customers}

* `52.247.108.70`
<!-- 
## US customers running on AWS {#aws}

The IP range below applies to Experience Platform customers running on Amazon Web Services (AWS). See the [Experience Platform Multi-Cloud overview](../../../landing/multi-cloud.md) for more information.

>[!NOTE]
>
>This IP range is not supported for customers running on AWS who use file-based destinations to export data to Amazon S3. -->

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
