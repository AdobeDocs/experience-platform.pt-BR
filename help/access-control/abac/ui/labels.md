---
keywords: Experience Platform;página inicial;tópicos populares;controle de acesso;controle de acesso baseado em atributo
title: Rótulos do gerenciador de controle de acesso baseado em atributos
description: Gerencie rótulos por meio da interface de Permissões na Adobe Experience Cloud.
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: 855f0a1384f658d39aa9d4fbb6bcb032933e59db
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 11%

---

# Gerenciar rótulos

Você pode usar rótulos para categorizar conjuntos de dados e campos de acordo com as políticas de uso de dados e controle de acesso baseado em atributos. Os rótulos podem ser aplicados a qualquer momento, proporcionando flexibilidade na maneira como você escolhe controlar os dados. As práticas recomendadas incentivam a rotulação de dados assim que eles forem assimilados na Adobe Experience Platform ou assim que os dados estiverem disponíveis para uso. Leia este documento para saber como gerenciar rótulos na interface do usuário de permissões.

Para obter uma lista abrangente de rótulos e suas políticas de governança correspondentes, leia o manual em [rótulos de uso de dados principais](../../../data-governance/labels/reference.md){target="_blank"}.

>[!NOTE]
>
>Para criar ou exibir [atributos computados](../../../profile/computed-attributes/overview.md){target="_blank"} com campos contendo determinado rótulo, você deve ter acesso a esse rótulo.

## Explorar rótulos {#explore-labels}

Para exibir todos os rótulos disponíveis, navegue até **[!UICONTROL Permissions]** em [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Selecione **[!UICONTROL Labels]** no painel esquerdo.

![O espaço de trabalho de rótulos em Permissões com Rótulos realçados no painel esquerdo.](../../images/ui/labels/labels-home.png){zoomable="yes"}

Os rótulos são categorizados por tipo e pertencem a uma das seguintes categorias:

| Tipo | Descrição |
| --- | --- |
| [Contrato](../../../data-governance/labels/reference.md#contract){target="_blank"} | Essa categoria é usada para categorizar dados que contêm obrigações contratuais ou estão relacionados às políticas de governança de dados da sua organização. |
| [Identidade](../../../data-governance/labels/reference.md#identity){target="_blank"} | Esta categoria é usada para categorizar dados que podem identificar direta ou indiretamente uma pessoa. |
| [Sensível](../../../data-governance/labels/reference.md#sensitive){target="_blank"} | Essa categoria é usada para categorizar dados que sua organização considera confidenciais. |
| [Ecossistema de parceiros](../../../data-governance/labels/reference.md#partner){target="_blank"} | Esta categoria é usada para categorizar dados obtidos de fontes externas à sua organização. |
| Envolvimento responsável | Esta categoria contém um único rótulo, **[!UICONTROL Potential for Bias]**, que reflete dados com potencial para introduzir viés. |
| Personalizado | Esta categoria inclui etiquetas criadas pela sua organização. |

Para filtrar rótulos, selecione o ícone de filtro (![ícone de filtro](/help/images/icons/filter.png)) e selecione o tipo de rótulo desejado na lista suspensa **[!UICONTROL Type]**.

![O espaço de trabalho de rótulos com a opção de filtro expandida e a lista suspensa de tipo realçada.](../../images/ui/labels/label-filter.png){zoomable="yes"}

Para exibir um rótulo individual, selecione o nome do rótulo na lista. A página de detalhes do rótulo será exibida. Os rótulos principais do Adobe são **não** editáveis.

![Página de detalhes de um rótulo individual.](../../images/ui/labels/label-details.png){zoomable="yes"}

## Criar um rótulo personalizado {#create-custom-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="Uso de rótulos"
>abstract="Você pode usar rótulos personalizados para aplicar configurações de governança de dados e controle de acesso aos seus dados."

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Criar novo rótulo"
>abstract="É possível criar seus próprios rótulos personalizados para atender às necessidades de sua organização. Os rótulos personalizados podem ser usados para aplicar configurações de governança de dados e controle de acesso aos seus dados."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=pt-BR#manage-labels" text="Gerenciar rótulos personalizados"

>[!NOTE]
>
>Para criar um rótulo personalizado, você precisará de uma função contendo as permissões **[!UICONTROL Manage Usage Labels]** e a sandbox `Prod`.

Para criar um novo rótulo, selecione **[!UICONTROL Labels]** no painel esquerdo do espaço de trabalho **[!UICONTROL Permissions]** e selecione **[!UICONTROL Create label]**.

![O espaço de trabalho de rótulos com a opção Criar rótulo foi realçada.](../../images/ui/labels/create-label.png){zoomable="yes"}

A caixa de diálogo **[!UICONTROL Create new label]** é exibida, solicitando que você insira um **[!UICONTROL Name]**, um **[!UICONTROL Friendly name]** e **[!UICONTROL Description]**.

>[!IMPORTANT]
>
> O rótulo [!UICONTROL Name] não pode ser alterado depois que o rótulo foi criado e não há suporte para exclusão de rótulo no momento.

Selecione **[!UICONTROL Confirm]** para concluir a criação do rótulo.

![A caixa de diálogo Criar novo rótulo com o Nome, Nome Amigável e Descrição foi preenchida e a opção Confirmar foi realçada.](../../images/ui/labels/create-new-label.png){zoomable="yes"}

## Editar um rótulo personalizado {#edit-custom-label}

Embora não seja possível editar o **[!UICONTROL Name]** de um rótulo personalizado, você pode editar o **[!UICONTROL Friendly name]** e o **[!UICONTROL Description]**. Para editar um rótulo personalizado, selecione o rótulo na lista dentro do espaço de trabalho **[!UICONTROL Labels]**.

![O espaço de trabalho de Rótulos com o rótulo realçado.](../../images/ui/labels/select-label.png){zoomable="yes"}

Edite qualquer um dos campos e clique em qualquer lugar fora da caixa de texto para salvar as alterações. Uma mensagem de confirmação será exibida na tela e o nome de **[!UICONTROL Modified by]** e a data de **[!UICONTROL Modified]** serão alterados.

![A página de detalhes do rótulo com uma mensagem &quot;atualizado com êxito&quot; é exibida.](../../images/ui/labels/edit-label.png){zoomable="yes"}

## Próximas etapas

Agora que você tem uma compreensão mais profunda dos rótulos, pode começar [aplicá-los aos esquemas](../../../xdm/tutorials/labels.md).
