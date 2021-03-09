---
keywords: Experience Platform, home, tópicos populares, Microsoft Dynamics, microsoft dynamics, Dynamics, Dynamics
solution: Experience Platform
title: Visão geral do Microsoft Dynamics Source Connector
topic: visão geral
description: Saiba como conectar o Microsoft Dynamics à Adobe Experience Platform usando APIs ou a interface do usuário.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---


# Conector do Microsoft Dynamics

A Adobe Experience Platform permite que os dados sejam assimilados de fontes externas, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando serviços [!DNL Platform]. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[!DNL Experience Platform] O oferece suporte para assimilar dados de um sistema de CRM de terceiros. O suporte para provedores de CRM inclui [!DNL Microsoft Dynamics].

## Lista de permissões de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a página [Lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

>[!IMPORTANT]
>
>No momento, o conector de origem [!DNL Microsoft Dynamics] não oferece suporte à conectividade de mesma região com a Plataforma. Isso significa que se a instância do Azure estiver usando a mesma região de rede que a Plataforma, uma conexão com as fontes da Plataforma não poderá ser estabelecida. Atualmente, somente a conectividade entre regiões é compatível. Entre em contato com o gerente de conta da Adobe para obter mais informações.

A documentação abaixo fornece informações sobre como se conectar [!DNL Microsoft Dynamics] a [!DNL Platform] usando APIs ou a interface do usuário:

## Conecte [!DNL Microsoft Dynamics] a [!DNL Platform] usando APIs

- [Criar uma conexão de origem do Microsoft Dynamics usando a API de Serviço de Fluxo](../../tutorials/api/create/crm/ms-dynamics.md)
- [Explorar um sistema CRM usando a API do Serviço de Fluxo](../../tutorials/api/explore/crm.md)
- [Coletar dados do CRM usando a API do Serviço de Fluxo](../../tutorials/api/collect/crm.md)

## Conecte [!DNL Microsoft Dynamics] a [!DNL Platform] usando a interface do usuário

- [Criar uma conexão de origem do Microsoft Dynamics na interface do usuário](../../tutorials/ui/create/crm/dynamics.md)
- [Configurar um fluxo de dados para uma conexão CRM na interface do usuário](../../tutorials/ui/dataflow/crm.md)