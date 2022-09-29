---
keywords: Experience Platform; home; tópicos populares; api; API; XDM; sistema XDM; modelo de dados de experiência; modelo de dados; ui; espaço de trabalho; enum; campo;
solution: Experience Platform
title: Definir campos de enumeração e valores sugeridos na interface do usuário
description: Saiba como definir enumerações e valores sugeridos para campos de sequência na interface do usuário do Experience Platform.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: ea27486a198f5248eeb5348ce20865bc41c2339a
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 0%

---

# Definir enumerações e valores sugeridos na interface do usuário {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="Enumerações e valores sugeridos"
>abstract="Um **Enum** restringe um campo de string para permitir somente dados que correspondam a um conjunto predefinido de valores a serem assimilados. Cada restrição pode receber uma **Nome de exibição** que preenche detalhamentos de atributos na interface do usuário de segmentação. **Valores sugeridos** para um campo, não restrinjam a assimilação e determinem apenas os nomes de exibição mostrados na Segmentação. Se você tiver vários esquemas que compartilham um campo pertencente a uma classe ou grupo de campos comum e definir diferentes enumerações ou valores sugeridos para esse campo entre cada schema, esses valores serão mesclados e anexados no schema de união."

No Experience Data Model (XDM), um campo de cadeia de caracteres pode receber um conjunto predefinido de valores aceitos ou sugeridos para controlar melhor quais valores são assimilados nesse campo ou como ele se comportará na segmentação.

Um **enum** restringe os valores que podem ser assimilados para um campo de string a um conjunto predefinido. Se você tentar assimilar dados para um campo enum e o valor não corresponder a nenhum daqueles definidos em sua configuração, a assimilação será negada.

Em contraste com enumerações, adicionar **valores sugeridos** para um campo de string não restringe os valores que ele pode assimilar. Em vez disso, os valores sugeridos afetam quais valores predefinidos estão disponíveis na variável [Interface do usuário de segmentação](../../../segmentation/ui/overview.md) ao incluir o campo de string como um atributo.

When [definição de um novo campo](./overview.md#define) na interface do usuário do Adobe Experience Platform e definir o tipo como [!UICONTROL String], você tem a opção de definir um [enum](#enum) ou [valores sugeridos](#suggested-values) para esse campo.

![Imagem que mostra a opção Enum &amp; Suggested Values ativada para um campo de string na interface do usuário](../../images/ui/fields/enum/enum-options-selected.png)

## Definir um enum {#enum}

Selecionar **[!UICONTROL Enumerações e valores sugeridos]**, em seguida selecione **[!UICONTROL Enumerações]**. Controles adicionais são exibidos, permitindo especificar as restrições de valor para o enum. Para adicionar uma restrição, selecione **[!UICONTROL Adicionar linha]**.

![Imagem que mostra a opção Enumerações selecionada na interface do usuário](../../images/ui/fields/enum/enum-add-row.png)

Em **[!UICONTROL Valor]** , é necessário fornecer o valor exato ao qual deseja restringir o campo. Como opção, você pode fornecer um **[!UICONTROL Nome de exibição]** para a restrição também, o que afeta como o valor será representado na segmentação.

Continue a usar **[!UICONTROL Adicionar linha]** para adicionar as restrições desejadas e os rótulos opcionais ao enum ou selecione o ícone excluir (![Imagem do ícone de exclusão](../../images/ui/fields/enum/remove-icon.png)) ao lado de uma linha adicionada anteriormente para removê-la. Quando terminar, selecione **[!UICONTROL Aplicar]** para aplicar as alterações ao schema.

![Imagem que mostra os valores de enumeração e os nomes de exibição preenchidos para o campo de string na interface do usuário](../../images/ui/fields/enum/enum-confirm.png)

A tela é atualizada para refletir as alterações. Ao explorar esse schema no futuro, você poderá visualizar e editar as restrições do campo enum no painel direito.

## Definir valores sugeridos {#suggested-values}

Selecionar **[!UICONTROL Enumerações e valores sugeridos]**, em seguida selecione **[!UICONTROL Valores Sugeridos]** para fazer com que controles adicionais apareçam. Aqui, selecione **[!UICONTROL Adicionar linha]** para começar a adicionar valores sugeridos.

![Imagem mostrando a opção Valores sugeridos selecionada na interface do usuário](../../images/ui/fields/enum/suggested-add-row.png)

Em **[!UICONTROL Nome de exibição]** , forneça um nome amigável para o valor como deseja que apareça na interface do usuário de segmentação. Para adicionar mais valores sugeridos, selecione **[!UICONTROL Adicionar linha]** e repita o processo conforme necessário. Para remover uma linha adicionada anteriormente, selecione ![o ícone excluir](../../images/ui/fields/enum/remove-icon.png) ao lado da linha em questão.

Quando terminar, selecione **[!UICONTROL Aplicar]** para aplicar as alterações ao schema.

![Imagem que mostra os valores de enumeração e os nomes de exibição preenchidos para o campo de string na interface do usuário](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>Há um atraso de aproximadamente cinco minutos para que os valores sugeridos atualizados de um campo sejam refletidos na interface do usuário de segmentação.

### Gerenciar valores sugeridos para campos padrão

Alguns campos dos componentes padrão do XDM contêm seus próprios valores sugeridos, como `eventType` do [[!UICONTROL ExperiênciaEvento XDM] classe](../../classes/experienceevent.md). Embora você possa criar valores sugeridos adicionais para um campo padrão, não é possível modificar ou remover quaisquer valores sugeridos que não sejam definidos pela organização. Ao visualizar um campo padrão na interface do usuário, os valores sugeridos são exibidos, mas são somente leitura.

![Imagem que mostra os valores de enumeração e os nomes de exibição preenchidos para o campo de string na interface do usuário](../../images/ui/fields/enum/suggested-standard.png)

Para adicionar novos valores sugeridos para um campo padrão, selecione **[!UICONTROL Adicionar linha]**. Para remover um valor sugerido que foi adicionado anteriormente por sua organização, selecione ![o ícone excluir](../../images/ui/fields/enum/remove-icon.png) ao lado da linha em questão.

![Imagem que mostra os valores de enumeração e os nomes de exibição preenchidos para o campo de string na interface do usuário](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## Regras de evolução para enumerações e valores sugeridos {#evolution}

Depois que um schema com um campo enum for usado para assimilar dados na Platform, qualquer outra alteração feita na definição do schema deverá estar em conformidade com os dados já existentes no sistema. Em geral, as alterações feitas em um campo existente só podem fazer esse campo **less** restritivo. Um campo não pode ser tornado mais restritivo do que já é.

Quando se trata de enumerações e valores sugeridos, as seguintes regras se aplicam após a assimilação:

* Você **CAN** adicione valores sugeridos para campos padrão e personalizados com valores sugeridos existentes.
* Você **CAN** remova os valores sugeridos de campos personalizados com valores sugeridos existentes.
* Você **CAN** adicione novos valores enum para um campo enum personalizado existente.
* Você **CAN** alterne os valores de enum de um campo personalizado somente para valores sugeridos ou converta-o em uma string sem enum ou valores sugeridos. **Este switch não pode ser desfeito uma vez aplicado.**
* Você **NÃO PODE** remova enumerações ou valores sugeridos de campos padrão.
* Você **NÃO PODE** adicione valores enum a um campo sem enum existente.
* Você **NÃO PODE** remova menos do que todos os valores enum existentes para um campo personalizado.
* Você **NÃO PODE** alterne de valores sugeridos para um enum.

## Mesclar regras para enumerações e valores sugeridos {#merging}

Se vários schemas usarem o mesmo campo de enumeração com configurações diferentes e esses schemas forem incluídos em uma união, determinadas regras se aplicarão quando se tratar de como as diferenças de enumeração são reconciliadas. As regras exatas dependem se os schemas que fazem referência ao mesmo campo padrão (como `eventType`) ou se estiverem referenciando o mesmo caminho de campo personalizado em grupos de campos diferentes.

Se estiver fazendo referência ao mesmo campo padrão:

* Quaisquer valores sugeridos adicionais são **ANEXADO** na união.
* As atualizações feitas nos valores sugeridos para a mesma chave de enumeração são **ATUALIZADO** na união.

Se estiver fazendo referência ao mesmo caminho de campo personalizado em grupos de campos diferentes:

* Quaisquer valores sugeridos adicionais são **ANEXADO** na união.
* Se o mesmo valor sugerido adicional for definido em mais de um schema, esses valores serão **MESCLADO** na união. Em outras palavras, o mesmo valor sugerido não aparecerá duas vezes após a mesclagem.

## Limitações de validação

Devido às limitações atuais do sistema, há dois casos em que um enum não é validado pelo sistema durante a ingestão:

1. O enum é definido em um [campo de matriz](./array.md).
1. O enum é definido com mais de um nível de profundidade na hierarquia do schema.

## Próximas etapas

Este guia abordou como definir enumerações e valores sugeridos para campos de sequência na interface do usuário do . Para obter informações sobre como gerenciar enumerações e valores sugeridos usando a API do Registro de Esquema, consulte o seguinte [tutorial](../../tutorials/suggested-values.md).

Para saber como definir outros tipos de campo XDM na variável [!DNL Schema Editor], consulte a visão geral em [definição de campos na interface do usuário](./overview.md#special).
