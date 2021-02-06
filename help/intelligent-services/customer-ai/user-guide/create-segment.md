---
keywords: Experience Platform;insights;ajuda do cliente;tópicos populares;segmentos de ajuda do cliente
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Criar segmentos do cliente com pontuações previstas
topic: Create a segment
description: Quando uma execução de previsão é concluída, as pontuações de propensão previstas são automaticamente consumidas pelos Perfis. Enriquecendo Perfis com pontuações de AI do cliente permite que a criação de segmentos do cliente localize audiências com base em suas pontuações de propensão. Esta seção fornece etapas para a criação de segmentos usando o Construtor de segmentos.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# Criar segmentos de clientes com pontuações previstas

Quando uma execução de previsão é concluída, as pontuações de propensão previstas são automaticamente consumidas pelos Perfis. Enriquecendo Perfis com pontuações de AI do cliente permite que a criação de segmentos do cliente localize audiências com base em suas pontuações de propensão. Esta seção fornece etapas para a criação de segmentos usando o Construtor de segmentos. Para obter um tutorial mais robusto sobre a criação de segmentos, consulte o [Guia do usuário do Construtor de segmentos](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Para utilizar esse método, o Perfil do cliente em tempo real precisa estar habilitado para o conjunto de dados.

Na interface do usuário da plataforma, clique em **[!UICONTROL Segmentos]** no painel de navegação esquerdo e clique em **[!UICONTROL Criar segmento]**.

![](../images/user-guide/segments.png)

O **Construtor de segmentos** é exibido. Na coluna **[!UICONTROL Campos]** à esquerda e na guia **[!UICONTROL Atributos]**, clique na pasta **[!UICONTROL Perfil individual XDM]** e clique na pasta com a namespace da sua organização. A pasta chamada **[!UICONTROL AI do cliente]** contém os resultados das execuções de previsão e são nomeados após a instância à qual as pontuações pertencem. Clique em uma pasta de instância para acessar os resultados da instância desejada.

![](../images/user-guide/results.png)

Localizado no centro do Construtor de segmentos, arraste e solte o atributo **[!UICONTROL Pontuação]** na tela *do construtor de regras* para definir uma regra.

Na coluna à direita *Propriedades do segmento*, forneça um nome para o segmento.

![](../images/user-guide/properties.png)

Acima da coluna à esquerda *Campos*, clique no ícone **engrenagem** e selecione uma *Política de mesclagem* no menu suspenso. Clique em **[!UICONTROL Salvar]** para criar o segmento.

![](../images/user-guide/merge_policy.png)

## Próximas etapas

Ao seguir este tutorial, você encontrou audiências com êxito com base em suas pontuações de propensão usando o Construtor de segmentos. Agora você pode público alvo suas audiências ativando-as para destinos. Consulte [visão geral de destinos](../../../destinations/home.md) para obter mais informações.