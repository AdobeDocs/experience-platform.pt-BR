---
title: Aplicar apresentações
description: Renderize apresentações em aplicativos de página única sem incrementar métricas.
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Aplicar apresentações

O tipo de ação **[!UICONTROL Apply propositions]** permite renderizar apresentações em aplicativos de página única sem incrementar métricas. Esse tipo de ação é útil ao trabalhar com aplicativos de página única em que partes da página são renderizadas novamente, substituindo potencialmente qualquer personalização já aplicada à página.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Rules]** e selecione a regra desejada.
1. Em [!UICONTROL Actions], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extension] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina [!UICONTROL Action type] como **[!UICONTROL Apply propositions]**.

![Interface do usuário de Marcas do Experience Platform mostrando o tipo de ação Aplicar Apresentações.](../assets/apply-propositions.png)

## Casos de uso

Você pode usar esse tipo de ação para vários casos de uso, como:

1. **Renderizar ofertas de mbox do HTML**. Proposições solicitadas explicitamente por um escopo ou superfície de uma ação **[!UICONTROL Send event]** não são renderizadas automaticamente. Você pode usar o tipo de ação **[!UICONTROL Apply propositions]** para informar ao Web SDK onde renderizá-los especificando os metadados da proposta.
2. **Renderizar as ofertas para uma exibição em um aplicativo de página única**. Ao renderizar um evento de alteração de exibição, se os dados de análise ainda não estiverem prontos, você poderá usar a ação **[!UICONTROL Apply propositions]** para renderizar as propostas de exibição na parte superior da página. Consulte [eventos de início e fim de página (Segunda exibição de página - Opção 2)](/help/collection/use-cases/personalization/top-bottom-page-events.md) para obter mais detalhes. Para usar isso, insira um **[!UICONTROL View name]** no formulário.
3. **Renderizar novamente as apresentações**. Quando o site usa uma estrutura como o React para renderizar o conteúdo novamente, talvez seja necessário reaplicar a personalização. Nesses casos, você pode usar o tipo de ação **[!UICONTROL Apply propositions]** para fazer isso.

Esse tipo de ação não envia um evento de exibição para apresentações renderizadas. Ela rastreia as apresentações renderizadas para que elas possam ser incluídas nas chamadas **[!UICONTROL Send event]** subsequentes.

## Campos disponíveis

Esse tipo de ação é compatível com os seguintes campos:

* **[!UICONTROL Instance]**: a instância do SDK à qual a ação se aplica. Esse menu suspenso estará desativado se sua implementação usar uma única instância do SDK.
* **[!UICONTROL Propositions]**: uma matriz de objetos de proposta que você deseja renderizar novamente.
* **[!UICONTROL View name]**: O nome do modo de exibição a ser renderizado.
* **[!UICONTROL Proposition metadata]**: um objeto que determina como as ofertas do HTML podem ser aplicadas. Essas informações podem ser fornecidas por meio do formulário ou por meio de um elemento de dados. Ele contém as seguintes propriedades:
   * **[!UICONTROL Scope]**
   * **[!UICONTROL Selector]**
   * **[!UICONTROL Action type]**
