---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados;ui;espaço de trabalho;enum;campo;
solution: Experience Platform
title: Definir campos de enumeração e valores sugeridos na interface
description: Saiba como definir enumerações e valores sugeridos para campos de sequência na interface do usuário do Experience Platform.
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 8%

---

# Definir enumerações e valores sugeridos na interface {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="Enumerações e valores sugeridos"
>abstract="Uma **Enumeração** restringe um campo de string para permitir somente dados que correspondam a um conjunto predefinido de valores a serem assimilados. Cada restrição de enumeração pode receber um **Nome de exibição** que preenche detalhamentos de atributos na interface de segmentação. **Valores sugeridos** para um campo não restringem a ingestão e determinam apenas os nomes de exibição mostrados na Segmentação. Se você tiver vários esquemas que compartilham um campo pertencente a uma classe ou grupo de campos comum e definir diferentes enumerações ou valores sugeridos para esse campo entre cada esquema, esses valores serão mesclados e anexados no esquema de união."

No Experience Data Model (XDM), um campo de sequência pode receber um conjunto predefinido de valores aceitos ou sugeridos para controlar melhor quais valores são assimilados nesse campo ou como ele se comportará na segmentação.

**[!UICONTROL Enumerações]** restringir os valores que podem ser assimilados de um campo de string para um conjunto predefinido. Se você tentar assimilar dados em um campo enum e o valor não corresponder a nenhum dos definidos em sua configuração, a assimilação será negada.

Ao contrário dos enums, a variável **[!UICONTROL Valores sugeridos]** permite que o indique um conjunto de valores recomendados para um campo de string que não restringem os valores que ele pode assimilar. Em vez disso, os valores sugeridos afetam quais valores predefinidos estão disponíveis no [Interface de segmentação](../../../segmentation/ui/overview.md) ao incluir o campo de string como um atributo.

Quando [definição de um novo campo](./overview.md#define) na interface do usuário do Adobe Experience Platform e definir o tipo como [!UICONTROL String], você terá a opção de definir uma [enum](#enum) ou [valores sugeridos](#suggested-values) para esse campo.

![Imagem mostrando a opção Enumeração e valores sugeridos ativada para um campo de string na interface do usuário](../../images/ui/fields/enum/enum-options-selected.png)

Este documento aborda como definir enumerações e valores sugeridos na [!UICONTROL Esquemas] Espaço de trabalho da interface do usuário. Para obter uma visão geral rápida sobre enumerações e valores sugeridos, incluindo como configurá-los na interface do usuário e seus efeitos downstream, assista ao seguinte vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## Definir um enum {#enum}

Selecionar **[!UICONTROL Enumerações e valores sugeridos]** e selecione **[!UICONTROL Enumerações]**. Controles adicionais são exibidos, permitindo especificar as restrições de valor para o enum. Para adicionar uma restrição, selecione **[!UICONTROL Adicionar linha]**.

![Imagem mostrando a opção Enumerações selecionada na interface do usuário](../../images/ui/fields/enum/enum-add-row.png)

No **[!UICONTROL Valor]** , você deve fornecer o valor exato ao qual deseja restringir o campo. Você pode, opcionalmente, fornecer um **[!UICONTROL Nome de exibição]** para a restrição também, o que afeta como o valor será representado na segmentação.

Continuar a usar **[!UICONTROL Adicionar linha]** para adicionar as restrições desejadas e os rótulos opcionais ao enum, ou selecione o ícone excluir (![Imagem do ícone de exclusão](../../images/ui/fields/enum/remove-icon.png)) ao lado de uma linha adicionada anteriormente para removê-la. Quando terminar, selecione **[!UICONTROL Aplicar]** para aplicar as alterações ao esquema.

![Imagem que mostra os valores de enumeração e nomes de exibição preenchidos para o campo de string na interface](../../images/ui/fields/enum/enum-confirm.png)

A tela é atualizada para refletir as alterações. Ao explorar esse esquema no futuro, você pode visualizar e editar as restrições para o campo de enumeração no painel direito.

## Definir valores sugeridos {#suggested-values}

Selecionar **[!UICONTROL Enumerações e valores sugeridos]** e selecione **[!UICONTROL Valores sugeridos]** para fazer com que controles adicionais apareçam. Aqui, selecione **[!UICONTROL Adicionar linha]** para começar a adicionar valores sugeridos.

![Imagem mostrando a opção Valores sugeridos selecionada na interface do usuário](../../images/ui/fields/enum/suggested-add-row.png)

No **[!UICONTROL Nome de exibição]** forneça um nome amigável para o valor como deseja que ele seja exibido na interface do usuário de segmentação. Para adicionar mais valores sugeridos, selecione **[!UICONTROL Adicionar linha]** novamente e repita o processo conforme necessário. Para remover uma linha adicionada anteriormente, selecione ![o ícone excluir](../../images/ui/fields/enum/remove-icon.png) ao lado da linha em questão.

Quando terminar, selecione **[!UICONTROL Aplicar]** para aplicar as alterações ao esquema.

![Imagem que mostra os valores de enumeração e nomes de exibição preenchidos para o campo de string na interface](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>Há um atraso de aproximadamente cinco minutos para que os valores sugeridos atualizados de um campo sejam refletidos na interface do usuário de segmentação.

### Gerenciar valores sugeridos para campos padrão

Alguns campos de componentes XDM padrão contêm seus próprios valores sugeridos, como `eventType` do [[!UICONTROL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Embora seja possível criar valores sugeridos adicionais para um campo padrão, não é possível modificar ou remover valores sugeridos que não estejam definidos pela organização. Ao visualizar um campo padrão na interface do usuário do, os valores sugeridos são exibidos, mas são somente leitura.

![Imagem que mostra os valores de enumeração e nomes de exibição preenchidos para o campo de string na interface](../../images/ui/fields/enum/suggested-standard.png)

Para adicionar novos valores sugeridos para um campo padrão, selecione **[!UICONTROL Adicionar linha]**. Para remover um valor sugerido que foi adicionado anteriormente por sua organização, selecione ![o ícone excluir](../../images/ui/fields/enum/remove-icon.png) ao lado da linha em questão.

![Imagem que mostra os valores de enumeração e nomes de exibição preenchidos para o campo de string na interface](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## Regras de evolução para enumerações e valores sugeridos {#evolution}

Depois que um esquema com um campo de enumeração é usado para assimilar dados na Platform, qualquer alteração adicional feita na definição do esquema deve estar em conformidade com os dados já existentes no sistema. Em geral, as alterações feitas em um campo existente só podem fazer com que esse campo **menos** restritivo. Um campo não pode se tornar mais restritivo do que já é.

Quando se trata de enumerações e valores sugeridos, as seguintes regras se aplicam após a assimilação:

* Você **PODE** adicione os valores sugeridos para campos padrão e personalizados com os valores sugeridos existentes.
* Você **PODE** remova os valores sugeridos dos campos personalizados com os valores sugeridos existentes.
* Você **PODE** adicione novos valores de enumeração para um campo de enumeração personalizado existente.
* Você **PODE** alterne os valores de enumeração de um campo personalizado somente para os valores sugeridos ou converta-os em uma sequência de caracteres sem enumeração ou valores sugeridos. **Essa opção não pode ser desfeita depois de aplicada.**
* Você **NÃO PODE** remova enumerações ou valores sugeridos dos campos padrão.
* Você **NÃO PODE** adicione valores de enumeração a um campo sem enumeração existente.
* Você **NÃO PODE** remova menos do que todos os valores de enumeração existentes para um campo personalizado.
* Você **NÃO PODE** alterne de valores sugeridos para um enum.

## Mesclar regras para enumerações e valores sugeridos {#merging}

Se vários esquemas usarem o mesmo campo de enumeração com configurações diferentes e esses esquemas forem incluídos em uma união, determinadas regras se aplicam quando se trata de como as diferenças de enumeração são reconciliadas. As regras exatas dependem se os esquemas que fazem referência ao mesmo campo padrão (como `eventType`) ou se estiverem fazendo referência ao mesmo caminho de campo personalizado em grupos de campos diferentes.

Se fizer referência ao mesmo campo padrão:

* Quaisquer valores adicionais sugeridos são **ANEXADO** na união.
* As atualizações feitas nos valores sugeridos para a mesma chave enum são **ATUALIZADO** na união.

Se estiver fazendo referência ao mesmo caminho de campo personalizado em grupos de campos diferentes:

* Quaisquer valores adicionais sugeridos são **ANEXADO** na união.
* Se o mesmo valor adicional sugerido for definido em mais de um schema, esses valores serão **MESCLADO** na união. Em outras palavras, o mesmo valor sugerido não aparecerá duas vezes após a mesclagem.

## Limitações da validação

Devido às limitações atuais do sistema, há dois casos em que um enum não é validado pelo sistema durante a assimilação:

1. O enum é definido em um [campo de matriz](./array.md).
1. A enumeração está definida em mais de um nível profundo na hierarquia de esquema.

## Próximas etapas

Este guia abordou como definir enumerações e valores sugeridos para campos de sequência na interface do usuário do. Para obter informações sobre como gerenciar enumerações e valores sugeridos usando a API do Registro de Esquema, consulte o seguinte [tutorial](../../tutorials/suggested-values.md).

Para saber como definir outros tipos de campo XDM na variável [!DNL Schema Editor], consulte a visão geral em [definição de campos na interface](./overview.md#special).
