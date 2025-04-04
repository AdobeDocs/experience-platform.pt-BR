---
keywords: Experience Platform;página inicial;tópicos populares;Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: Conector do Marketo Engage
description: Este documento fornece uma visão geral do conector de origem do Marketo Engage, incluindo informações sobre autenticação, mapeamento e latência de dados.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 1%

---

# [!DNL Marketo Engage] conector

>[!IMPORTANT]
>
>Agora você pode usar a origem [!DNL Marketo Engage] ao executar o Adobe Experience Platform no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../../landing/multi-cloud.md).

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) é uma solução completa para o gerenciamento de clientes potenciais e para os profissionais de marketing B2B que procuram transformar as experiências dos clientes se envolvendo em cada estágio de jornadas de compra complexas.

Com o conector de origem [!DNL Marketo Engage], você pode trazer dados B2B de [!DNL Marketo Engage] para a Experience Platform e manter esses dados atualizados usando aplicativos conectados à Experience Platform.

>[!IMPORTANT]
>
>Você deve ter acesso ao [Adobe Real-Time Customer Data Platform B2B edition](../../../../rtcdp/b2b-overview.md) para usar todos os conjuntos de dados da Marketo para segmentação com o [Perfil de cliente em tempo real](../../../../profile/home.md). Sem o Real-Time CDP B2B edition, ainda é possível usar a fonte do Marketo para trazer dados dos conjuntos de dados de pessoas e atividades para o Perfil do cliente em tempo real para segmentação.

Este documento fornece uma visão geral do conector de origem [!DNL Marketo Engage], incluindo informações sobre como autenticar o conector, como mapear campos [!DNL Marketo Engage] para o Experience Data Model (XDM) e a latência de dados do conector.

## Configurar o mapeamento da organização da Adobe

Antes de estabelecer conjuntos de mapeamento para [!DNL Marketo Engage], você deve primeiro configurar o Mapeamento da Organização da Adobe. Para obter etapas detalhadas sobre como concluir, consulte o manual sobre [configuração do Adobe Organization Mapping para [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Autentique seu conector [!DNL Marketo Engage]

Para conectar o [!DNL Marketo Engage] ao Experience Platform, primeiro você deve recuperar os valores do `munchkinId`, `clientId` e `clientSecret`.

Consulte as etapas descritas no documento [Autenticar o conector de origem do Marketo](./marketo-auth.md) para recuperar suas credenciais.

## Configurar namespaces B2B e o utilitário de geração automática de esquema

Em seguida, use o namespace B2B e o utilitário de geração automática de esquema para configurar o console do desenvolvedor do Experience Platform e o ambiente do Postman. Isso permite preencher automaticamente os namespaces e esquemas B2B. Para obter instruções detalhadas, consulte o guia em [configuração dos namespaces B2B e do utilitário de geração automática de esquema](./marketo-namespaces.md)

## Experience Data Model (XDM)

O XDM é uma especificação documentada publicamente que fornece estruturas e definições comuns que permitem assimilar dados de fontes de terceiros para uso em serviços downstream do Experience Platform.

Seguir os padrões XDM permite que os dados sejam incorporados uniformemente ao ecossistema do Experience Platform, facilitando a entrega de dados e a coleta de informações.

Para saber mais sobre o XDM e sua função no Experience Platform, consulte a [visão geral do sistema XDM](../../../../xdm/home.md).

## Mapeamento de campo de [!DNL Marketo Engage] para XDM

Para estabelecer uma conexão de origem entre [!DNL Marketo Engage] e o Experience Platform, os campos de dados de origem do Marketo devem ser mapeados para os campos XDM de destino apropriados antes de serem assimilados na Experience Platform.

Consulte o seguinte para obter informações detalhadas sobre as regras de mapeamento de campos entre [!DNL Marketo Engage] conjuntos de dados e a Experience Platform:

* [Atividades](../mapping/marketo.md#activities)
* [Programas](../mapping/marketo.md#programs)
* [Associações ao programa](../mapping/marketo.md#program-memberships)
* [Empresas](../mapping/marketo.md#companies)
* [Listas estáticas](../mapping/marketo.md#static-lists)
* [Associações de lista estática](../mapping/marketo.md#static-list-memberships)
* [Contas Nomeadas](../mapping/marketo.md#named-accounts)
* [Oportunidades](../mapping/marketo.md#opportunities)
* [Funções do contato da oportunidade](../mapping/marketo.md#opportunity-contact-roles)
* [Pessoas](../mapping/marketo.md#persons)

## Latência esperada dos dados de [!DNL Marketo Engage] no Experience Platform

A tabela a seguir descreve a latência esperada para trazer dados do [!DNL Marketo Engage] para o Experience Platform, com base na natureza da assimilação e no destino desejado:

| Destino | Latência esperada |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10 minutos |
| Data lake | &lt; 60 minutos |

>[!NOTE]
>
>Os números de latência acima representam expectativas em um nível de confiança de 95%. As latências reais variam e podem ultrapassar esses números em 50% em casos raros.

## Próximas etapas e recursos adicionais

A documentação a seguir fornece mais informações sobre como criar uma conexão de origem [!DNL Marketo Engage]:

* Para obter informações sobre como conectar os dados do [!DNL Marketo Engage] ao Experience Platform, leia o tutorial sobre [criação de uma [!DNL Marketo Engage] conexão de origem na interface](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * Para obter informações sobre como configurar seus esquemas e assimilar dados de atividade personalizados, leia o tutorial sobre [criação de uma conexão de origem e fluxo de dados para [!DNL Marketo Engage] dados de atividade personalizados](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
   * Para obter informações sobre como migrar o mapeamento ECID do conjunto de dados [!DNL Person] para o conjunto de dados [!DNL Activity], leia o [guia de migração de mapeamento ECID](./migration.md).
* Para obter informações sobre a configuração subjacente dos namespaces B2B e esquemas usados com [!DNL Marketo Engage], leia a documentação para [namespaces B2B e esquemas](./marketo-namespaces.md).
* Para obter informações sobre como encontrar sua ID do munchkin [!DNL Marketo Engage] e gerar suas credenciais, leia o [[!DNL Marketo Engage] guia de autenticação](./marketo-auth.md).
* Para obter informações sobre as regras de mapeamento específicas que se aplicam aos conjuntos de dados do [!DNL Marketo Engage], leia a documentação em [[!DNL Marketo Engage] mapeamentos de campos](../mapping/marketo.md).
* Para obter informações gerais sobre [!DNL Real-Time Customer Data Platform B2B Edition] e seus recursos, leia a documentação em [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
