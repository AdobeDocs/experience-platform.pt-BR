---
keywords: Experience Platform;home;popular topics;api;API;XDM;sistema XDM;experimentar modelo de dados;modelo de dados;ui;espaço de trabalho;campo;
solution: Experience Platform
title: Definir campos XDM na interface do usuário
description: Saiba como definir campos XDM na interface do usuário do Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: a489ab248793a063295578943ad600d8eacab6a2
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 4%

---


# Definir campos XDM na interface do usuário

O [!DNL Schema Editor] na interface do usuário do Adobe Experience Platform permite que você defina seus próprios campos nas classes e combinações personalizadas do Experience Data Model (XDM). Este guia aborda as etapas para definir campos XDM na interface do usuário, incluindo as opções de configuração disponíveis para cada tipo de campo.

## Pré-requisitos

Este guia requer um entendimento prático do sistema XDM. Consulte a [visão geral do XDM](../../home.md) para obter uma introdução à função do XDM dentro do ecossistema do Experience Platform, e as [noções básicas da composição do schema](../../schema/composition.md) para saber como as classes e as combinações contribuem com os campos para os schemas XDM.

Embora não seja necessário para este guia, é recomendável que você também siga o tutorial sobre [compondo um schema na interface do usuário](../../tutorials/create-schema-ui.md) para se familiarizar com os vários recursos do [!DNL Schema Editor].

## Selecione um recurso para adicionar campos a {#select-resource}

Para definir novos campos XDM na interface do usuário, primeiro abra um schema dentro de [!DNL Schema Editor]. Dependendo de quais schemas estão disponíveis atualmente em [!DNL Schema Library], você pode optar por [criar um novo schema](../resources/schemas.md#create) ou [selecionar um schema existente para editar](../resources/schemas.md#edit).

Depois que você tiver [!DNL Schema Editor] aberto, use o painel esquerdo para selecionar a classe ou combinação para a qual deseja definir os campos. Se o recurso for um recurso personalizado definido pela organização, os controles para adicionar ou editar campos serão exibidos na tela. Esses controles são exibidos ao lado do nome do schema, bem como de qualquer campo de tipo de objeto que tenha sido definido na classe ou combinação selecionada.

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>Se a classe ou combinação selecionada for um recurso principal fornecido pelo Adobe, não poderá ser editado e, portanto, os controles mostrados acima não aparecerão. Se o schema ao qual você deseja adicionar campos for baseado em uma classe XDM principal e não contiver misturas personalizadas, você poderá [criar uma nova combinação](../resources/mixins.md#create) para adicionar ao schema.

Para adicionar um novo campo ao recurso, selecione o ícone **mais (+)** ao lado do nome do schema na tela ou ao lado do campo do tipo de objeto no qual você deseja definir o campo.

![](../../images/ui/fields/overview/plus-icon.png)

## Definir um campo para um recurso {#define}

Depois de selecionar o ícone **mais (+)**, um **[!UICONTROL Novo campo]** aparece na tela, localizada dentro de um objeto de nível raiz que é nomeado para sua ID de locatário exclusiva (mostrado como `_tenantId` no exemplo abaixo). Todos os campos adicionados a um schema por meio de classes e mixagens personalizadas são automaticamente colocados dentro dessa namespace para evitar conflitos com outros campos a partir de classes e mixagens fornecidas por Adobe.

![](../../images/ui/fields/overview/new-field.png)

No painel direito em **[!UICONTROL Propriedades de campo]**, é possível configurar os detalhes dos novos campos. As seguintes informações são obrigatórias para cada campo:

| Propriedade de campo | Descrição |
| --- | --- |
| [!UICONTROL Nome do campo] | Um nome exclusivo e descritivo para o campo. Observe que o nome do campo não pode ser alterado depois que o schema é salvo.<br><br>O nome deveria ser escrito em camelCase. Ele pode conter caracteres alfanuméricos, traço ou sublinhado, mas **pode não** start com um sublinhado.<ul><li>**Correto**:  `fieldName`</li><li>**Aceitável:** `field_name2`,  `Field-Name`,  `field-name_3`</li><li>**Incorreto**:  `_fieldName`</li></ul> |
| [!UICONTROL Nome de exibição] | Um nome amigável para o campo. |
| [!UICONTROL Tipo] | O tipo de dados que o campo conterá. Neste menu suspenso, você pode selecionar um dos [tipos escalares padrão](../../schema/field-constraints.md) suportados pelo XDM, ou um dos [tipos de dados](../resources/data-types.md) de vários campos que foram previamente definidos em [!DNL Schema Registry].<br><br>Você também pode selecionar  **[!UICONTROL Avançado tipo]** pesquisar para pesquisar e filtrar os tipos de dados existentes e localizar o tipo desejado mais facilmente. |

Você também pode fornecer um **[!UICONTROL Descrição]** opcional legível por humanos ao campo para fornecer mais contexto sobre o caso de uso pretendido do campo.

>[!NOTE]
>
>Dependendo do **[!UICONTROL Tipo]** selecionado para o campo, controles de configuração adicionais podem aparecer no painel direito. Consulte a seção sobre [propriedades de campos específicos ao tipo](#type-specific-properties) para obter mais informações sobre esses controles.
>
>O painel direito também fornece caixas de seleção para designar tipos de campos especiais. Consulte a seção sobre [tipos de campos especiais](#special) para obter mais informações.

Depois de concluir a configuração do campo, selecione **[!UICONTROL Aplicar]**.

![](../../images/ui/fields/overview/field-details.png)

A tela é atualizada para mostrar o nome e o tipo do campo, e o painel direito agora lista o caminho do campo, além de suas outras propriedades.

![](../../images/ui/fields/overview/field-added.png)

Você pode continuar seguindo as etapas acima para adicionar mais campos ao schema. Depois que o schema é salvo, sua classe base e suas combinações também são salvas se alguma alteração tiver sido feita.

>[!NOTE]
>
>Quaisquer alterações feitas nas combinações ou na classe de um schema serão refletidas em todos os outros schemas que os empregam.

## Propriedades de campos específicos do tipo {#type-specific-properties}

Ao definir um novo campo, opções de configuração adicionais podem aparecer no painel direito, dependendo do **[!UICONTROL Tipo]** escolhido para o campo. A tabela a seguir descreve essas propriedades de campos adicionais juntamente com seus tipos compatíveis:

| Propriedade de campo | Tipos compatíveis | Descrição |
| --- | --- | --- |
| [!UICONTROL Valor padrão] | [!UICONTROL String],  [!UICONTROL Duplo],  [!UICONTROL Longo],  [!UICONTROL Inteiro],  [!UICONTROL Curto],    [!UICONTROL Byte, Booleano] | Um valor padrão que será atribuído a esse campo se nenhum outro valor for fornecido durante a ingestão. Esse valor deve estar em conformidade com o tipo selecionado do campo. |
| [!UICONTROL Padrão] | [!UICONTROL String] | Uma [expressão regular](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) que o valor deste campo deve estar em conformidade para ser aceite durante a ingestão. |
| [!UICONTROL Formato] | [!UICONTROL String] | Selecione de uma lista de formatos predefinidos para strings que o valor deve estar em conformidade. Os formatos disponíveis incluem: <ul><li>[[!UICONTROL data e hora]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL nome do host]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL referência uri]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL ponteiro json]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Comprimento mínimo] | [!UICONTROL String] | O número mínimo de caracteres que a string deve conter para que o valor seja aceito durante a ingestão. |
| [!UICONTROL Tamanho máximo] | [!UICONTROL String] | O número máximo de caracteres que a string deve conter para que o valor seja aceito durante a ingestão. |
| [!UICONTROL Valor mínimo] | [!UICONTROL Duplo] | Valor mínimo para o Duplo a aceitar durante a ingestão. Se o valor ingerido corresponder exatamente ao valor inserido aqui, então o valor será aceito. Ao usar essa restrição, a restrição &quot;[!UICONTROL Valor mínimo exclusivo]&quot; deve ser deixada em branco. |
| [!UICONTROL Valor máximo] | [!UICONTROL Duplo] | O valor máximo para o Duplo a aceitar durante a ingestão. Se o valor ingerido corresponder exatamente ao valor inserido aqui, então o valor será aceito. Ao usar essa restrição, a restrição &quot;[!UICONTROL Valor máximo exclusivo]&quot; deve ser deixada em branco. |
| [!UICONTROL Valor mínimo exclusivo] | [!UICONTROL Duplo] | O valor máximo para o Duplo a aceitar durante a ingestão. Se o valor ingerido corresponder exatamente ao valor inserido aqui, o valor será rejeitado. Ao usar essa restrição, a restrição &quot;[!UICONTROL Valor mínimo]&quot; (não exclusiva) deve ser deixada em branco. |
| [!UICONTROL Valor máximo exclusivo] | [!UICONTROL Duplo] | O valor máximo para o Duplo a aceitar durante a ingestão. Se o valor ingerido corresponder exatamente ao valor inserido aqui, o valor será rejeitado. Ao usar essa restrição, a restrição &quot;[!UICONTROL Valor máximo]&quot; (não exclusiva) deve ser deixada em branco. |

## Tipos de campos especiais {#special}

O painel direito fornece várias caixas de seleção para designar funções especiais para o campo selecionado. Os casos de uso para algumas dessas opções envolvem considerações importantes sobre sua estratégia de modelagem de dados e como você pretende usar os serviços de plataforma downstream.

Para saber mais sobre esses tipos especiais, consulte a seguinte documentação:

* [[!UICONTROL Obrigatório]](./required.md)
* [[!UICONTROL Matriz]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identidade]](./identity.md)  (Disponível somente para campos de string)
* [[!UICONTROL Relacionamento]](./relationship.md) (Disponível somente para campos de string)

Embora tecnicamente não seja um tipo de campo especial, também é recomendável visitar o guia em [definindo campos do tipo de objeto](./object.md) para saber mais sobre como definir subcampos aninhados se suas estruturas de schema.

## Próximas etapas

Este guia fornece uma visão geral de como definir campos XDM na interface do usuário. Lembre-se de que os campos só podem ser adicionados aos schemas por meio do uso de classes e misturas. Para saber mais sobre como gerenciar esses recursos na interface do usuário, consulte os guias sobre como criar e editar [classes](../resources/classes.md) e [mixins](../resources/mixins.md).

Para obter mais informações sobre os recursos do espaço de trabalho [!UICONTROL Schemas], consulte a [[!UICONTROL visão geral do espaço de trabalho dos Schemas]](../overview.md).