---
keywords: conectar destino, conexão de destino, como conectar destino
title: Criar uma nova conexão de destino
type: Tutorial
description: Este tutorial lista as etapas para se conectar a um destino no Adobe Experience Platform
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: b275621d9c6552327e0e55c00c8fcf0397088168
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Criar uma nova conexão de destino

## Visão geral {#overview}

Antes de enviar dados do público-alvo para um destino, você deve configurar uma conexão com a plataforma de destino. Este artigo mostra como configurar um novo destino usando a interface do usuário do Adobe Experience Platform.

## Criar uma nova conexão de destino {#setup}

1. Ir para **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]** e selecione o **[!UICONTROL Catálogo]** guia .

   ![Página do catálogo](../assets/ui/connect-destinations/catalog.png)

1. Dependendo de você ter uma conexão existente com seu destino, você pode ver uma **[!UICONTROL Configurar]** ou **[!UICONTROL Ativar segmentos]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativar segmentos]** e **[!UICONTROL Configurar]**, consulte o [Catálogo](../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino.

   Selecione um **[!UICONTROL Configurar]** ou **[!UICONTROL Ativar segmentos]**, dependendo de qual botão está disponível.

   ![Página do catálogo](../assets/ui/connect-destinations/set-up.png)

   ![Ativar segmentos](../assets/ui/connect-destinations/activate-segments.png)

1. Se você selecionou **[!UICONTROL Configurar]**, pule para a próxima etapa.

   Se você selecionou **[!UICONTROL Ativar segmentos]**, agora é possível ver uma lista de conexões de destino existentes.

   Selecionar **[!UICONTROL Configurar novo destino]**.

   ![Configurar novo destino](../assets/ui/connect-destinations/configure-new-destination.png)

1. Insira os detalhes de conexão da plataforma de destino e selecione **[!UICONTROL Ligar ao destino]**.

   >[!NOTE]
   >
   >A imagem abaixo é usada somente para fins ilustrativos. Os detalhes da conexão de destino variam entre destinos. Para obter informações detalhadas sobre os detalhes da conexão com seu destino, consulte o **Parâmetros de conexão** em cada [catálogo de destino](../catalog/overview.md) page (por exemplo, [Correspondência de cliente do Google](..//catalog/advertising/google-customer-match.md#parameters)).

   ![Ligar ao destino](../assets/ui/connect-destinations/connect-destination.png)

1. (Opcional) Selecione os alertas de fluxo de dados de destino que você deseja assinar. Você pode assinar alertas ao criar um fluxo de dados para receber mensagens de alerta sobre o status, o sucesso ou a falha da execução do fluxo. Consulte [Assinar alertas de destino no contexto](alerts.md) para obter informações detalhadas sobre alertas de fluxo de dados de destino.

   ![Imagem da interface do usuário que mostra as opções de assinatura de alertas de destino no contexto](../assets/ui/connect-destinations/subscribe-to-alerts.png)

1. Selecione **[!UICONTROL Próximo]**.

   ![Ligar ao destino](../assets/ui/connect-destinations/next.png)

1. Selecione as ações de marketing aplicáveis aos dados que você deseja exportar para o destino. As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte o [visão geral das políticas de uso de dados](../../data-governance/policies/overview.md) página.

   ![Selecionar ações de marketing](../assets/ui/connect-destinations/governance.png)

1. Selecionar **[!UICONTROL Salvar e sair]** para salvar a configuração de destino, ou selecione **[!UICONTROL Próximo]** para prosseguir para os dados do público-alvo [fluxo de ativação](activation-overview.md).