---
keywords: Experience Platform;interface do usuário;painéis;painel;perfis;segmentos;destinos;;user interface;dashboards;dashboard;profiles;segments;destinations
title: Visão geral da personalização do painel
description: Saiba mais sobre as maneiras de personalizar os dados exibidos nos painéis do Adobe Experience Platform.
exl-id: efabdb61-4148-4b0e-b7a1-6e788b5e43a8
source-git-commit: 32dd90018c990e7013d826b29608a61022ba808b
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---

# Visão geral da personalização do painel

Os perfis, segmentos e painéis de destinos disponíveis no Adobe Experience Platform podem ser personalizados de várias maneiras diferentes. Este guia fornece uma visão geral das personalizações disponíveis, com links para instruções passo a passo que orientam você sobre como personalizar quais widgets são exibidos em seus painéis, bem como o tamanho, a forma e o local desses widgets.

>[!NOTE]
>
>Todas as atualizações feitas nos painéis são por organização e por sandbox.

## Modificar painel

Selecionar **[!UICONTROL Modificar painel]** nos painéis de perfis, segmentos ou destinos permite que você ajuste o tamanho, a ordem e o local dos widgets que estão visíveis no seu painel. Para obter informações sobre como modificar a aparência dos widgets nos painéis, consulte o [guia de modificação de painéis](modify.md).

## A biblioteca de widgets

A biblioteca de widgets no Experience Platform é onde você pode exibir todos os widgets [padrão](#standard-widgets) e [personalizados](#custom-widgets) disponíveis na sua organização. Nos seus painéis (por exemplo, o painel de perfis), você pode selecionar **[!UICONTROL Modificar painel]** para exibir o botão **[!UICONTROL Biblioteca de widgets]**.

![O painel Perfis com o painel Modificar realçado.](../images/customization/modify-dashboard.png)

Selecione **[!UICONTROL Biblioteca de widgets]** para abrir a biblioteca de widgets e exibir todas as métricas padrão disponíveis ou começar a criar widgets personalizados.

![O painel Perfis com a biblioteca Widget realçada.](../images/customization/widget-library-button.png)

### Widgets padrão {#standard-widgets}

Os widgets padrão se referem aos widgets fornecidos pelo Adobe para uso em seus painéis. Esses widgets são somente leitura e não podem ser editados por sua organização.

Na biblioteca de widgets, a guia **[!UICONTROL Padrão]** contém todos os widgets padrão disponíveis fornecidos pelo Adobe. Você pode atualizar seus painéis usando qualquer uma dessas métricas padrão. Para saber mais sobre como adicionar widgets padrão ao seu painel, consulte o guia para [usar widgets padrão em painéis](standard-widgets.md).

### Widgets personalizados {#custom-widgets}

Widgets personalizados se referem a widgets criados e compartilhados por membros de sua organização. Esses widgets são criados por meio da guia **[!UICONTROL Personalizado]** da biblioteca de widgets e exigem que sua organização especifique as métricas disponíveis usando um [esquema](#edit-schema)

Para obter as etapas completas para criar seus próprios widgets, consulte o [guia de widgets personalizados para painéis](custom-widgets.md).

![O espaço de trabalho da biblioteca de dispositivos com realce Padrão e Personalizado.](../images/customization/widget-library.png)

#### Editar esquema {#edit-schema}

Para criar um [widget personalizado](#custom-widgets) para seus painéis, primeiro você deve identificar o atributo Perfil do cliente em tempo real no qual o widget será baseado.

Para obter instruções passo a passo sobre como editar o esquema da sua organização para criar widgets de painel personalizados, visite o manual para [editar seu esquema de painel](edit-schema.md).

## Próximas etapas

Depois de ler este documento, você estará pronto para começar a personalizar seus painéis de Experience Platform, modificando o tamanho, a forma e a ordem dos widgets existentes, adicionando widgets padrão fornecidos pelo Adobe ou criando e compartilhando widgets personalizados com sua organização.
