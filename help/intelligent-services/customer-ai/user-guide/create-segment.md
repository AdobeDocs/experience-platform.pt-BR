---
keywords: Experience Platform;insights; customer ai;popular topics
solution: Experience Platform
title: Criar segmentos de clientes com pontuações previstas
topic: Create a segment
translation-type: tm+mt
source-git-commit: e351a2d489730c1f1bd5f87be8d85612090bc009
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---


# Criar segmentos de clientes com pontuações previstas

Quando uma execução de previsão é concluída, as pontuações de propensão previstas são automaticamente consumidas pelos Perfis. Enriquecendo Perfis com pontuações de AI do cliente permite que a criação de segmentos do cliente localize audiências com base em suas pontuações de propensão. Esta seção fornece etapas para a criação de segmentos usando o Construtor de segmentos. Para obter um tutorial mais robusto sobre a criação de segmentos, consulte o guia [do usuário do Construtor de](../../../segmentation/ui/segment-builder.md)segmentos.

>[!IMPORTANT]
>
>Para utilizar esse método, o Perfil do cliente em tempo real precisa estar habilitado para o conjunto de dados.

Na interface do usuário da plataforma, clique em **[!UICONTROL Segmentos]** no painel de navegação esquerdo e clique em **[!UICONTROL Criar segmento]**.

![](../images/user-guide/segments.png)

O Construtor *de segmentos* é exibido. Na coluna *Campos* à esquerda e na guia *Atributos* , clique na pasta chamada Perfil **[!UICONTROL individual]** XDM e clique na pasta com a namespace de sua organização. A pasta chamada AI **[!UICONTROL do]** cliente contém os resultados de execuções de previsão e são nomeados após a instância à qual as pontuações pertencem. Clique em uma pasta de instância para acessar os resultados da instância desejada.

![](../images/user-guide/results.png)

Localizado no centro do Construtor de segmentos, arraste e solte o atributo **[!UICONTROL Pontuação]** na tela *do construtor de* regras para definir uma regra.

Na coluna de propriedades *do* segmento à direita, forneça um nome para o segmento.

![](../images/user-guide/properties.png)

Acima da coluna *Campos* à esquerda, clique no ícone de **engrenagem** e selecione uma política *de* mesclagem no menu suspenso. Click **[!UICONTROL Save]** to create the segment.

![](../images/user-guide/merge_policy.png)

## Próximas etapas

Ao seguir este tutorial, você encontrou audiências com êxito com base em suas pontuações de propensão usando o Construtor de segmentos. Agora você pode público alvo suas audiências ativando-as para destinos. Consulte a visão geral [de](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) destinos para obter mais informações.