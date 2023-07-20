---
keywords: Experience Platform;insights;ia do cliente;tópicos populares;segmentos de ia do cliente
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Criar segmentos do cliente com pontuações previstas
description: Quando uma execução de previsão é concluída, as pontuações de propensão previstas são consumidas automaticamente pelos Perfis. O enriquecimento dos perfis com pontuações da IA do cliente permite a criação de segmentos de clientes para encontrar públicos com base em suas pontuações de propensão. Esta seção fornece etapas para criar segmentos usando o Construtor de segmentos.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Criar segmentos de clientes com pontuações previstas

Quando uma execução de previsão é concluída, as pontuações de propensão previstas são consumidas automaticamente pelos Perfis. O enriquecimento dos perfis com pontuações da IA do cliente permite a criação de segmentos de clientes para encontrar públicos com base em suas pontuações de propensão. Esta seção fornece etapas para criar segmentos usando o Construtor de segmentos. Para obter um tutorial mais robusto sobre a criação de segmentos, consulte [Guia do usuário do Construtor de segmentos](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Para utilizar esse método, o Perfil do cliente em tempo real precisa ser ativado para o conjunto de dados.

Na interface da Platform, clique em **[!UICONTROL Segmentos]** no painel de navegação esquerdo e, em seguida, clique em **[!UICONTROL Criar segmento]**.

![](../images/user-guide/segments.png)

A variável **Construtor de segmentos** é exibida. Da esquerda **[!UICONTROL Campos]** e abaixo de **[!UICONTROL Atributos]** clique na pasta chamada **[!UICONTROL Perfil individual XDM]** e, em seguida, clique na pasta com o namespace de sua organização. A pasta chamada **[!UICONTROL IA do cliente]** contém os resultados de execuções de previsão e são nomeados com base na instância à qual as pontuações pertencem. Clique em uma pasta de instâncias para acessar os resultados da instância desejada.

![](../images/user-guide/results.png)

Localizado no centro do Construtor de segmentos, arraste e solte a **[!UICONTROL Pontuação]** atributo na *tela do construtor de regras* para definir uma regra.

Sob a mão direita *Propriedades do segmento* , forneça um nome para o segmento.

![](../images/user-guide/properties.png)

Acima da mão esquerda *Campos* clique no link **engrenagem** e selecione um *Política de mesclagem* no menu suspenso. Clique em **[!UICONTROL Salvar]** para criar o segmento.

![](../images/user-guide/merge_policy.png)

## Próximas etapas

Ao seguir este tutorial, você encontrou públicos-alvo com sucesso com base em suas pontuações de propensão usando o Construtor de segmentos. Agora é possível direcionar os públicos-alvo ativando-os para destinos. Consulte a [visão geral dos destinos](../../../destinations/home.md) para obter mais informações.
