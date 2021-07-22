---
keywords: Experience Platform, interface do usuário, interface do usuário, painéis, painel, perfis, segmentos, destinos, uso de licença
title: Editar esquema para criar widgets de painel personalizados
description: 'Este guia fornece instruções passo a passo para selecionar atributos e configurar o esquema da sua organização para criar widgets personalizados para painéis do Adobe Experience Platform. '
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: 16a8764fd27e6b1ae32bc37b3abcd521aaf88887
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Editar esquema para criar widgets personalizados

Para criar widgets personalizados para painéis do Adobe Experience Platform, primeiro você deve identificar os atributos de Perfil do cliente em tempo real nos quais os widgets serão baseados.

Este guia fornece instruções passo a passo para editar o esquema da organização selecionando atributos para criar widgets de painel personalizados.

Depois que os atributos tiverem sido selecionados e o esquema tiver sido configurado, você poderá prosseguir com as etapas para [criar widgets personalizados para seus painéis](custom-widgets.md).

>[!NOTE]
>
>Os usuários devem receber a permissão &quot;Gerenciar painéis padrão&quot; para poder editar o esquema. Para obter etapas sobre a concessão de permissões de acesso para painéis, consulte o [guia de permissões do painel](../permissions.md).

## Biblioteca de widgets {#widget-library}

Este guia requer acesso à [!UICONTROL biblioteca de widgets] no Experience Platform. Para saber mais sobre a biblioteca de widgets e como acessá-la na interface do usuário, comece lendo a [visão geral da biblioteca de widgets](widget-library.md).

## Editar esquema

Na biblioteca de widgets, a guia **[!UICONTROL Custom]** permite criar widgets e compartilhá-los com outros usuários na organização para personalizar a aparência dos painéis.

Antes de criar widgets personalizados, os atributos de Perfil do cliente em tempo real devem ser selecionados para garantir que os dados sejam incluídos como parte do instantâneo diário.

>[!IMPORTANT]
>
>Sua organização pode selecionar no máximo 20 atributos.

Se sua organização não tiver selecionado nenhum atributo de perfil, comece selecionando **[!UICONTROL Editar esquema]** no canto superior direito da biblioteca de widgets.

Quando pelo menos um atributo personalizado tiver sido criado, selecione **[!UICONTROL Edit schema]** para exibir os atributos selecionados e adicionar mais.

![](../images/customization/edit-schema.png)

## Selecionar um atributo

Para selecionar um atributo na caixa de diálogo **[!UICONTROL Selecionar campo de esquema de união]**, navegue até o atributo no esquema de união (ou use pesquisa) e marque a caixa de seleção ao lado do atributo. Marcar a caixa de seleção também adiciona o atributo à lista **[!UICONTROL Atributos selecionados]** no lado direito da caixa de diálogo.

>[!NOTE]
>
>Para que um atributo fique visível para seleção, ele deve ser um dos seguintes: Sequência, Data, Data-Hora, Booleano, Curto, Longo, Número Inteiro ou Byte. Os tipos de dados Mapear e Duplicar não são suportados e ficam esmaecidos para que não possam ser selecionados.

Depois de escolher os atributos que deseja adicionar, selecione **[!UICONTROL Save]** para salvar os atributos e retornar à guia de widgets personalizados.

>[!WARNING]
>Os atributos recém-selecionados ficam disponíveis após o próximo instantâneo diário quando os dados são atualizados.

![](../images/customization/select-attribute.png)

## Próximas etapas

Após a leitura deste guia, você pode navegar até a biblioteca de widgets e selecionar Atributos de perfil do cliente em tempo real para configurar seu esquema. Com os atributos de perfil selecionados, você pode começar a [criar widgets personalizados para seus painéis](custom-widgets.md).