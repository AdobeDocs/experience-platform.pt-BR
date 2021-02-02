---
keywords: Experience Platform;home;popular topics;api;API;XDM;sistema XDM;experimentar modelo de dados;modelo de dados;ui;espaço de trabalho;identidade;campo;
solution: Experience Platform
title: Definir um campo de identidade na interface do usuário
description: Saiba como definir um campo de identidade na interface do usuário do Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: f5f507c2e962e2ff9f81376bfe363a6f438056cd
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---


# Definir um campo de identidade na interface do usuário

No Experience Data Model (XDM), um campo de identidade representa um campo que pode ser usado para identificar uma pessoa individual relacionada a um evento de registro ou série de tempo. Este documento aborda como definir um campo de identidade na interface do usuário do Adobe Experience Platform.

## Pré-requisitos

Os campos de identidade são um componente crucial na forma como os gráficos de identidade do cliente são construídos na Plataforma, o que, em última análise, afeta a forma como o Perfil do cliente em tempo real une os fragmentos de dados diferentes para obter uma visualização completa do cliente. Antes de definir campos de identidade em seus schemas, consulte a seguinte documentação para saber mais sobre os principais serviços e conceitos relacionados aos campos de identidade:

* [Serviço](../../../identity-service/home.md) de identidade Adobe Experience Platform: Corresponde identidades entre dispositivos e sistemas, vinculando conjuntos de dados com base nos campos de identidade definidos pelos schemas XDM aos quais eles estão em conformidade.
   * [Namespaces](../../../identity-service/namespaces.md) de identidade: As namespaces de identidade definem os diferentes tipos de informações de identidade que podem estar relacionadas a uma única pessoa e são um componente necessário para cada campo de identidade.
* [Perfil](../../../profile/home.md) do cliente em tempo real: Aproveita os gráficos de identidade do cliente para fornecer um perfil unificado do consumidor com base em dados agregados de várias fontes, atualizados em tempo quase real.

## Definir um campo de identidade

Quando [definir um novo campo](./overview.md#define) na interface do usuário, você pode defini-lo como um campo de identidade marcando a caixa de seleção **[!UICONTROL Identity]** no painel direito.

![](../../images/ui/fields/special/identity.png)

Os controles adicionais são exibidos depois de marcar a caixa de seleção. Se desejar que esse campo seja a identidade primária do schema, marque a caixa de seleção **[!UICONTROL Identidade primária]**.

>[!NOTE]
>
>Um único schema pode ter muitos campos de identidade definidos, mas só pode ter uma identidade primária. Todos os campos de identidade (principal ou não) contribuem para o gráfico de identidade de um cliente individual, mas o Perfil de cliente em tempo real usa apenas a identidade primária como fonte de verdade ao unir fragmentos de dados. Se você quiser ativar um schema para uso no Perfil, ele deverá ter uma identidade primária definida.

Em **[!UICONTROL namespace de identidade]**, use o menu suspenso para selecionar a namespace apropriada para o campo de identidade. Namespaces padrão fornecidas pelo Adobe são listadas, juntamente com quaisquer namespaces personalizadas definidas por sua organização.

Quando terminar, selecione **[!UICONTROL Aplicar]** para aplicar a alteração ao schema.

![](../../images/ui/fields/special/identity-config.png)

A tela é atualizada para refletir as alterações, com o campo selecionado ganhando um símbolo de impressão digital (![](../../images/ui/fields/special/identity-symbol.png)) para designá-lo como uma identidade. No painel esquerdo, o campo de identidade agora é listado sob o nome da classe ou mixin que fornece o campo para o schema.

Como todos os campos de identidade são obrigatórios por padrão, o campo agora é listado em **[!UICONTROL Campos obrigatórios]** no painel esquerdo. Se o campo de identidade estiver aninhado dentro da estrutura do schema, todos os campos pai também serão listados como obrigatório.

![](../../images/ui/fields/special/identity-applied.png)

Se você definiu uma identidade primária para o schema, agora é possível ir para [ativar o schema para uso no Perfil do cliente em tempo real](../resources/schemas.md#profile).

## Próximas etapas

Este guia aborda como definir um campo de identidade na interface do usuário. À medida que os dados são ingeridos usando esse schema, seus gráficos de identidade do cliente serão atualizados para refletir os campos de identidade do schema. Consulte o guia no [visualizador de gráficos de identidade](../../../identity-service/ui/identity-graph-viewer.md) para saber como explorar o gráfico privado da sua organização na interface do usuário.

Consulte a visão geral em [definindo campos na interface do usuário](./overview.md#special) para saber como definir outros tipos de campos XDM no [!DNL Schema Editor].