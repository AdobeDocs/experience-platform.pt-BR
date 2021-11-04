---
keywords: Experience Platform, home, tópicos populares, governança de dados, rótulo de uso de dados, serviço de política, guia do usuário de rótulos de uso de dados
solution: Experience Platform
title: Gerenciar rótulos de uso de dados na interface do usuário
topic-legacy: labels
description: Este guia aborda as etapas para trabalhar com rótulos de uso de dados na interface do usuário do Adobe Experience Platform.
exl-id: aa44d5cc-416a-4ef2-be14-b4f32aec162c
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 0%

---

# Gerenciar rótulos de uso de dados na interface do usuário

Este guia do usuário aborda as etapas para trabalhar com rótulos de uso de dados na [!DNL Experience Platform] interface do usuário. Antes de usar o guia, consulte o [Visão geral da governança de dados](../home.md) para obter uma introdução mais robusta à estrutura de Governança de dados.

## Gerenciar rótulos no nível do conjunto de dados

Para gerenciar rótulos de uso de dados no nível do conjunto de dados, é necessário selecionar um conjunto de dados existente ou criar um novo. Depois de fazer logon no Adobe Experience Platform, selecione **[!UICONTROL Conjuntos de dados]** na navegação à esquerda para abrir o **[!UICONTROL Conjuntos de dados]** espaço de trabalho. Esta página lista todos os conjuntos de dados criados pertencentes à sua organização, juntamente com detalhes úteis relacionados a cada conjunto de dados.

![Guia Conjunto de dados no Data Workspace](../images/labels/datasets-tab.png)

A próxima seção fornece etapas para criar um novo conjunto de dados para aplicar rótulos. Se desejar editar rótulos para um conjunto de dados existente, selecione o conjunto de dados na lista e ignore para [adicionar rótulos de uso de dados ao conjunto de dados](#add-labels).

### Criar um novo conjunto de dados

>[!NOTE]
>
>Neste exemplo, um conjunto de dados é criado usando um [!DNL Experience Data Model] (XDM). Para obter mais informações sobre esquemas XDM, consulte a [Visão geral do sistema XDM](../../xdm/home.md) e [noções básicas da composição do schema](../../xdm/schema/composition.md).

Para criar um novo conjunto de dados, selecione **[!UICONTROL Criar conjunto de dados]** no canto superior direito do **[!UICONTROL Conjuntos de dados]** espaço de trabalho.

![](../images/labels/create-dataset.png)

O **[!UICONTROL Criar conjunto de dados]** será exibida. Aqui, selecione **[!UICONTROL Criar conjunto de dados a partir do esquema]**.

![Criar conjunto de dados a partir do esquema](../images/labels/create-from-dataset.png)

O **[!UICONTROL Selecionar esquema]** é exibida, listando todos os esquemas disponíveis que você pode usar para criar um conjunto de dados. Selecione o botão de opção ao lado de um schema para selecioná-lo. O **[!UICONTROL Esquemas]** no lado direito exibe detalhes adicionais sobre o schema selecionado. Após selecionar um esquema, selecione **[!UICONTROL Próximo]**.

![Selecionar esquema do conjunto de dados](../images/labels/select-schema.png)

O **[!UICONTROL Configurar conjunto de dados]** será exibida. Forneça um nome (obrigatório) e uma descrição (opcional, mas recomendado) para seu novo conjunto de dados, em seguida selecione **[!UICONTROL Concluir]**.

![Configurar conjunto de dados com nome e descrição](../images/labels/configure-dataset.png)

O **[!UICONTROL Atividade do conjunto de dados]** for exibida, exibindo informações sobre o conjunto de dados recém-criado. Neste exemplo, o conjunto de dados é denominado &quot;Membros de fidelidade&quot;, portanto, a navegação superior mostra **Conjuntos de dados > Membros de fidelidade**.

![Página Atividade do conjunto de dados](../images/labels/dataset-created.png)

### Adicionar rótulos de uso de dados ao conjunto de dados {#add-labels}

Depois de criar um novo conjunto de dados ou selecionar um conjunto de dados existente na lista na **[!UICONTROL Conjuntos de dados]** espaço de trabalho, selecione **[!UICONTROL Governança de dados]** para abrir o **[!UICONTROL Governança de dados]** espaço de trabalho. O espaço de trabalho permite gerenciar rótulos de uso de dados no nível do conjunto de dados e no nível do campo.

![Guia Governança de dados do conjunto de dados](../images/labels/dataset-governance.png)

Para editar rótulos de uso de dados no nível do conjunto de dados, comece selecionando o ícone de lápis ao lado do nome do conjunto de dados.

![Editar rótulos no nível do conjunto de dados](../images/labels/dataset-level-edit.png)

O **[!UICONTROL Editar rótulos de governança]** será aberta. Na caixa de diálogo , marque as caixas ao lado dos rótulos que deseja aplicar ao conjunto de dados. Lembre-se de que esses rótulos serão herdados por todos os campos no conjunto de dados. O **[!UICONTROL Rótulos aplicados]** O cabeçalho é atualizado conforme você marca cada caixa, mostrando os rótulos escolhidos. Após selecionar os rótulos desejados, selecione **[!UICONTROL Salvar alterações]**.

![Aplicar rótulos de governança no nível do conjunto de dados](../images/labels/apply-labels-dataset.png)

O **[!UICONTROL Governança de dados]** O espaço de trabalho será exibido novamente, mostrando os rótulos que você aplicou no nível do conjunto de dados. Você também pode ver que os rótulos são herdados para cada um dos campos no conjunto de dados.

![Rótulos do conjunto de dados herdados pelos campos](../images/labels/dataset-labels-applied.png)

Observe que um &quot;x&quot; é exibido ao lado dos rótulos no nível do conjunto de dados, permitindo remover os rótulos. Os rótulos herdados ao lado de cada campo não têm um &quot;x&quot; ao lado e aparecem &quot;esmaecidos&quot; sem capacidade de remover ou editar. Isso ocorre porque **os campos herdados são somente leitura**, o que significa que elas não podem ser removidas no nível do campo.

O **[!UICONTROL Mostrar rótulos herdados]** está ativada por padrão, o que permite visualizar qualquer rótulo herdado do conjunto de dados para seus campos. A desativação da alternância oculta todos os rótulos herdados no conjunto de dados.

![Ocultar rótulos herdados](../images/labels/inherited-labels.png)

## Gerenciar rótulos no nível do campo

Continuar o workflow para [adicionar e editar rótulos de uso de dados no nível do conjunto de dados](#add-labels), também é possível gerenciar rótulos em nível de campo no **[!UICONTROL Governança de dados]** espaço de trabalho para esse conjunto de dados.

Para aplicar rótulos de uso de dados a um campo individual, marque a caixa de seleção ao lado do nome do campo e selecione **[!UICONTROL Editar rótulos de governança]**.

![Editar rótulos de campo](../images/labels/field-label-edit.png)

O **[!UICONTROL Editar rótulos de governança]** será exibida. A caixa de diálogo exibe cabeçalhos mostrando campos selecionados, rótulos aplicados e rótulos herdados. Observe que os rótulos herdados (C2 e C5) estão esmaecidos na caixa de diálogo. Eles são rótulos somente leitura herdados do nível do conjunto de dados e, portanto, só podem ser editados no nível do conjunto de dados.

![Editar rótulos de governança para um campo individual](../images/labels/field-label-inheritance.png)

Selecione rótulos de nível de campo marcando a caixa de seleção ao lado de cada rótulo que deseja usar. À medida que você seleciona rótulos, a variável **[!UICONTROL Rótulos aplicados]** atualizações de cabeçalho para mostrar rótulos aplicados aos campos mostrados no **[!UICONTROL Campos selecionados]** cabeçalho. Depois de concluir a seleção de rótulos de nível de campo, selecione **[!UICONTROL Salvar alterações]**.

![Aplicar rótulos de nível de campo](../images/labels/apply-labels-field.png)

O **[!UICONTROL Governança de dados]** o espaço de trabalho será exibido novamente, exibindo agora os rótulos de nível de campo selecionados na linha ao lado do nome do campo. Observe que o rótulo de nível de campo tem um &quot;x&quot; ao lado dele, permitindo remover o rótulo.

![Campo que mostra rótulos de nível de campo](../images/labels/field-labels-applied.png)

É possível repetir essas etapas para continuar adicionando e editando rótulos de nível de campo para campos adicionais, incluindo a seleção de vários campos para aplicar rótulos de nível de campo simultaneamente.

![Selecione vários campos para aplicar rótulos de nível de campo simultaneamente.](../images/labels/multiple-fields.png)

É importante lembrar que a herança se move somente do nível superior para baixo (campos do conjunto de dados → ), o que significa que os rótulos aplicados no nível do campo não são propagados para outros campos ou conjuntos de dados.

## Gerenciar rótulos personalizados

Você pode criar seus próprios rótulos de uso personalizados na **[!UICONTROL Políticas]** na área de trabalho do [!DNL Experience Platform] IU. Selecionar **[!UICONTROL Políticas]** na navegação à esquerda, selecione **[!UICONTROL Rótulos]** para exibir uma lista de rótulos existentes. Aqui, selecione **[!UICONTROL Criar rótulo]**.

![](../images/labels/create-label-btn.png)

O **[!UICONTROL Criar rótulo]** será exibida. A partir daqui, forneça as seguintes informações para o novo rótulo:

* **[!UICONTROL Identificador]**: Um identificador exclusivo para o rótulo. Esse valor é usado para fins de pesquisa e, portanto, deve ser curto e conciso.
* **[!UICONTROL Nome]**: Um nome de exibição amigável para o rótulo.
* **[!UICONTROL Descrição]**: (Opcional) Uma descrição do rótulo para fornecer um contexto adicional.

Quando terminar, selecione **[!UICONTROL Criar]**.

![](../images/labels/create-label.png)

A caixa de diálogo é fechada e o rótulo personalizado recém-criado aparece na lista sob a variável **[!UICONTROL Rótulos]** guia .

![](../images/labels/label-created.png)

O rótulo agora pode ser selecionado em **[!UICONTROL Rótulos personalizados]** ao editar rótulos de uso para conjuntos de dados e campos, ou ao criar políticas de uso de dados.

<img src="../images/labels/add-custom-label.png" width="600" /><br>

## Próximas etapas

Agora que você adicionou rótulos de uso de dados no nível do conjunto de dados e do campo, é possível começar a assimilar dados no [!DNL Experience Platform]. Para saber mais, comece lendo o [documentação de ingestão de dados](../../ingestion/home.md).

Agora, também é possível definir políticas de uso de dados com base nos rótulos aplicados. Para obter mais informações, consulte o [visão geral das políticas de uso de dados](../policies/overview.md).

## Recursos adicionais

O vídeo a seguir tem como objetivo auxiliar a compreensão da Governança de dados e descreve como aplicar rótulos a um conjunto de dados e campos individuais.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
