---
keywords: Experience Platform;interface do usuário;painéis;painel;perfis;segmentos;destinos;uso de licença;user interface;dashboards;dashboard;profiles;segments;destinations;license usage
title: Editar esquema para criar widgets de painel personalizados
description: Este guia fornece instruções passo a passo para selecionar atributos e configurar o esquema da sua organização para criar widgets personalizados para painéis do Adobe Experience Platform.
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Editar esquema para criar widgets personalizados

Para criar widgets personalizados para painéis do Adobe Experience Platform, você deve primeiro identificar os atributos do Perfil do cliente em tempo real nos quais os widgets serão baseados.

Este guia fornece instruções passo a passo para editar o esquema da sua organização selecionando atributos para criar widgets de painel personalizados.

Depois que os atributos forem selecionados e o esquema for configurado, você poderá continuar com as etapas para [criação de widgets personalizados para seus painéis](custom-widgets.md).

>[!NOTE]
>
>Os usuários devem receber a permissão &quot;Gerenciar painéis padrão&quot; para poderem editar o esquema. Para obter etapas sobre como conceder permissões de acesso para painéis, consulte o [guia de permissões do painel](../permissions.md).

## Biblioteca de widgets {#widget-library}

Este guia requer acesso à [!UICONTROL Biblioteca de widgets] no Experience Platform. Para saber mais sobre a biblioteca de widgets e como acessá-la na interface do usuário, comece lendo o [visão geral da biblioteca de widgets](widget-library.md).

## Editar esquema

Na biblioteca de widgets, a variável **[!UICONTROL Personalizado]** A guia permite criar widgets e compartilhá-los com outros usuários em sua organização para personalizar a aparência dos painéis.

Antes de criar widgets personalizados, os atributos do Perfil do cliente em tempo real devem ser selecionados para garantir que os dados sejam incluídos como parte do instantâneo diário.

>[!IMPORTANT]
>
>Sua organização pode selecionar no máximo 20 atributos.

Se sua organização não tiver selecionado atributos de perfil, comece selecionando **[!UICONTROL Configurar]** no centro da tela.

![A guia Personalizado da área de trabalho da biblioteca de widgets com Configurar realçado.](../images/customization/configure-schema.png)

Quando pelo menos um atributo personalizado for criado, selecione **[!UICONTROL Editar esquema]** para visualizar os atributos selecionados e adicionar mais.

![A guia Personalizado do espaço de trabalho da biblioteca de widgets com Editar schema realçado.](../images/customization/edit-schema.png)

## Selecionar um atributo

Para selecionar um atributo na variável **[!UICONTROL Selecionar campo de esquema de união]** , navegue até o atributo no esquema de união (ou use pesquisar) e marque a caixa de seleção ao lado do atributo. Marcar a caixa de seleção também adiciona o atributo à variável **[!UICONTROL Atributos Selecionados]** no lado direito da caixa de diálogo.

>[!NOTE]
>
>Para que um atributo seja visível para seleção, ele deve ser um dos seguintes: String, Date, Date-Time, Boolean, Short, Long, Integer ou Byte. Os tipos de dados Map e Double não são compatíveis e estão esmaecidos para que não possam ser selecionados.

Após escolher os atributos que deseja adicionar, selecione **[!UICONTROL Salvar]** para salvar seus atributos e retornar à guia widgets personalizados.

>[!WARNING]
>Os atributos recém-selecionados ficam disponíveis após o próximo snapshot diário quando os dados são atualizados.

![A caixa de diálogo para selecionar atributos de esquema com atributos e Salvar está realçada.](../images/customization/select-attribute.png)

## Próximas etapas

Depois de ler este guia, você pode navegar até a biblioteca de widgets e selecionar atributos do Perfil do cliente em tempo real para configurar seu esquema. Com os atributos de perfil selecionados, você pode começar [criação de widgets personalizados para seus painéis](custom-widgets.md).
