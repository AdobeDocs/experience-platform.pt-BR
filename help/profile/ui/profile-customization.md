---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Personalização de detalhes do perfil
description: 'Este guia fornece instruções passo a passo para personalizar a forma como os dados do Perfil do cliente em tempo real são exibidos na interface do usuário do Adobe Experience Platform. '
topic: guide
translation-type: tm+mt
source-git-commit: c3076b37d2242fce4fa62e747adeb8b0534e995d
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] personalização detalhada {#profile-detail-customization}

Na interface do usuário do Adobe Experience Platform, você pode visualização e interagir com [!DNL Real-time Customer Profile] dados na forma de perfis do cliente. As informações do perfil exibidas na interface do usuário foram unidas de vários fragmentos de perfil para formar uma única visualização de cada cliente individual. Isso inclui detalhes como atributos básicos, identidades vinculadas e preferências de canal. Os campos padrão mostrados em perfis também podem ser alterados em um nível organizacional para exibir [!DNL Profile] os atributos preferenciais. Este guia fornece instruções passo a passo para personalizar a forma como [!DNL Profile] os dados são exibidos na interface da plataforma.

Para obter um guia completo da interface do usuário dos [!UICONTROL Perfis] , visite o guia [do usuário do](user-guide.md)Perfil.

## Reorganizar e redimensionar cartões {#reorder-and-resize-cards}

Na guia [!UICONTROL Detalhe] do perfil do cliente, é possível selecionar **[!UICONTROL Modificar painel]** para redimensionar e reordenar os cartões existentes.

![](../images/profile-customization/profiles-modify-dashboard.png)

Depois de escolher modificar o painel, você pode reordenar os cartões selecionando o título do cartão e arrastando e soltando os cartões na ordem desejada. Você também pode redimensionar um cartão selecionando o símbolo de ângulo no canto inferior direito do cartão (`⌟`) e arrastando o cartão para o tamanho desejado. Neste exemplo, o cartão de atributos **** básicos está sendo redimensionado.

![](../images/profile-customization/profiles-resize-cards.png)

O cartão selecionado se ajusta ao tamanho desejado e as placas adjacentes são reposicionadas dinamicamente. Isso pode fazer com que alguns cartões sejam movidos para linhas adicionais, exigindo que você role para baixo para ver todos os cartões. Por exemplo, quando o cartão de atributos  básicos é redimensionado, o cartão de identidades  vinculadas não fica mais visível na linha superior e agora aparece em uma nova segunda linha dentro do perfil (não exibido). Para retornar o cartão de identidades [!UICONTROL vinculadas à linha superior, você pode arrastá-lo e soltá-lo na posição atual do cartão de preferências] do  Canal.

![](../images/profile-customization/profiles-card-resized.png)

## Editar e remover cartões

Além de redimensionar e reorganizar cartões, você pode editar o conteúdo de certos cartões e remover alguns cartões do painel totalmente. Selecione as elipses (`...`) no canto superior direito do cartão para editá-lo ou removê-lo. Isso abre uma lista suspensa com opções para editar ou remover o cartão, dependendo das propriedades do cartão selecionado.

>[!NOTE]
>
>Nem todos os cartões podem ser editados ou removidos. Isso ocorre porque alguns cartões contêm informações somente leitura ou obrigatórias. Se um cartão não tiver elipses no canto superior direito, ele contém informações somente leitura E necessárias e não pode ser editado nem removido. Se um cartão tiver elipses no canto e selecioná-lo mostrará apenas uma opção para remover o cartão, as informações do cartão serão somente leitura e não poderão ser editadas.

![](../images/profile-customization/profiles-edit-remove-resized.png)

Selecione **[!UICONTROL Editar]** na lista suspensa para abrir a área de trabalho **[!UICONTROL Editar widget]** , onde você pode atualizar o título do cartão, reordenar ou remover os atributos visíveis ou adicionar outros atributos usando o botão [!UICONTROL Adicionar atributos] .

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## Adicionar atributos {#add-attributes}

Na tela [!UICONTROL Editar widget] , selecione **[!UICONTROL Adicionar atributos]** no canto superior direito do cartão para começar a adicionar atributos ao cartão.

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

Quando a caixa de diálogo [!UICONTROL Selecionar schema] da união é aberta, o lado esquerdo da caixa de diálogo mostra o schema completo da união do Perfil [!UICONTROL individual] XDM, com os campos aninhados abaixo. Para obter mais informações sobre schemas de união, consulte a seção schemas de [união do guia [!DNL Profile] ](user-guide.md#union-schema)do usuário.

A seção Atributos **** selecionados no lado direito da caixa de diálogo mostra os atributos que estão incluídos no cartão que você está editando. Você também pode remover e reordenar atributos aqui. O número total de atributos selecionados é mostrado, assim como o número máximo de atributos (20) que podem ser adicionados a um único cartão.

![](../images/profile-customization/profiles-select-field-before.png)

Você pode selecionar qualquer um dos campos de schema de união disponíveis para personalizar os atributos no cartão que você está editando. Os campos selecionados são mostrados com uma marca de seleção ao lado deles e são adicionados automaticamente à lista dos atributos selecionados. Depois de adicionar todos os atributos que você gostaria que fossem exibidos no cartão, escolha **[!UICONTROL Selecionar]** para retornar à tela [!UICONTROL Editar widget] .

![](../images/profile-customization/profiles-select-field-after.png)

Quando você retorna à tela [!UICONTROL Editar widget] , a lista de atributos no cartão agora deve ser atualizada para refletir suas opções. Você ainda pode remover ou reordenar os atributos do cartão ou editar o título do cartão, conforme necessário. Quando as edições estiverem concluídas, selecione **[!UICONTROL Salvar]** para salvar as alterações.

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

Depois de salvar, você retornará à guia [!UICONTROL Detalhe] , onde o cartão e os atributos atualizados estarão visíveis.

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## Add a new card {#add-a-new-card}

Para personalizar ainda mais a aparência dos perfis dentro do Experience Platform, você pode optar por adicionar novos cartões ao painel e selecionar os atributos que deseja exibir nesses cartões. Para começar, selecione **[!UICONTROL Modificar painel]** na guia [!UICONTROL Detalhe] .

![](../images/profile-customization/profiles-modify-dashboard.png)

Em seguida, selecione **[!UICONTROL Adicionar widget]** no canto superior esquerdo do painel.

![](../images/profile-customization/profiles-add-widget.png)

A opção de adicionar um novo cartão abre a tela [!UICONTROL Editar widget] , onde você pode fornecer um título para o novo cartão e escolher os atributos que deseja que o cartão exiba. Para começar a adicionar atributos ao cartão, selecione **[!UICONTROL Adicionar atributos]**.

![](../images/profile-customization/profiles-edit-new-widget.png)

Quando a caixa de diálogo **[!UICONTROL Selecionar schema da união]** é aberta, o lado esquerdo da caixa de diálogo mostra o schema completo da união do Perfil [!UICONTROL individual] XDM e a seção Atributos **** selecionados no lado direito da caixa de diálogo mostra os atributos que você selecionou para o cartão. Para obter mais informações sobre como adicionar atributos, consulte a [seção sobre como adicionar atributos](#add-attributes) que aparece anteriormente neste documento.

O número total de atributos selecionados é mostrado, assim como o número máximo de atributos (20) que podem ser adicionados a um único cartão. Você também pode remover e reordenar os atributos selecionados desta tela. Depois de adicionar todos os atributos que você gostaria de exibir no cartão, escolha **[!UICONTROL Selecionar]** para retornar à tela [!UICONTROL Editar widget] .

![](../images/profile-customization/profiles-add-fields-new-widget.png)

Quando você retorna à tela [!UICONTROL Editar widget] , a lista de atributos no cartão deve refletir suas opções da tela anterior. Você também pode reordenar e remover atributos de cartão, conforme necessário.

Para salvar seu novo cartão, é necessário fornecer primeiro um título **[!UICONTROL de]** cartão, em seguida, você poderá selecionar **[!UICONTROL Salvar]** e concluir o processo de criação do cartão.

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

Depois de salvar, você retornará à guia [!UICONTROL Detalhe] , onde seu novo cartão e os atributos ficam visíveis.

![](../images/profile-customization/profiles-detail-new-widget.png)

## Restaurar cartões padrão

Se você decidir remover as edições e retornar à visualização padrão a qualquer momento, poderá restaurar rápida e facilmente todos os cartões e atributos padrão. Para fazer isso, selecione **[UICONTROL Modify painel]** e, em seguida, selecione **[UICONTROL Restore default cards]**. Isso removerá todas as personalizações (incluindo o redimensionamento) feitas. Para continuar, selecione **[UICONTROL Salvar]** para salvar as alterações ou, se você tiver selecionado restaurar por engano, selecione **[UICONTROL Cancelar]** para evitar salvar as alterações e manter as edições feitas.

>[!NOTE]
>
>Tenha cuidado ao restaurar cartões e atributos padrão. Depois que o padrão for restaurado e salvo, a única maneira de retornar às personalizações de visualização será criá-las novamente usando as etapas descritas neste documento.

![](../images/profile-customization/profiles-restore-default.png)

## Próximas etapas

Ao seguir este documento, você deve ser capaz de atualizar a visualização do perfil de sua organização, incluindo adicionar e remover cartões, editar detalhes e atributos do cartão e reorganizar e redimensionar cartões. Para saber mais sobre como trabalhar com [!DNL Profile] dados na interface do usuário do Experience Platform, consulte o guia do [[!DNL Profile] usuário](user-guide.md).