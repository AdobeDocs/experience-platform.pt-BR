---
title: Tipos de ação na extensão SDK da Web do Adobe Experience Platform
description: Saiba mais sobre os diferentes tipos de ação fornecidos pela extensão de tag do Adobe Experience Platform Web SDK.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: e5fd8a53cfd612034d12a761ac4779ed930557d4
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 1%

---


# Tipos de ação

Após configurar o [Extensão de tag do SDK da Web da Adobe Experience Platform](web-sdk-extension-configuration.md), você deve configurar seus tipos de ação.

Esta página descreve os tipos de ação compatíveis com o [Extensão de tag do SDK da Web da Adobe Experience Platform](web-sdk-extension-configuration.md).


## Aplicar resposta {#apply-response}

Use o **[!UICONTROL Aplicar resposta]** tipo de ação quando quiser executar várias ações com base em uma resposta do Edge Network. Normalmente, esse tipo de ação é usado em implantações híbridas em que o servidor faz uma chamada inicial para o Edge Network, em seguida, esse tipo de ação recebe a resposta dessa chamada e inicializa o SDK da Web no navegador.

O uso desse tipo de ação pode reduzir os tempos de carregamento do cliente para casos de uso de personalização híbrida.

![Imagem da interface do usuário do Experience Platform mostrando o tipo de ação Aplicar resposta.](assets/apply-response.png)

Esse tipo de ação oferece suporte às seguintes opções de configuração:

* **[!UICONTROL Instância]**: selecione a instância do SDK da Web que você está usando.
* **[!UICONTROL Cabeçalhos de resposta]**: selecione o elemento de dados que retorna um objeto contendo as chaves do cabeçalho e os valores retornados da chamada do servidor Edge Network.
* **[!UICONTROL Corpo da resposta]**: selecione o elemento de dados que retorna o objeto que contém a carga JSON fornecida pela resposta Edge Network.
* **[!UICONTROL Renderizar decisões de personalização visual]**: habilite essa opção para renderizar automaticamente o conteúdo de personalização fornecido pelo Edge Network e pré-ocultar o conteúdo para evitar cintilação.

## Enviar evento {#send-event}

Envia um evento para o Adobe [!DNL Experience Platform] para que a Adobe Experience Platform possa coletar os dados enviados e agir de acordo com essas informações. Selecione uma instância (se você tiver mais de uma). Todos os dados que deseja enviar podem ser enviados no **[!UICONTROL Dados XDM]** campo. Use um objeto JSON que esteja em conformidade com a estrutura do esquema XDM. Esse objeto pode ser criado na sua página ou por meio de uma **[!UICONTROL Custom Code]** **[!UICONTROL Elemento de dados]**.

Há alguns outros campos no tipo de ação Enviar evento que também podem ser úteis, dependendo da implementação. Observe que todos esses campos são opcionais.

* **Tipo:** Esse campo permite especificar um tipo de evento que será gravado no esquema XDM. Consulte [`type`](/help/web-sdk/commands/sendevent/type.md) no `sendEvent` para obter mais informações.
* **Dados:** Os dados que não correspondem a um esquema XDM podem ser enviados usando esse campo. Este campo é útil se você estiver tentando atualizar um perfil do Adobe Target ou enviar atributos do Target Recommendations. Consulte [`data`](/help/web-sdk/commands/sendevent/data.md) no `sendEvent` para obter mais informações.<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
* **ID do conjunto de dados:** Se precisar enviar dados para um conjunto de dados diferente daquele especificado no fluxo de dados, você pode especificar essa ID de conjunto de dados aqui.
* **O documento será descarregado:** Se quiser garantir que os eventos cheguem ao servidor mesmo se o usuário sair da página, verifique a **[!UICONTROL O documento será descarregado]** caixa de seleção Isso permite que os eventos alcancem o servidor, mas as respostas são ignoradas.
* **Renderizar decisões de personalização visual:** Se quiser renderizar um conteúdo personalizado na sua página, marque a opção **[!UICONTROL Renderizar decisões de personalização visual]** caixa de seleção Você também pode especificar escopos de decisão e/ou superfícies, se necessário. Consulte a [documentação de personalização](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) para obter mais informações sobre renderização de conteúdo personalizado.

## Definir consentimento {#set-consent}

Após receber o consentimento do usuário, esse consentimento deve ser comunicado ao SDK da Web da Adobe Experience Platform usando o tipo de ação &quot;Definir consentimento&quot;. Atualmente, há suporte para dois tipos de padrões: &quot;Adobe&quot; e &quot;IAB TCF&quot;. Consulte [Suporte às preferências de consentimento do cliente](/help/web-sdk/consent/supporting-consent.md). Ao usar a versão 2.0 do Adobe, somente um valor de elemento de dados é compatível. Será necessário criar um elemento de dados que resolva para o objeto de consentimento.

Nesta ação, você também recebe um campo opcional para incluir um Mapa de identidade, de modo que as identidades possam ser sincronizadas assim que o consentimento for recebido. A sincronização é útil quando o consentimento é configurado como &quot;Pendente&quot; ou &quot;Fora&quot;, pois a chamada de consentimento provavelmente é a primeira chamada a ser acionada.

## Atualizar variável {#update-variable}

Use esta ação para modificar um objeto XDM como resultado de um evento. Esta ação destina-se a criar um objeto que pode ser referenciado posteriormente de uma **[!UICONTROL Enviar evento]** para registrar o objeto XDM do evento.

Para usar esse tipo de ação, você deve ter definido um [variável](data-element-types.md#variable) elemento de dados. Depois que você escolhe um elemento de dados variável para modificar, é exibido um editor, semelhante ao editor da variável [Objeto XDM](data-element-types.md#xdm-object) elemento de dados.

![](assets/update-variable.png)

O esquema XDM usado para o editor é o esquema selecionado na variável [!UICONTROL variável] elemento de dados. Você pode definir uma ou mais propriedades do objeto clicando em uma das propriedades na árvore à esquerda e modificando o valor à direita. Por exemplo, na captura de tela abaixo, a propriedade productionBy está sendo definida como o elemento de dados &quot;Produced by data element&quot;.

![](assets/update-variable-set-property.png)

Há algumas diferenças entre o editor na ação de atualização de variáveis e o editor no elemento de dados do objeto XDM. Primeiro, a ação atualizar variável tem um item de nível raiz rotulado como &quot;xdm&quot;. Se você clicar nesse item, poderá especificar um elemento de dados a ser usado para definir o objeto inteiro. Segundo, a ação de atualização da variável tem caixas de seleção para limpar os dados do objeto xdm. Clique em uma das propriedades à esquerda e marque a caixa de seleção à direita para limpar o valor. Isso limpará o valor atual antes de definir quaisquer valores na variável.

## Enviar evento de mídia {#send-media-event}

Envia um evento de mídia para o Adobe Experience Platform e/ou Adobe Analytics. Essa ação é útil ao rastrear eventos de mídia no site. Selecione uma instância (se você tiver mais de uma). A ação requer um `playerId` que representa um identificador exclusivo de uma sessão de mídia rastreada. Exige também uma **[!UICONTROL Qualidade da experiência]** e uma `playhead` elemento de dados ao iniciar uma sessão de mídia.

![Imagem da interface do usuário da Platform mostrando a tela de evento enviar mídia.](assets/send-media-event.png)

A variável **[!UICONTROL Enviar evento de mídia]** o tipo de ação é compatível com as seguintes propriedades:

* **[!UICONTROL Instância]**: a instância do SDK da Web que está sendo usada.
* **[!UICONTROL Tipo de evento de mídia]**: o tipo de evento de mídia que está sendo rastreado.
* **[!UICONTROL ID do player]**: O identificador exclusivo da sessão de mídia.
* **[!UICONTROL Indicador de reprodução]**: a posição atual da reprodução de mídia, em segundos.
* **[!UICONTROL Detalhes da sessão de mídia]**: ao enviar um evento de início de mídia, os detalhes da sessão de mídia necessários devem ser especificados.
* **[!UICONTROL Detalhes do capítulo]**: nesta seção, você pode especificar os detalhes do capítulo ao enviar um evento de mídia de início de capítulo.
* **[!UICONTROL Detalhes de publicidade]**: ao enviar um `AdBreakStart` evento, você deve especificar os detalhes de publicidade necessários.
* **[!UICONTROL Detalhes do pod de publicidade]**: detalhes sobre o pod de publicidade ao enviar um `AdStart` evento.
* **[!UICONTROL Detalhes do erro]**: detalhes sobre o erro de reprodução que está sendo rastreado.
* **[!UICONTROL Detalhes da atualização de estado]**: o estado do player que está sendo atualizado.
* **[!UICONTROL Metadados personalizados]**: os metadados personalizados sobre o evento de mídia que está sendo rastreado.
* **[!UICONTROL Qualidade da experiência]**: a qualidade da mídia dos dados de experiência que estão sendo rastreados.

## Obter o Media Analytics Tracker {#get-media-analytics-tracker}

Essa ação é usada para obter a API herdada do Media Analytics. Ao configurar a ação e um nome de objeto é fornecido, a API herdada do Media Analytics será exportada para esse objeto de janela. Se nenhum for fornecido, ele será exportado para `window.Media` como a biblioteca Media JS atual faz.

![Imagem da interface do usuário da plataforma mostrando o tipo de ação Obter rastreador do Media Analytics.](assets/get-media-analytics-tracker.png)

## Redirecionar com identidade {#redirect-with-identity}

Use esse tipo de ação para compartilhar identidades da página atual com outros domínios. Esta ação foi projetada para ser usada com um **[!UICONTROL click]** tipo de evento e uma condição de comparação de valor. Consulte [anexar identidade ao URL usando a extensão SDK da Web](../../../../web-sdk/commands/appendidentitytourl.md#extension) para obter mais informações sobre como usar este tipo de ação.

## Próximas etapas {#next-steps}

Depois de ler este artigo, você terá que entender melhor como configurar suas ações. Em seguida, leia sobre como [configurar os tipos de elementos de dados](data-element-types.md).
