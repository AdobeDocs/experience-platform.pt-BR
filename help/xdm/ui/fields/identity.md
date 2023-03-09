---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados;iu;espaço de trabalho;identidade;campo;
solution: Experience Platform
title: Definir campos de identidade na interface
description: Saiba como definir um campo de identidade na interface do usuário do Experience Platform.
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: 857c1d4f74b6352e90f9c97ef22d686a883e3563
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Definir campos de identidade na interface

No Experience Data Model (XDM), um campo de identidade representa um campo que pode ser usado para identificar uma pessoa individual relacionada a um registro ou evento de série temporal. Este documento aborda como definir um campo de identidade na interface do usuário do Adobe Experience Platform.

## Pré-requisitos

Os campos de identidade são um componente essencial em como os gráficos de identidade do cliente são construídos na Platform, o que afeta como o Perfil do cliente em tempo real mescla fragmentos de dados diferentes para obter uma visão completa do cliente. Antes de definir campos de identidade em seus esquemas, consulte a seguinte documentação para saber mais sobre os serviços principais e conceitos relacionados aos campos de identidade:

* [Serviço de identidade da Adobe Experience Platform](../../../identity-service/home.md): une as identidades em dispositivos e sistemas, vinculando conjuntos de dados com base nos campos de identidade definidos pelos esquemas XDM aos quais estão em conformidade.
   * [Namespaces de identidade](../../../identity-service/namespaces.md): os namespaces de identidade definem os diferentes tipos de informações de identidade que podem se relacionar a uma única pessoa e são um componente obrigatório para cada campo de identidade.
* [Perfil do cliente em tempo real](../../../profile/home.md): aproveita os gráficos de identidade do cliente para fornecer um perfil de consumidor unificado com base em dados agregados de várias fontes, atualizados em tempo quase real.

## Definir um campo de identidade {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="Restrições à identidade principal"
>abstract="Este esquema usa um grupo de campos destinado ao uso em uma conexão de origem específica. A conexão requer que identityMap seja usado como identidade primária e o definiu automaticamente."

Quando [definição de um novo campo](./overview.md#define) na interface, é possível defini-lo como um campo de identidade selecionando o **[!UICONTROL Identidade]** no painel direito.

![](../../images/ui/fields/special/identity.png)

Controles adicionais são exibidos após marcar a caixa de seleção. Se quiser que esse campo seja a identidade principal do esquema, selecione a variável **[!UICONTROL Identidade principal]** caixa de seleção

>[!NOTE]
>
>Um único esquema pode ter muitos campos de identidade definidos, mas pode ter apenas uma identidade principal. Todos os campos de identidade (primários ou não) contribuem para o gráfico de identidade de um cliente individual, mas o Perfil do cliente em tempo real usa somente a identidade primária como a fonte da verdade ao mesclar fragmentos de dados. Se quiser ativar um esquema para uso em Perfil, ele deverá ter uma identidade primária definida.

Em **[!UICONTROL Namespace de identidade]**, use o menu suspenso para selecionar o namespace apropriado para o campo de identidade. Os namespaces padrão fornecidos pelo Adobe são listados, juntamente com quaisquer namespaces personalizados definidos pela sua organização.

Quando terminar, selecione **[!UICONTROL Aplicar]** para aplicar a alteração ao esquema.

![](../../images/ui/fields/special/identity-config.png)

A tela é atualizada para refletir as alterações, com o campo selecionado ganhando um símbolo de impressão digital (![](../../images/ui/fields/special/identity-symbol.png)) para designá-la como uma identidade. No painel à esquerda, o campo de identidade agora está listado sob o nome da classe ou do grupo de campos de esquema que fornece o campo ao esquema.

Se o campo também tiver sido definido como a identidade primária, ele também será listado em **[!UICONTROL Campos obrigatórios]** no painel esquerdo. Se o campo de identidade estiver aninhado na estrutura do esquema, todos os campos principais também serão listados conforme necessário.

![](../../images/ui/fields/special/identity-applied.png)

Se você definiu uma identidade primária para o esquema, agora é possível prosseguir para [ativar o esquema para uso no Perfil de cliente em tempo real](../resources/schemas.md#profile).

## Próximas etapas

Este guia abordou como definir um campo de identidade na interface do usuário do. À medida que os dados são assimilados usando esse esquema, seus gráficos de identidade do cliente serão atualizados para refletir os campos de identidade do esquema. Consulte o guia no [visualizador de gráficos de identidade](../../../identity-service/ui/identity-graph-viewer.md) para saber como explorar o gráfico privado de sua organização na interface do usuário.

Consulte a visão geral em [definição de campos na interface](./overview.md#special) para saber como definir outros tipos de campo XDM na variável [!DNL Schema Editor].
