---
keywords: Experience Platform;interface do usuário;UI;painéis;painel;perfis;segmentos;destinos;uso de licença;widgets;métricas;
title: Criação de widgets personalizados para painéis
description: Este guia fornece instruções passo a passo para criar widgets personalizados para uso em painéis do Adobe Experience Platform.
exl-id: 0168ab1e-0b7d-4faf-852e-7208a2b09a04
source-git-commit: 32dd90018c990e7013d826b29608a61022ba808b
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 0%

---

# Criação de widgets personalizados para painéis

No Adobe Experience Platform, você pode visualizar e interagir com os dados de sua organização usando vários painéis. Você também pode atualizar determinados painéis adicionando novos widgets à visualização de painel. Além dos widgets padrão fornecidos pelo Adobe, você também pode criar widgets personalizados e compartilhá-los em toda a sua organização.

Este guia fornece instruções passo a passo para criar e adicionar widgets personalizados aos painéis [!UICONTROL Perfis], [!UICONTROL Segmentos] e [!UICONTROL Destinos] na interface do usuário da plataforma.

>[!NOTE]
>
>Todas as atualizações feitas nos painéis são por organização e por sandbox.

Para saber mais sobre widgets padrão, consulte o manual para [adicionar widgets padrão aos seus painéis](standard-widgets.md).

## Biblioteca de dispositivos {#widget-library}

Este guia requer acesso à [!UICONTROL Biblioteca de widgets] no Experience Platform. Para saber mais sobre a biblioteca de widgets e como acessá-la na interface do usuário, comece lendo a [visão geral da biblioteca de widgets](widget-library.md).

## Introdução a widgets personalizados

Na biblioteca de widgets, a guia **[!UICONTROL Personalizado]** permite criar widgets e compartilhá-los com outros usuários em sua organização para personalizar a aparência de seus painéis.

>[!IMPORTANT]
>
>Sua organização pode criar no máximo 20 widgets personalizados na biblioteca de widgets.

Selecione a guia **[!UICONTROL Personalizado]** para começar a criar widgets personalizados ou para exibir widgets personalizados já criados por sua organização.

![O espaço de trabalho da biblioteca de widgets com a guia Personalizada realçada.](../images/customization/custom-widgets.png)

## Criar um widget personalizado

Para criar um widget personalizado, selecione **[!UICONTROL Criar widget]** no canto superior direito da biblioteca de widgets ou, se este for o primeiro widget personalizado de sua organização, selecione **[!UICONTROL Criar]** no centro da biblioteca de widgets.

![A guia Personalizado do espaço de trabalho da biblioteca de widgets com Criar realçado.](../images/customization/create-widget.png)

Na caixa de diálogo **[!UICONTROL Criar widget]**, forneça um título e uma descrição para o novo widget e escolha o atributo que deseja que o widget exiba.

>[!NOTE]
>
>A lista de atributos disponíveis depende do esquema que foi configurado para sua organização. Para saber mais sobre a seleção de atributos e a configuração de esquema, leia o manual sobre [edição do esquema para criar widgets personalizados](edit-schema.md).

Para escolher um atributo, selecione o botão de opção ao lado do atributo que deseja adicionar.

>[!NOTE]
>
>Somente um atributo pode ser selecionado por widget e somente um widget pode ser criado por atributo. Se um widget já tiver sido criado para um atributo, ele aparecerá esmaecido.

![A caixa de diálogo Criar widget.](../images/customization/create-widget-dialog.png)

## Selecionar uma visualização

Depois de selecionar um atributo, uma visualização do novo widget é exibida na caixa de diálogo. A inteligência artificial é usada para selecionar automaticamente uma visualização que melhor se adapta aos dados do atributo e para fornecer opções de visualização adicionais que você pode selecionar manualmente.

Dependendo do atributo, a IA recomenda opções de visualização diferentes. A lista completa de visualizações inclui:

* Gráfico de barras horizontal: as linhas horizontais são usadas para representar valores.
* Gráfico de barras vertical: as linhas verticais são usadas para representar valores.
* Gráfico de rosca: semelhante a um gráfico de pizza, os valores são mostrados como partes ou partes de um todo.
* Gráfico de dispersão: usa um eixo horizontal e vertical para indicar valores.
* Gráfico de linha: Os valores são exibidos usando uma única linha para mostrar as alterações em um período.
* Cartão de número: exibe um número de resumo para representar um único valor de chave.
* Tabela de dados: Os valores são exibidos como linhas em uma tabela.

>[!NOTE]
>
>A única métrica atualmente compatível para todos os atributos é a contagem de perfis.
>
>Os dados mostrados no widget de exemplo são apenas para fins de ilustração. A visualização não exibe os dados reais da sua organização.

Para salvar o novo widget e retornar à guia [!UICONTROL Personalizado], selecione **[!UICONTROL Criar]**.

![A caixa de diálogo Criar widget com as opções de visualização e Criar realçado.](../images/customization/create-widget-select-attribute.png)

O novo widget agora está disponível para ser adicionado a um painel. Para isso, escolha o widget na biblioteca e selecione **[!UICONTROL Adicionar widget]**.

![A guia Personalizado do espaço de trabalho da biblioteca de widgets com o novo widget e Adicionar widget realçados.](../images/customization/custom-widgets-new.png)

## Ocultar um widget personalizado

Após adicionar um widget à biblioteca, ele pode ser oculto selecionando-se as reticências (`...`) no cartão do widget e selecionando-se **[!UICONTROL Ocultar widget]**. Você também pode visualizar e editar o widget na mesma lista suspensa.

Para exibir widgets que foram ocultados, selecione **[!UICONTROL Mostrar widgets ocultos]** no canto superior direito da biblioteca de widgets.

>[!WARNING]
>
>Ocultar um widget na biblioteca não o remove dos painéis de usuários individuais. Se um widget não deve mais ser usado em sua organização, certifique-se de comunicá-lo diretamente a todos os usuários da Platform, pois eles precisarão remover o widget de seus painéis.

![A guia Personalizado do espaço de trabalho da biblioteca de widgets com as opções de menu suspenso de widget e Mostrar widgets ocultos realçados.](../images/customization/hide-widget.png)

## Editar um widget personalizado

Você pode editar widgets personalizados na biblioteca de widgets selecionando as reticências (`...`) no cartão de widget e, em seguida, selecionando **[!UICONTROL Editar]** no menu suspenso.

![As opções de menu suspenso do widget com as reticências e a opção Editar realçada.](../images/customization/custom-widget-edit.png)

Na caixa de diálogo **[!UICONTROL Editar widget]**, você pode editar o título e a descrição do widget, bem como pré-visualizar e selecionar diferentes visualizações. Depois de fazer suas edições, selecione **[!UICONTROL Salvar]** para salvar suas alterações e retornar à guia widgets personalizados.

>[!WARNING]
>
>Editar um widget na biblioteca não atualiza o widget para usuários individuais. Se um widget tiver sido atualizado, certifique-se de comunicar isso diretamente a todos os usuários da Platform, pois eles precisarão remover o widget desatualizado de seus painéis e, em seguida, selecionar e adicionar o widget atualizado da biblioteca de widgets.

![A caixa de diálogo Editar widget.](../images/customization/edit-widget.png)

## Próximas etapas

Depois de ler este documento, você pode acessar a biblioteca de widgets e usá-la para criar e adicionar widgets personalizados para sua organização. Para modificar o tamanho e o local dos widgets exibidos no painel, consulte o [guia de modificação de painéis](modify.md).
