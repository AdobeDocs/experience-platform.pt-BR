---
title: Tipos de ação na extensão do Adobe Experience Platform Web SDK
description: Saiba mais sobre os diferentes tipos de ação fornecidos pela extensão de tag do Adobe Experience Platform Web SDK.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: e274dda06c678bdbd230bc2f06204724bac633e8
workflow-type: tm+mt
source-wordcount: '2301'
ht-degree: 1%

---


# Tipos de ação

Após configurar a [extensão de tag do Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md), você deve configurar seus tipos de ação.

Esta página descreve os tipos de ação suportados pela [extensão de tag do Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md).

## Aplicar apresentações {#apply-propositions}

O tipo de ação **[!UICONTROL Aplicar apresentações]** permite renderizar apresentações em aplicativos de página única sem incrementar métricas.

Esse tipo de ação é útil ao trabalhar com aplicativos de página única em que partes da página são renderizadas novamente, substituindo potencialmente qualquer personalização já aplicada à página.

Você pode usar esse tipo de ação para vários casos de uso, como:

1. **Renderizar ofertas de mbox do HTML**. Proposições solicitadas explicitamente por um escopo ou superfície de uma ação **[!UICONTROL Enviar evento]** não são renderizadas automaticamente. Você pode usar o tipo de ação **[!UICONTROL Aplicar propostas]** para informar ao Web SDK onde renderizá-las especificando os metadados da proposta.
2. **Renderizar as ofertas para uma exibição em um aplicativo de página única**. Ao renderizar um evento de alteração de exibição, se os dados de análise ainda não estiverem prontos, você poderá usar a ação **[!UICONTROL Aplicar propostas]** para renderizar as propostas de exibição na parte superior da página. Consulte [eventos de início e fim de página (Segunda exibição de página - Opção 2)](../../../../web-sdk/use-cases/top-bottom-page-events.md) para obter mais detalhes. Para usar isso, insira um **[!UICONTROL Nome da exibição]** no formulário.
3. **Renderizar novamente as apresentações**. Quando o site usa uma estrutura como o React para renderizar o conteúdo novamente, talvez seja necessário reaplicar a personalização. Nesses casos, você pode usar o tipo de ação **[!UICONTROL Aplicar propostas]** para fazer isso.

Esse tipo de ação não enviará um evento de exibição para apresentações renderizadas. Ele rastreará as apresentações renderizadas para que elas possam ser incluídas nas chamadas **[!UICONTROL Enviar evento]** subsequentes.


![Interface do usuário de Marcas do Experience Platform mostrando o tipo de ação Aplicar Apresentações.](assets/apply-propositions.png)

Esse tipo de ação é compatível com os seguintes campos:

* **[!UICONTROL Propositions]**: uma matriz de objetos de proposta que você deseja renderizar novamente.
* **[!UICONTROL Nome da exibição]**: o nome da exibição a ser renderizada.
* **[!UICONTROL Metadados de apresentação]**: um objeto que determina como as ofertas do HTML podem ser aplicadas. Essas informações podem ser fornecidas por meio do formulário ou por meio de um elemento de dados. Ele contém as seguintes propriedades:
   * **[!UICONTROL Escopo]**
   * **[!UICONTROL Seletor]**
   * **[!UICONTROL Tipo de ação]**

## Aplicar resposta {#apply-response}

Use o tipo de ação **[!UICONTROL Aplicar resposta]** quando desejar executar várias ações com base em uma resposta do Edge Network. Normalmente, esse tipo de ação é usado em implantações híbridas em que o servidor faz uma chamada inicial para o Edge Network. Em seguida, esse tipo de ação recebe a resposta dessa chamada e inicializa a Web SDK no navegador.

O uso desse tipo de ação pode reduzir os tempos de carregamento do cliente para casos de uso de personalização híbrida.

![Imagem da interface do usuário do Experience Platform mostrando o tipo de ação Aplicar resposta.](assets/apply-response.png)

Esse tipo de ação oferece suporte às seguintes opções de configuração:

* **[!UICONTROL Instância]**: selecione a instância do Web SDK que você está usando.
* **[!UICONTROL Cabeçalhos de resposta]**: selecione o elemento de dados que retorna um objeto contendo as chaves e os valores do cabeçalho retornados da chamada do servidor Edge Network.
* **[!UICONTROL Corpo da resposta]**: selecione o elemento de dados que retorna o objeto que contém a carga JSON fornecida pela resposta do Edge Network.
* **[!UICONTROL Renderizar decisões de personalização visual]**: habilite esta opção para renderizar automaticamente o conteúdo de personalização fornecido pelo Edge Network e pré-ocultar o conteúdo para evitar cintilação.

## Avaliar conjuntos de regras {#evaluate-rulesets}

Esse tipo de ação aciona manualmente a avaliação do conjunto de regras. Os conjuntos de regras são retornados pelo Adobe Journey Optimizer para oferecer suporte a recursos como mensagens no navegador.

![Imagem da interface do usuário do Experience Platform mostrando o tipo de ação de resposta Avaliar conjuntos de regras.](assets/evaluate-rulesets.png)

Esse tipo de ação é compatível com as seguintes opções:

* **[!UICONTROL Renderizar decisões de personalização visual]**: habilite essa opção para renderizar decisões de personalização visual para os itens do conjunto de regras correspondentes.
* **[!UICONTROL Contexto de decisão]**: é um mapa de valores chave usado ao avaliar conjuntos de regras do Adobe Journey Optimizer para decisão no dispositivo. Você pode fornecer o contexto de decisão manualmente ou por meio de um elemento de dados.

## Obter o Media Analytics Tracker {#get-media-analytics-tracker}

Essa ação é usada para obter a API herdada do Media Analytics. Ao configurar a ação e um nome de objeto é fornecido, a API herdada do Media Analytics será exportada para esse objeto de janela. Se nenhum for fornecido, ele será exportado para `window.Media` como a biblioteca Media JS atual faz.

![Imagem da interface do usuário do Experience Platform mostrando o tipo de ação Obter Media Analytics Tracker.](assets/get-media-analytics-tracker.png)

## Redirecionar com identidade {#redirect-with-identity}

Use esse tipo de ação para compartilhar identidades da página atual com outros domínios. Esta ação foi projetada para ser usada com um tipo de evento **[!UICONTROL click]** e uma condição de comparação de valor. Consulte [anexar identidade à URL usando a extensão do Web SDK](../../../../web-sdk/commands/appendidentitytourl.md#extension) para obter mais informações sobre como usar este tipo de ação.

## Enviar evento {#send-event}

Envia um evento para o Experience Platform para que o Experience Platform possa coletar os dados enviados e agir de acordo com essas informações. Todos os dados que deseja enviar podem ser enviados no campo **[!UICONTROL Dados XDM]**. Use um objeto [!DNL JSON] que esteja em conformidade com a estrutura do esquema [!DNL XDM]. Este objeto pode ser criado na sua página ou através de um **[!UICONTROL Código personalizado]** **[!UICONTROL Elemento de dados]**.

O tipo de ação **[!UICONTROL Enviar Evento]** dá suporte aos campos e configurações descritos abaixo. Todos esses campos são opcionais.

### Configurações de instância {#instance}

Use o seletor **[!UICONTROL Instância]** para escolher a instância do Web SDK que deseja configurar. Se você tiver apenas uma instância, ela será pré-selecionada.

![Imagem da interface do usuário de Marcas do Experience Platform mostrando as configurações de instância para o tipo de ação Enviar Evento.](assets/instance-settings.png)

* **[!UICONTROL Instância]**: selecione a instância do Web SDK que deseja configurar. Se você tiver apenas uma instância, ela será pré-selecionada.
* **[!UICONTROL Usar eventos guiados]**: habilite esta opção para preencher ou ocultar automaticamente determinados campos para habilitar um caso de uso específico. Habilitar essa opção aciona a exibição das seguintes configurações.
   * **[!UICONTROL Solicitar personalização]**: este evento deve ser chamado na parte superior da página. Quando selecionado, esse evento define os seguintes campos:
      * **[!UICONTROL Tipo]**: **[!UICONTROL Busca de Apresentação de Decisão]**
      * **[!UICONTROL Enviar automaticamente um evento de exibição]**: **[!UICONTROL false]**
      * Para renderizar automaticamente a personalização neste caso, habilite a opção **[!UICONTROL Renderizar decisões de personalização visual]**.
   * **[!UICONTROL Coletar análises]**: este evento deve ser chamado na parte inferior da página. Quando selecionado, esse evento define os seguintes campos:
      * **[!UICONTROL Incluir propostas renderizadas]**: **[!UICONTROL true]**
      * As configurações do **[!UICONTROL Personalization]** estão ocultas

  >[!NOTE]
  >
  >Os eventos guiados estão relacionados a [eventos de início e fim de página](../../../../web-sdk/use-cases/top-bottom-page-events.md).


### Dados {#data}

![Imagem da interface do usuário de Marcas do Experience Platform mostrando as configurações do elemento de dados para o tipo de ação Enviar Evento.](assets/data.png)

* **[!UICONTROL Tipo]**: este campo permite especificar um tipo de evento que será gravado no esquema XDM. Consulte [`type`](/help/web-sdk/commands/sendevent/type.md) no comando `sendEvent` para obter mais informações.
* **[!UICONTROL XDM]**:
* **[!UICONTROL Dados]**: use este campo para enviar dados que não correspondam a um esquema XDM. Este campo é útil se você estiver tentando atualizar um perfil do Adobe Target ou enviar atributos do Target Recommendations. Consulte [`data`](/help/web-sdk/commands/sendevent/data.md) no comando `sendEvent` para obter mais informações.
* **[!UICONTROL Incluir propostas renderizadas]**: habilite esta opção para incluir todas as propostas que foram renderizadas, mas um evento de exibição não foi enviado. Use isso em conjunto com **[!UICONTROL Enviar automaticamente um evento de exibição]** desabilitado. Esta configuração atualiza o campo XDM `_experience.decisioning` com informações sobre as propostas renderizadas.
* **[!UICONTROL Documento será descarregado]**: habilite esta opção para garantir que os eventos cheguem ao servidor mesmo se o usuário sair da página. Isso permite que os eventos alcancem o servidor, mas as respostas são ignoradas.
* **[!UICONTROL ID de Mesclagem]**: **Este campo está obsoleto**. Isso preencherá o campo XDM `eventMergeId`.

### Personalização {#personalization}

![Imagem da interface do usuário de Marcas do Experience Platform mostrando as configurações do Personalization para o tipo de ação Enviar Evento.](assets/personalization-settings.png)

* **[!UICONTROL Escopos]**: selecione os escopos (Adobe Target [!DNL mboxes]) que você deseja solicitar explicitamente da personalização. Você pode inserir os escopos manualmente ou fornecendo um elemento de dados.
* **[!UICONTROL Superfícies]**: defina as superfícies da Web que estão disponíveis na página para personalização. Consulte a [documentação do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=pt-BR) para obter mais detalhes.
* **Renderizar decisões de personalização visual**: se você quiser renderizar conteúdo personalizado em sua página, marque a caixa de seleção **[!UICONTROL Renderizar decisões de personalização visual]**. Você também pode especificar escopos de decisão e/ou superfícies, se necessário. Consulte a [documentação de personalização](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) para obter mais informações sobre renderização de conteúdo personalizado.
* **[!UICONTROL Solicitar personalização padrão]**: use esta seção para controlar se o escopo de toda a página (mbox global) e a superfície padrão (superfície da web com base na URL atual) são solicitados. Por padrão, isso é solicitado automaticamente durante a primeira chamada `sendEvent` do carregamento da página. Você pode escolher entre as seguintes opções:
   * **[!UICONTROL Automático]**: este é o comportamento padrão. Somente solicite a personalização padrão quando ainda não tiver sido solicitada. Isso corresponde a `requestDefaultPersonalization` não definido no comando do Web SDK.
   * **[!UICONTROL Habilitado]**: solicitar explicitamente o escopo de página e a superfície padrão. Isso atualiza o cache de visualização de SPA. Isso corresponde a `requestDefaultPersonalization` definido como `true`.
   * **[!UICONTROL Desabilitado]**: suprimir explicitamente a solicitação para o escopo de página e a superfície padrão. Isso corresponde a `requestDefaultPersonalization` definido como `false`.
* **[!UICONTROL Contexto de decisão]**: é um mapa de valores chave usado ao avaliar conjuntos de regras do Adobe Journey Optimizer para decisão no dispositivo. Você pode fornecer o contexto de decisão manualmente ou por meio de um elemento de dados.

### Advertising {#advertising}

Ao selecionar o componente **[!UICONTROL Advertising]** para o componente de compilação personalizada do Web SDK, as configurações de regra para ações `sendEvent` incluem uma seção [!UICONTROL Advertising], que define como os dados de publicidade são usados para a medição de atribuição. Essa configuração é útil quando a regra inclui uma sequência de várias ações.

![Imagem da interface do usuário de Marcas do Experience Platform mostrando as configurações do Advertising para o tipo de ação Enviar Evento.](assets/send-event-advertising.png)

A seção **[!UICONTROL Solicitar dados padrão do Advertising]** fornece as seguintes opções:

* **[!UICONTROL Automático]**: todos os dados de publicidade disponíveis no momento deste evento serão adicionados automaticamente ao XDM.
* **[!UICONTROL Aguardar]**: atrasar a execução desta chamada até que os dados de publicidade sejam recuperados e resolvidos. Em seguida, adicione os dados ao XDM.
* **[!UICONTROL Desabilitado]**: não adicionar dados de publicidade ao XDM. Use-a para qualquer solicitação que não se destine ao Customer Journey Analytics ou Adobe Analytics.
* **[!UICONTROL Fornecer um elemento de dados]**: use um elemento de dados para incluir ou excluir dados de publicidade durante o carregamento da página. Os valores resolvidos para o elemento de dados podem incluir `automatic`, `wait` e `disabled`.

Se você não usar uma regra para configurar uma ação `sendEvent`, os dados de anúncio serão enviados como um evento de enriquecimento de Anúncio separado.

### Substituições de configuração da sequência de dados {#datastream-overrides}

As substituições de sequência de dados permitem definir configurações adicionais para suas sequências de dados, que são transmitidas para a rede de borda por meio do SDK da Web.

Isso ajuda a acionar comportamentos de sequência de dados diferentes dos padrão, sem criar uma nova sequência de dados ou modificar as configurações existentes. Consulte a documentação em [configurando substituições de sequência de dados](web-sdk-extension-configuration.md#datastream-overrides) para obter mais detalhes.

## Enviar evento de mídia {#send-media-event}

Envia um evento de mídia para o Adobe Experience Platform e/ou Adobe Analytics. Essa ação é útil ao rastrear eventos de mídia no site. Selecione uma instância (se você tiver mais de uma). A ação requer um `playerId` que representa um identificador exclusivo para uma sessão de mídia rastreada. Também requer uma **[!UICONTROL Qualidade de experiência]** e um elemento de dados `playhead` ao iniciar uma sessão de mídia.

![Imagem da interface do usuário do Experience Platform mostrando a tela de evento de envio de mídia.](assets/send-media-event.png)

O tipo de ação **[!UICONTROL Enviar evento de mídia]** dá suporte às seguintes propriedades:

* **[!UICONTROL Instância]**: a instância do Web SDK que está sendo usada.
* **[!UICONTROL Tipo de evento de mídia]**: o tipo de evento de mídia que está sendo rastreado.
* **[!UICONTROL ID do player]**: o identificador exclusivo da sessão de mídia.
* **[!UICONTROL Indicador de reprodução]**: a posição atual da reprodução de mídia, em segundos.
* **[!UICONTROL Detalhes da sessão de mídia]**: Ao enviar um evento de início de mídia, os detalhes da sessão de mídia necessários devem ser especificados.
* **[!UICONTROL Detalhes do capítulo]**: nesta seção, você pode especificar os detalhes do capítulo ao enviar um evento de mídia de início de capítulo.
* **[!UICONTROL Detalhes do Advertising]**: ao enviar um evento `AdBreakStart`, você deve especificar os detalhes de publicidade necessários.
* **[!UICONTROL Detalhes do pod do Advertising]**: detalhes sobre o pod de publicidade ao enviar um evento `AdStart`.
* **[!UICONTROL Detalhes do erro]**: detalhes sobre o erro de reprodução que está sendo rastreado.
* **[!UICONTROL Detalhes da atualização de estado]**: o estado do player que está sendo atualizado.
* **[!UICONTROL Metadados personalizados]**: os metadados personalizados sobre o evento de mídia que está sendo rastreado.
* **[!UICONTROL Qualidade de experiência]**: a qualidade de mídia dos dados de experiência que estão sendo rastreados.

## Definir consentimento {#set-consent}

Após receber o consentimento do usuário, esse consentimento deve ser comunicado ao Adobe Experience Platform Web SDK usando o tipo de ação &quot;Definir consentimento&quot;. Atualmente, há suporte para dois tipos de padrões: &quot;Adobe&quot; e &quot;IAB TCF&quot;. Consulte [Suporte às preferências de consentimento do cliente](../../../../web-sdk/commands/setconsent.md). Ao usar a versão 2.0 do Adobe, somente um valor de elemento de dados é compatível. Será necessário criar um elemento de dados que resolva para o objeto de consentimento.

Nesta ação, você também recebe um campo opcional para incluir um Mapa de identidade, de modo que as identidades possam ser sincronizadas assim que o consentimento for recebido. A sincronização é útil quando o consentimento é configurado como &quot;Pendente&quot; ou &quot;Fora&quot;, pois a chamada de consentimento provavelmente é a primeira chamada a ser acionada.

## Atualizar variável {#update-variable}

Use esta ação para modificar um objeto XDM como resultado de um evento. Esta ação destina-se a criar um objeto que pode ser referenciado posteriormente de uma ação **[!UICONTROL Enviar evento]**, para registrar o objeto XDM do evento.

Para usar este tipo de ação, você deve ter definido um elemento de dados [variável](data-element-types.md#variable). Depois que você escolher um elemento de dados variável para modificar, será exibido um editor semelhante ao editor do elemento de dados [objeto XDM](data-element-types.md#xdm-object).

![](assets/update-variable.png)

O esquema XDM usado para o editor é o esquema selecionado no elemento de dados [!UICONTROL variável]. Você pode definir uma ou mais propriedades do objeto clicando em uma das propriedades na árvore à esquerda e modificando o valor à direita. Por exemplo, na captura de tela abaixo, a propriedade productionBy está sendo definida como o elemento de dados &quot;Produced by data element&quot;.

![](assets/update-variable-set-property.png)

Há algumas diferenças entre o editor na ação de atualização de variáveis e o editor no elemento de dados do objeto XDM. Primeiro, a ação atualizar variável tem um item de nível raiz rotulado como &quot;xdm&quot;. Se você clicar nesse item, poderá especificar um elemento de dados a ser usado para definir o objeto inteiro. Segundo, a ação de atualização da variável tem caixas de seleção para limpar os dados do objeto xdm. Clique em uma das propriedades à esquerda e marque a caixa de seleção à direita para limpar o valor. Isso limpará o valor atual antes de definir quaisquer valores na variável.

## Próximas etapas {#next-steps}

Depois de ler este artigo, você terá que entender melhor como configurar suas ações. Em seguida, leia sobre como [configurar seus tipos de elementos de dados](data-element-types.md).
