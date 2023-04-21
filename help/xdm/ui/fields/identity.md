---
keywords: Experience Platform; home; tópicos populares; api; API; XDM; sistema XDM; modelo de dados de experiência; modelo de dados; ui; espaço de trabalho; identidade; campo;
solution: Experience Platform
title: Definir campos de identidade na interface do usuário
description: Saiba como definir um campo de identidade na interface do usuário do Experience Platform.
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: 857c1d4f74b6352e90f9c97ef22d686a883e3563
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 5%

---

# Definir campos de identidade na interface do usuário

No Experience Data Model (XDM), um campo de identidade representa um campo que pode ser usado para identificar uma pessoa individual relacionada a um registro ou evento de série de tempo. Este documento aborda como definir um campo de identidade na interface do usuário do Adobe Experience Platform.

## Pré-requisitos

Os campos de identidade são um componente essencial na forma como os gráficos de identidade do cliente são construídos na plataforma, o que afeta o modo como o Perfil do cliente em tempo real mescla fragmentos de dados diferentes para obter uma visualização completa do cliente. Antes de definir campos de identidade em seus esquemas, consulte a seguinte documentação para saber mais sobre os principais serviços e conceitos relacionados aos campos de identidade:

* [Serviço de identidade da Adobe Experience Platform](../../../identity-service/home.md): Corresponde identidades entre dispositivos e sistemas, vinculando conjuntos de dados com base nos campos de identidade definidos pelos esquemas XDM aos quais eles estão em conformidade.
   * [Namespaces de identidade](../../../identity-service/namespaces.md): Os namespaces de identidade definem os diferentes tipos de informações de identidade que podem estar relacionadas a uma única pessoa e são um componente obrigatório para cada campo de identidade.
* [Perfil do cliente em tempo real](../../../profile/home.md): Aproveita os gráficos de identidade do cliente para fornecer um perfil unificado do consumidor com base em dados agregados de várias fontes, atualizados em tempo quase real.

## Definir um campo de identidade {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="Restrições à identidade principal"
>abstract="Esse esquema usa um grupo de campos destinado ao uso em uma conexão de origem específica. A conexão requer que o identityMap seja usado como identidade principal e o define automaticamente."

When [definição de um novo campo](./overview.md#define) na interface do usuário, você pode defini-la como um campo de identidade selecionando o **[!UICONTROL Identidade]** caixa de seleção no painel direito.

![](../../images/ui/fields/special/identity.png)

Controles adicionais são exibidos após marcar a caixa de seleção. Se quiser que esse campo seja a identidade primária do schema, selecione a variável **[!UICONTROL Identidade primária]** caixa de seleção.

>[!NOTE]
>
>Um único schema pode ter muitos campos de identidade definidos, mas só pode ter uma identidade primária. Todos os campos de identidade (primários ou não) contribuem para o gráfico de identidade de um cliente individual, mas o Perfil do cliente em tempo real usa apenas a identidade primária como fonte de verdade ao mesclar fragmentos de dados. Se quiser ativar um schema para uso no Perfil, o schema deve ter uma identidade primária definida.

Em **[!UICONTROL Namespace de identidade]**, use o menu suspenso para selecionar o namespace apropriado para o campo de identidade. Os namespaces padrão fornecidos pelo Adobe são listados, juntamente com qualquer namespace personalizado definido pela organização.

Quando terminar, selecione **[!UICONTROL Aplicar]** para aplicar a alteração ao schema.

![](../../images/ui/fields/special/identity-config.png)

A tela é atualizada para refletir as alterações, com o campo selecionado ganhando um símbolo de impressão digital (![](../../images/ui/fields/special/identity-symbol.png)) para designá-la como uma identidade. No painel à esquerda, o campo de identidade agora é listado sob o nome da classe ou do grupo de campos do esquema que fornece o campo para o esquema.

Se o campo também tiver sido definido como a identidade primária, ele também será listado em **[!UICONTROL Campos obrigatórios]** no painel esquerdo. Se o campo de identidade estiver aninhado dentro da estrutura do schema, todos os campos pai também serão listados conforme necessário.

![](../../images/ui/fields/special/identity-applied.png)

Se você definiu uma identidade primária para o schema, agora poderá prosseguir para [ativar o schema para uso no Perfil do cliente em tempo real](../resources/schemas.md#profile).

## Próximas etapas

Este guia abordou como definir um campo de identidade na interface do usuário do . À medida que os dados são assimilados usando esse esquema, os gráficos de identidade do cliente serão atualizados para refletir os campos de identidade do esquema. Consulte o guia sobre [visualizador de gráficos de identidade](../../../identity-service/ui/identity-graph-viewer.md) para saber como explorar o gráfico privado de sua organização na interface do usuário do .

Consulte a visão geral em [definição de campos na interface do usuário](./overview.md#special) para saber como definir outros tipos de campo XDM na variável [!DNL Schema Editor].
