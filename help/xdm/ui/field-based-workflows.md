---
title: Workflows baseados em campo no Editor de esquemas
description: Saiba como adicionar campos individualmente de grupos de campos existentes aos esquemas do modelo de dados de experiência (XDM).
hide: true
hidefromtoc: true
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: b224783922c3b6c5e2045134be2512748ca2575b
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# Workflows baseados em campo no Editor de esquemas

O Adobe Experience Platform fornece um conjunto robusto de [grupos de campos](../schema/composition.md#field-group) para uso em esquemas do Experience Data Model (XDM). A estrutura e a semântica por trás desses grupos de campos são cuidadosamente adaptadas para atender a uma grande variedade de casos de uso de segmentação e outros aplicativos downstream na Platform. Você também pode definir seus próprios grupos de campos personalizados para atender a necessidades comerciais exclusivas.

Quando você adiciona um grupo de campos a um esquema, esse esquema herda todos os campos contidos nesse grupo. No entanto, agora é possível adicionar campos individuais ao esquema sem precisar incluir outros campos do grupo de campos associado que você não necessariamente pode usar.

Este guia aborda os diferentes métodos para adicionar campos individuais a um esquema na interface do usuário da plataforma.

## Pré-requisitos

Este tutorial pressupõe que você esteja familiarizado com o [composição de esquemas XDM](../schema/composition.md) e como usar o Editor de esquemas na interface do Platform. Para acompanhar, você deve iniciar o processo de [criação de um novo schema](./resources/schemas.md) e atribuindo-a a uma classe padrão antes de continuar com este guia.

## Remover campos adicionados de grupos de campos padrão {#remove-field-group}

Depois de ter adicionado um grupo de campos padrão a um esquema, você pode remover todos os campos padrão que não são necessários.

>[!NOTE]
>
>A remoção de campos de um grupo de campos padrão afeta apenas o esquema que está sendo trabalhado e não afeta o próprio grupo de campos. Se você remover campos padrão em um esquema, esses campos ainda estarão disponíveis em todos os outros esquemas que empregam o mesmo grupo de campos.

No exemplo a seguir, o grupo de campos padrão **[!UICONTROL Detalhes demográficos]** foi adicionado a um esquema. Para remover um único campo, como `taxId`, selecione o campo na tela e selecione **[!UICONTROL Remover]** no painel direito.

![Remover campo único](../images/ui/field-based-workflows/remove-single-field.png)

Se houver vários campos que você deseja remover, é possível gerenciar o grupo de campos como um todo. Selecione um campo pertencente ao grupo na tela e selecione **[!UICONTROL Gerenciar campos relacionados]** no painel direito.

![Gerenciar campos relacionados](../images/ui/field-based-workflows/manage-related-fields.png)

Uma caixa de diálogo é exibida mostrando a estrutura do grupo de campos em questão. Aqui, é possível usar as caixas de seleção fornecidas para marcar ou desmarcar os campos necessários. Quando estiver satisfeito, selecione **[!UICONTROL Confirmar o]**.

![Selecionar campos do grupo de campos](../images/ui/field-based-workflows/select-fields.png)

A tela reaparece com apenas os campos selecionados presentes na estrutura do esquema.

![Campos adicionados](../images/ui/field-based-workflows/fields-added.png)

## Adicionar campos padrão diretamente a um esquema

Você pode adicionar campos de grupos de campos padrão diretamente a um esquema sem precisar saber seu grupo de campos correspondente antecipadamente. Para adicionar um campo padrão a um esquema, selecione o sinal de mais (**+**) ao lado do nome do esquema na tela. Um **[!UICONTROL Campo sem título]** o espaço reservado é exibido na estrutura do esquema e o painel direito é atualizado para revelar controles para configurar o campo.

![Espaço reservado do campo](../images/ui/field-based-workflows/root-custom-field.png)

Em **[!UICONTROL Nome do campo]**, comece digitando o nome do campo que deseja adicionar. O sistema procura automaticamente por campos padrão que correspondam à consulta e os lista em **[!UICONTROL Campos padrão recomendados]**, incluindo os grupos de campos aos quais pertencem.

![Campos padrão recomendados](../images/ui/field-based-workflows/standard-field-search.png)

Embora alguns campos padrão compartilhem o mesmo nome, sua estrutura pode variar dependendo do grupo de campos de onde vêm. Se um campo padrão estiver aninhado em um objeto principal na estrutura do grupo de campos, o campo principal também será incluído no esquema se o campo secundário for adicionado.

Selecione o ícone de visualização (![Ícone Visualizar](../images/ui/field-based-workflows/preview-icon.png)) ao lado de um campo padrão para exibir a estrutura do grupo de campos e entender melhor como ele pode estar aninhado. Para adicionar o campo padrão ao esquema, selecione o ícone de adição (![Ícone de adição](../images/ui/field-based-workflows/add-icon.png)).

![Adicionar campo padrão](../images/ui/field-based-workflows/add-standard-field.png)

A tela é atualizada para mostrar o campo padrão adicionado ao esquema, incluindo todos os campos principais sob os quais ele está aninhado dentro da estrutura do grupo de campos. O nome do grupo de campos também está listado em **[!UICONTROL Grupos de campos]** no painel esquerdo. Se quiser adicionar mais campos do mesmo grupo, selecione **[!UICONTROL Gerenciar campos relacionados]** no painel direito.

![Campo padrão adicionado](../images/ui/field-based-workflows/standard-field-added.png)

## Adicionar campos personalizados diretamente a um esquema

Semelhante ao fluxo de trabalho para campos padrão, também é possível adicionar seus próprios campos personalizados diretamente a um esquema.

Para adicionar campos ao nível raiz de um esquema, selecione o sinal de mais (**+**) ao lado do nome do esquema na tela. Um **[!UICONTROL Campo sem título]** o espaço reservado é exibido na estrutura do esquema e o painel direito é atualizado para revelar controles para configurar o campo.

![Campo personalizado da raiz](../images/ui/field-based-workflows/root-custom-field.png)

Comece a digitar o nome do campo que deseja adicionar e o sistema inicia automaticamente a pesquisa por campos padrão correspondentes. Para criar um novo campo personalizado, selecione a opção superior anexada com **([!UICONTROL Novo campo])**.

![Novo campo](../images/ui/field-based-workflows/custom-field-search.png)

Aqui, forneça um nome para exibição e um tipo de dados para o campo. Em **[!UICONTROL Atribuir grupo de campos]**, você deve selecionar um grupo de campos ao qual o novo campo será associado. Comece a digitar o nome do grupo de campos e se você já tiver [grupos de campos personalizados criados](./resources/field-groups.md#create) eles aparecerão na lista suspensa. Como alternativa, você pode digitar um nome exclusivo no campo para criar um novo grupo de campos.

![Selecionar grupo de campos](../images/ui/field-based-workflows/select-field-group.png)

>[!WARNING]
>
>Se você selecionar um grupo de campos personalizado existente, todos os outros esquemas que empregam esse grupo de campos também herdarão o campo recém-adicionado depois que você salvar as alterações. Por esse motivo, somente selecione um grupo de campos existente se desejar esse tipo de propagação. Caso contrário, você deve optar por criar um novo grupo de campos personalizados.

Quando terminar, selecione **[!UICONTROL Aplicar]**.

![Aplicar campo](../images/ui/field-based-workflows/apply-field.png)

O novo campo é adicionado à tela e seu namespace é alterado em [ID do inquilino](../api/getting-started.md#know-your-tenant_id) para evitar conflitos com campos XDM padrão. O grupo de campos ao qual você associou o novo campo também aparece em **[!UICONTROL Grupos de campos]** no painel esquerdo.

![ID do inquilino](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>O restante dos campos fornecidos pelo grupo de campos personalizados selecionado são removidos do esquema por padrão. Se quiser adicionar alguns desses campos ao esquema, selecione um campo pertencente ao grupo e selecione **[!UICONTROL Gerenciar campos relacionados]** no painel direito.

### Adicionar campos personalizados à estrutura de grupos de campos padrão

Se o esquema em que você está trabalhando tiver um campo do tipo objeto fornecido por um grupo de campos padrão, será possível adicionar seus próprios campos personalizados a esse objeto padrão. Selecione o sinal de mais (**+**) ao lado da raiz do objeto e forneça os detalhes do campo personalizado no painel direito.

![Adicionar campo ao objeto padrão](../images/ui/field-based-workflows/add-field-to-standard-object.png)

Depois de aplicar as alterações, o novo campo aparece sob o namespace da ID do locatário dentro do objeto padrão. Esse namespace aninhado impede conflitos de nome de campo dentro do próprio grupo de campos para evitar alterações em outros esquemas que usam o mesmo grupo de campos.

![Campo adicionado ao objeto padrão](../images/ui/field-based-workflows/added-to-standard-object.png)

## Próximas etapas

Este guia abordou os novos fluxos de trabalho baseados em campo para o Editor de esquemas na interface do usuário da plataforma. Para obter mais informações sobre o gerenciamento de esquemas na interface, consulte [Visão geral da interface](./overview.md).
