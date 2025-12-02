---
title: Enviar evento
description: Envie dados para o Adobe Experience Platform Edge Network.
source-git-commit: d6aea91d6989775ff5b6038b216ed2518f4a7d98
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# Enviar evento

A ação **[!UICONTROL Send event]** envia uma carga para uma sequência de dados no Adobe Experience Platform Edge Network. É um recurso principal da coleta e personalização de dados; quase todas as organizações usam essa ação como parte de sua implementação do Web SDK.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Rules]** e selecione a regra desejada.
1. Em [!UICONTROL Actions], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extension] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina [!UICONTROL Action type] como **[!UICONTROL Send event]**.

## Campos gerais

![Imagem da interface do usuário de Marcas do Experience Platform mostrando as configurações de instância para o tipo de ação Enviar Evento.](../assets/instance-settings.png)

* **[!UICONTROL Instance]**: a instância do SDK à qual a ação se aplica. Esse menu suspenso estará desativado se sua implementação usar uma única instância do SDK.
* **[!UICONTROL Use guided events]**: Habilite esta opção para preencher ou ocultar automaticamente determinados campos para habilitar um caso de uso específico. Esta configuração pode ajudar a reduzir o ruído das opções disponíveis ao configurar a ação para cada finalidade respectiva, e segue as práticas recomendadas da Adobe de [eventos de página superior/inferior](/help/collection/use-cases/personalization/top-bottom-page-events.md). Habilitar essa caixa de seleção aciona a exibição dos seguintes botões de opção:
   * **[!UICONTROL Request personalization]**: obtenha as decisões de personalização mais recentes sem gravar um evento do Adobe Analytics. Ele é chamado com mais frequência na parte superior da página. Quando selecionado, esse botão de opção define os seguintes campos:
      * [!UICONTROL Type] está bloqueado para [!UICONTROL Decisioning Proposition Fetch]
      * [!UICONTROL Render visual personalization decisions] está bloqueado para habilitado
      * [!UICONTROL Automatically send a display event] está bloqueado para desabilitado
   * **[!UICONTROL Collect analytics]**: Registre um evento sem obter decisões de personalização. Ele é chamado mais comumente na parte inferior da página. Quando selecionado, esse botão de opção define os seguintes campos:
      * [!UICONTROL Include rendered propositions] está bloqueado para habilitado

## Campos de dados

![Imagem da interface do usuário de Marcas do Experience Platform mostrando as configurações do elemento de dados para o tipo de ação Enviar Evento.](../assets/data.png)

* **[!UICONTROL Type]**: O tipo de evento. Você pode selecionar a partir de um conjunto predefinido de valores ou definir seu próprio valor. Consulte [Valores aceitos para `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) para obter mais informações. O equivalente da biblioteca JavaScript para este campo é [`eventType`](/help/collection/js/commands/sendevent/eventtype.md).
* **[!UICONTROL XDM]**: a carga XDM que você deseja enviar para o Adobe. Você pode usar um [objeto XDM](../data-element-types.md#xdm-object) ou uma [Variável](../data-element-types.md#variable) neste campo. Se você tiver regras que preenchem vários objetos XDM, poderá usar [Objetos mesclados](../../core/overview.md#merged-objects) para combiná-los.
* **[!UICONTROL Data]**: a carga de dados que você deseja enviar para o Adobe. Alguns aplicativos e serviços não exigem a adesão a um esquema XDM, como Adobe Analytics ou Adobe Target. Use um tipo de elemento de dados [Variável](../data-element-types.md#variable) para este campo.
* **[!UICONTROL Include rendered propositions]**: Habilite esta caixa de seleção para usar este evento como um evento de exibição, incluindo as apresentações renderizadas quando a opção &quot;enviar automaticamente um evento de exibição&quot; estava desmarcada. O campo XDM `_experience.decisioning` é preenchido com informações sobre personalização renderizada.
* **[!UICONTROL Document will unload]**: Ative esta caixa de seleção para garantir que o evento chegue ao servidor mesmo se o usuário sair da página. Essa configuração permite que os eventos alcancem o servidor, mas as respostas da Edge Network são ignoradas.
* **[!UICONTROL Merge ID]** _(Obsoleto)_: preenche o campo XDM `eventMergeId`.

## Campos de personalização

![Imagem da interface do usuário de Marcas do Experience Platform mostrando as configurações do Personalization para o tipo de ação Enviar Evento.](../assets/personalization-settings.png)

* **[!UICONTROL Scopes]**: uma matriz de escopos que você deseja solicitar explicitamente da personalização. Você pode inserir os escopos manualmente ou fornecer um elemento de dados. Ao inserir escopos manualmente, cada campo representa um escopo. Selecione **[!UICONTROL Add scope]** para adicionar mais escopos à ação.
* **[!UICONTROL Surfaces]**: uma matriz de superfícies para consultar com o evento. Consulte [Criar experiências da Web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) na documentação do Adobe Journey Optimizer para obter mais informações. Ao inserir superfícies manualmente, cada campo representa uma superfície. Selecione **[!UICONTROL Add surface]** para adicionar mais superfícies à ação.
* **Renderizar decisões de personalização visual:** uma caixa de seleção que, quando habilitada, permite renderizar conteúdo personalizado na página. Consulte [Renderizar conteúdo personalizado](/help/collection/use-cases/personalization/rendering-personalization-content.md#automatically-rendering-content) para obter mais informações.
* **[!UICONTROL Request default personalization]**: controla se o escopo da página e a superfície padrão são solicitados. Por padrão, ele é solicitado automaticamente durante a primeira chamada `sendEvent` do carregamento da página. O equivalente da biblioteca JavaScript a esses botões de opção é [`requestDefaultPersonalization`](/help/collection/js/commands/sendevent/personalization.md). Você pode escolher entre as seguintes opções:
   * **[!UICONTROL Automatic]**: O comportamento padrão. Somente solicite a personalização padrão quando ainda não tiver sido solicitada.
   * **[!UICONTROL Enabled]**: solicitar explicitamente o escopo e a superfície padrão da página. Isso atualiza o cache de visualização de SPA.
   * **[!UICONTROL Disabled]**: suprimir explicitamente a solicitação para o escopo de página e superfície padrão.
* **[!UICONTROL Decision context]**: um mapa de valor chave que é usado ao avaliar conjuntos de regras do Adobe Journey Optimizer para a tomada de decisão no dispositivo. Você pode fornecer o contexto de decisão manualmente ou por meio de um elemento de dados.

## Campos do Advertising

![Interface do usuário de marcas do Experience Platform mostrando configurações de publicidade para a ação Enviar evento](../assets/send-event-advertising.png)

* **[!UICONTROL Request default advertising data]**: determina quando (ou se) a biblioteca adiciona informações de publicidade à carga XDM. Você pode escolher entre as seguintes opções:
   * **[!UICONTROL Automatic]**: Quaisquer dados de publicidade disponíveis no momento do evento são adicionados à carga do evento.
   * **[!UICONTROL Wait]**: atrasar o envio do evento até que os dados de publicidade sejam recebidos.
   * **[!UICONTROL Disabled]**: não adicionar dados de publicidade à carga do evento. Selecione esta opção se sua implementação não usar o Adobe Analytics ou o Customer Journey Analytics.

## Substituições de configuração da sequência de dados

Esse comando oferece suporte a substituições de configuração de sequência de dados, fornecendo controle sobre quais aplicativos e serviços recebem esses dados. Ao definir uma substituição da configuração do fluxo de dados em um comando individual e nas configurações da extensão de tag, o comando individual tem prioridade. Consulte [Substituições da configuração da sequência de dados](../configure/configuration-overrides.md) para obter mais informações.
