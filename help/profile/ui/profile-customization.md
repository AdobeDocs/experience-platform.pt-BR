---
keywords: Experience Platform;perfil;perfil; do cliente em tempo real;interface do usuário;personalização;detalhes do perfil;detalhes
title: Personalizar como você Visualização Perfis na interface do usuário
description: 'Este guia fornece instruções passo a passo para personalizar a forma como os dados do Perfil do cliente em tempo real são exibidos na interface do usuário do Adobe Experience Platform. '
topic: guide
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] personalização detalhada  {#profile-detail-customization}

Na interface do usuário do Adobe Experience Platform, você pode visualização e interagir com [!DNL Real-time Customer Profile] dados na forma de perfis do cliente. As informações do perfil exibidas na interface do usuário foram unidas de vários fragmentos de perfil para formar uma única visualização de cada cliente individual. Isso inclui detalhes como atributos básicos, identidades vinculadas e preferências de canal. Os campos padrão mostrados em perfis também podem ser alterados em um nível organizacional para exibir os atributos preferenciais [!DNL Profile]. Este guia fornece instruções passo a passo para personalizar a forma como os dados [!DNL Profile] são exibidos na interface do usuário da plataforma.

Para obter um guia completo da interface do usuário do Perfil, visite o [guia da interface do usuário do Perfil](user-guide.md).

## Reorganizar e redimensionar cartões {#reorder-and-resize-cards}

Na guia **[!UICONTROL Detail]** do perfil do cliente, você pode selecionar **[!UICONTROL Modificar painel]** para redimensionar e reordenar os cartões existentes.

![](../images/profile-customization/profiles-modify-dashboard.png)

Depois de escolher modificar o painel, você pode reordenar os cartões selecionando o título do cartão e arrastando e soltando os cartões na ordem desejada. Você também pode redimensionar um cartão selecionando o símbolo de ângulo no canto inferior direito do cartão (`⌟`) e arrastando o cartão para o tamanho desejado. Neste exemplo, o cartão **[!UICONTROL Atributos básicos]** está sendo redimensionado.

![](../images/profile-customization/profiles-resize-cards.png)

O cartão selecionado se ajusta ao tamanho desejado e as placas adjacentes são reposicionadas dinamicamente. Isso pode fazer com que alguns cartões sejam movidos para linhas adicionais, exigindo que você role para baixo para ver todos os cartões. Por exemplo, quando o cartão &quot;[!UICONTROL Atributos básicos]&quot; é redimensionado, o cartão &quot;[!UICONTROL Identidades vinculadas]&quot; não é mais visível na linha superior e agora aparece em uma nova segunda linha dentro do perfil (não é exibido). Para retornar o cartão &quot;[!UICONTROL Identidades vinculadas]&quot; para a linha superior, você pode arrastá-lo e soltá-lo na posição atual do cartão &quot;[!UICONTROL Preferências de Canal]&quot;.

![](../images/profile-customization/profiles-card-resized.png)

## Editar e remover cartões

Além de redimensionar e reorganizar cartões, você pode editar o conteúdo de certos cartões e remover alguns cartões do painel totalmente. Selecione as elipses (`...`) no canto superior direito do cartão para editá-lo ou removê-lo. Isso abre uma lista suspensa com opções para editar ou remover o cartão, dependendo das propriedades do cartão selecionado.

>[!NOTE]
>
>Nem todos os cartões podem ser editados ou removidos. Isso ocorre porque alguns cartões contêm informações somente leitura ou obrigatórias. Se um cartão não tiver elipses no canto superior direito, ele contém informações somente leitura E necessárias e não pode ser editado nem removido. Se um cartão tiver elipses no canto e selecioná-lo mostrará apenas uma opção para remover o cartão, as informações do cartão serão somente leitura e não poderão ser editadas.

![](../images/profile-customization/profiles-edit-remove-resized.png)

Selecione **[!UICONTROL Editar]** na lista suspensa para abrir a área de trabalho **[!UICONTROL Editar widget]**, onde você pode atualizar o título do cartão, reordenar ou remover os atributos visíveis, ou adicionar outros atributos usando o botão **[!UICONTROL Adicionar atributos]**.

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## Adicionar atributos {#add-attributes}

Na tela **[!UICONTROL Editar widget]**, selecione **[!UICONTROL Adicionar atributos]** no canto superior direito do cartão para começar a adicionar atributos ao cartão.

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

Quando a caixa de diálogo **[!UICONTROL Selecionar schema de união campo]** é aberta, o lado esquerdo da caixa de diálogo mostra o schema de união [!UICONTROL Perfil Individual XDM] completo, com os campos aninhados abaixo. Para obter mais informações sobre schemas de união, consulte a seção [schemas de união do [!DNL Profile] guia do usuário](user-guide.md#union-schema).

A seção **[!UICONTROL Atributos Selecionados]** no lado direito da caixa de diálogo mostra os atributos que estão incluídos atualmente no cartão que você está editando. Você também pode remover e reordenar atributos aqui. O número total de atributos selecionados é mostrado, assim como o número máximo de atributos (20) que podem ser adicionados a um único cartão.

![](../images/profile-customization/profiles-select-field-before.png)

Você pode selecionar qualquer um dos campos de schema de união disponíveis para personalizar os atributos no cartão que você está editando. Os campos selecionados são mostrados com uma marca de seleção ao lado deles e são adicionados automaticamente à lista dos atributos selecionados. Depois de adicionar todos os atributos que você gostaria que fossem exibidos no cartão, escolha **[!UICONTROL Selecionar]** para retornar à tela **[!UICONTROL Editar widget]**.

![](../images/profile-customization/profiles-select-field-after.png)

Quando você retorna à tela **[!UICONTROL Editar widget]**, a lista de atributos no cartão agora deve ser atualizada para refletir suas opções. Você ainda pode remover ou reordenar os atributos do cartão ou editar o título do cartão, conforme necessário. Quando as edições estiverem concluídas, selecione **[!UICONTROL Salvar]** para salvar as alterações.

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

Depois de salvar, você retornará à guia **[!UICONTROL Detail]**, na qual o cartão e os atributos atualizados ficam visíveis.

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## Adicionar um novo cartão {#add-a-new-card}

Para personalizar ainda mais a aparência dos perfis dentro do Experience Platform, você pode optar por adicionar novos cartões ao painel e selecionar os atributos que deseja exibir nesses cartões. Para começar, selecione **[!UICONTROL Modificar painel]** na guia **[!UICONTROL Detalhe]**.

![](../images/profile-customization/profiles-modify-dashboard.png)

Em seguida, selecione **[!UICONTROL Adicionar widget]** no canto superior esquerdo do painel.

![](../images/profile-customization/profiles-add-widget.png)

Escolher adicionar um novo cartão abre a tela **[!UICONTROL Editar widget]**, onde você pode fornecer um título para o novo cartão e escolher os atributos que deseja que o cartão exiba. Para começar a adicionar atributos ao cartão, selecione **[!UICONTROL Adicionar atributos]**.

![](../images/profile-customization/profiles-edit-new-widget.png)

Quando a caixa de diálogo **[!UICONTROL Selecionar schema de união campo]** é aberta, o lado esquerdo da caixa de diálogo mostra o schema de união [!UICONTROL Perfil Individual XDM] completo e a seção **[!UICONTROL Atributos Selecionados]** no lado direito da caixa de diálogo mostra os atributos selecionados para o cartão. Para obter mais informações sobre como adicionar atributos, consulte a seção [sobre como adicionar atributos](#add-attributes) que aparece anteriormente neste documento.

O número total de atributos selecionados é mostrado, assim como o número máximo de atributos (20) que podem ser adicionados a um único cartão. Você também pode remover e reordenar os atributos selecionados desta tela. Depois de adicionar todos os atributos que você gostaria de exibir no cartão, escolha **[!UICONTROL Selecionar]** para retornar à tela **[!UICONTROL Editar widget]**.

![](../images/profile-customization/profiles-add-fields-new-widget.png)

Quando você retorna à tela **[!UICONTROL Editar widget]**, a lista de atributos no cartão deve refletir suas opções da tela anterior. Você também pode reordenar e remover atributos de cartão, conforme necessário.

Para salvar seu novo cartão, primeiro forneça um **[!UICONTROL título do cartão]**, você poderá selecionar **[!UICONTROL Salvar]** e concluir o processo de criação do cartão.

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

Depois de salvar, você retornará à guia **[!UICONTROL Detail]**, na qual seu novo cartão e atributos ficam visíveis.

![](../images/profile-customization/profiles-detail-new-widget.png)

## Restaurar cartões padrão

Se você decidir que deseja restaurar os cartões padrão que foram removidos desde então, poderá fazê-lo de forma rápida e fácil. Primeiro, selecione **[!UICONTROL Modificar painel]** e, em seguida, **[!UICONTROL Restaurar cartões predefinidos]**. Quando os cartões padrão estiverem visíveis, você poderá selecionar **[!UICONTROL Salvar]** para salvar suas alterações ou selecionar **[!UICONTROL Cancelar]** se não desejar restaurar os cartões padrão.

![](../images/profile-customization/profiles-restore-default.png)

## Próximas etapas

Ao seguir este documento, você deve ser capaz de atualizar a visualização do perfil de sua organização, incluindo adicionar e remover cartões, editar detalhes e atributos do cartão e reorganizar e redimensionar cartões. Para saber mais sobre como trabalhar com [!DNL Profile] dados na interface do usuário do Experience Platform, consulte [[!DNL Profile] guia do usuário](user-guide.md).