---
title: Notas de versão da extensão SDK da Web da Adobe Experience Platform
description: Extensão de tag do SDK da Web da Adobe Experience Platform
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '1688'
ht-degree: 38%

---


# Notas de versão da extensão SDK da Web da Adobe Experience Platform

Este documento aborda as notas de versão da extensão de tag do SDK da Web da Adobe Experience Platform. Para obter as notas de versão mais recentes sobre o próprio SDK, consulte a [Notas de versão do SDK da Web da Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html?lang=pt-BR).

## Versão 2.19.0 - 21 de junho de 2023

* A variável **[!UICONTROL Variável]** elemento de dados e **[!UICONTROL Atualizar variável]** As ações da estão agora disponíveis em geral.

## Versão 2.18.0 - 18 de maio de 2023

* Contém a versão 2.17.0 do SDK da Web do Adobe Experience Platform.

## Versão 2.17.0 - 25 de abril de 2023

**Novos recursos**

* Contém a versão 2.16.0 do SDK da Web do Adobe Experience Platform.
* Suporte adicionado para [substituições de configuração da sequência de dados](../../../../datastreams/overrides.md).
* Adicionar aviso de desativação à `datasetId` opção no `sendEvent` comando.


**Correções e melhorias**

* Correção de um problema em que a rolagem no Safari fechava o seletor de sequência de dados.

## Versão 2.16.1 - 14 de abril de 2023

* Correção de um problema com elementos de dados Objeto XDM e Variável, em que não era possível selecionar um esquema de uma sandbox não padrão.

## Versão 2.16.0 - 30 de março de 2023

**Novos recursos**

* (Beta) Adicionado **[!UICONTROL Atualizar variável]** ação e **[!UICONTROL Variável]** elemento de dados.
* Adição de configuração para [`onBeforeLinkClickSend`](../../../../edge/fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend) função de retorno de chamada.

**Correções e melhorias**

* Correção de um problema que fazia com que os cliques em elementos em uma tag de âncora não funcionassem quando a variável **[!UICONTROL Redirecionar com identidade]** ação foi usada.
* Correção de um problema em que os elementos de dados do objeto XDM não funcionavam quando havia apenas um esquema presente.
* Contém a versão 2.15.0 do SDK da Web da Adobe Experience Platform.


## Versão 2.15.1 - 26 de janeiro de 2023

* Correção de um problema em que os usuários sem acesso a sequências de dados não podiam editar a configuração da extensão.
* Adição de suporte para superfícies no `sendEvent` ação.

Contém a versão 2.14.0 do SDK da Web do Adobe Experience Platform.


## Versão 2.14.1 - 13 de outubro de 2022

* Correção de um problema em que o SDK da Web não respeitava a ID do serviço de ID de Experience Cloud.

Contém a versão 2.13.1 da biblioteca do SDK da Web da Adobe Experience Platform.

## Versão 2.14.0 - 28 de setembro de 2022

* Adição de novo `targetMigrationEnabled` configuração que permite a migração completa de página por página.
* Adição de uma ação aplicar resposta para ativar implementações híbridas de cliente-servidor.
* Adição da opção de contexto de dicas do cliente de agente do usuário de alta entropia.

Contém a versão 2.13.0 da biblioteca do SDK da Web da Adobe Experience Platform.

## Versão 2.13.0 - 29 de junho de 2022

* Correção da ordem de classificação das propriedades numéricas no elemento de dados Objeto XDM, como eVars.

Contém a versão 2.12.0 da biblioteca do SDK da Web da Adobe Experience Platform.

## Versão 2.12.0 - 13 de junho de 2022

* Atualização do `identityMap` elemento de dados para preencher as opções de namespace com base nas sandboxes definidas pelas configurações de extensão.
* Adicionado **[!UICONTROL Redirecionar com identidade]** ação para permitir o compartilhamento de identidade entre domínios.
* Adição de links de documentação para a `sendEvent` ação.
* Atualização da biblioteca da interface do usuário do Espectro React.
* Várias melhorias na interface do usuário.

Contém a versão 2.11.0 da biblioteca do SDK da Web da Adobe Experience Platform.

## Versão 2.11.2 - 3 de maio de 2022

Contém a versão 2.10.1 da biblioteca do SDK da Web da Adobe Experience Platform.

## Versão 2.11.1 - 22 de abril de 2022

* Correção do erro do comando configure na versão 2.11.0.

Contém a versão 2.10.0 da biblioteca do SDK da Web da Adobe Experience Platform.

## Versão 2.11.0 - 22 de abril de 2022

* Aprimoramento do desempenho da interface do usuário de tags.
* Adicionar seletores de sandbox à configuração da extensão datastreams.

Contém a versão 2.10.0 da biblioteca do SDK da Web da Adobe Experience Platform.

## Versão 2.10.0 - 10 de março de 2022

* Atualize o trecho pré-ocultação disponível para cópia na página de configuração para funcionar com o editor atualizado do Adobe Target VEC.

Contém a versão 2.9.0 da biblioteca de SDK da Web da Adobe Experience Platform.

## Versão 2.9.0 - 19 de janeiro de 2022

Contém a versão 2.8.0 da biblioteca de SDK da Web da Adobe Experience Platform.

## Versão 2.8.0 - 26 de outubro de 2021

Contém a versão 2.7.0 da biblioteca de SDK da Web da Adobe Experience Platform.

* Informações adicionais da Experience Edge estão disponíveis no evento Enviar evento concluído, incluindo `inferences` e `destinations`. O formato dessas propriedades pode mudar, pois esses recursos estão sendo lançados como parte de uma versão beta. Para obter mais informações, consulte [Rastreamento de eventos.](../../../../edge/fundamentals/tracking-events.md)

## Versão 2.7.3 - 7 de setembro de 2021

Contém a versão 2.6.4 da biblioteca de SDK da Web da Adobe Experience Platform.

* Não há mais um aviso de desativação do `container.buildInfo.environment.`

## Versão 2.7.0 - 16 de agosto de 2021

Contém a versão 2.6.3 da biblioteca de SDK da Web da Adobe Experience Platform.

* Ao usar o tipo de elemento de dados Mapa de identidade, os identificadores cujas IDs resolvem para valores que não são cadeias de caracteres preenchidas agora são removidos automaticamente do mapa de identidade.
* Correção de um erro que ocorria ao tentar salvar um elemento de dados usando o tipo de elemento de dados Objeto XDM e nenhum esquema era selecionado.
* Tipografia da interface do usuário aprimorada.

## Versão 2.6.2 - 4 de agosto de 2021

Contém a versão 2.6.2 da biblioteca de SDK da Web da Adobe Experience Platform.

## Versão 2.6.1 - 29 de julho de 2021

Contém a versão 2.6.1 da biblioteca de SDK da Web da Adobe Experience Platform.

## Versão 2.6.0 - 27 de julho de 2021

Contém a versão 2.6.0 da biblioteca de SDK da Web da Adobe Experience Platform.

* Rótulos, descrições e mensagens de erro que usam o termo &quot;configuração de borda&quot; foram alterados para usar o termo &quot;sequência de dados&quot; para se alinharem à terminologia mais recente do Adobe Experience Platform.
* Na visualização de configuração de extensão, foi adicionado suporte para lidar com grandes números de datastreams e ambientes de datastream.
* Na visualização do elemento de dados Objeto XDM, foi adicionado suporte para lidar com grandes números de esquemas.
* Um tipo de evento Enviar evento concluído foi adicionado, que pode ser usado para executar uma regra depois que um evento é enviado ao servidor e uma resposta é recebida. Mais documentação estará disponível em breve.
* O tipo de evento Decisões recebidas foi descontinuado. Em vez disso, use o tipo de evento Enviar evento concluído.
* A interface do usuário e o tratamento de erros foram aprimorados.

## Versão 2.5.0 - 1 de junho de 2021

Contém a versão 2.5.0 da biblioteca de SDK da Web da Adobe Experience Platform.

* Adição de um `data` para a ação Enviar evento. A documentação futura descreverá como isso pode ser usado em determinados cenários.
* Na visualização do elemento de dados Objeto XDM, um problema foi corrigido em que um erro era lançado se o usuário tivesse acesso às sandboxes da Adobe Experience Platform, mas não à sandbox configurada como padrão para a organização.
* Na visualização do elemento de dados Objeto XDM, um problema foi corrigido em que um campo de esquema obrigatório era considerado inválido mesmo se o objeto pai não contivesse valores.

## Versão 2.4.0 - 9 de março de 2021

Contém a versão 2.4.0 da biblioteca de SDK da Web da Adobe Experience Platform.

* Adicionado [&quot;descarregamento de documento&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) para Enviar a interface de ação de Evento.
* Adição de suporte para um `out` opção quando [configuração do consentimento padrão](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) que elimina todos os eventos até que o consentimento seja recebido (o evento `pending` opção enfileira eventos e os envia quando o consentimento é recebido).
* Adição de uma dica de ferramenta ao campo de consentimento padrão.
* Suporte adicionado para [Adobe Consent 2.0 padrão](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Um erro melhor agora é exibido na interface do usuário do elemento de dados Objeto XDM se o token de acesso do usuário for inválido ou provisionado incorretamente.
* Correção de um erro entre origens (que não afeta a operação da extensão) que aparecia no console do desenvolvedor do navegador ao visualizar um elemento de dados do Objeto XDM.

## Versão 2.3.0 - 4 de novembro de 2020

Contém a versão 2.3.0 da biblioteca de SDK da Web da Adobe Experience Platform.

* Adição de suporte para o uso de um elemento de dados ao configurar o consentimento padrão.
* Adição da capacidade de pesquisar esquemas XDM com o tipo de elemento de dados Objeto XDM.
* Adição de clonagem de dados XDM no tipo de ação Enviar evento para garantir que todas as alterações subsequentes no objeto de dados XDM não serão refletidas na solicitação.

## Versão 2.2.0 - 1 de outubro de 2020

* Quando tentavam criar um objeto XDM a partir de esquemas da sandbox, os clientes tinham problemas de autenticação. A API que chama a Platform agora reconhece os ambientes, de modo que os usuários somente são apresentados aos esquemas que eles têm acesso para editar.
* Ao usar o `identityMap` elemento de dados, os namespaces agora são pré-preenchidos em uma lista suspensa para que você não precise preenchê-los manualmente.
* A interface do usuário do elemento de dados `xdmObject` foi alterada. Na nova interface do usuário, você pode ver quais campos foram preenchidos sem precisar inserir cada item no objeto.

## Versão 2.1.1 - 26 de agosto de 2020

* Correção de um problema em que as sandboxes da Adobe Experience Platform na visualização de objeto XDM eram exibidas incorretamente. Se, ao usar essa versão da extensão, uma sandbox esperada não for exibida na lista, o usuário deve verificar com o administrador da Adobe Experience Platform se as permissões de acesso estão definidas corretamente.

## Versão 2.1.0 - 5 de agosto de 2020

* Nova alteração: remove a ação `syncIdentity` e oferece suporte à transmissão dessas IDs na ação `sendEvent`. Desative qualquer regra existente que use essa ação antes de atualizar a extensão.
* Atualizar para Alloy v. 2.1.0 ([Notas de versão](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html?lang=pt-BR)).
* Suporte ao Padrão de consentimento IAB 2.0 na ação `setConsent`.
* Suporte à substituição da ID do conjunto de dados na ação `sendEvent`.
* Adiciona um novo Elemento de dados do tipo `IdentityMap`, que pode ser usado para preencher a entrada `identityMap` no Elemento de dados do objeto XDM (agora ativado) e na ação `setConsent`.
* Suporte à transmissão de um mapa de identidade na ação `setConsent`.
* Suporte à escolha de uma sandbox da Platform no Elemento de dados do objeto XDM.

## Versão 1.0.0 - 26 de maio de 2020

* Suporte à seleção do ambiente no Serviço de configuração.

## Versão 0.1.2 - 4 de maio de 2020

* `configId` renomeado para `edgeConfigId`.
* `viewStart` renomeado para `renderDecisions`, definido como falso por padrão. Se definido como verdadeiro, as ofertas de personalização serão buscadas e renderizadas automaticamente.
* Alterações relacionadas com `Get Decisions`:
   * O comando `getDecisions` foi removido.
   * Adição de uma opção `scopes` ao comando `sendEvent`. As decisões são devolvidas na promessa `sendEvent` resolvida.
   * Adição de um escopo `__view__` integrado que resultará na reversão de ofertas de toda a página/visualização. (Ofertas VEC no Target, por exemplo.)
Essas decisões retornam do comando `sendEvent` somente se `renderDecisions` estiver definido como falso.
   * Adição de um evento `Decisions Received`, que é acionado quando as decisões são disponibilizadas.
* Várias notificações de personalização combinadas em uma única chamada de servidor.
* Correção do problema na ID de mesclagem de evento em que ele era redefinido sempre que o elemento de dados era referenciado.
* A ação `setCustomerIds` foi renomeada para `syncIdentity`.
* Adição de um comando `getIdentity`. Isso pode ser consumido somente por código personalizado por enquanto.
* Ativar a depuração usando `_satellite` agora ativa a depuração no Adobe Experience Platform Web SDK.
* Adição de suporte para valores digitados no Objeto XDM: Booleanos, números e decimais.

## Versão 0.0.10 - 16 de março de 2020

* Os conceitos de aceitação e recusa foram combinados em `Consent` e foi adicionado um novo comando `setConsent`.
* Adição de um novo Elemento de dados do tipo `XDM Object` que permite o mapeamento de JavaScript/JSON para XDM.

## Versão 0.0.7 - 18 de fevereiro de 2020

* Remoção das opções idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled e cookieDestinationsEnabled.
* Adição de suporte a hifens no valor de opção edgeDomain.
* A solicitação feita durante a migração da ID é enviada para o endpoint demdex para melhorar a identificação entre domínios quando o cookie demdex não está definido.
* A solicitação feita durante a migração de ID sempre espera uma resposta para garantir que o cookie de identidade seja definido.
* Ao executar um comando inválido, uma lista de nomes de comando válidos será registrada no console.
* Adição de uma caixa de seleção para alternar o suporte a cookies de terceiros na extensão de tag. Isso desativa chamadas com demdex.net.

## Versão 0.0.5 - 20 de dezembro de 2019

* Adicionar configurações do Rastreador de atividade à extensão de tag
* Expor EventType e EventMergeId no comando do evento.
* Adicionar configuração onBeforeEventSend à extensão de tag
* Adicionar configuração edgeBasePath à extensão de tag

## Versão 0.0.3 - 25 de novembro de 2019

* Novos campos ID de Mesclagem e Tipo na ação Enviar evento. O ID de Mesclagem mapeia para o `xdm.eventMergeID` no esquema XDM e o Tipo mapeia para o `xdm.eventType` no esquema XDM.

## Versão 0.0.2 - 18 de novembro de 2019

* Versão inicial
