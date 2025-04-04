---
keywords: Experience Platform;página inicial;tópicos populares;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Visão geral do Microsoft Dynamics Source Connector
description: Saiba como conectar o Microsoft Dynamics ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 3%

---

# Conector do Microsoft Dynamics

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform]. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O [!DNL Experience Platform] oferece suporte para assimilação de dados de um sistema CRM de terceiros. O suporte para provedores de CRM inclui [!DNL Microsoft Dynamics].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Mapeamento de campo de [!DNL Microsoft Dynamics] para XDM

Para estabelecer uma conexão de origem entre [!DNL Microsoft Dynamics] e o Experience Platform, os campos de dados de origem [!DNL Microsoft Dynamics] devem ser mapeados para seus campos XDM de destino apropriados antes de serem assimilados na Experience Platform.

Consulte o seguinte para obter informações detalhadas sobre as regras de mapeamento de campos entre [!DNL Microsoft Dynamics] conjuntos de dados e a Experience Platform:

- [Contatos](../adobe-applications/mapping/dynamics.md#contacts)
- [Clientes potenciais](../adobe-applications/mapping/dynamics.md#leads)
- [Contas](../adobe-applications/mapping/dynamics.md#accounts)
- [Oportunidades](../adobe-applications/mapping/dynamics.md#opportunities)
- [Funções do contato da oportunidade](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Campanhas](../adobe-applications/mapping/dynamics.md#campaigns)
- [Lista de marketing](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Membros da lista de marketing](../adobe-applications/mapping/dynamics.md#marketing-list-members)

A documentação abaixo fornece informações sobre como conectar o [!DNL Microsoft Dynamics] ao [!DNL Experience Platform] usando APIs ou a interface do usuário:

## Conectar [!DNL Microsoft Dynamics] a [!DNL Experience Platform] usando APIs

- [Criar uma conexão básica do Microsoft Dynamics usando a API do serviço de fluxo](../../tutorials/api/create/crm/ms-dynamics.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma origem de CRM usando a API do Serviço de Fluxo](../../tutorials/api/collect/crm.md)

## Conectar [!DNL Microsoft Dynamics] a [!DNL Experience Platform] usando a interface

- [Criar uma conexão de origem do Microsoft Dynamics na interface](../../tutorials/ui/create/crm/dynamics.md)
- [Criar um fluxo de dados para uma conexão de CRM na interface](../../tutorials/ui/dataflow/crm.md)
