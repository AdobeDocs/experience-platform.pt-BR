---
keywords: Experience Platform, insights, atendimento ao cliente, tópicos populares, segmentos de atendimento ao cliente
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Criar segmentos de clientes com pontuações previstas
topic-legacy: Create a segment
description: Quando uma execução de previsão é concluída, as pontuações de propensão previstas são automaticamente consumidas pelos Perfis. Enriquecer perfis com pontuações do Customer AI permite que a criação de segmentos de clientes encontre públicos com base em suas pontuações de propensão. Esta seção fornece etapas para a criação de segmentos usando o Construtor de segmentos.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Criar segmentos de clientes com pontuações previstas

Quando uma execução de previsão é concluída, as pontuações de propensão previstas são automaticamente consumidas pelos Perfis. Enriquecer perfis com pontuações do Customer AI permite que a criação de segmentos de clientes encontre públicos com base em suas pontuações de propensão. Esta seção fornece etapas para a criação de segmentos usando o Construtor de segmentos. Para obter um tutorial mais robusto sobre a criação de segmentos, consulte o [Guia do usuário do Construtor de segmentos](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Para utilizar esse método, o Perfil do cliente em tempo real precisa ser ativado para o conjunto de dados.

Na interface do usuário da plataforma, clique em **[!UICONTROL Segmentos]** na navegação à esquerda e, em seguida, clique em **[!UICONTROL Criar segmento]**.

![](../images/user-guide/segments.png)

O **Construtor de segmentos** é exibido. Na coluna **[!UICONTROL Campos]** à esquerda e na guia **[!UICONTROL Atributos]**, clique na pasta chamada **[!UICONTROL Perfil individual XDM]** e clique na pasta com o namespace da sua organização. A pasta chamada **[!UICONTROL Customer AI]** contém os resultados de execuções de previsão e são nomeadas após a instância à qual as pontuações pertencem. Clique em uma pasta de instância para acessar os resultados da instância desejada.

![](../images/user-guide/results.png)

Localizado no centro do Construtor de segmentos, arraste e solte o atributo **[!UICONTROL Pontuação]** na tela do construtor de regras *para definir uma regra.*

Na coluna *Segment properties* à direita, forneça um nome para o segmento.

![](../images/user-guide/properties.png)

Acima da coluna *Campos* à esquerda, clique no ícone **engrenagem** e selecione uma *Mesclar política* no menu suspenso. Clique em **[!UICONTROL Salvar]** para criar o segmento.

![](../images/user-guide/merge_policy.png)

## Próximas etapas

Ao seguir este tutorial, você encontrou públicos-alvo com base em suas pontuações de propensão usando o Construtor de segmento. Agora é possível direcionar seus públicos-alvo ativando-os para destinos. Consulte a [visão geral de destinos](../../../destinations/home.md) para obter mais informações.
