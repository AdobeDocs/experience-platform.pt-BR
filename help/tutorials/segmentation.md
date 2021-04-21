---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Tutoriais de segmentação
topic-legacy: tutorial
type: Tutorial
description: O Serviço de segmentação da Adobe Experience Platform fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar públicos-alvo a partir dos dados do Perfil do cliente em tempo real. Esses segmentos são configurados e mantidos centralmente na Platform e são prontamente acessíveis por qualquer solução de Adobe.
exl-id: e45de6b5-ff71-4908-ad79-898084763704
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Tutoriais de segmentação

O Adobe Experience Platform [!DNL Segmentation Service] fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar públicos-alvo a partir dos dados [!DNL Real-time Customer Profile]. Esses segmentos são configurados e mantidos centralmente em [!DNL Platform] e são prontamente acessíveis por qualquer solução de Adobe. Para saber mais sobre a segmentação, comece lendo a [Visão geral do serviço de segmentação](../segmentation/home.md).

## Criar uma definição de segmento

Uma definição de segmento é o conjunto de regras usado para descrever as principais características ou o comportamento de um público-alvo. Depois de conceitualizadas, as regras descritas em uma definição de segmento são usadas para determinar membros de público-alvo qualificados para um segmento. O desenvolvimento, teste, visualização e salvamento de uma definição de segmento pode ser feito usando a [!DNL Platform] interface do usuário ou APIs. Para criar uma definição de segmento, siga o [criar um tutorial de API de segmento](../segmentation/tutorials/create-a-segment.md) ou o [Guia do usuário do Construtor de segmentos](../segmentation/ui/overview.md).

## Avaliar um segmento e acessar resultados

Depois de desenvolver, testar e salvar a definição de segmento, você pode avaliar o segmento por meio de avaliação programada ou sob demanda. A avaliação agendada (também conhecida como &quot;segmentação agendada&quot;) permite criar uma programação recorrente para executar um trabalho de exportação em um horário específico, enquanto a avaliação sob demanda envolve a criação de um trabalho de segmento para criar o público-alvo imediatamente. Para saber mais, visite o tutorial para [avaliar e acessar os resultados do segmento](../segmentation/tutorials/evaluate-a-segment.md).

## Exportar dados de segmento

Exportar segmentos contendo dados [!DNL Profile] requer primeiro [criar um conjunto de dados no qual os dados serão exportados](../segmentation/tutorials/create-dataset-export-segment.md), em seguida, iniciar um novo trabalho de exportação. As etapas para gerar um trabalho de exportação podem ser encontradas no tutorial em [avaliar um segmento](../segmentation/tutorials/evaluate-a-segment.md).

## Configurar políticas de mesclagem

O Adobe Experience Platform permite reunir dados de várias fontes e combiná-los para ver uma visualização completa de cada um dos clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] usa para determinar como os dados serão priorizados e quais dados serão combinados para criar essa exibição unificada. Usando RESTful APIs ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Para trabalhar com políticas de mesclagem na interface do usuário [!DNL Platform], visite o [guia do usuário de políticas de mesclagem](../profile/ui/merge-policies.md). Para trabalhar com políticas de mesclagem usando a API [!DNL Real-time Customer Profile], consulte o [guia do desenvolvedor de políticas de mesclagem](../profile/api/merge-policies.md).

## Impor conformidade de uso de dados para segmentos

Os segmentos ativados para uso em [!DNL Real-time Customer Profile] contêm uma ID de política de mesclagem na definição do segmento. Essa política de mesclagem contém informações sobre quais conjuntos de dados devem ser incluídos no segmento, que, por sua vez, contêm quaisquer rótulos de uso de dados aplicáveis. Para obter etapas específicas que abrangem a imposição da conformidade do uso de dados para um segmento de público-alvo, siga o [tutorial de imposição de conformidade do uso de dados para segmentos](../segmentation/tutorials/governance.md).

## Segmentação de streaming

A segmentação por streaming é a capacidade de avaliar instantaneamente um cliente assim que um evento entrar em um grupo de segmentos específico. Com esse recurso, a maioria das regras de segmento agora pode ser avaliada à medida que os dados são passados para o Adobe Experience Platform, o que significa que a associação de segmento será mantida atualizada sem executar tarefas de segmentação programadas. Para saber mais, visite a [visão geral da segmentação de transmissão](../segmentation/api/streaming-segmentation.md).

## Segmentação de várias entidades

A segmentação de várias entidades é a capacidade de estender [!DNL Profile] dados com dados adicionais com base em produtos, lojas ou outras classes que não sejam de perfil. Depois de conectados, os dados das classes adicionais ficam disponíveis como se fossem nativos do schema [!DNL Profile]. Para aprender a mover-se, consulte a [documentação de segmentação de várias entidades](../segmentation/multi-entity-segmentation.md).
