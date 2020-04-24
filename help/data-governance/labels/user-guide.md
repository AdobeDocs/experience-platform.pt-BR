---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do usuário de etiquetas de uso de dados
topic: labels
translation-type: tm+mt
source-git-commit: 475e774d5e7ebac036b42aa94736ba8e22c7185f

---


# Guia do usuário de etiquetas de uso de dados

Este guia do usuário aborda as etapas para trabalhar com rótulos de uso de dados (também conhecidos como rótulos DULE) na interface do usuário da plataforma Experience. Antes de usar o guia, consulte a visão geral [do](../home.md) Data Governance para obter uma introdução mais robusta à estrutura DULE.

## Gerenciamento de rótulos de uso de dados no nível do conjunto de dados

Para gerenciar rótulos de uso de dados no nível do conjunto de dados, é necessário selecionar um conjunto de dados existente ou criar um novo. Depois de fazer logon na Adobe Experience Platform, selecione **[!UICONTROL Datasets]** na navegação à esquerda para abrir a área de trabalho _de conjuntos de dados_ . Esta página lista todos os conjuntos de dados criados pertencentes à sua organização, juntamente com detalhes úteis relacionados a cada conjunto de dados.

![Guia Conjunto de dados na área de trabalho de dados](../images/labels/datasets.png)

A próxima seção fornece etapas para a criação de um novo conjunto de dados para aplicar rótulos. Se desejar editar rótulos para um conjunto de dados existente, selecione o conjunto de dados na lista e pule para frente para [adicionar rótulos de uso de dados ao conjunto de dados](#add-labels).

### Criar um novo conjunto de dados

>[!NOTE] Neste exemplo, um conjunto de dados é criado usando um schema do Modelo de Dados de Experiência (XDM) pré-configurado. Para obter mais informações sobre schemas XDM, consulte a visão geral [do Sistema](../../xdm/home.md) XDM e [as noções básicas da composição](../../xdm/schema/composition.md)do schema.

Para criar um novo conjunto de dados, clique **[!UICONTROL Create Dataset]** no canto superior direito do espaço de _[!UICONTROL Datasets]_trabalho.

![](../images/labels/create_dataset.png)

A _[!UICONTROL Create Dataset]_tela é exibida. Daqui, clique em **[!UICONTROL Create Dataset from Schema]**.

![Criar conjunto de dados a partir do Schema](../images/labels/dataset_create.png)

A _[!UICONTROL Select Schema]_tela é exibida, que lista todos os schemas disponíveis que você pode usar para criar um conjunto de dados. Clique no botão de opção ao lado de um schema para selecioná-lo. A_[!UICONTROL Schemas]_ seção no lado direito exibe detalhes adicionais sobre o schema selecionado. Depois de selecionar um schema, clique em **[!UICONTROL Next]**.

![Selecionar Schema de conjunto de dados](../images/labels/dataset_schema.png)

A tela _Configurar conjunto de dados_ é exibida. Forneça um **nome** (obrigatório) e uma **descrição** (opcional, mas recomendado) para seu novo conjunto de dados, em seguida, clique em **[!UICONTROL Finish]**.

![Configurar conjunto de dados com nome e descrição](../images/labels/dataset_configure.png)

A _[!UICONTROL Dataset Activity]_página é exibida, exibindo informações sobre o conjunto de dados recém-criado. Neste exemplo, o conjunto de dados é denominado &quot;Membros de Fidelidade&quot;, portanto, a navegação superior mostra_ Conjuntos de Dados > Membros _de Fidelidade.

![Página Atividade do conjunto de dados](../images/labels/dataset_activity.png)

### Adicionar rótulos de uso de dados ao conjunto de dados {#add-labels}

Depois de criar um novo conjunto de dados ou selecionar um conjunto de dados existente da lista no _[!UICONTROL Datasets]_espaço de trabalho, clique **[!UICONTROL Data Governance]**para abrir o_[!UICONTROL Data Governance]_ espaço de trabalho. A área de trabalho permite gerenciar rótulos de uso de dados no nível do conjunto de dados e no nível do campo.

![Guia Controle de dados do conjunto de dados](../images/labels/dataset_data_governance.png)

Para editar rótulos de uso de dados no nível do conjunto de dados, clique no start ao lado do nome do conjunto de dados.

![Editar rótulos de nível de conjunto de dados](../images/labels/dataset_labels_edit_button.png)

A caixa de _[!UICONTROL Edit Governance Labels]_diálogo é aberta. Na caixa de diálogo, marque as caixas ao lado dos rótulos que deseja aplicar ao conjunto de dados. Lembre-se de que esses rótulos serão herdados por todos os campos no conjunto de dados. O_[!UICONTROL Applied Labels]_ cabeçalho é atualizado conforme você marca cada caixa, mostrando os rótulos que você escolheu. Depois de selecionar os rótulos desejados, clique em **[!UICONTROL Save Changes]**.

<img alt="Aplicar rótulos de controle no nível do conjunto de dados" src="../images/labels/apply-labels-dataset.png" width="700"><br>

A _[!UICONTROL Data Governance]_área de trabalho é exibida novamente, mostrando os rótulos que você aplicou no nível do conjunto de dados. Você também pode ver que os rótulos são herdados para cada um dos campos no conjunto de dados.

![Rótulos de conjunto de dados herdados pelos campos](../images/labels/dataset_inherited_labels.png)

Observe que um &quot;x&quot; é exibido ao lado dos rótulos no nível do conjunto de dados, permitindo que você remova os rótulos. Os rótulos herdados ao lado de cada campo não têm um &quot;x&quot; ao lado deles e aparecem &quot;acinzentados&quot; sem a capacidade de remover ou editar. Isso ocorre porque os campos **herdados são somente** leitura, o que significa que não podem ser removidos no nível do campo.

A **[!UICONTROL Show Inherited Labels]** alternância está ativada por padrão, o que permite que você veja quaisquer rótulos herdados do conjunto de dados para seus campos. A alternância oculta qualquer rótulo herdado no conjunto de dados.

![Ocultar etiquetas herdadas](../images/labels/hide_inherited_labels.png)

## Gerenciamento de rótulos de uso de dados no nível do campo do conjunto de dados

Continuando o fluxo de trabalho para [adicionar e editar rótulos de uso de dados no nível](#add-labels)do conjunto de dados, você também pode gerenciar rótulos no nível do campo dentro da área de trabalho _[!UICONTROL Data Governance]_desse conjunto de dados.

Para aplicar rótulos de uso de dados a um campo individual, marque a caixa de seleção ao lado do nome do campo e clique em **[!UICONTROL Edit Governance Labels]**.

![Editar rótulos de campo](../images/labels/fields_single_field.png)

A _[!UICONTROL Edit Governance Labels]_caixa de diálogo é exibida. A caixa de diálogo exibe cabeçalhos mostrando campos selecionados, rótulos aplicados e rótulos herdados. Observe que os rótulos herdados (C2 e C5) ficam esmaecidos na caixa de diálogo. Eles são rótulos somente leitura herdados do nível do conjunto de dados e, portanto, só podem ser editados no nível do conjunto de dados.

<img alt="Editar rótulos de controle para um campo individual" src="../images/labels/field-label-inheritance.png" width="700"><br>

Selecione rótulos de nível de campo clicando na caixa de seleção ao lado de cada rótulo que você deseja usar. À medida que você seleciona rótulos, o _[!UICONTROL Applied Labels]_cabeçalho é atualizado para mostrar os rótulos aplicados aos campos exibidos no_[!UICONTROL Selected Fields]_ cabeçalho. Depois de terminar de selecionar rótulos de nível de campo, clique em **[!UICONTROL Save Changes]**.

<img alt="Aplicar etiquetas em nível de campo" src="../images/labels/apply-labels-field.png" width="700"><br>

A _[!UICONTROL Data Governance]_área de trabalho é reexibida, que agora exibe os rótulos de nível de campo selecionados na linha ao lado do nome do campo. Observe que a etiqueta de nível de campo tem um &quot;x&quot; ao lado, permitindo que você remova a etiqueta.

![Campo que mostra rótulos de nível de campo](../images/labels/fields_show_field_level_labels.png)

Você pode repetir essas etapas para continuar adicionando e editando rótulos de nível de campo para campos adicionais, incluindo a seleção de vários campos para aplicar rótulos de nível de campo simultaneamente.

![Selecione vários campos para aplicar rótulos de nível de campo simultaneamente.](../images/labels/fields_select_multiple.png)

É importante lembrar que a herança move somente do nível superior para baixo (conjunto de dados → campos), o que significa que os rótulos aplicados no nível do campo não são propagados para outros campos ou conjuntos de dados.

## Próximas etapas

Agora que você adicionou rótulos de uso de dados no nível do conjunto de dados e do campo, é possível começar a assimilar dados na Experience Platform. Para saber mais, leia a documentação [de ingestão de](../../ingestion/home.md)dados em start.

Agora você também pode definir políticas de uso de dados com base nos rótulos aplicados. Para obter mais informações, consulte a visão geral [das políticas de uso de](../policies/overview.md)dados.

## Recursos adicionais

O vídeo a seguir tem como objetivo oferecer suporte para a compreensão do Data Governance e descreve como aplicar rótulos a um conjunto de dados e a campos individuais.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
