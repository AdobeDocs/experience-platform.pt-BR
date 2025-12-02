---
title: Redirecionar com identidade
description: Permite compartilhar um identificador de visitante nos domínios de sua organização.
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# Redirecionar com identidade

O tipo de ação **[!UICONTROL Redirect with identity]** permite compartilhar um identificador de visitante da página atual para outro domínio de propriedade da sua organização. Ele foi projetado para ser usado com um evento de clique e uma condição de comparação de valor. É funcionalmente semelhante ao comando [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) na biblioteca do JavaScript.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Rules]** e selecione a regra desejada.
1. Em [!UICONTROL Actions], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extension] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina [!UICONTROL Action type] como **[!UICONTROL Redirect with identity]**.

## Casos de uso

* **Identificar um indivíduo entre domínios**: se um visitante clicar de um domínio para outro pertencente à sua organização, você poderá usar essa ação para que ele ainda seja considerado o mesmo indivíduo. Esse método de identificação é especialmente útil se você tiver relatórios que combinam dados de vários domínios, evitando a inflação de visitantes.
* **Identifique um indivíduo de um aplicativo móvel para um aplicativo Web**: se um visitante estiver dentro do aplicativo móvel e clicar em um link para o aplicativo Web, você poderá usar esta ação para que o Web SDK reconheça que é o mesmo indivíduo. Esse fluxo de trabalho permite uma experiência consistente para relatórios e personalização.

## Campos disponíveis

* **[!UICONTROL Instance]**: a instância do SDK à qual a ação se aplica. Esse menu suspenso estará desativado se sua implementação usar uma única instância do SDK.
* **[!UICONTROL Datastream configuration overrides]**: Esse comando oferece suporte a substituições de configuração de sequência de dados, fornecendo controle sobre quais aplicativos e serviços recebem esses dados. Ao definir uma substituição da configuração do fluxo de dados em um comando individual e nas configurações da extensão de tag, o comando individual tem prioridade. Consulte [Substituições da configuração da sequência de dados](../configure/configuration-overrides.md) para obter mais informações.

## Exemplo de regra

Normalmente, esse comando é usado com uma regra específica que ouve cliques e verifica domínios desejados.

+++Critérios de evento da regra

Acionado quando um tag de âncora com uma propriedade `href` é clicado.

* **[!UICONTROL Extension]**: Principal
* **[!UICONTROL Event type]**: Clique
* **[!UICONTROL When the user clicks on]**: Elementos específicos
* **[!UICONTROL Elements matching the CSS selector]**: `a[href]`

![Evento de regra](../assets/id-sharing-event-configuration.png)

+++

+++Condição da regra

Aciona somente nos domínios desejados.

* **[!UICONTROL Logic type]**: Normal
* **[!UICONTROL Extension]**: Principal
* **[!UICONTROL Condition Type]**: Comparação de valores
* **[!UICONTROL Left Operand]**: `%this.hostname%`
* **[!UICONTROL Operator]**: Corresponde a Regex
* **[!UICONTROL Right Operand]**: uma expressão regular que corresponde aos domínios desejados. Por exemplo, `adobe.com$|behance.com$`

![Condição de regra](../assets/id-sharing-condition-configuration.png)

+++

+++Ação da regra

Anexe a identidade ao URL.

* **[!UICONTROL Extension]**: Adobe Experience Platform Web SDK
* **[!UICONTROL Action Type]**: Redirecionar com identidade

![Ação da regra](../assets/id-sharing-action-configuration.png)

+++
