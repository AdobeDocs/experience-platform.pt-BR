---
title: Workflows baseados em campo no Editor de esquemas
description: Saiba como adicionar campos individualmente de grupos de campos existentes aos esquemas do modelo de dados de experiência (XDM).
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 0%

---

# Workflows baseados em campo no Editor de esquemas

O Adobe Experience Platform fornece um conjunto robusto de [grupos de campos](../schema/composition.md#field-group) padronizados para uso em esquemas do Experience Data Model (XDM). A estrutura e a semântica por trás desses grupos de campos são cuidadosamente adaptadas para atender a uma grande variedade de casos de uso de segmentação e outros aplicativos downstream no Experience Platform. Você também pode definir seus próprios grupos de campos personalizados para atender a necessidades comerciais exclusivas.

Quando você adiciona um grupo de campos a um esquema, esse esquema herda todos os campos contidos nesse grupo. No entanto, agora é possível adicionar campos individuais ao esquema sem precisar incluir outros campos do grupo de campos associado que você não necessariamente pode usar.

Este guia aborda os diferentes métodos para adicionar campos individuais a um esquema na interface do Experience Platform.

## Pré-requisitos

Este tutorial presume que você esteja familiarizado com a [composição de esquemas XDM](../schema/composition.md) e como usar o Editor de esquemas na interface do Experience Platform. Para dar continuidade, você deve iniciar o processo de [criação de um novo esquema](./resources/schemas.md) e atribuí-lo a uma classe padrão antes de continuar com este guia.

## Remover campos adicionados de grupos de campos padrão {#remove-field-group}

Depois de ter adicionado um grupo de campos padrão a um esquema, você pode remover todos os campos padrão que não são necessários.

>[!NOTE]
>
>A remoção de campos de um grupo de campos padrão afeta apenas o esquema que está sendo trabalhado e não afeta o próprio grupo de campos. Se você remover campos padrão em um esquema, esses campos ainda estarão disponíveis em todos os outros esquemas que empregam o mesmo grupo de campos.

No exemplo a seguir, o grupo de campos padrão **[!UICONTROL Detalhes demográficos]** foi adicionado a um esquema. Para remover um único campo, como `maritalStatus`, selecione o campo na tela e selecione **[!UICONTROL Remover]** no painel direito.

![O Editor de Esquemas com o grupo de campos, campo Estado Civil e Remover realçados.](../images/ui/field-based-workflows/remove-single-field.png)

Se houver vários campos que você deseja remover, é possível gerenciar o grupo de campos como um todo. Selecione um campo pertencente ao grupo na tela e selecione **[!UICONTROL Gerenciar campos relacionados]** no painel direito.

![O Editor de Esquemas com um campo e Gerenciar campos relacionados está realçado.](../images/ui/field-based-workflows/manage-related-fields.png)

Uma caixa de diálogo é exibida mostrando a estrutura do grupo de campos em questão. Aqui, é possível usar as caixas de seleção fornecidas para marcar ou desmarcar os campos necessários. Quando estiver satisfeito, selecione **[!UICONTROL Confirmar]**.

![A caixa de diálogo Gerenciar campos relacionados com o diagrama do grupo de campos e Confirmar realçados.](../images/ui/field-based-workflows/select-fields.png)

A tela reaparece com apenas os campos selecionados presentes na estrutura do esquema.

![O Editor de Esquemas com o grupo de campos recém-editado está realçado.](../images/ui/field-based-workflows/fields-added.png)

## Adicionar campos padrão diretamente a um esquema

Você pode adicionar campos de grupos de campos padrão diretamente a um esquema sem precisar saber seu grupo de campos correspondente antecipadamente. Para adicionar um campo padrão a um esquema, selecione o ícone de adição (**+**) ao lado do nome do esquema na tela. Um espaço reservado para **[!UICONTROL Campo sem título]** aparece na estrutura do esquema e o painel direito atualiza para revelar controles para configurar o campo.

![O Editor de Esquemas com um espaço reservado para campo raiz foi realçado.](../images/ui/field-based-workflows/root-custom-field.png)

Em **[!UICONTROL Nome do campo]**, comece digitando o nome do campo que deseja adicionar. O sistema procura automaticamente por campos padrão que correspondam à consulta e os lista em **[!UICONTROL Campos Padrão Recomendados]**, incluindo os grupos de campos aos quais pertencem.

![O nome do campo realçado e uma lista de campos padrão recomendados exibidos nas propriedades do campo do Editor de Esquemas.](../images/ui/field-based-workflows/standard-field-search.png)

Embora alguns campos padrão compartilhem o mesmo nome, sua estrutura pode variar dependendo do grupo de campos de onde vêm. Se um campo padrão estiver aninhado em um objeto principal na estrutura do grupo de campos, o campo principal também será incluído no esquema se o campo secundário for adicionado.

Selecione o ícone de visualização (![Ícone de visualização](/help/images/icons/preview.png)) ao lado de um campo padrão para exibir a estrutura do grupo de campos e entender melhor como ele pode estar aninhado. Para adicionar o campo padrão ao esquema, selecione o ícone de adição (![ícone de adição](/help/images/icons/add-circle.png)).

![O ícone de adição foi realçado em um item dos campos padrão sugeridos.](../images/ui/field-based-workflows/add-standard-field.png)

A tela é atualizada para mostrar o campo padrão adicionado ao esquema, incluindo todos os campos principais sob os quais ele está aninhado dentro da estrutura do grupo de campos. O nome do grupo de campos também está listado em **[!UICONTROL Grupos de campos]** no painel esquerdo. Se quiser adicionar mais campos do mesmo grupo de campos, selecione **[!UICONTROL Gerenciar campos relacionados]** no painel direito.

![O Editor de Esquemas com o grupo Campo, campo padrão e Gerenciar campos relacionados está realçado.](../images/ui/field-based-workflows/standard-field-added.png)

## Adicionar campos personalizados diretamente a um esquema

Semelhante ao fluxo de trabalho para campos padrão, também é possível adicionar seus próprios campos personalizados diretamente a um esquema.

Para adicionar campos ao nível raiz de um esquema, selecione o ícone de adição (**+**) ao lado do nome do esquema na tela. Um espaço reservado para **[!UICONTROL Campo sem título]** aparece na estrutura do esquema e o painel direito atualiza para revelar controles para configurar o campo.

![O Editor de Esquemas com o ícone adicionar e um campo de nível raiz sem título foi realçado.](../images/ui/field-based-workflows/root-custom-field.png)

Comece a digitar o nome do campo que deseja adicionar e o sistema inicia automaticamente a pesquisa por campos padrão correspondentes. Para criar um novo campo personalizado, selecione a opção superior anexada com **([!UICONTROL Novo campo])**.

![O nome do campo e a sugestão de Novo Campo destacados nas propriedades do campo do Editor de Esquemas.](../images/ui/field-based-workflows/custom-field-search.png)

Aqui, forneça um nome para exibição e um tipo de dados para o campo. Em **[!UICONTROL Atribuir grupo de campos]**, você deve selecionar um grupo de campos ao qual o novo campo será associado. Comece a digitar o nome do grupo de campos e, se você já tiver [criado grupos de campos personalizados](./resources/field-groups.md#create), eles aparecerão na lista suspensa. Como alternativa, você pode digitar um nome exclusivo no campo para criar um novo grupo de campos.

![As configurações de propriedade do campo Nome de exibição, Tipo e Atribuir a estão realçadas no Editor de Esquemas.](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>Se você selecionar um grupo de campos personalizado existente, todos os outros esquemas que empregam esse grupo de campos também herdarão o campo recém-adicionado depois que você salvar as alterações. Por esse motivo, somente selecione um grupo de campos existente se desejar esse tipo de propagação. Caso contrário, você deve optar por criar um novo grupo de campos personalizados.

Quando terminar, selecione **[!UICONTROL Aplicar]**.

![Aplicar está realçado nas propriedades de campo do Editor de Esquemas.](../images/ui/field-based-workflows/apply-field.png)

O novo campo é adicionado à tela e tem namespace sob sua [ID de locatário](../api/getting-started.md#know-your-tenant_id) para evitar conflitos com campos XDM padrão. O grupo de campos ao qual você associou o novo campo também aparece em **[!UICONTROL Grupos de campos]** no painel esquerdo.

![O Editor de esquemas com o novo campo adicionado à tela e com o namespace sob sua ID de locatário. O grupo de campos e o campo estão realçados.](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>O restante dos campos fornecidos pelo grupo de campos personalizados selecionado são removidos do esquema por padrão. Se quiser adicionar alguns desses campos ao esquema, selecione um campo pertencente ao grupo e selecione **[!UICONTROL Gerenciar campos relacionados]** no painel direito.

### Adicionar campos personalizados à estrutura de grupos de campos padrão

Se o esquema em que você está trabalhando tiver um campo do tipo objeto fornecido por um grupo de campos padrão, será possível adicionar seus próprios campos personalizados a esse objeto padrão. Selecione o ícone de adição (**+**) ao lado da raiz do objeto.

>[!IMPORTANT]
>
>Quaisquer campos adicionados a um grupo de campos em um esquema também aparecerão em todos os outros esquemas que empregam esse mesmo grupo de campos.

![O Editor de Esquemas com o ícone de adição ao lado de um objeto padrão realçado.](../images/ui/field-based-workflows/add-field-to-standard-object.png)

Consulte o [Criar e editar esquemas no guia da interface](./resources/schemas.md#custom-fields-for-standard-groups) para obter mais informações sobre como adicionar campos personalizados.

## Próximas etapas

Este guia abordou os novos fluxos de trabalho baseados em campo para o Editor de esquemas na interface do Experience Platform. Para obter mais informações sobre o gerenciamento de esquemas na interface, consulte a [visão geral da interface](./overview.md).
