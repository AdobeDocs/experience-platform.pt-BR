---
keywords: Experience Platform;página inicial;tópicos populares;Microsoft Dynamics;microsoft dynamics;dynamics;popular topics;Dynamics
solution: Experience Platform
title: Visão geral do Conector de origem do Microsoft Dynamics
description: Saiba como conectar o Microsoft Dynamics ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 2%

---

# Conector do Microsoft Dynamics

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[!DNL Experience Platform] O fornece suporte para assimilação de dados de um sistema CRM de terceiros. O suporte para provedores de CRM inclui [!DNL Microsoft Dynamics].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Mapeamento de campo de [!DNL Microsoft Dynamics] ao XDM

Para estabelecer uma conexão de origem entre [!DNL Microsoft Dynamics] e Platform, a [!DNL Microsoft Dynamics] os campos de dados de origem devem ser mapeados para os campos XDM de destino apropriados antes de serem assimilados na Platform.

Consulte o seguinte para obter informações detalhadas sobre as regras de mapeamento de campo entre [!DNL Microsoft Dynamics] conjuntos de dados e plataforma:

- [Contatos](../adobe-applications/mapping/dynamics.md#contacts)
- [Clientes potenciais](../adobe-applications/mapping/dynamics.md#leads)
- [Contas](../adobe-applications/mapping/dynamics.md#accounts)
- [Oportunidades](../adobe-applications/mapping/dynamics.md#opportunities)
- [Funções do contato da oportunidade](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Campanhas](../adobe-applications/mapping/dynamics.md#campaigns)
- [Lista de marketing](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Membros da lista de marketing](../adobe-applications/mapping/dynamics.md#marketing-list-members)

A documentação abaixo fornece informações sobre como se conectar [!DNL Microsoft Dynamics] para [!DNL Platform] uso de APIs ou da interface do usuário:

## Conectar [!DNL Microsoft Dynamics] para [!DNL Platform] uso de APIs

- [Criar uma conexão básica do Microsoft Dynamics usando a API do Serviço de fluxo](../../tutorials/api/create/crm/ms-dynamics.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma origem de CRM usando a API do Serviço de Fluxo](../../tutorials/api/collect/crm.md)

## Conectar [!DNL Microsoft Dynamics] para [!DNL Platform] uso da interface

- [Criar uma conexão de origem do Microsoft Dynamics na interface](../../tutorials/ui/create/crm/dynamics.md)
- [Criar um fluxo de dados para uma conexão de CRM na interface](../../tutorials/ui/dataflow/crm.md)
