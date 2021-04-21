---
keywords: Experience Platform; home; tópicos populares; api; API; XDM; sistema XDM; modelo de dados de experiência; modelo de dados; ui; espaço de trabalho; campo;
solution: Experience Platform
title: Definir campos XDM na interface do usuário
description: Saiba como definir campos XDM na interface do usuário do Experience Platform.
topic-legacy: user guide
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 3%

---

# Definir campos XDM na interface do usuário

O [!DNL Schema Editor] na interface do usuário do Adobe Experience Platform permite definir seus próprios campos nas classes e combinações personalizadas do Experience Data Model (XDM). Este guia aborda as etapas para definir campos XDM na interface do usuário, incluindo as opções de configuração disponíveis para cada tipo de campo.

## Pré-requisitos

Este guia requer uma compreensão funcional do Sistema XDM. Consulte a [Visão geral do XDM](../../home.md) para obter uma introdução à função do XDM no ecossistema do Experience Platform e as [noções básicas da composição do schema](../../schema/composition.md) para saber como classes e mixins contribuem com campos para esquemas XDM.

Embora não seja necessário para este guia, é recomendável seguir também o tutorial em [composição de um schema na interface do usuário](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do [!DNL Schema Editor].

## Selecione um recurso para adicionar campos a {#select-resource}

Para definir novos campos XDM na interface do usuário, primeiro você deve abrir um schema dentro do [!DNL Schema Editor]. Dependendo de quais schemas estão disponíveis no momento no [!DNL Schema Library], você pode optar por [criar um novo schema](../resources/schemas.md#create) ou [selecionar um schema existente para editar](../resources/schemas.md#edit).

Depois de abrir o [!DNL Schema Editor], use o painel esquerdo para selecionar a classe ou mixin para a qual deseja definir os campos. Se o recurso for um recurso personalizado definido pela organização, os controles para adicionar ou editar campos serão exibidos na tela. Esses controles são exibidos ao lado do nome do schema, bem como qualquer campo do tipo de objeto que foi definido na classe ou mixin selecionado.

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>Se a classe ou mixin selecionado for um recurso principal fornecido pelo Adobe, ele não poderá ser editado e, portanto, os controles mostrados acima não aparecerão. Se o esquema ao qual você deseja adicionar campos for baseado em uma classe XDM principal e não contiver mixins personalizados, você poderá [criar um novo mixin](../resources/mixins.md#create) para adicionar ao esquema.

Para adicionar um novo campo ao recurso, selecione o ícone de **mais (+)** ao lado do nome do schema na tela ou ao lado do campo do tipo de objeto no qual você deseja definir o campo.

![](../../images/ui/fields/overview/plus-icon.png)

## Definir um campo para um recurso {#define}

Depois de selecionar o ícone de **mais (+)**, um **[!UICONTROL New field]** aparece na tela, localizada em um objeto de nível raiz que é namespacado para sua ID de locatário exclusiva (mostrado como `_tenantId` no exemplo abaixo). Todos os campos adicionados a um schema por meio de classes e mixins personalizados são colocados automaticamente nesse namespace para evitar conflitos com outros campos a partir de classes e mixins fornecidos pelo Adobe.

![](../../images/ui/fields/overview/new-field.png)

No painel direito em **[!UICONTROL Field properties]**, é possível configurar os detalhes dos novos campos. As seguintes informações são necessárias para cada campo:

| Propriedade do campo | Descrição |
| --- | --- |
| [!UICONTROL Field name] | Um nome descritivo e exclusivo para o campo. Observe que o nome do campo não pode ser alterado depois que o esquema é salvo.<br><br>O nome deve ser escrito em camelCase. Ele pode conter caracteres alfanuméricos, traço ou sublinhados, mas **pode não** começar com um sublinhado.<ul><li>**Correto**:  `fieldName`</li><li>**Aceitável:** `field_name2`,  `Field-Name`,  `field-name_3`</li><li>**Incorreto**:  `_fieldName`</li></ul> |
| [!UICONTROL Display name] | Um nome amigável para o campo. |
| [!UICONTROL Type] | O tipo de dados que o campo conterá. Nesse menu suspenso, é possível selecionar um dos [tipos escalares padrão](../../schema/field-constraints.md) suportados pelo XDM ou um dos [tipos de dados](../resources/data-types.md) de vários campos que foram definidos anteriormente no [!DNL Schema Registry].<br><br>Você também pode selecionar  **[!UICONTROL Advanced type search]** para pesquisar e filtrar os tipos de dados existentes e localizar o tipo desejado mais facilmente. |

Você também pode fornecer um **[!UICONTROL Description]** opcional legível para o campo para fornecer mais contexto sobre o caso de uso pretendido do campo.

>[!NOTE]
>
>Dependendo do **[!UICONTROL Type]** selecionado para o campo, controles de configuração adicionais podem aparecer no painel direito. Consulte a seção sobre [propriedades de campo específicas do tipo](#type-specific-properties) para obter mais informações sobre esses controles.
>
>O painel direito também fornece caixas de seleção para designar tipos de campos especiais. Consulte a seção sobre [tipos de campo especiais](#special) para obter mais informações.

Depois de concluir a configuração do campo, selecione **[!UICONTROL Apply]**.

![](../../images/ui/fields/overview/field-details.png)

A tela é atualizada para mostrar o nome e o tipo do campo, e o painel direito agora lista o caminho do campo, além de suas outras propriedades.

![](../../images/ui/fields/overview/field-added.png)

Você pode continuar a seguir as etapas acima para adicionar mais campos ao schema. Depois que o schema é salvo, sua classe base e as combinações também são salvas se alguma alteração for feita a elas.

>[!NOTE]
>
>Quaisquer alterações feitas nas combinações ou na classe de um schema serão refletidas em todos os outros esquemas que as utilizam.

## Propriedades de campos específicos do tipo {#type-specific-properties}

Ao definir um novo campo, opções de configuração adicionais podem aparecer no painel direito, dependendo do **[!UICONTROL Type]** que você escolher para o campo . A tabela a seguir descreve essas propriedades de campos adicionais, juntamente com seus tipos compatíveis:

| Propriedade do campo | Tipos compatíveis | Descrição |
| --- | --- | --- |
| [!UICONTROL Default value] | [!UICONTROL String], [!UICONTROL Double], [!UICONTROL Long], [!UICONTROL Integer], [!UICONTROL Short], [!UICONTROL Byte], [!UICONTROL Boolean] | Um valor padrão que será atribuído a esse campo se nenhum outro valor for fornecido durante a assimilação. Esse valor deve estar em conformidade com o tipo selecionado do campo. |
| [!UICONTROL Pattern] | [!UICONTROL String] | Uma [expressão regular](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) que o valor desse campo deve estar em conformidade para ser aceita durante a assimilação. |
| [!UICONTROL Format] | [!UICONTROL String] | Selecione de uma lista de formatos predefinidos para cadeias de caracteres que o valor deve estar em conformidade. Os formatos disponíveis incluem: <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Minimum length] | [!UICONTROL String] | O número mínimo de caracteres que a cadeia de caracteres deve conter para que o valor seja aceito durante a assimilação. |
| [!UICONTROL Maximum length] | [!UICONTROL String] | O número máximo de caracteres que a cadeia de caracteres deve conter para que o valor seja aceito durante a assimilação. |
| [!UICONTROL Minimum value] | [!UICONTROL Double] | O valor mínimo para Double a ser aceito durante a ingestão. Se o valor assimilado corresponder exatamente ao inserido aqui, o valor será aceito. Ao usar essa restrição, a restrição &quot;[!UICONTROL Exclusive minimum value]&quot; deve ser deixada em branco. |
| [!UICONTROL Maximum value] | [!UICONTROL Double] | O valor máximo para Double a ser aceito durante a ingestão. Se o valor assimilado corresponder exatamente ao inserido aqui, o valor será aceito. Ao usar essa restrição, a restrição &quot;[!UICONTROL Exclusive maximum value]&quot; deve ser deixada em branco. |
| [!UICONTROL Exclusive minimum value] | [!UICONTROL Double] | O valor máximo para Double a ser aceito durante a ingestão. Se o valor assimilado corresponder exatamente ao inserido aqui, o valor será rejeitado. Ao usar essa restrição, a restrição &quot;[!UICONTROL Minimum value]&quot; (não exclusiva) deve ser deixada em branco. |
| [!UICONTROL Exclusive maximum value] | [!UICONTROL Double] | O valor máximo para Double a ser aceito durante a ingestão. Se o valor assimilado corresponder exatamente ao inserido aqui, o valor será rejeitado. Ao usar essa restrição, a restrição &quot;[!UICONTROL Maximum value]&quot; (não exclusiva) deve ser deixada em branco. |

## Tipos de campo especiais {#special}

O painel direito fornece várias caixas de seleção para designar funções especiais para o campo selecionado. Os casos de uso para algumas dessas opções envolvem considerações importantes sobre sua estratégia de modelagem de dados e como você pretende usar os serviços downstream da plataforma.

Para saber mais sobre esses tipos especiais, consulte a seguinte documentação:

* [[!UICONTROL Required]](./required.md)
* [[!UICONTROL Array]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identity]](./identity.md) (Disponível somente para campos de string)
* [[!UICONTROL Relationship]](./relationship.md) (Disponível somente para campos de string)

Embora tecnicamente não seja um tipo de campo especial, também é recomendável visitar o guia em [definindo campos do tipo de objeto](./object.md) para saber mais sobre como definir subcampos aninhados se suas estruturas de esquema.

## Próximas etapas

Este guia forneceu uma visão geral de como definir campos XDM na interface do usuário. Lembre-se de que os campos só podem ser adicionados a schemas por meio de classes e mixins. Para saber mais sobre como gerenciar esses recursos na interface do usuário, consulte os guias sobre como criar e editar [classes](../resources/classes.md) e [mixins](../resources/mixins.md).

Para obter mais informações sobre os recursos do espaço de trabalho [!UICONTROL Schemas], consulte a [[!UICONTROL Schemas] visão geral do espaço de trabalho](../overview.md).
