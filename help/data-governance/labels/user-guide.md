---
keywords: Experience Platform;página inicial;tópicos populares;governança de dados;rótulo de uso de dados;serviço de política;rótulos de uso de dados guia do usuário
solution: Experience Platform
title: Gerenciar rótulos de uso de dados na interface
description: Este guia aborda etapas para trabalhar com rótulos de uso de dados na interface do usuário do Adobe Experience Platform.
exl-id: aa44d5cc-416a-4ef2-be14-b4f32aec162c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 17%

---

# Gerenciar rótulos de uso de dados na interface {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_description"
>title="Governar o uso de dados na Experience Platform"
>abstract="<h2>Descrição</h2><p>A estrutura de Governança de dados na Experience Platform permite rotular atributos e esquemas de acordo com restrições de uso de dados e configurar políticas que identifiquem e respeitem essas restrições para ações de marketing específicas.</p>"

Este guia do usuário aborda etapas para trabalhar com rótulos de uso de dados na interface do usuário do [!DNL Experience Platform].

## Gerenciar rótulos {#manage-labels}

Para aplicar rótulos aos seus dados, você precisa da permissão **[!UICONTROL Gerenciar rótulos de uso]** para usar na sandbox de produção padrão chamada &quot;prod&quot;. Para criar um rótulo personalizado, você também deve ter direitos administrativos no perfil do produto. Cada organização tem apenas uma lista de rótulos aplicáveis. Você **não pode** excluir rótulos. Em vez disso, você pode removê-los dos conjuntos de dados ou campos aos quais são aplicados.

Consulte o manual sobre como [configurar permissões](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=pt-BR) ou a [visão geral do controle de acesso](../../access-control/home.md) para obter mais informações sobre como atribuir uma permissão. Se você não tiver acesso à Admin Console para sua organização, entre em contato com o administrador da organização.

## Gerenciar rótulos no nível do esquema

Você pode adicionar rótulos diretamente a um esquema ou campos dentro desse esquema. Quaisquer campos aplicados no nível do esquema serão propagados para todos os conjuntos de dados baseados nesse esquema.

>[!NOTE]
>
>Se suas políticas de uso de dados foram criadas antes de você rotular o campo, é possível encontrar uma caixa de diálogo de violação de política de governança ao aplicar rótulos ao novo esquema. Esta caixa de diálogo indica que a aplicação deste rótulo violará uma política de uso existente. Use o diagrama de linhagem de dados para entender quais outras alterações de configuração precisam ser feitas antes de você poder adicionar o rótulo ao campo de esquema.
>
>![A violação da política de governança de dados detectou uma caixa de diálogo com o resumo da violação e o diagrama de linhagem de dados destacados.](../images/labels/policy-violation-dialog.png)
>
>Consulte a [documentação de violação da política de uso de dados](../enforcement/auto-enforcement.md#data-usage-violation) para obter mais informações sobre violações de política.

Para gerenciar rótulos de uso de dados no nível do esquema, você deve selecionar um esquema existente ou criar um novo. Depois de fazer logon no Adobe Experience Platform, selecione **[!UICONTROL Esquemas]** na navegação à esquerda para abrir o espaço de trabalho **[!UICONTROL Esquemas]**. Essa página lista todos os esquemas criados que pertencem à sua organização, juntamente com detalhes úteis relacionados a cada esquema.

![A interface do usuário do Adobe Experience Platform com a guia Esquema realçada.](../images/labels/schema-tab.png)

A próxima seção fornece etapas para criar um novo esquema ao qual aplicar rótulos. Se quiser editar rótulos para um esquema existente, selecione o esquema na lista e vá para [adicionando rótulos de uso de dados ao esquema](#add-labels).

### Criar um novo esquema

Para criar um novo esquema, selecione **[!UICONTROL Criar esquema]** no canto superior direito do espaço de trabalho **[!UICONTROL Esquemas]**. Consulte o guia sobre [como criar um esquema usando o Editor de Esquemas](../../xdm/tutorials/create-schema-ui.md#create) para obter instruções completas. Como alternativa, você pode [criar um esquema usando a API de Registro de Esquema](../../xdm/tutorials/create-schema-api.md), se necessário.

### Adicionar rótulos de uso de dados a um esquema {#add-labels-to-schema}

Depois de criar um novo esquema ou selecionar um esquema existente da lista na guia [!UICONTROL Procurar] do espaço de trabalho [!UICONTROL Esquemas], selecione um campo do esquema no Editor de Esquemas. Na barra lateral [!UICONTROL Propriedades do campo], selecione **[!UICONTROL Aplicar rótulos de acesso e governança de dados]**.

![A guia Estrutura do espaço de trabalho de Esquemas exibindo a visualização do esquema com os rótulos Aplicar Acesso e Governança de Dados realçados.](../images/labels/schema-label-governance.png)

É exibida uma caixa de diálogo com a qual é possível aplicar e gerenciar rótulos de uso de dados no nível do esquema e do campo. Consulte o tutorial do XDM para obter instruções completas sobre [como adicionar ou editar rótulos de uso de dados para esquemas XDM](../../xdm/tutorials/labels.md#select-schema-field).

### Adicionar rótulos de uso de dados a um conjunto de dados específico {#add-labels-to-dataset}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_instructions"
>title="Instruções"
>abstract="<ol><li>Selecione <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/user-guide.html?lang=pt-BR">Conjuntos de dados</a> na navegação à esquerda e selecione o conjunto de dados cujos dados você deseja restringir.</li><li>Na visualização de detalhes do conjunto de dados, selecione a guia <b>Governança de dados</b>.</li><li>Selecione os campos do conjunto de dados que deseja restringir e selecione <b>Editar rótulos de governança</b> para rotular os dados com base em restrições de uso.</li><li>Depois de rotular os dados, selecione <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=pt-BR">Políticas</a> na navegação à esquerda, e selecione <b>Criar Política</b>.</li><li>Escolha criar uma <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=pt-BR#create-governance-policy">Política de governança de dados</a>, em seguida, selecione os rótulos de uso de dados que a política aplicará à política.</li><li>Selecione as ações de marketing que a política negará para quaisquer dados que contenham esses rótulos. Depois que a política for criada, selecione-a na lista e habilite-a usando o botão de alternância no painel direito.</li><li>Para cada política habilitada, a Experience Platform impede que quaisquer dados que contenham os rótulos especificados sejam usados para as ações de marketing definidas. Essa imposição ocorre automaticamente quando você tenta ativar dados rotulados para um destino com ações de marketing associadas (casos de uso).</li></ol>"

>[!IMPORTANT]
>
>Os rótulos não podem mais ser aplicados a campos no nível do conjunto de dados. Esse workflow foi substituído em favor da aplicação de rótulos no nível do schema. Quaisquer rótulos aplicados anteriormente no nível do objeto do conjunto de dados ainda serão compatíveis por meio da interface do usuário do Experience Platform até 31 de maio de 2024. Para garantir que seus rótulos sejam consistentes em todos os esquemas, todos os rótulos anteriormente anexados a campos no nível do conjunto de dados devem ser migrados para o nível do esquema por você no ano seguinte. Consulte a documentação para obter instruções sobre [como migrar rótulos aplicados anteriormente do conjunto de dados para o nível de esquema](../e2e.md#migrate-labels).

Os rótulos podem ser aplicados a todo o conjunto de dados da guia **[!UICONTROL Governança de dados]** do espaço de trabalho **[!UICONTROL Conjuntos de dados]**. O espaço de trabalho permite gerenciar rótulos de uso de dados no nível do conjunto de dados.

![A guia [!UICONTROL Governança de Dados] do espaço de trabalho [!UICONTROL Conjuntos de Dados] com Governança de Dados realçada.](../images/labels/dataset-governance.png)

Para editar rótulos de uso de dados no nível do conjunto de dados, comece selecionando o ícone de lápis (![Um ícone de lápis.](/help/images/icons/edit.png)) na linha do nome do conjunto de dados.

![A guia [!UICONTROL Governança de Dados] do espaço de trabalho [!UICONTROL Conjuntos de Dados] com o ícone de lápis de edição realçado.](../images/labels/dataset-level-edit.png)

A caixa de diálogo **[!UICONTROL Editar rótulos de governança]** é aberta. Na caixa de diálogo, marque as caixas ao lado dos rótulos que deseja aplicar ao conjunto de dados. Lembre-se de que esses rótulos serão herdados por todos os campos no conjunto de dados. O cabeçalho **[!UICONTROL Rótulos Aplicados]** é atualizado à medida que você marca cada caixa, mostrando os rótulos que você escolheu. Depois de selecionar os rótulos desejados, selecione **[!UICONTROL Salvar alterações]**.

![A caixa de diálogo Editar Rótulos de Governança com caixas de seleção de rótulo e Salvar alterações foi realçada.](../images/labels/apply-labels-dataset.png)

O espaço de trabalho **[!UICONTROL Governança de dados]** será exibido novamente, mostrando os rótulos que você aplicou no nível do conjunto de dados na linha inicial da tabela. Você também pode ver os rótulos, indicados por cartões individuais, que são herdados para cada um dos campos no conjunto de dados.

![A guia [!UICONTROL Governança de Dados] do espaço de trabalho [!UICONTROL Conjuntos de Dados] com rótulos de nível de conjunto de dados aplicados e rótulos de campo de conjunto de dados herdados realçados.](../images/labels/applied-dataset-labels.png)

### Remover rótulos de um conjunto de dados {#remove-labels-from-a-dataset}

Os rótulos adicionados no nível do conjunto de dados têm um &quot;x&quot; ao lado do cartão. Isso permite remover os rótulos de todo o conjunto de dados. Os rótulos herdados ao lado de cada campo não têm um &quot;x&quot; ao lado deles e aparecem &quot;esmaecidos&quot;. Estes **rótulos herdados são somente leitura**, o que significa que eles não podem ser removidos ou editados no nível do campo.

<!-- ## View labels at the dataset field level {#view-labels-at-dataset-field-level} -->

<!-- To view labels inherited by the dataset from the schema level, select **[!UICONTROL Datasets]** to navigate to the datasets workspace and select the relevant dataset from the list. 

![The Browse tab of the Datasets workspace with Datasets highlighted in the left sidebar.](../images/labels/dataset-navigation.png)

Next, select the **[!UICONTROL Data Governance]** tab to show the labels that have been applied to the dataset. You can also see that the labels are inherited down to each of the fields within the dataset.

![Dataset Labels inherited by fields](../images/labels/dataset-labels-applied.png)

The inherited labels beside each field do not have an "x" next to them and appear "greyed out" with no ability to remove or edit. This is because **inherited fields are read-only**, meaning they cannot be removed at the field level. -->

<!--Beleive can cut above here  -->

A opção **[!UICONTROL Mostrar rótulos herdados]** está ativada por padrão, o que permite que você veja quaisquer rótulos herdados do esquema para seus campos. A desativação da alternância oculta todos os rótulos herdados no conjunto de dados.

![A guia Governança de Dados do espaço de trabalho Conjuntos de Dados com a opção Mostrar rótulos herdados realçada.](../images/labels/inherited-labels.png)

<!-- Labels applied to the dataset appear in read-only form within the **[!UICONTROL Data Governance]** view for that dataset. 

![The Data Governance tab of the Datasets workspace with labels highlighted.](../images/labels/read-only-governance-labels.png) -->

>[!NOTE]
>
>Os rótulos aplicados antes da desativação do recurso de rotulagem do conjunto de dados podem ser removidos do conjunto de dados localizando o conjunto de dados relevante e selecionando o ícone de cancelamento no rótulo.
>&#x200B;>![A guia Governança de Dados do espaço de trabalho Conjuntos de Dados com um rótulo excluível destacado.](../images/labels/remove-governance-labels.png)
>&#x200B;>Consulte a documentação para obter instruções sobre [como migrar rótulos aplicados anteriormente do conjunto de dados para o nível de esquema](../e2e.md#migrate-labels).

## Gerenciar rótulos personalizados {#manage-custom-labels}

>[!CONTEXTUALHELP]
>id="platform_governance_createlabels"
>title="Criar rótulos"
>abstract="Os rótulos permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. A Experience Platform fornece um conjunto padrão de rótulos para você usar, mas também é possível criar rótulos personalizados específicos para a sua organização."

Você pode criar seus próprios rótulos de uso personalizados dentro do espaço de trabalho **[!UICONTROL Políticas]** na interface do usuário do [!DNL Experience Platform]. Selecione **[!UICONTROL Políticas]** no menu de navegação esquerdo e, em seguida, **[!UICONTROL Rótulos]** para exibir uma lista de rótulos existentes. Aqui, selecione **[!UICONTROL Criar rótulo]**.

![O espaço de trabalho de Políticas com a política de criação foi realçado.](../images/labels/create-label-btn.png)

A caixa de diálogo **[!UICONTROL Criar rótulo]** é exibida. Aqui, forneça as seguintes informações para o novo rótulo:

* **[!UICONTROL Nome]**: um identificador exclusivo para o rótulo. Esse valor é usado para fins de pesquisa e, portanto, deve ser curto e conciso.
* **[!UICONTROL Nome amigável]**: Um nome de exibição amigável para o rótulo.
* **[!UICONTROL Descrição]**: (opcional) uma descrição para o rótulo para fornecer mais contexto.

Quando terminar, selecione **[!UICONTROL Criar]**.

![A caixa de diálogo Criar rótulo do espaço de trabalho de Políticas com Create foi realçada.](../images/labels/create-label-dialog.png)

A caixa de diálogo é fechada e o rótulo personalizado recém-criado aparece na lista na guia **[!UICONTROL Rótulos]**.

![A guia Rótulos do espaço de trabalho Políticas com o novo rótulo personalizado realçado.](../images/labels/label-created.png)

O rótulo agora pode ser selecionado em **[!UICONTROL Rótulos personalizados]** ao editar rótulos de uso para conjuntos de dados e campos ou ao criar políticas de uso de dados.

![A caixa de diálogo Aplicar Rótulos de Acesso e Governança de Dados com os rótulos personalizados destacados.](../images/labels/add-custom-label.png)

## Próximas etapas

Agora que você adicionou rótulos de uso de dados no nível do conjunto de dados e do campo, você pode começar a assimilar dados no [!DNL Experience Platform]. Para saber mais, comece lendo a [documentação de assimilação de dados](../../ingestion/home.md).

Agora também é possível definir políticas de uso de dados com base nos rótulos aplicados. Para obter mais informações, consulte a [visão geral das políticas de uso de dados](../policies/overview.md).

<!-- The workflow of this video is now outdated. This can be enabled once the video has been updated

## Additional resources

The following video is intended to support your understanding of Data Governance, and outlines how to apply labels to a dataset and individual fields.

>[!VIDEO](https://video.tv.adobe.com/v/3422793?quality=12&enable10seconds=on&speedcontrol=on&captions=por_br) -->
