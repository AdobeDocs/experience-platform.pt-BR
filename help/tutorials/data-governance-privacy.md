---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriais sobre controle de dados e privacidade
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# Tutoriais de privacidade e controle de dados

A DULE (Data Usage Labeling and Implementation) é o mecanismo principal do Adobe Experience Platform Data Governance. Os recursos DULE permitem aplicar rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com as políticas de uso de dados relacionadas. Antes de começar a usar as etiquetas, consulte a visão geral [do](../data-governance/home.md) Data Governance para obter uma introdução mais robusta à estrutura DULE dentro da plataforma.

O Adobe Experience Platform Privacy Service fornece uma API RESTful e uma interface de usuário que permitem coordenar solicitações de privacidade e conformidade em várias soluções. Para saber mais, comece lendo a visão geral [](../privacy-service/home.md)do Privacy Service.

## Adicionar rótulos de uso de dados

Rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. As etiquetas podem ser aplicadas a qualquer momento, proporcionando flexibilidade na forma como você escolhe administrar os dados. As práticas recomendadas incentivam a rotulação de dados assim que eles são ingeridos na plataforma da experiência, ou assim que os dados se tornarem disponíveis para uso na plataforma. Os rótulos de uso de dados aplicados no nível do conjunto de dados são propagados para todos os campos no conjunto de dados. Os rótulos também podem ser aplicados diretamente a campos individuais (cabeçalhos de coluna) em um conjunto de dados, sem propagação. Para saber como aplicar rótulos de uso de dados aos seus dados, visite a visão geral [dos rótulos de uso de](../data-governance/labels/overview.md)dados.

## Criar políticas de uso de dados

A DULE Policy Service API permite que você crie e gerencie políticas DULE para determinar quais ações de marketing podem ser tomadas em relação aos dados que contêm determinados rótulos DULE. Para começar, leia a visão geral [das políticas de uso de](../data-governance/policies/overview.md)dados.

## Impor políticas de uso de dados

Depois que você tiver criado rótulos DULE (Data Usage Labeling and Implementation) para seus dados e tiver criado políticas DULE para ações de marketing contra esses rótulos, poderá usar a DULE Policy Service API para avaliar se uma ação de marketing executada em um conjunto de dados, ou um grupo arbitrário de rótulos DULE, constitui uma violação de política. Em seguida, você pode configurar seus próprios protocolos internos para lidar com violações de política com base na resposta da API. Para começar, visite a visão geral [da aplicação de](../data-governance/enforcement/overview.md)políticas.

## Impor conformidade de uso de dados para um segmento de audiência

Os segmentos que estão habilitados para uso no Perfil de cliente em tempo real contêm uma ID de política de mesclagem na definição do segmento. Esta política de mesclagem contém informações sobre quais conjuntos de dados devem ser incluídos no segmento, que por sua vez contêm quaisquer rótulos de uso de dados aplicáveis. Para obter etapas específicas que abrangem a imposição da conformidade de uso de dados para um segmento de audiência, siga o tutorial de imposição de conformidade de uso de [dados para segmentos](../segmentation/tutorials/governance.md).

## Introdução ao Privacy Service

O Privacy Service fornece uma API RESTful e uma interface de usuário que permitem gerenciar os dados pessoais de seus participantes (clientes) nos aplicativos da Adobe Experience Cloud. O Privacy Service também fornece um mecanismo central de auditoria e registro que permite acessar o status e os resultados de trabalhos que envolvem aplicativos da Experience Cloud. Para obter instruções sobre como criar e monitorar trabalhos do Privacy Service, siga as etapas fornecidas no guia [do desenvolvedor do Privacy Service ou no guia](../privacy-service/api/getting-started.md) do usuário do [](../privacy-service/ui/overview.md)Privacy Service.