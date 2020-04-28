---
keywords: Experience Platform;insights; customer ai;popular topics
solution: Experience Platform
title: Criar segmentos de clientes com pontuações previstas
topic: Create a segment
translation-type: tm+mt
source-git-commit: 66ccea896846c1da4310c1077e2dc7066a258063

---


# Criar segmentos de clientes com pontuações previstas

Quando uma execução de previsão é concluída, as pontuações de propensão previstas são automaticamente consumidas pelos Perfis. Enriquecendo Perfis com pontuações de AI do cliente permite que a criação de segmentos do cliente localize audiências com base em suas pontuações de propensão. Esta seção fornece etapas para a criação de segmentos usando o Construtor de segmentos. Para obter um tutorial mais robusto sobre a criação de segmentos, consulte o guia [do usuário do Construtor de](../../../segmentation/tutorials/create-a-segment.md)segmentos.

>[!IMPORTANT] Para utilizar esse método, o Perfil do cliente em tempo real precisa estar habilitado para o conjunto de dados.

Na interface do usuário da plataforma, clique **[!UICONTROL Segments]** no painel de navegação esquerdo e clique em **[!UICONTROL Create segment]**.

![](../images/user-guide/segments.png)

O Construtor *de segmentos* é exibido. Na coluna *Campos* à esquerda e na guia *Atributos* , clique na pasta nomeada **[!UICONTROL XDM Individual Profile]** e clique na pasta com a namespace de sua organização. A pasta nomeada **[!UICONTROL Customer AI]** contém os resultados das execuções de previsão e é nomeada após a instância à qual as pontuações pertencem. Clique em uma pasta de instância para acessar os resultados da instância desejada.

![](../images/user-guide/results.png)

Localizado no centro do Construtor de segmentos, arraste e solte o **[!UICONTROL Score]** atributo na tela *do construtor de* regras para definir uma regra.

Na coluna de propriedades *do* segmento à direita, forneça um nome para o segmento.

![](../images/user-guide/properties.png)

Acima da coluna *Campos* à esquerda, clique no ícone de **engrenagem** e selecione uma política *de* mesclagem no menu suspenso. Clique em **[!UICONTROL Save]** para criar o segmento.

![](../images/user-guide/merge_policy.png)

## Próximas etapas

Ao seguir este tutorial, você encontrou audiências com êxito com base em suas pontuações de propensão usando o Construtor de segmentos. Agora você pode público alvo suas audiências ativando-as para destinos. Consulte a visão geral [de](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) destinos para obter mais informações.