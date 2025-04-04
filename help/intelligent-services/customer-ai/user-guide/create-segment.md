---
keywords: Experience Platform;insights;ia do cliente;tópicos populares;segmentos de ia do cliente
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Criar segmentos do cliente com pontuações previstas
description: Quando uma execução de previsão é concluída, as pontuações de propensão previstas são consumidas automaticamente pelos Perfis. O enriquecimento dos perfis com pontuações da IA do cliente permite a criação de segmentos de clientes para encontrar públicos com base em suas pontuações de propensão. Esta seção fornece etapas para criar segmentos usando o Construtor de segmentos.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Criar segmentos de clientes com pontuações previstas

Quando uma execução de previsão é concluída, as pontuações de propensão previstas são consumidas automaticamente pelos Perfis. O enriquecimento dos perfis com pontuações da IA do cliente permite a criação de segmentos de clientes para encontrar públicos com base em suas pontuações de propensão. Esta seção fornece etapas para criar segmentos usando o Construtor de segmentos. Para obter um tutorial mais robusto sobre como criar segmentos, consulte o [guia do usuário do Construtor de segmentos](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Para utilizar esse método, o Perfil do cliente em tempo real precisa ser ativado para o conjunto de dados.

Na interface do Experience Platform, clique em **[!UICONTROL Segmentos]** na navegação à esquerda e em **[!UICONTROL Criar segmento]**.

![](../images/user-guide/segments_new.png)

O **Construtor de segmentos** é exibido. Na coluna **[!UICONTROL Campos]** esquerda e na guia **[!UICONTROL Atributos]**, clique na pasta denominada **[!UICONTROL Perfil Individual XDM]** e, em seguida, clique na pasta com o namespace da sua organização. A pasta denominada **[!UICONTROL IA do cliente]** contém os resultados de execuções de previsão e é nomeada após a instância à qual as pontuações pertencem. Clique em uma pasta de instâncias para acessar os resultados da instância desejada.

![](../images/user-guide/results_new.png)

Localizado no centro do Construtor de segmentos, arraste e solte o atributo **[!UICONTROL Pontuação]** na *tela do construtor de regras* para definir uma regra.

Na coluna à direita *Propriedades do segmento*, forneça um nome para o segmento.

![](../images/user-guide/properties_new.png)

Acima da coluna à esquerda *Campos*, clique no ícone **engrenagem** e selecione uma *Política de mesclagem* no menu suspenso. Clique em **[!UICONTROL Salvar]** para criar o segmento.

![](../images/user-guide/merge_policy_new.png)

## Próximas etapas

Ao seguir este tutorial, você encontrou públicos-alvo com sucesso com base em suas pontuações de propensão usando o Construtor de segmentos. Agora é possível direcionar os públicos-alvo ativando-os para destinos. Consulte a [visão geral dos destinos](../../../destinations/home.md) para obter mais informações.
