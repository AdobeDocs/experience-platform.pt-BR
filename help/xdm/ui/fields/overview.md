---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados;ui;espaço de trabalho;campo;
solution: Experience Platform
title: Definir campos XDM na interface do
description: Saiba como definir campos XDM na interface do usuário do Experience Platform.
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 1%

---

# Definir campos XDM na interface do

O [!DNL Schema Editor] na interface do usuário do Adobe Experience Platform permite definir seus próprios campos nas classes personalizadas do Experience Data Model (XDM) e nos grupos de campos de esquema. Este guia aborda as etapas para definir campos XDM na interface do usuário, incluindo as opções de configuração disponíveis para cada tipo de campo.

## Pré-requisitos

Este guia requer uma compreensão funcional do Sistema XDM. Consulte a [Visão geral do XDM](../../home.md) para obter uma introdução à função do XDM no ecossistema do Experience Platform e as [noções básicas da composição de esquemas](../../schema/composition.md) para saber como classes e grupos de campos contribuem com campos para esquemas XDM.

Embora não seja necessário para este guia, é recomendável que você também siga o tutorial sobre [composição de um esquema na interface](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do [!DNL Schema Editor].

## Selecionar um recurso ao qual adicionar campos {#select-resource}

Para definir novos campos XDM na interface do usuário, primeiro abra um esquema no [!DNL Schema Editor]. Dependendo dos esquemas que estão atualmente disponíveis para você no [!DNL Schema Library], você pode optar por [criar um novo esquema](../resources/schemas.md#create) ou [selecionar um esquema existente para editar](../resources/schemas.md#edit).

Depois que o [!DNL Schema Editor] estiver aberto, os controles para adicionar campos aparecerão na tela. Esses controles aparecem ao lado do nome do esquema, bem como quaisquer campos do tipo objeto que tenham sido definidos na classe ou no grupo de campos selecionado.

![O Editor de Esquemas com os ícones de adição realçados.](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>Se você tentar adicionar um campo a um objeto fornecido por um grupo de campos padrão, esse grupo de campos será convertido em um grupo de campos personalizado e o grupo de campos original não estará mais disponível. Consulte a seção sobre [adição de campos a grupos de campos padrão](../resources/schemas.md#custom-fields-for-standard-groups) no guia de interface do usuário de esquemas para obter mais informações.

Para adicionar um novo campo ao recurso, selecione o ícone de **adição (+)** ao lado do nome do esquema na tela ou ao lado do campo do tipo de objeto no qual você deseja definir o campo.

![O Editor de Esquemas com um ícone de adição está realçado.](../../images/ui/fields/overview/plus-icon.png)

Dependendo de você estar adicionando um campo diretamente a um esquema ou a sua classe constituinte e grupos de campos, as etapas necessárias para adicionar o campo variam. O restante deste documento se concentra em como configurar as propriedades de um campo, independentemente de onde esse campo aparece no esquema. Para obter mais informações sobre as diferentes maneiras de adicionar campos a um esquema, consulte as seguintes seções no guia da interface do usuário de schemas:

* [Adicionar campos a grupos de campos](../resources/schemas.md#add-fields)
* [Adicionar campos diretamente a um esquema](../resources/schemas.md#add-individual-fields)

## Definir as propriedades de um campo {#define}

Depois de selecionar o ícone **de adição (+)**, um espaço reservado para **[!UICONTROL Campo sem título]** aparece na tela.

![O Editor de Esquemas com um novo campo sem título realçado.](../../images/ui/fields/overview/new-field.png)

No painel direito, em **[!UICONTROL Propriedades do campo]**, você pode configurar os detalhes do novo campo. As seguintes informações são necessárias para cada campo:

| Propriedade do campo | Descrição |
| --- | --- |
| [!UICONTROL Nome do campo] | Um nome descritivo exclusivo para o campo. Observe que o nome do campo não pode ser alterado depois que o esquema é salvo. Este valor é usado para identificar e fazer referência ao campo no código e em outros aplicativos downstream<br><br>Idealmente, o nome deve ser escrito em camelCase. Ela pode conter caracteres alfanuméricos ou sublinhados, mas **não** pode começar com um sublinhado.<ul><li>**Correto**: `fieldName`</li><li>**Aceitável:** `field_name2`, `fieldName_3`</li><li>**Incorreto**: `_fieldName`</li></ul> |
| [!UICONTROL Nome de exibição] | Um nome de exibição para o campo. Este é o nome que será usado para representar o campo dentro da tela Editor de esquemas. O nome do campo pode ser alterado para o nome de exibição usando a [alternância de nome de exibição](../resources/schemas.md#display-name-toggle). |
| [!UICONTROL Tipo] | O tipo de dados que o campo conterá. Nesse menu suspenso, você pode selecionar um dos [tipos escalares padrão](../../schema/field-constraints.md) com suporte do XDM, ou um dos [tipos de dados](../resources/data-types.md) de vários campos que foram definidos anteriormente no [!DNL Schema Registry].<br>Observação: se você selecionar o tipo de dados do mapa, a propriedade [!UICONTROL Tipo de valor do mapa] será exibida.<br><br>Você também pode selecionar **[!UICONTROL Pesquisa avançada de tipos]** para pesquisar e filtrar tipos de dados existentes e localizar o tipo desejado com mais facilidade. |
| [!UICONTROL Tipo de valor do mapa] | Este valor será necessário se você selecionar [!UICONTROL Mapa] como o tipo de dados do campo. Os valores disponíveis para o mapa são [!UICONTROL String] e [!UICONTROL Integer]. Selecione um valor na lista suspensa de opções disponíveis.<br>Para saber mais sobre [propriedades de campo específicas de tipo](#type-specific-properties), consulte a visão geral de definição de campos. |

{style="table-layout:auto"}

Você também pode optar por fornecer uma descrição e notas para cada campo. Use o campo **[!UICONTROL Descrição]** para adicionar contexto e descrever a funcionalidade do tipo de dados do mapa. Isso contribui para a manutenção e a legibilidade da implementação. Você também pode adicionar observações para complementar a descrição inicial. Isso deve oferecer informações mais granulares e específicas para ajudar os desenvolvedores a entender, manter e utilizar o mapa de maneira eficaz no contexto da base de código. |


>[!NOTE]
>
>Dependendo do **[!UICONTROL Tipo]** selecionado para o campo, controles de configuração adicionais podem aparecer no painel direito. Consulte a seção sobre [propriedades do campo específico do tipo](#type-specific-properties) para obter mais informações sobre esses controles.
>
>O painel direito também fornece caixas de seleção para designar tipos de campo especiais. Consulte a seção sobre [tipos de campos especiais](#special) para obter mais informações.

Após concluir a configuração do campo, selecione **[!UICONTROL Aplicar]**.

![A seção [!UICONTROL Propriedades do campo] do Editor de Esquemas está realçada.](../../images/ui/fields/overview/field-details.png)

A tela é atualizada para mostrar o campo recém-adicionado, localizado em um objeto com namespace para sua ID de locatário exclusiva (mostrado como `_tenantId` no exemplo abaixo). Todos os campos personalizados adicionados a um esquema são automaticamente colocados dentro desse namespace para evitar conflitos com outros campos de classes e grupos de campos fornecidos pela Adobe. O painel direito agora lista o caminho do campo, além de suas outras propriedades.

![Um novo campo no diagrama de esquema e seu caminho correspondente na seção [!UICONTROL Propriedades do campo] estão realçados.](../../images/ui/fields/overview/field-added.png)

Você pode continuar seguindo as etapas acima para adicionar mais campos ao esquema. Depois que o esquema for salvo, sua classe base e grupos de campos também serão salvos se alguma alteração tiver sido feita neles.

>[!NOTE]
>
>Quaisquer alterações feitas aos grupos de campos ou à classe de um esquema serão refletidas em todos os outros esquemas que as empregam.

## Propriedades de campo específico do tipo {#type-specific-properties}

Ao definir um novo campo, opções de configuração adicionais podem aparecer no painel direito, dependendo do **[!UICONTROL Tipo]** escolhido para o campo. A tabela a seguir descreve essas propriedades de campo adicionais, juntamente com seus tipos compatíveis:

| Propriedade do campo | Tipos compatíveis | Descrição |
| --- | --- | --- |
| [!UICONTROL Tipo de valor do mapa] | [!UICONTROL Mapa] | A propriedade [!UICONTROL Tipo de valor do mapa] só aparecerá na interface do usuário se você selecionar o Valor do mapa nas opções suspensas [!UICONTROL Tipo]. Você pode selecionar entre os tipos de valor String e Integer para o Mapa.<br>![O Editor de esquemas com os campos de tipo de valor Tipo e Mapa realçados.](../../images/ui/fields/overview/map-type.png "O Editor de esquemas com os campos de tipo de valor Tipo e Mapa realçados."){width="100" zoomable="yes"}<br>Observação: todos os tipos de dados de mapa criados por meio da API que não são do tipo Cadeia de Caracteres ou Integer são exibidos como um tipo de dados &#39;[!UICONTROL Complexo]&#39;. Você não pode criar tipos de dados &#39;[!UICONTROL Complexos]&#39; por meio da interface do usuário. |
| [!UICONTROL Padrão] | [!UICONTROL String] | Uma [expressão regular](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) que o valor deste campo deve estar em conformidade para ser aceita durante a assimilação. |
| [!UICONTROL Formato] | [!UICONTROL String] | Selecione em uma lista de formatos predefinidos para cadeias de caracteres às quais o valor deve estar em conformidade. Os formatos disponíveis são: <ul><li>[[!UICONTROL data-hora]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL nome do host]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL modelo-url]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL ponteiro-json]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Comprimento mínimo] | [!UICONTROL String] | O número mínimo de caracteres que a cadeia de caracteres deve conter para que o valor seja aceito durante a assimilação. |
| [!UICONTROL Tamanho máximo] | [!UICONTROL String] | O número máximo de caracteres que a cadeia de caracteres deve conter para que o valor seja aceito durante a assimilação. |
| [!UICONTROL Valor mínimo] | [!UICONTROL Duplo] | O valor mínimo para o Duplo a ser aceito durante a assimilação. Se o valor assimilado corresponder exatamente ao inserido aqui, o valor será aceito. Ao usar esta restrição, a restrição &quot;[!UICONTROL Valor mínimo exclusivo]&quot; deve ser deixada em branco. |
| [!UICONTROL Valor máximo] | [!UICONTROL Duplo] | O valor máximo para o Duplo a ser aceito durante a assimilação. Se o valor assimilado corresponder exatamente ao inserido aqui, o valor será aceito. Ao usar esta restrição, a restrição &quot;[!UICONTROL Valor máximo exclusivo]&quot; deve ser deixada em branco. |
| [!UICONTROL Valor mínimo exclusivo] | [!UICONTROL Duplo] | O valor máximo para o Duplo a ser aceito durante a assimilação. Se o valor assimilado corresponder exatamente ao inserido aqui, o valor será rejeitado. Ao usar esta restrição, a restrição (não exclusiva) &quot;[!UICONTROL Valor mínimo]&quot; deve ser deixada em branco. |
| [!UICONTROL Valor máximo exclusivo] | [!UICONTROL Duplo] | O valor máximo para o Duplo a ser aceito durante a assimilação. Se o valor assimilado corresponder exatamente ao inserido aqui, o valor será rejeitado. Ao usar esta restrição, a restrição (não exclusiva) &quot;[!UICONTROL Valor máximo]&quot; deve ser deixada em branco. |

{style="table-layout:auto"}

## Tipos de campo especial {#special}

O painel direito fornece várias caixas de seleção para designar funções especiais para o campo selecionado. Os casos de uso de algumas dessas opções envolvem considerações importantes sobre sua estratégia de modelagem de dados e como você pretende usar os serviços downstream do Experience Platform.

Para saber mais sobre esses tipos especiais, consulte a seguinte documentação:

* [Mapa](./map.md)
* [[!UICONTROL Obrigatório]](./required.md)
* [Matriz [!UICONTROL 1}]](./array.md)
* [[!UICONTROL Enumeração]](./enum.md)
* [[!UICONTROL Identidade]](./identity.md) (Disponível somente para campos de cadeia de caracteres)
* [[!UICONTROL Relacionamento]](./relationship.md) (Disponível somente para campos de sequência de caracteres)

Embora tecnicamente não seja um tipo de campo especial, também é recomendável que você visite o guia em [definindo campos de tipo de objeto](./object.md) para saber mais sobre como definir subcampos aninhados se suas estruturas de esquema.

## Próximas etapas

Este guia forneceu uma visão geral sobre como definir campos XDM na interface do usuário. Lembre-se de que os campos só podem ser adicionados a esquemas por meio do uso de classes e grupos de campos. Para saber mais sobre como gerenciar esses recursos na interface, consulte os guias sobre criação e edição de [classes](../resources/classes.md) e [grupos de campos](../resources/field-groups.md).

Para obter mais informações sobre os recursos do espaço de trabalho [!UICONTROL Esquemas], consulte a [[!UICONTROL visão geral do espaço de trabalho de ]](../overview.md).
