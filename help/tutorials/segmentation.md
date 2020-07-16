---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriais de segmentação
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Tutoriais de segmentação

O Adobe Experience Platform [!DNL Segmentation Service] fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar audiências a partir de seus [!DNL Real-time Customer Profile] dados. Esses segmentos são configurados e mantidos centralmente [!DNL Platform]e são prontamente acessíveis por qualquer solução da Adobe. Para saber mais sobre a segmentação, comece lendo a visão geral [do Serviço de](../segmentation/home.md)segmentação.

## Criar uma definição de segmento

Uma definição de segmento é o conjunto de regras usado para descrever as principais características ou comportamento de uma audiência de público alvo. Depois de conceitualizadas, as regras descritas em uma definição de segmento são usadas para determinar os membros da audiência qualificados para um segmento. O desenvolvimento, teste, visualização e salvamento de uma definição de segmento pode ser feito usando a interface do [!DNL Platform] usuário ou as APIs. Para criar uma definição de segmento, siga o tutorial [da API de](../segmentation/tutorials/create-a-segment.md) criação de um segmento ou o guia [de usuário da interface do usuário do Construtor de](../segmentation/ui/overview.md)segmentos.

## Avaliar um segmento e acessar os resultados

Depois de desenvolver, testar e salvar sua definição de segmento, você pode avaliar o segmento por meio de avaliação programada ou por demanda. A avaliação programada (também conhecida como &quot;segmentação programada&quot;) permite criar uma programação recorrente para executar uma tarefa de exportação em um horário específico, enquanto a avaliação sob demanda envolve a criação de uma tarefa de segmento para criar a audiência imediatamente. Para saber mais, visite o tutorial para [avaliar e acessar os resultados](../segmentation/tutorials/evaluate-a-segment.md)do segmento.

## Exportar dados de segmento

A exportação de segmentos que contêm [!DNL Profile] dados requer primeiro a [criação de um conjunto de dados no qual os dados serão exportados](../segmentation/tutorials/create-dataset-export-segment.md)e, em seguida, o início de uma nova tarefa de exportação. As etapas para gerar um trabalho de exportação podem ser encontradas no tutorial [da API de](../segmentation/tutorials/export-data.md)exportação.

## Configurar políticas de mesclagem

O Adobe Experience Platform permite que você reúna dados de várias fontes e os combine para ver uma visualização completa de cada um de seus clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] usam para determinar como os dados serão priorizados e quais dados serão combinados para criar essa visualização unificada. Usando RESTful APIs ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Para trabalhar com políticas de mesclagem na [!DNL Platform] interface do usuário, visite o guia [do usuário das políticas de](../profile/ui/merge-policies.md)mesclagem. Para trabalhar com políticas de mesclagem usando a [!DNL Real-time Customer Profile] API, consulte o guia [do desenvolvedor de políticas de](../profile/api/merge-policies.md)mesclagem.

## Reforçar a conformidade de uso de dados para segmentos

Os segmentos que estão habilitados para uso em [!DNL Real-time Customer Profile] contêm uma ID de política de mesclagem dentro de sua definição de segmento. Esta política de mesclagem contém informações sobre quais conjuntos de dados devem ser incluídos no segmento, que por sua vez contêm quaisquer rótulos de uso de dados aplicáveis. Para obter etapas específicas que abrangem a imposição da conformidade de uso de dados para um segmento de audiência, siga o tutorial de imposição de conformidade de uso de [dados para segmentos](../segmentation/tutorials/governance.md).

## Segmentação em streaming

A segmentação contínua é a capacidade de avaliar instantaneamente um cliente assim que um evento entra em um grupo de segmentos específico. Com esse recurso, a maioria das regras de segmento pode ser avaliada à medida que os dados são passados para o Adobe Experience Platform, o que significa que a associação de segmento será mantida atualizada sem executar trabalhos de segmentação programados. Para saber mais, visite a visão geral [da segmentação de](../segmentation/api/streaming-segmentation.md)streaming.

## Segmentação de várias entidades

A segmentação de várias entidades é a capacidade de estender [!DNL Profile] dados com dados adicionais baseados em produtos, lojas ou outras classes que não sejam de perfil. Depois de conectados, os dados de classes adicionais ficam disponíveis como se fossem nativos para o [!DNL Profile] schema. Para saber como mover-se, consulte a documentação [de segmentação de](../segmentation/multi-entity-segmentation.md)várias entidades.