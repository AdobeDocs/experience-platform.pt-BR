---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, interface do usuário, interface do usuário, personalização, detalhes do perfil, detalhes
title: Personalização de detalhes do perfil na interface do usuário
description: Este guia fornece instruções passo a passo para personalizar a maneira como os dados do Perfil do cliente em tempo real são exibidos na interface do usuário do Adobe Experience Platform.
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] personalização detalhada {#profile-detail-customization}

Na interface do usuário do Adobe Experience Platform, é possível visualizar e interagir com [!DNL Real-Time Customer Profile] dados no formato de perfis do cliente. As informações de perfil exibidas na interface do usuário foram unidas de vários fragmentos de perfil para formar uma única visualização de cada cliente individual. Isso inclui detalhes como atributos básicos, identidades vinculadas e preferências de canal. Os campos padrão mostrados nos perfis também podem ser alterados em um nível organizacional para exibir o preferido [!DNL Profile] atributos. Este guia fornece instruções passo a passo para personalizar a maneira pela qual [!DNL Profile] Os dados são exibidos na interface do usuário da plataforma.

Para obter um guia completo da interface do usuário de perfis, visite o [Guia da interface do usuário do perfil](user-guide.md).

## Reordenar e redimensionar cartões {#reorder-and-resize-cards}

No **[!UICONTROL Detalhe]** do perfil do cliente, você pode selecionar **[!UICONTROL Personalizar detalhes do perfil]** para redimensionar e reorganizar os cartões existentes.

![O botão Personalizar detalhes do perfil é realçado no painel Perfil.](../images/profile-customization/customize-profile-details.png)

Depois de escolher modificar o painel, você pode reorganizar os cartões selecionando o título do cartão e arrastando e soltando os cartões na ordem desejada. Você também pode redimensionar um cartão selecionando o símbolo de ângulo no canto inferior direito (`⌟`) e arrastar o cartão para o tamanho desejado. Neste exemplo, a variável **[!UICONTROL Atributos básicos]** cartão está sendo redimensionado.

![O botão resize é realçado no cartão Basic attributes.](../images/profile-customization/resize.png)

O cartão selecionado se ajusta ao tamanho desejado e as placas ao redor são reposicionadas dinamicamente. Isso pode fazer com que alguns cartões sejam movidos para linhas adicionais, o que exige a rolagem para baixo para visualizar todas as placas. Por exemplo, quando a variável[!UICONTROL Atributos básicos]&quot; o cartão é redimensionado[!UICONTROL Identidades vinculadas]&quot;O cartão não está mais visível na linha superior e agora aparece em uma nova segunda linha no perfil (não exibido). Para retornar o &quot;[!UICONTROL Identidades vinculadas]&quot; para a linha superior, você pode arrastá-lo e soltá-lo na posição atual do &quot;[!UICONTROL Preferências de canal]&quot; cartão.

![Um cartão redimensionado é realçado.](../images/profile-customization/resized.png)

## Editar e remover cartões

Além de redimensionar e reorganizar cartões, você pode editar o conteúdo de determinados cartões e remover alguns cartões totalmente do painel. Selecione as reticências (`...`) no canto superior direito do cartão para editá-lo ou removê-lo. Isso abre uma lista suspensa com opções para editar ou remover o cartão, dependendo das propriedades do cartão selecionado.

>[!NOTE]
>
>Nem todas as placas podem ser editadas ou removidas. Isso ocorre porque alguns cartões contêm informações somente leitura ou obrigatórias. Se um cartão não tiver um elipses no canto superior direito, ele conterá informações somente leitura E obrigatórias e não poderá ser editado nem removido. Se um cartão tiver elipses no canto e selecioná-lo mostrar apenas uma opção para remover o cartão, as informações do cartão serão somente leitura e não poderão ser editadas.

![A lista suspensa editar cartão está realçada. Isso inclui opções para editar ou remover o cartão.](../images/profile-customization/edit-card.png)

Selecionar **[!UICONTROL Editar]** na lista suspensa para abrir o **[!UICONTROL Editar widget]** , onde é possível atualizar o título do cartão, reordenar ou remover os atributos visíveis, ou adicionar outros atributos usando a **[!UICONTROL Adicionar atributos]** botão.

![O cartão Basic attributes é exibido.](../images/profile-customization/basic-attributes.png)

## Adicionar atributos {#add-attributes}

No **[!UICONTROL Editar widget]** , selecione **[!UICONTROL Adicionar atributos]** no canto superior direito do cartão para começar a adicionar atributos a esse cartão.

![O botão Add attributes no cartão Basic attributes é realçado.](../images/profile-customization/add-attributes.png)

Quando a variável **[!UICONTROL Selecionar campo de esquema de união]** for aberta, o lado esquerdo da caixa de diálogo mostrará a caixa de diálogo cheia [!UICONTROL Perfil individual XDM] schema de união, com campos aninhados abaixo. Para obter mais informações sobre schemas de união, consulte [seção de schemas da união do [!DNL Profile] guia do usuário](user-guide.md#union-schema).

O **[!UICONTROL Atributos selecionados]** A seção no lado direito da caixa de diálogo mostra os atributos incluídos no cartão que você está editando. Também é possível remover e reordenar atributos aqui. O número total de atributos selecionados é exibido, bem como o número máximo de atributos (20) que podem ser adicionados a um único cartão.

![Os atributos que atualmente compõem os atributos no cartão são realçados.](../images/profile-customization/select-before.png)

Você pode selecionar qualquer um dos campos de esquema de união disponíveis para personalizar os atributos no cartão que você está editando. Os campos selecionados são mostrados com uma marca de seleção ao lado deles e são automaticamente adicionados à lista de atributos selecionados. Depois de adicionar todos os atributos que você gostaria que fossem exibidos no cartão, escolha **[!UICONTROL Selecionar]** para retornar ao **[!UICONTROL Editar widget]** tela.

![Os atributos recém adicionados são realçados.](../images/profile-customization/select-after.png)

Quando você retorna ao **[!UICONTROL Editar widget]** , a lista de atributos no cartão agora deve ser atualizada para refletir suas opções. Você ainda pode remover ou reordenar os atributos do cartão ou editar o título do cartão, conforme necessário. Depois que as edições forem concluídas, selecione **[!UICONTROL Salvar]** para salvar as alterações.

![Os atributos recém adicionados são exibidos no cartão editado.](../images/profile-customization/new-attributes.png)

Depois de salvar, você volta para a função **[!UICONTROL Detalhe]** , onde o cartão e os atributos atualizados ficam visíveis.

![Os atributos recém adicionados são exibidos no cartão no painel Perfil .](../images/profile-customization/added-attributes.png)

## Adicionar um novo cartão {#add-a-new-card}

Para personalizar ainda mais a aparência dos perfis no Experience Platform, é possível optar por adicionar novos cartões ao painel e selecionar os atributos que deseja exibir nesses cartões. Para começar, selecione **[!UICONTROL Modificar painel]** no **[!UICONTROL Detalhe]** guia .

![O botão Personalizar detalhes do perfil é realçado.](../images/profile-customization/customize-profile-details.png)

Em seguida, selecione **[!UICONTROL Adicionar widget]** no canto superior esquerdo do painel.

![O botão Adicionar widget é realçado.](../images/profile-customization/add-widget.png)

A opção de adicionar um novo cartão abre o **[!UICONTROL Editar widget]** , onde é possível fornecer um título para o novo cartão e escolher os atributos que deseja que o cartão exiba. Para começar a adicionar atributos ao cartão, selecione **[!UICONTROL Adicionar atributos]**.

![Um novo cartão de widget em branco é exibido na tela Editar widget.](../images/profile-customization/edit-widget.png)

Quando a variável **[!UICONTROL Selecionar campo de esquema de união]** for aberta, o lado esquerdo da caixa de diálogo mostrará o [!UICONTROL Perfil individual XDM] schema de união e o **[!UICONTROL Atributos selecionados]** No lado direito da caixa de diálogo, a seção mostra os atributos selecionados para o cartão. Para obter mais informações sobre como adicionar atributos, consulte a [seção sobre adição de atributos](#add-attributes) que aparece anteriormente neste documento.

O número total de atributos selecionados é exibido, bem como o número máximo de atributos (20) que podem ser adicionados a um único cartão. Também é possível remover e reordenar os atributos selecionados nessa tela. Depois de adicionar todos os atributos que você deseja exibir no cartão, escolha **[!UICONTROL Selecionar]** para retornar ao **[!UICONTROL Editar widget]** tela.

![Os campos que você está adicionando ao cartão são realçados.](../images/profile-customization/add-widget-attributes.png)

Quando você retorna ao **[!UICONTROL Editar widget]** , a lista de atributos no cartão deve refletir suas opções na tela anterior. Você também pode reordenar e remover atributos do cartão, conforme necessário.

Para salvar seu novo cartão, você deve primeiro fornecer um **[!UICONTROL Título do cartão]**, você poderá selecionar **[!UICONTROL Salvar]** e conclua o processo de criação do cartão.

![O novo widget é visualizado na tela Editar widget.](../images/profile-customization/new-widget.png)

Depois de salvar, você volta para a função **[!UICONTROL Detalhe]** , onde o novo cartão e atributos ficam visíveis.

![O novo widget é adicionado ao painel Perfil.](../images/profile-customization/added-widget.png)

## Restaurar cartões padrão

Se, a qualquer momento, você decidir que deseja restaurar os cartões padrão que foram removidos, você terá a capacidade de fazer isso rápida e facilmente. Primeiro, selecione **[!UICONTROL Modificar painel]**, em seguida selecione **[!UICONTROL Restaurar cartões padrão]**. Depois que os cartões padrão estiverem visíveis, você poderá selecionar **[!UICONTROL Salvar]** para salvar suas alterações ou selecione **[!UICONTROL Cancelar]** se não quiser restaurar os cartões padrão.

![O botão Restore default cards é realçado no painel Perfil.](../images/profile-customization/restore-default.png)

## Próximas etapas

Ao seguir este documento, você agora deve ser capaz de atualizar a visualização do perfil de sua organização, incluindo adicionar e remover cartões, editar detalhes e atributos do cartão, além de reorganizar e redimensionar cartões. Para saber mais sobre como trabalhar com a [!DNL Profile] na interface do usuário do Experience Platform, consulte o [[!DNL Profile] guia do usuário](user-guide.md).
