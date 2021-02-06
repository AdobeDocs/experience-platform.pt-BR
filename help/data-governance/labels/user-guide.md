---
keywords: Experience Platform;home;popular topics;controle de dados;etiqueta de uso de dados;serviço de política;guia do usuário de etiquetas de uso de dados
solution: Experience Platform
title: Gerenciar rótulos de uso de dados na interface do usuário
topic: labels
description: Este guia aborda as etapas para trabalhar com rótulos de uso de dados na interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 0%

---


# Gerenciar rótulos de uso de dados na interface do usuário

Este guia do usuário aborda as etapas para trabalhar com rótulos de uso de dados na [!DNL Experience Platform] interface do usuário. Antes de usar o guia, consulte a [[!DNL Data Governance] visão geral](../home.md) para obter uma introdução mais robusta à estrutura [!DNL Data Governance].

## Gerenciar rótulos no nível do conjunto de dados

Para gerenciar rótulos de uso de dados no nível do conjunto de dados, é necessário selecionar um conjunto de dados existente ou criar um novo. Depois de fazer logon no Adobe Experience Platform, selecione **[!UICONTROL Conjuntos de dados]** na navegação à esquerda para abrir a área de trabalho **[!UICONTROL Conjuntos de dados]**. Esta página lista todos os conjuntos de dados criados pertencentes à sua organização, juntamente com detalhes úteis relacionados a cada conjunto de dados.

![Guia Conjunto de dados na área de trabalho de dados](../images/labels/datasets.png)

A próxima seção fornece etapas para a criação de um novo conjunto de dados para aplicar rótulos. Se desejar editar rótulos para um conjunto de dados existente, selecione o conjunto de dados na lista e passe para [adicionar rótulos de uso de dados ao conjunto de dados](#add-labels).

### Criar um novo conjunto de dados

>[!NOTE]
>
>Neste exemplo, um conjunto de dados é criado usando um schema [!DNL Experience Data Model] (XDM) pré-configurado. Para obter mais informações sobre schemas XDM, consulte [Visão geral do sistema XDM](../../xdm/home.md) e [noções básicas de composição de schemas](../../xdm/schema/composition.md).

Para criar um novo conjunto de dados, selecione **[!UICONTROL Criar conjunto de dados]** no canto superior direito da área de trabalho **[!UICONTROL Conjuntos de dados]**.

![](../images/labels/create_dataset.png)

A tela **[!UICONTROL Criar conjunto de dados]** é exibida. Aqui, selecione **[!UICONTROL Criar conjunto de dados do Schema]**.

![Criar conjunto de dados a partir do Schema](../images/labels/dataset_create.png)

A tela **[!UICONTROL Selecionar Schema]** é exibida, que lista todos os schemas disponíveis que você pode usar para criar um conjunto de dados. Selecione o botão de opção ao lado de um schema para selecioná-lo. A seção **[!UICONTROL Schemas]** no lado direito exibe detalhes adicionais sobre o schema selecionado. Depois de selecionar um schema, selecione **[!UICONTROL Próximo]**.

![Selecionar Schema de conjunto de dados](../images/labels/dataset_schema.png)

A tela **[!UICONTROL Configurar conjunto de dados]** é exibida. Forneça um nome (obrigatório) e uma descrição (opcional, mas recomendado) para seu novo conjunto de dados, em seguida, selecione **[!UICONTROL Concluir]**.

![Configurar conjunto de dados com nome e descrição](../images/labels/dataset_configure.png)

A página **[!UICONTROL Atividade do conjunto de dados]** é exibida, exibindo informações sobre o conjunto de dados recém-criado. Neste exemplo, o conjunto de dados é denominado &quot;Membros de Fidelidade&quot;, portanto, a navegação superior mostra **Conjuntos de Dados > Membros de Fidelidade**.

![Página Atividade do conjunto de dados](../images/labels/dataset_activity.png)

### Adicionar rótulos de uso de dados ao conjunto de dados {#add-labels}

Depois de criar um novo conjunto de dados ou selecionar um conjunto de dados existente na lista no espaço de trabalho **[!UICONTROL conjuntos de dados]**, selecione **[!UICONTROL Data Governance]** para abrir o espaço de trabalho **[!UICONTROL Data Governance]**. A área de trabalho permite gerenciar rótulos de uso de dados no nível do conjunto de dados e no nível do campo.

![Guia Controle de dados do conjunto de dados](../images/labels/dataset_data_governance.png)

Para editar rótulos de uso de dados no nível do conjunto de dados, selecione o start ao lado do nome do conjunto de dados.

![Editar rótulos de nível de conjunto de dados](../images/labels/dataset_labels_edit_button.png)

A caixa de diálogo **[!UICONTROL Editar rótulos de controle]** é aberta. Na caixa de diálogo, marque as caixas ao lado dos rótulos que deseja aplicar ao conjunto de dados. Lembre-se de que esses rótulos serão herdados por todos os campos no conjunto de dados. O cabeçalho **[!UICONTROL Rótulos aplicados]** é atualizado conforme você marca cada caixa, mostrando os rótulos escolhidos. Depois de selecionar os rótulos desejados, selecione **[!UICONTROL Salvar alterações]**.

<img alt="Aplicar rótulos de controle no nível do conjunto de dados" src="../images/labels/apply-labels-dataset.png" width="700"><br>

A área de trabalho **[!UICONTROL Data Governance]** é exibida novamente, mostrando os rótulos que você aplicou no nível do conjunto de dados. Você também pode ver que os rótulos são herdados para cada um dos campos no conjunto de dados.

![Rótulos de conjunto de dados herdados pelos campos](../images/labels/dataset_inherited_labels.png)

Observe que um &quot;x&quot; é exibido ao lado dos rótulos no nível do conjunto de dados, permitindo que você remova os rótulos. Os rótulos herdados ao lado de cada campo não têm um &quot;x&quot; ao lado deles e aparecem &quot;acinzentados&quot; sem a capacidade de remover ou editar. Isso ocorre porque os campos herdados **são somente leitura**, o que significa que não podem ser removidos no nível do campo.

A alternância **[!UICONTROL Mostrar rótulos herdados]** está ativada por padrão, o que permite ver quaisquer rótulos herdados do conjunto de dados para seus campos. A alternância oculta qualquer rótulo herdado no conjunto de dados.

![Ocultar etiquetas herdadas](../images/labels/hide_inherited_labels.png)

## Gerenciar rótulos no nível do campo

Continuando o fluxo de trabalho para [adicionar e editar rótulos de uso de dados no nível do conjunto de dados](#add-labels), você também pode gerenciar rótulos no nível do campo na área de trabalho **[!UICONTROL Data Governance]** desse conjunto de dados.

Para aplicar rótulos de uso de dados a um campo individual, marque a caixa de seleção ao lado do nome do campo e selecione **[!UICONTROL Editar rótulos de controle]**.

![Editar rótulos de campo](../images/labels/fields_single_field.png)

A caixa de diálogo **[!UICONTROL Editar rótulos de controle]** é exibida. A caixa de diálogo exibe cabeçalhos mostrando campos selecionados, rótulos aplicados e rótulos herdados. Observe que os rótulos herdados (C2 e C5) ficam esmaecidos na caixa de diálogo. Eles são rótulos somente leitura herdados do nível do conjunto de dados e, portanto, só podem ser editados no nível do conjunto de dados.

<img alt="Editar rótulos de controle para um campo individual" src="../images/labels/field-label-inheritance.png" width="700"><br>

Selecione rótulos de nível de campo marcando a caixa de seleção ao lado de cada rótulo que você deseja usar. À medida que você seleciona rótulos, o cabeçalho **[!UICONTROL Rótulos aplicados]** é atualizado para mostrar os rótulos aplicados aos campos exibidos no cabeçalho **[!UICONTROL Campos selecionados]**. Depois de terminar de selecionar rótulos de nível de campo, selecione **[!UICONTROL Salvar alterações]**.

<img alt="Aplicar etiquetas em nível de campo" src="../images/labels/apply-labels-field.png" width="700"><br>

A área de trabalho **[!UICONTROL Data Governance]** reaparece, que agora exibe os rótulos de nível de campo selecionados na linha ao lado do nome do campo. Observe que a etiqueta de nível de campo tem um &quot;x&quot; ao lado, permitindo que você remova a etiqueta.

![Campo que mostra rótulos de nível de campo](../images/labels/fields_show_field_level_labels.png)

Você pode repetir essas etapas para continuar adicionando e editando rótulos de nível de campo para campos adicionais, incluindo a seleção de vários campos para aplicar rótulos de nível de campo simultaneamente.

![Selecione vários campos para aplicar rótulos de nível de campo simultaneamente.](../images/labels/fields_select_multiple.png)

É importante lembrar que a herança move somente do nível superior para baixo (conjunto de dados → campos), o que significa que os rótulos aplicados no nível do campo não são propagados para outros campos ou conjuntos de dados.

## Gerenciar rótulos personalizados

Você pode criar seus próprios rótulos de uso personalizados na área de trabalho **[!UICONTROL Policies]** na interface do usuário [!DNL Experience Platform]. Selecione **[!UICONTROL Policies]** na navegação à esquerda e selecione **[!UICONTROL Labels]** para visualização de uma lista de rótulos existentes. Aqui, selecione **[!UICONTROL Criar rótulo]**.

![](../images/labels/create-label-btn.png)

A caixa de diálogo **[!UICONTROL Criar rótulo]** é exibida. Aqui, forneça as seguintes informações para a nova etiqueta:

* **[!UICONTROL Identificador]**: Um identificador exclusivo para o rótulo. Esse valor é usado para fins de pesquisa e, portanto, deve ser curto e conciso.
* **[!UICONTROL Nome]**: Um nome de exibição amigável para o rótulo.
* **[!UICONTROL Descrição]**: (Opcional) Uma descrição do rótulo para fornecer mais contexto.

Quando terminar, selecione **[!UICONTROL Criar]**.

![](../images/labels/create-label.png)

A caixa de diálogo é fechada e o rótulo personalizado recém-criado é exibido na lista na guia **[!UICONTROL Labels]**.

![](../images/labels/label-created.png)

O rótulo agora pode ser selecionado em **[!UICONTROL Rótulos personalizados]** ao editar rótulos de uso para conjuntos de dados e campos, ou ao criar políticas de uso de dados.

<img src="../images/labels/add-custom-label.png" width="600" /><br>

## Próximas etapas

Agora que você adicionou rótulos de uso de dados no nível do conjunto de dados e do campo, é possível começar a assimilar dados em [!DNL Experience Platform]. Para saber mais, leia a documentação de [ingestão de dados](../../ingestion/home.md).

Agora você também pode definir políticas de uso de dados com base nos rótulos aplicados. Para obter mais informações, consulte a [visão geral das políticas de uso de dados](../policies/overview.md).

## Recursos adicionais

O vídeo a seguir tem como objetivo oferecer suporte à sua compreensão de [!DNL Data Governance] e descreve como aplicar rótulos a um conjunto de dados e a campos individuais.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
