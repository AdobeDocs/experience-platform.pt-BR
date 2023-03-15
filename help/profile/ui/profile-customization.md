---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;interface do usuário;UI;personalização;detalhes do perfil;detalhes
title: Personalização de detalhes do perfil na interface
description: Este guia fornece instruções passo a passo para personalizar a forma como os dados do Perfil do cliente em tempo real são exibidos na interface do usuário do Adobe Experience Platform.
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] personalização de detalhes {#profile-detail-customization}

Na interface do usuário do Adobe Experience Platform, você pode visualizar e interagir com [!DNL Real-Time Customer Profile] dados sob a forma de perfis de clientes. As informações de perfil exibidas na interface do usuário foram mescladas de vários fragmentos de perfil para formar uma única visualização de cada cliente individual. Isso inclui detalhes como atributos básicos, identidades vinculadas e preferências de canal. Os campos padrão mostrados em perfis também podem ser alterados em um nível organizacional para exibir campos preferenciais [!DNL Profile] atributos. Este guia fornece instruções passo a passo para personalizar a maneira como [!DNL Profile] Os dados do são exibidos na interface do usuário da Platform.

Para obter um guia completo sobre a interface do usuário de perfis, visite o [Guia da interface do usuário do perfil](user-guide.md).

## Reordenar e redimensionar cartões {#reorder-and-resize-cards}

No **[!UICONTROL Detalhe]** do perfil do cliente, é possível selecionar **[!UICONTROL Personalizar detalhes do perfil]** para redimensionar e reordenar os cartões existentes.

![O botão Personalizar detalhes do perfil está realçado no painel Perfil.](../images/profile-customization/customize-profile-details.png)

Depois de optar por modificar o painel, é possível reordenar os cartões selecionando o título do cartão e arrastando e soltando os cartões na ordem desejada. Você também pode redimensionar um cartão selecionando o símbolo de ângulo no canto inferior direito do cartão (`⌟`) e arrastando o cartão para o tamanho desejado. Neste exemplo, a variável **[!UICONTROL Atributos básicos]** está sendo redimensionado.

![O botão de redimensionamento é realçado no cartão de atributos básicos.](../images/profile-customization/resize.png)

A placa selecionada se ajusta ao tamanho desejado e as placas ao redor são reposicionadas dinamicamente. Isso pode fazer com que alguns cartões sejam movidos para linhas adicionais, exigindo que você role para baixo para ver todos os cartões. Por exemplo, quando a variável &quot;[!UICONTROL Atributos básicos]O cartão &quot; foi redimensionado para &quot;[!UICONTROL Identidades vinculadas]O cartão &quot; não está mais visível na linha superior e agora aparece em uma nova segunda linha no perfil (não exibido). Para retornar o &quot;[!UICONTROL Identidades vinculadas]&quot; para a linha superior, você pode arrastá-lo e soltá-lo na posição atual da &quot;[!UICONTROL Preferências de canal]&quot;.

![Uma placa redimensionada é realçada.](../images/profile-customization/resized.png)

## Editar e remover cartões

Além de redimensionar e reordenar cartões, você pode editar o conteúdo de determinados cartões e remover alguns cartões totalmente do painel. Selecione as reticências (`...`) no canto superior direito do cartão para editá-lo ou removê-lo. Isso abre uma lista suspensa com opções para editar ou remover o cartão, dependendo das propriedades do cartão selecionado.

>[!NOTE]
>
>Nem todos os cartões podem ser editados ou removidos. Isso ocorre porque alguns cartões contêm informações somente leitura ou obrigatórias. Se um cartão não tiver elipses no canto superior direito, ele conterá informações somente leitura E necessárias e não poderá ser editado nem removido. Se um cartão tiver elipses no canto e selecioná-lo mostrar apenas uma opção para remover o cartão, as informações do cartão serão somente leitura e não poderão ser editadas.

![A lista suspensa do cartão de edição está realçada. Isso inclui opções para editar ou remover o cartão.](../images/profile-customization/edit-card.png)

Selecionar **[!UICONTROL Editar]** na lista suspensa para abrir a variável **[!UICONTROL Editar widget]** espaço de trabalho, onde é possível atualizar o título do cartão, reordenar ou remover os atributos visíveis ou adicionar outros atributos usando o **[!UICONTROL Adicionar atributos]** botão.

![O cartão Basic attributes é exibido.](../images/profile-customization/basic-attributes.png)

## Adicionar atributos {#add-attributes}

No **[!UICONTROL Editar widget]** , selecione **[!UICONTROL Adicionar atributos]** no canto superior direito do cartão para começar a adicionar atributos a ele.

![O botão Add attributes (Adicionar atributos) no cartão Basic attributes (Atributos básicos) é realçado.](../images/profile-customization/add-attributes.png)

Quando a variável **[!UICONTROL Selecionar campo de esquema de união]** será aberta, o lado esquerdo da caixa de diálogo mostrará a [!UICONTROL Perfil individual XDM] esquema de união, com campos aninhados abaixo de. Para obter mais informações sobre schemas de união, consulte o [esquemas de união seção do [!DNL Profile] guia do usuário](user-guide.md#union-schema).

A variável **[!UICONTROL Atributos Selecionados]** A seção no lado direito da caixa de diálogo mostra os atributos que estão incluídos atualmente no cartão que você está editando. Também é possível remover e reordenar atributos aqui. O número total de atributos selecionados é exibido, bem como o número máximo de atributos (20) que podem ser adicionados a um único cartão.

![Os atributos que atualmente compõem os atributos no cartão são destacados.](../images/profile-customization/select-before.png)

Selecione qualquer um dos campos de esquema de união disponíveis para personalizar os atributos no cartão que você está editando. Os campos selecionados são mostrados com uma marca de seleção ao lado deles e são adicionados automaticamente à lista de atributos selecionados. Depois de adicionar todos os atributos que gostaria de exibir no cartão, escolha **[!UICONTROL Selecionar]** para retornar ao **[!UICONTROL Editar widget]** tela.

![Os atributos recém-adicionados são destacados.](../images/profile-customization/select-after.png)

Quando você retornar ao **[!UICONTROL Editar widget]** , a lista de atributos no cartão agora deve ser atualizada para refletir suas escolhas. Você ainda pode remover ou reordenar os atributos do cartão ou editar o título do cartão, conforme necessário. Quando as edições estiverem concluídas, selecione **[!UICONTROL Salvar]** para salvar as alterações.

![Os atributos recém-adicionados são exibidos no cartão editado.](../images/profile-customization/new-attributes.png)

Depois de salvar, você retornará para a **[!UICONTROL Detalhe]** guia, onde o cartão atualizado e os atributos estão visíveis.

![Os atributos recém-adicionados são exibidos no cartão, no painel Perfil.](../images/profile-customization/added-attributes.png)

## Adicionar um novo cartão {#add-a-new-card}

Para personalizar ainda mais a aparência dos perfis no Experience Platform, você pode optar por adicionar novos cartões ao painel e selecionar os atributos que deseja exibir nesses cartões. Para começar, selecione **[!UICONTROL Modificar painel]** no **[!UICONTROL Detalhe]** guia.

![O botão Personalizar detalhes do perfil é realçado.](../images/profile-customization/customize-profile-details.png)

Em seguida, selecione **[!UICONTROL Adicionar widget]** no canto superior esquerdo do painel.

![O botão Adicionar widget está realçado.](../images/profile-customization/add-widget.png)

Optar por adicionar um novo cartão abre a **[!UICONTROL Editar widget]** tela onde você pode fornecer um título para o novo cartão e escolher os atributos que deseja que o cartão exiba. Para começar a adicionar atributos ao cartão, selecione **[!UICONTROL Adicionar atributos]**.

![Um novo cartão de widget em branco é exibido na tela Editar widget.](../images/profile-customization/edit-widget.png)

Quando a variável **[!UICONTROL Selecionar campo de esquema de união]** será aberta, o lado esquerdo da caixa de diálogo mostrará a [!UICONTROL Perfil individual XDM] esquema de união e o **[!UICONTROL Atributos Selecionados]** A seção no lado direito da caixa de diálogo mostra os atributos selecionados para o cartão. Para obter mais informações sobre a adição de atributos, consulte [seção sobre adição de atributos](#add-attributes) que aparece anteriormente neste documento.

O número total de atributos selecionados é exibido, bem como o número máximo de atributos (20) que podem ser adicionados a um único cartão. Você também pode remover e reordenar os atributos selecionados nesta tela. Depois de adicionar todos os atributos que gostaria de exibir no cartão, escolha **[!UICONTROL Selecionar]** para retornar ao **[!UICONTROL Editar widget]** tela.

![Os campos que você está adicionando ao cartão são realçados.](../images/profile-customization/add-widget-attributes.png)

Quando você retornar ao **[!UICONTROL Editar widget]** , a lista de atributos no cartão deve refletir suas escolhas da tela anterior. Também é possível reordenar e remover atributos do cartão, conforme necessário.

Para salvar o novo cartão, primeiro forneça um **[!UICONTROL Título do cartão]**, você poderá selecionar **[!UICONTROL Salvar]** e conclua o processo de criação do cartão.

![O novo widget é visualizado na tela Editar widget.](../images/profile-customization/new-widget.png)

Depois de salvar, você retornará para a **[!UICONTROL Detalhe]** onde seu novo cartão e atributos estarão visíveis.

![O novo widget é adicionado ao painel Perfil.](../images/profile-customization/added-widget.png)

## Restaurar cartões padrão

Se, a qualquer momento, você decidir que deseja restaurar os cartões padrão que foram removidos desde então, poderá fazê-lo de forma rápida e fácil. Primeiro, selecione **[!UICONTROL Modificar painel]** e selecione **[!UICONTROL Restaurar cartões padrão]**. Quando os cartões padrão estiverem visíveis, você poderá selecionar **[!UICONTROL Salvar]** para salvar as alterações ou selecionar **[!UICONTROL Cancelar]** se não quiser restaurar os cartões padrão.

![O botão Restaurar cartões padrão é realçado no painel Perfil.](../images/profile-customization/restore-default.png)

## Próximas etapas

Ao seguir esse documento, agora você pode atualizar a visualização de perfil da sua organização, incluindo adicionar e remover cartões, editar detalhes e atributos do cartão e reordenar e redimensionar cartões. Para saber mais sobre como trabalhar com [!DNL Profile] na interface do usuário do Experience Platform, consulte a seção [[!DNL Profile] guia do usuário](user-guide.md).
