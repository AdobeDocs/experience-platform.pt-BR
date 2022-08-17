---
keywords: Experience Platform; home; tópicos populares; api; API; XDM; sistema XDM; modelo de dados de experiência; modelo de dados; ui; espaço de trabalho; enum; campo;
solution: Experience Platform
title: Definir campos de enumeração na interface do usuário
description: Saiba como definir um campo enum na interface do usuário do Experience Platform.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: f6fefda974d2ae6fd4b035ef3b5fe633311c9772
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 2%

---

# Definir campos de enumeração na interface do usuário {#enum}

>[!CONTEXTUALHELP]
>id="platform_xdm_enumsuggestedvalue"
>title="Enumerações e valores sugeridos"
>abstract="Um enum restringe um campo de string para permitir somente dados que correspondem a um conjunto predefinido de valores a serem assimilados. Como alternativa, é possível definir um conjunto de valores sugeridos para o campo que não restringem a assimilação, mas, em vez disso, definir os atributos que podem ser escolhidos na segmentação. Consulte a documentação da para obter mais informações."

No Experience Data Model (XDM), um campo enum representa um campo restrito a uma lista predefinida de valores aceitáveis.

When [definição de um novo campo](./overview.md#define) na interface do usuário do Adobe Experience Platform, é possível defini-lo como um campo enum selecionando o **[!UICONTROL Enum]** caixa de seleção no painel direito.

![](../../images/ui/fields/special/enum.png)

Controles adicionais são exibidos depois de marcar a caixa de seleção, permitindo especificar as restrições de valor para o enum. Em **[!UICONTROL Valor]** , é necessário fornecer o valor exato ao qual deseja restringir o campo. Esse valor deve estar em conformidade com o [!UICONTROL Tipo] você selecionou para o campo enum . Como opção, você pode fornecer um **[!UICONTROL Rótulo]** para a restrição também.

Para adicionar restrições adicionais à enumeração, selecione **[!UICONTROL Adicionar linha]**.

![](../../images/ui/fields/special/enum-add-row.png)

Continue a adicionar as restrições desejadas e os rótulos opcionais ao enum. Quando terminar, selecione **[!UICONTROL Aplicar]** para aplicar as alterações ao schema.

![](../../images/ui/fields/special/enum-configured.png)

A tela é atualizada para refletir as alterações. Ao explorar esse schema no futuro, você poderá visualizar e editar as restrições do campo enum no painel direito.

![](../../images/ui/fields/special/enum-applied.png)

## Próximas etapas

Este guia abordou como definir um campo enum na interface do usuário do . Consulte a visão geral em [definição de campos na interface do usuário](./overview.md#special) para saber como definir outros tipos de campo XDM na variável [!DNL Schema Editor].
