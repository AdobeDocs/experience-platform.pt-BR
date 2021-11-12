---
keywords: Experience Platform, home, tópicos populares, Marketo Engage, marketing de engajamento, marketo
solution: Experience Platform
title: Marketo Engage connector
topic-legacy: overview
description: Este documento fornece uma visão geral do conector de fonte Marketo Engage, incluindo informações sobre autenticação, mapeamento e latência de dados.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 21617c6ec364fc05d7b8b6d00daa68608d1ed318
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---

# [!DNL Marketo Engage] conector

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. You can ingest data from a variety of sources such as Adobe applications, cloud-based storage, databases, and many others.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (hereinafter referred to as &quot;[!DNL Marketo]&quot;) is a complete solution for lead management and B2B marketers looking to transform customer experiences by engaging across every stage of complex buying journeys.

Com o [!DNL Marketo] conector de origem, você pode trazer dados B2B de [!DNL Marketo] para a Platform e mantenha esses dados atualizados usando aplicativos conectados à plataforma.

Este documento fornece uma visão geral do [!DNL Marketo] conector de origem, incluindo informações sobre como autenticar o conector, como mapear [!DNL Marketo] campos para o Experience Data Model (XDM) e a latência de dados do conector.

## Autentique seu [!DNL Marketo] conector

In order to connect [!DNL Marketo] to Platform, you must first retrieve values for your `munchkinId`, `clientId`, and `clientSecret`.

See the steps outlined in the [Authenticate your Marketo source connector](./marketo-auth.md) document to retrieve your credentials.

## Set up Adobe Experience Cloud Audience Sharing

Antes de estabelecer conjuntos de mapeamento para [!DNL Marketo], primeiro você deve configurar o Compartilhamento de público da Adobe Experience Cloud. Para obter etapas detalhadas sobre como concluir isso, consulte o guia em [configuração do compartilhamento de público da Adobe Experience Cloud para [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-experience-cloud-audience-sharing.html?lang=en).

## Experience Data Model (XDM)

XDM is a publicly documented specification that provides common structures and definitions that allow you to ingest data from third-party sources for use in downstream Platform services.

O cumprimento dos padrões XDM permite que os dados sejam uniformemente incorporados no ecossistema da plataforma, facilitando a entrega de dados e a coleta de informações.

To learn more about XDM and its role in Platform, please see the [XDM System overview](../../../../xdm/home.md).

## Mapeamento de campo de [!DNL Marketo] para XDM

To establish a source connection between [!DNL Marketo] and Platform, the Marketo source data fields must be mapped to their appropriate target XDM fields prior to being ingested into Platform.

See the following for detailed information on the field mapping rules between [!DNL Marketo] datasets and Platform:

* [Atividades](../mapping/marketo.md#activities)
* [Programas](../mapping/marketo.md#programs)
* [Associações do programa](../mapping/marketo.md#program-memberships)
* [Empresas](../mapping/marketo.md#companies)
* [Listas estáticas](../mapping/marketo.md#static-lists)
* [Associações da lista estática](../mapping/marketo.md#static-list-memberships)
* [Contas Nomeadas](../mapping/marketo.md#named-accounts)
* [Oportunidades](../mapping/marketo.md#opportunities)
* [Funções de contato da oportunidade](../mapping/marketo.md#opportunity-contact-roles)
* [Pessoas](../mapping/marketo.md#persons)

## Latência esperada de [!DNL Marketo] dados na plataforma

A tabela a seguir descreve a latência esperada para trazer [!DNL Marketo] dados no Platform, com base na natureza da assimilação e no destino desejado:

| Destino | Latência esperada |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1 minuto |
| Data Lake | &lt; 60 minutos |

## Next steps and additional resources

A documentação a seguir fornece mais informações sobre a criação de um [!DNL Marketo] conexão de origem:

* Para obter informações sobre como conectar seu [!DNL Marketo] dados para a Platform, consulte o tutorial em [criar um conector de origem do Marketo na interface do usuário](../../../tutorials/ui/create/adobe-applications/marketo.md).
* Para obter informações sobre a configuração subjacente para namespaces e esquemas B2B usados com o [!DNL Marketo], consulte a documentação para [Espaços de nomes e esquemas B2B](./marketo-namespaces.md).
* Para obter informações sobre como encontrar seu [!DNL Marketo] munchkin ID e gerar suas credenciais, consulte o [[!DNL Marketo] guia de autenticação](./marketo-auth.md).
* Para obter informações sobre as regras de mapeamento específicas que se aplicam a [!DNL Marketo] conjuntos de dados, consulte a documentação em [[!DNL Marketo] mapeamentos de campo](../mapping/marketo.md).
* For general information on [!DNL Real-time Customer Data Platform B2B Edition] and its features, see the documentation on [[!DNL Real-time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
