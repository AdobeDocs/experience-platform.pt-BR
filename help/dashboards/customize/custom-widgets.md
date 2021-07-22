---
keywords: Experience Platform, interface do usuário, interface do usuário, painéis, painel, perfis, segmentos, destinos, uso de licença, widgets, métricas;
title: Criação de widgets personalizados para painéis
description: 'Este guia fornece instruções passo a passo para a criação de widgets personalizados para uso em painéis do Adobe Experience Platform. '
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: a07eb2baec48ad514ff0afc0548f53baf34da561
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# Criação de widgets personalizados para painéis

No Adobe Experience Platform, você pode visualizar e interagir com os dados de sua organização usando vários painéis. Você também pode atualizar determinados painéis adicionando novos widgets à visualização do painel. Além dos widgets padrão fornecidos pelo Adobe, você também pode criar widgets personalizados e compartilhá-los em toda a organização.

Este guia fornece instruções passo a passo para criar e adicionar widgets personalizados aos painéis [!UICONTROL Perfis], [!UICONTROL Segmentos] e [!UICONTROL Destinos] na interface do usuário da plataforma.

Para saber mais sobre widgets padrão, consulte o guia para [adicionar widgets padrão a seus painéis](standard-widgets.md).

>[!NOTE]
>
>Os widgets mostrados no painel de uso da licença [!UICONTROL Não podem ser personalizados. ] Para saber mais sobre esse painel exclusivo, leia a [documentação do painel de uso da licença](../guides/license-usage.md).

## Biblioteca de widgets {#widget-library}

Este guia requer acesso à [!UICONTROL biblioteca de widgets] no Experience Platform. Para saber mais sobre a biblioteca de widgets e como acessá-la na interface do usuário, comece lendo a [visão geral da biblioteca de widgets](widget-library.md).

## Introdução aos widgets personalizados

Na biblioteca de widgets, a guia **[!UICONTROL Custom]** permite criar widgets e compartilhá-los com outros usuários na organização para personalizar a aparência dos painéis.

>[!IMPORTANT]
>
>Sua organização pode criar no máximo 20 widgets personalizados na biblioteca de widgets.

Selecione a guia **[!UICONTROL Personalizado]** para começar a criar widgets personalizados ou exibir widgets personalizados que sua organização já criou.

![](../images/customization/custom-widgets.png)

## Criar um widget personalizado

Para criar um widget personalizado, selecione **[!UICONTROL Criar]** no centro da biblioteca de widgets ou, se os widgets personalizados já tiverem sido criados, selecione **[!UICONTROL Criar widget]** no canto superior direito da biblioteca de widgets.

![](../images/customization/create-widget.png)

Na caixa de diálogo **[!UICONTROL Criar widget]**, você pode fornecer um título e uma descrição para o novo widget e escolher o atributo que deseja que o widget exiba.

>[!NOTE]
>
>A lista de atributos disponíveis depende do esquema que foi configurado para sua organização. Para saber mais sobre a seleção de atributos e a configuração de esquema, leia o guia em [editar o esquema para criar widgets personalizados](edit-schema.md).

Para escolher um atributo, selecione o botão de opção ao lado do atributo que deseja adicionar.

>[!NOTE]
>
>Somente um atributo pode ser selecionado por widget e apenas um widget pode ser criado por atributo. Se um widget já tiver sido criado para um atributo, o atributo aparecerá esmaecido.

![](../images/customization/create-widget-dialog.png)

## Visualizar widget personalizado

Uma visualização do novo widget é exibida na caixa de diálogo, mostrando um gráfico de barras horizontal com dados de zombaria.

>[!NOTE]
>
>A única métrica atualmente suportada para todos os atributos é a contagem de perfis e a única visualização atualmente suportada para widgets personalizados é um gráfico de barras horizontal.
>
>Os dados mostrados no widget de exemplo são apenas para fins ilustrativos. A visualização não exibe os dados reais da organização.

![](../images/customization/create-widget-select-attribute.png)

Para salvar seu novo widget e retornar à guia [!UICONTROL Personalizado], selecione **[!UICONTROL Criar]**. O novo widget agora está disponível para ser adicionado a um painel ao escolher o widget da biblioteca e selecionar **[!UICONTROL Adicionar widget]**.

## Arquivar um widget personalizado

Depois que um widget é adicionado à biblioteca, ele pode ser arquivado usando o botão **[!UICONTROL Arquivar]**. Também é possível editar o widget para atualizar o título ou os campos de descrição.

## Próximas etapas

Após a leitura deste documento, você poderá acessar a biblioteca de widgets e usá-la para criar e adicionar widgets personalizados à sua organização. Para modificar o tamanho e o local dos widgets exibidos no painel, consulte o [guia modificar painéis](modify.md).
