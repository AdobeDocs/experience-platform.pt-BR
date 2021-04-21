---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Tutoriais sobre governança e privacidade de dados
topic-legacy: tutorial
type: Tutorial
description: Este documento fornece uma visão geral dos diferentes tutoriais disponíveis relacionados à Governança de dados do Adobe Experience Platform e ao Adobe Experience Platform Privacy Service.
exl-id: c3cef447-b343-445b-a3ed-54f873f6dfb9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# [!DNL Data Governance] e  [!DNL Privacy] Tutorials

A Governança de dados do Adobe Experience Platform permite que você aplique rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com as políticas de uso de dados relacionadas e avaliando violações de política quando determinadas ações são executadas nesses conjuntos de dados e/ou campos. Antes de começar a usar os tutoriais listados neste documento, consulte a [[!DNL Data Governance] visão geral](../data-governance/home.md) para obter uma introdução mais robusta à estrutura.

O Adobe Experience Platform [!DNL Privacy Service] fornece uma API RESTful e a interface do usuário que permitem coordenar solicitações de privacidade e conformidade em várias soluções. Para saber mais, comece lendo a [Privacy Service overview](../privacy-service/home.md).

## Adicionar rótulos de uso de dados

Os rótulos de uso de dados permitem categorizar os conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Rótulos podem ser aplicados a qualquer momento, fornecendo flexibilidade na maneira como você decide controlar os dados. As práticas recomendadas incentivam a rotulagem de dados assim que eles são assimilados em [!DNL Experience Platform], ou assim que os dados forem disponibilizados para uso em [!DNL Platform]. Os rótulos de uso de dados que são aplicados no nível do conjunto de dados são propagados para todos os campos no conjunto de dados. Os rótulos também podem ser aplicados diretamente a campos individuais (cabeçalhos de coluna) em um conjunto de dados, sem propagação. Para saber como aplicar rótulos de uso de dados aos seus dados, visite a [visão geral dos rótulos de uso de dados](../data-governance/labels/overview.md).

## Criar políticas de uso de dados

A API [!DNL Policy Service] permite criar e gerenciar políticas de uso de dados para determinar quais ações de marketing podem ser tomadas em relação aos dados que contêm determinados rótulos de uso. Para começar, leia a [visão geral das políticas de uso de dados](../data-governance/policies/overview.md).

## Impor políticas de uso de dados

Depois de adicionar rótulos de uso para seus dados e criar políticas para ações de marketing em relação a esses rótulos, você pode usar o [!DNL Policy Service API] para avaliar se uma ação de marketing constitui uma violação de política quando executada em um conjunto de dados ou em um grupo arbitrário de rótulos de uso. Em seguida, você pode configurar seus próprios protocolos internos para lidar com violações de política com base na resposta da API. Para começar, visite a [visão geral de aplicação de política](../data-governance/enforcement/overview.md).

## Impor conformidade de uso de dados para um segmento de público-alvo

Os segmentos ativados para uso em [!DNL Real-time Customer Profile] contêm uma ID de política de mesclagem na definição do segmento. Essa política de mesclagem contém informações sobre quais conjuntos de dados devem ser incluídos no segmento, que, por sua vez, contêm quaisquer rótulos de uso de dados aplicáveis. Para obter etapas específicas que abrangem a imposição da conformidade do uso de dados para um segmento de público-alvo, siga o [tutorial de imposição de conformidade do uso de dados para segmentos](../segmentation/tutorials/governance.md).

## Introdução ao [!DNL Privacy Service]

[!DNL Privacy Service] O fornece uma API RESTful e a interface do usuário que permitem gerenciar os dados pessoais dos titulares de dados (clientes) nos aplicativos do Adobe Experience Cloud. [!DNL Privacy Service] O também fornece um mecanismo central de auditoria e registro que permite acessar o status e os resultados de tarefas envolvendo  [!DNL Experience Cloud] aplicativos. Para obter instruções sobre como criar e monitorar tarefas [!DNL Privacy Service], siga as etapas fornecidas no [Guia do desenvolvedor do Privacy Service](../privacy-service/api/getting-started.md) ou no [Guia do usuário do Privacy Service](../privacy-service/ui/overview.md).
