---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definir uma relação entre dois schemas usando o Editor de Schemas de Schemas
topic: tutorials
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# Definir uma relação entre dois schemas usando o Editor de Schemas

A capacidade de entender os relacionamentos entre seus clientes e suas interações com a sua marca em vários canais é uma parte importante do Adobe Experience Platform. A definição desses relacionamentos na estrutura dos schemas do Modelo de Dados de Experiência (XDM) permite que você obtenha insights complexos sobre os dados do cliente.

Este documento fornece um tutorial para definir uma relação um para um entre dois schemas definidos pela sua organização usando o Editor de Schemas na interface do usuário do Experience Platform. Para obter etapas sobre como definir relações de schema usando a API, consulte o tutorial sobre como [definir uma relação usando a API](relationship-api.md)de Registro de Schemas.

## Introdução

Este tutorial requer uma compreensão funcional do Sistema XDM e do Editor de Schemas na interface do usuário do Experience Platform. Antes de iniciar este tutorial, reveja a seguinte documentação:

* [Sistema XDM no Experience Platform](../home.md): Uma visão geral do XDM e sua implementação no Experience Platform.
* [Noções básicas da composição](../schema/composition.md)do schema: Uma introdução dos blocos de construção dos schemas XDM.
* [Crie um schema usando o Editor](create-schema-ui.md)de Schemas: Um tutorial que aborda as noções básicas de como trabalhar com o Editor de Schemas.

## Definir um schema de origem e de destino

Espera-se que você já tenha criado os dois schemas que serão definidos no relacionamento. Para fins de demonstração, este tutorial cria uma relação entre os membros do programa de fidelidade de uma organização (definido em um schema &quot;Membros da Fidelidade&quot;) e seus hotéis favoritos (definido em um schema &quot;Hotéis&quot;).

As relações de Schema são representadas por um schema **de** origem com um campo que se refere a outro campo dentro de um schema **de** destino. Nas etapas a seguir, &quot;Membros da fidelidade&quot; será o schema de origem, enquanto &quot;Hotéis&quot; atuará como o schema de destino.

Para fins de referência, as seções a seguir descrevem a estrutura de cada schema usado neste tutorial antes que uma relação seja definida.

### schema de Membros de Fidelidade

O schema de origem &quot;Membros de fidelidade&quot; é o schema que foi construído no tutorial para [criar um schema na interface do usuário](create-schema-ui.md). Ele inclui um objeto &quot;fidelidade&quot; na namespace &quot;\_locatárioId&quot;, que inclui vários campos específicos de fidelidade. Um desses campos, &quot;loyaltyId&quot;, serve como a principal identidade para o schema sob a namespace &quot;Email&quot;. Conforme mostrado em Propriedades _do_ Schema, este schema foi habilitado para uso no Perfil [do cliente em tempo](../../profile/home.md)real.

![](../images/tutorials/relationship/loyalty-members.png)

### schema Hotéis

O schema de destino &quot;Hotéis&quot; contém campos que descrevem um hotel, incluem seu endereço, marca, número de salas e classificação de estrelas. O campo &quot;hotelId&quot; serve como a principal identidade do schema sob a namespace &quot;ECID&quot;. Ao contrário de &quot;Membros de fidelidade&quot;, este schema não foi ativado para o Perfil de clientes em tempo real.

![](../images/tutorials/relationship/hotels.png)

## Criar uma mistura de relacionamento

>[!NOTE]
>
>Essa etapa só é necessária se o schema de origem não tiver um campo do tipo string dedicado para ser usado como referência a outro schema. Se esse campo já estiver definido no schema de origem, pule para a próxima etapa da [definição de um campo](#relationship-field)de relação.

Para definir uma relação entre dois schemas, o schema de origem deve ter um campo dedicado para ser usado como referência ao schema de destino. É possível adicionar esse campo ao schema de origem criando uma nova combinação.

Start clicando em **Adicionar** na seção _Misturas_ .

![](../images/tutorials/relationship/loyalty-add-mixin.png)

A caixa de diálogo _Adicionar mistura_ é exibida. Aqui, clique em **Criar nova mistura**. Nos campos de texto exibidos, insira um nome de exibição e uma descrição para a nova combinação. Clique em **Adicionar mistura** quando terminar.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

A tela reaparece com &quot;Relacionamento de fidelidade&quot; que aparece na seção _Misturas_ . Clique no nome da combinação e, em seguida, clique em **Adicionar campo** ao lado do campo de nível raiz &quot;Membros de fidelidade&quot;.

![](../images/tutorials/relationship/loyalty-add-field.png)

Um novo campo é exibido na tela sob a namespace &quot;\_locatárioId&quot;. Em Propriedades _do_ campo, forneça um nome de campo e de exibição para o campo e defina seu tipo como &quot;String&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Quando terminar, clique em **Aplicar**.

![](../images/tutorials/relationship/relationship-field-apply.png)

O campo atualizado &quot;loyaltyRelationship&quot; aparece na tela. Clique em **Salvar** para finalizar as alterações no schema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definir um campo de relacionamento para o schema de origem {#relationship-field}

Depois que o schema de origem tiver um campo de referência dedicado definido, você poderá designá-lo como um campo de relacionamento.

Clique no campo de referência na tela e role para baixo em Propriedades _do_ campo até que a caixa de seleção **Relacionamento** seja exibida. Marque a caixa de seleção para revelar os parâmetros necessários para configurar um campo de relação.

![](../images/tutorials/relationship/relationship-checkbox.png)

Clique na lista suspensa para Schema **de** referência e selecione o schema de destino para a relação (&quot;Hotéis&quot; neste exemplo). Se o schema de destino estiver habilitado para união, o campo Namespace **de identidade de** referência será automaticamente definido para a namespace da identidade principal do schema de destino. Se o schema não tiver uma identidade primária definida, você deverá selecionar manualmente a namespace que planeja usar no menu suspenso. Click **Apply** when finished.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

O campo aparece como uma relação na tela, exibindo o nome e a namespace de identidade de referência do schema de destino. Clique em **Salvar** para salvar suas alterações e concluir o fluxo de trabalho.

![](../images/tutorials/relationship/relationship-save.png)

## Próximas etapas

Ao seguir este tutorial, você criou com êxito uma relação um para um entre dois schemas usando o Editor de Schemas. Para obter etapas sobre como definir relações usando a API, consulte o tutorial sobre como [definir uma relação usando a API](relationship-api.md)do Registro de Schemas.