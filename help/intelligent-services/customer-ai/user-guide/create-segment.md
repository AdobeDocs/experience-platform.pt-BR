---
keywords: Experience Platform, insights, atendimento ao cliente, tópicos populares, segmentos de atendimento ao cliente
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Criar segmentos de clientes com pontuações previstas
topic-legacy: Create a segment
description: Quando uma execução de previsão é concluída, as pontuações de propensão previstas são automaticamente consumidas pelos Perfis. Enriquecer perfis com pontuações do Customer AI permite que a criação de segmentos de clientes encontre públicos com base em suas pontuações de propensão. Esta seção fornece etapas para a criação de segmentos usando o Construtor de segmentos.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Criar segmentos de clientes com pontuações previstas

Quando uma execução de previsão é concluída, as pontuações de propensão previstas são automaticamente consumidas pelos Perfis. Enriquecer perfis com pontuações do Customer AI permite que a criação de segmentos de clientes encontre públicos com base em suas pontuações de propensão. Esta seção fornece etapas para a criação de segmentos usando o Construtor de segmentos. Para obter um tutorial mais robusto sobre a criação de segmentos, consulte o [Guia do usuário do Construtor de segmentos](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Para utilizar esse método, o Perfil do cliente em tempo real precisa ser ativado para o conjunto de dados.

Na interface do usuário da plataforma, clique em **[!UICONTROL Segments]** na navegação à esquerda e, em seguida, clique em **[!UICONTROL Create segment]**.

![](../images/user-guide/segments.png)

O **Construtor de segmentos** é exibido. Na coluna **[!UICONTROL Fields]** à esquerda e na guia **[!UICONTROL Attributes]** , clique na pasta chamada **[!UICONTROL XDM Individual Profile]** e, em seguida, clique na pasta com o namespace da sua organização. A pasta chamada **[!UICONTROL Customer AI]** contém os resultados de execuções de previsão e são nomeadas após a instância à qual as pontuações pertencem. Clique em uma pasta de instância para acessar os resultados da instância desejada.

![](../images/user-guide/results.png)

Localizado no centro do Construtor de segmentos, arraste e solte o atributo **[!UICONTROL Score]** na tela do construtor de regras *para definir uma regra.*

Na coluna *Segment properties* à direita, forneça um nome para o segmento.

![](../images/user-guide/properties.png)

Acima da coluna *Campos* à esquerda, clique no ícone **engrenagem** e selecione uma *Mesclar política* no menu suspenso. Clique em **[!UICONTROL Save]** para criar o segmento.

![](../images/user-guide/merge_policy.png)

## Próximas etapas

Ao seguir este tutorial, você encontrou públicos-alvo com base em suas pontuações de propensão usando o Construtor de segmento. Agora é possível direcionar seus públicos-alvo ativando-os para destinos. Consulte a [visão geral de destinos](../../../destinations/home.md) para obter mais informações.
