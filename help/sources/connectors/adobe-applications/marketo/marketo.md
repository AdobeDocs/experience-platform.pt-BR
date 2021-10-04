---
keywords: Experience Platform, home, tópicos populares, Marketo Engage, marketing de engajamento, marketo
solution: Experience Platform
title: conector Marketo Engage
topic-legacy: overview
description: Este documento fornece uma visão geral do conector de fonte Marketo Engage, incluindo informações sobre autenticação, mapeamento e latência de dados.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 0661d124ffe520697a1fc8e2cae7b0b61ef4edfc
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# Conector (Beta) [!DNL Marketo Engage]

>[!IMPORTANT]
>
>A fonte [!DNL Marketo Engage] no Adobe Experience Platform está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (a seguir denominado &quot;[!DNL Marketo]&quot;) é uma solução completa para o gerenciamento de clientes potenciais e para os profissionais de marketing B2B que procuram transformar as experiências dos clientes ao se envolverem em todas as jornadas de compras complexas.

Com o conector de origem [!DNL Marketo], você pode trazer dados B2B de [!DNL Marketo] para a Plataforma e manter esses dados atualizados usando aplicativos conectados à plataforma.

Este documento fornece uma visão geral do conector de origem [!DNL Marketo], incluindo informações sobre como autenticar o conector, como mapear campos [!DNL Marketo] para o Experience Data Model (XDM) e a latência de dados do conector.

## Autentique seu conector [!DNL Marketo]

Para se conectar [!DNL Marketo] à Plataforma, primeiro você deve recuperar valores para `munchkinId`, `clientId` e `clientSecret`.

Consulte as etapas descritas no documento [Autentique seu conector de origem do Marketo](./marketo-auth.md) para recuperar suas credenciais.

## Experience Data Model (XDM)

O XDM é uma especificação documentada publicamente que fornece estruturas e definições comuns que permitem assimilar dados de fontes de terceiros para uso nos serviços downstream da plataforma.

O cumprimento dos padrões XDM permite que os dados sejam uniformemente incorporados no ecossistema da plataforma, facilitando a entrega de dados e a coleta de informações.

Para saber mais sobre o XDM e sua função na Platform, consulte a [Visão geral do sistema XDM](../../../../xdm/home.md).

## Mapeamento de campo de [!DNL Marketo] para XDM

Para estabelecer uma conexão de origem entre [!DNL Marketo] e a Plataforma, os campos de dados de origem do Marketo devem ser mapeados para os campos XDM de destino apropriados antes de serem assimilados na Plataforma.

Consulte o seguinte para obter informações detalhadas sobre as regras de mapeamento de campo entre conjuntos de dados e plataforma [!DNL Marketo]:

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

A tabela a seguir descreve a latência esperada para trazer os dados [!DNL Marketo] para a Plataforma, com base na natureza da assimilação e do destino desejado:

| Destino | Latência esperada |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1 minuto |
| Data Lake | &lt; 60 minutos |

## Próximas etapas e recursos adicionais

A documentação a seguir fornece mais informações sobre a criação de uma conexão de origem [!DNL Marketo]:

* Para obter informações sobre como conectar seus dados [!DNL Marketo] à Platform, consulte o tutorial em [criar um conector de origem Marketo na interface do usuário](../../../tutorials/ui/create/adobe-applications/marketo.md).
* Para obter informações sobre a configuração subjacente para os namespaces e esquemas B2B usados com [!DNL Marketo], consulte a documentação para [namespaces e esquemas B2B](./marketo-namespaces.md).
* Para obter informações sobre como encontrar sua [!DNL Marketo] ID do munchkin e gerar suas credenciais, consulte o [[!DNL Marketo] guia de autenticação](./marketo-auth.md).
* Para obter informações sobre as regras de mapeamento específicas que se aplicam aos conjuntos de dados [!DNL Marketo], consulte a documentação sobre [[!DNL Marketo] mapeamentos de campo](../mapping/marketo.md).
* Para obter informações gerais sobre [!DNL Real-time Customer Data Platform B2B Edition] e seus recursos, consulte a documentação em [[!DNL Real-time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
