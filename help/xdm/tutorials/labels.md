---
title: Gerenciar rótulos de uso de dados para um esquema
description: Saiba como adicionar rótulos de uso de dados aos campos de esquema do Experience Data Model (XDM) na interface do Adobe Experience Platform.
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---

# Gerenciar rótulos de uso de dados para um esquema

>[!IMPORTANT]
>
>A rotulagem baseada em esquema faz parte da [controle de acesso baseado em atributos](../../access-control/abac/overview.md), que está disponível atualmente em uma versão limitada para clientes de serviços de saúde nos EUA. Esse recurso estará disponível para todos os clientes da Adobe Real-time Customer Data Platform depois de totalmente lançado.

Todos os dados trazidos para a Adobe Experience Platform são restritos pelos esquemas do Experience Data Model (XDM). Esses dados podem estar sujeitos a restrições de uso definidas por sua organização ou por regulamentos legais. Para levar em conta isso, a Plataforma permite restringir o uso de determinados conjuntos de dados e campos por meio do uso de [rótulos de uso de dados](../../data-governance/labels/overview.md).

Um rótulo aplicado a um campo de esquema indica as políticas de uso que se aplicam aos dados contidos nesse campo específico.

Embora os rótulos possam ser aplicados a conjuntos de dados individuais (e campos nesses conjuntos de dados), você também pode aplicar rótulos no nível do esquema. Quando os rótulos são aplicados diretamente a um esquema, eles são propagados para todos os conjuntos de dados existentes e futuros baseados nesse esquema.

Além disso, qualquer rótulo de campo adicionado em um esquema se propaga para todos os outros esquemas que empregam o mesmo campo de uma classe compartilhada ou grupo de campos. Isso ajuda a garantir que as regras de uso para campos semelhantes sejam consistentes em todo o modelo de dados.

Este tutorial aborda as etapas para adicionar rótulos a um esquema usando o Editor de esquemas na interface do usuário da plataforma.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Editor de esquema](../ui/overview.md): saiba como criar e gerenciar esquemas e outros recursos na interface do Platform.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): fornece a infraestrutura para aplicar restrições de uso de dados nas operações da Platform, usando políticas que definem quais ações de marketing podem (ou não) ser executadas em dados rotulados.

## Selecione um esquema ou campo para adicionar rótulos {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="Editar rótulos de governança"
>abstract="Aplique um rótulo a um campo de esquema para indicar as políticas de uso que se aplicam aos dados contidos nesse campo específico."

Para começar a adicionar rótulos, você deve primeiro [selecionar um esquema existente para editar](../ui/resources/schemas.md#edit) ou [criar um novo esquema](../ui/resources/schemas.md#create) para exibir sua estrutura no Editor de esquemas.

Para editar os rótulos de um campo individual, você pode selecionar o campo na tela e selecionar **[!UICONTROL Gerenciar acesso]** no painel direito.

![Selecione um campo na tela Editor de esquemas](../images/tutorials/labels/manage-access.png)

Você também pode selecionar a variável **[!UICONTROL Rótulos]** escolha o campo desejado na lista e selecione **[!UICONTROL Editar rótulos de governança]** no painel direito.

![Selecione um campo na [!UICONTROL Rótulos] guia](../images/tutorials/labels/select-field-on-labels-tab.png)

Para editar os rótulos para todo o esquema, selecione o ícone de lápis (![](../images/tutorials/labels/pencil-icon.png)) ao lado do nome do esquema sob o **[!UICONTROL Rótulos]** guia.

![Selecione o nome do esquema na caixa [!UICONTROL Rótulos] guia](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>Uma mensagem de aviso é exibida ao tentar editar os rótulos de um esquema ou campo pela primeira vez, explicando como o uso do rótulo afeta as operações de downstream, dependendo das políticas da organização. Selecionar **[!UICONTROL Continuar]** para continuar editando.
>
>![Isenção de responsabilidade sobre o uso de rótulo](../images/tutorials/labels/disclaimer.png)

## Editar os rótulos do esquema ou campo

Uma caixa de diálogo é exibida, permitindo editar os rótulos do campo selecionado. Se você selecionou um campo de tipo de objeto individual, o painel direito listará os subcampos para os quais os rótulos aplicados serão propagados.

![Campos selecionados exibidos](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>Se você estiver editando campos para o esquema inteiro, o painel direito não listará os campos aplicáveis e exibirá o nome do esquema.

Use a lista exibida para selecionar os rótulos que deseja adicionar ao esquema ou campo. Como os rótulos são escolhidos, a variável **[!UICONTROL Rótulos aplicados]** A seção é atualizada para mostrar os rótulos que foram selecionados até o momento.

![Rótulos aplicados exibidos](../images/tutorials/labels/applied-labels.png)

Para filtrar os rótulos exibidos por tipo, selecione a categoria desejada no painel esquerdo. Para criar um novo rótulo personalizado, selecione **[!UICONTROL Criar rótulo]**.

![Filtrar rótulos exibidos ou criar um novo rótulo](../images/tutorials/labels/filter-and-create-custom.png)

Quando estiver satisfeito com os rótulos escolhidos, selecione **[!UICONTROL Salvar]** para aplicá-los ao campo ou esquema.

![Salvar os rótulos selecionados](../images/tutorials/labels/save-labels.png)

A variável **[!UICONTROL Rótulos]** reaparecerá, mostrando os rótulos aplicados para o esquema.

![Rótulos de campo aplicados](../images/tutorials/labels/field-labels-added.png)

## Próximas etapas

Este guia abordou como gerenciar rótulos de uso de dados para esquemas e campos. Para obter informações sobre como gerenciar rótulos de uso de dados, incluindo como adicioná-los a conjuntos de dados específicos em vez de no nível do esquema, consulte a [guia da interface do usuário de rótulos de uso de dados](../../data-governance/labels/user-guide.md).
