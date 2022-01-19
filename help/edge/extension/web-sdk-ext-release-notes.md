---
title: Notas de versão da extensão do Adobe Experience Platform Web SDK
description: Extensão de tag do Adobe Experience Platform Web SDK
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: a768cde86215ed9aad19e45362c6185276456703
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 48%

---

# Notas de versão da extensão do Adobe Experience Platform Web SDK

Este documento aborda as notas de versão da extensão de tag Adobe Experience Platform Web SDK. Para obter as notas de versão mais recentes sobre o próprio SDK, consulte o [Notas de versão do SDK da Web da plataforma](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## Versão 2.9.0 - 19 de janeiro de 2022

Contém a versão 2.8.0 da biblioteca de SDK da Web da Adobe Experience Platform.

## Versão 2.8.0 - 26 de outubro de 2021

Contém a versão 2.7.0 da biblioteca de SDK da Web da Adobe Experience Platform.

* Informações adicionais do Experience Edge estão disponíveis no evento Enviar evento concluído, incluindo `inferences` e `destinations`. O formato dessas propriedades pode mudar, pois esses recursos estão sendo lançados como parte de um Beta. Para obter mais informações, consulte [Rastreamento de eventos.](../fundamentals/tracking-events.md)

## Versão 2.7.3 - 7 de setembro de 2021

Contém a versão 2.6.4 da biblioteca de SDK da Web da Adobe Experience Platform.

* Não há mais um aviso de desativação para `container.buildInfo.environment.`

## Versão 2.7.0 - 16 de agosto de 2021

Contém a versão 2.6.3 da biblioteca de SDK da Web da Adobe Experience Platform.

* Ao usar o tipo de elemento de dados do Mapa de identidade , os identificadores cujas IDs são resolvidas para valores que não são strings preenchidas são automaticamente removidos do mapa de identidade.
* Correção de um erro que ocorria ao tentar salvar um elemento de dados usando o tipo de elemento de dados Objeto XDM e nenhum esquema era selecionado.
* Tipografia da interface do usuário aprimorada.

## Versão 2.6.2 - 4 de agosto de 2021

Contém a versão 2.6.2 da biblioteca de SDK da Web da Adobe Experience Platform.

## Versão 2.6.1 - 29 de julho de 2021

Contém a versão 2.6.1 da biblioteca de SDK da Web da Adobe Experience Platform.

## Versão 2.6.0 - 27 de julho de 2021

Contém a versão 2.6.0 da biblioteca de SDK da Web da Adobe Experience Platform.

* Rótulos, descrições e mensagens de erro usando o termo &quot;configuração de borda&quot; foram alteradas para usar o termo &quot;datastream&quot; para alinhar-se à terminologia mais recente do Adobe Experience Platform.
* Na visualização de configuração de extensão, foi adicionado suporte para lidar com um grande número de conjuntos de dados e ambientes de fluxo de dados.
* Na exibição do elemento de dados Objeto XDM, foi adicionado suporte para lidar com um grande número de esquemas.
* Um tipo de evento Enviar evento concluído foi adicionado, que pode ser usado para executar uma regra depois que um evento for enviado ao servidor e uma resposta recebida. Mais documentação estará disponível em breve.
* O tipo de evento Decisões recebidas foi substituído. Em vez disso, use o tipo de evento Enviar evento concluído .
* A interface do usuário e o tratamento de erros geralmente foram aprimorados.

## Versão 2.5.0 - 1 de junho de 2021

Contém a versão 2.5.0 da biblioteca de SDK da Web da Adobe Experience Platform.

* Adicionado um `data` para a ação Enviar evento . A documentação futura descreverá como isso pode ser usado em determinados cenários.
* Na exibição do elemento de dados Objeto XDM, foi corrigido um problema em que um erro era lançado se o usuário tivesse acesso às sandboxes da Adobe Experience Platform, mas não à sandbox configurada como padrão para a organização.
* Na exibição do elemento de dados Objeto XDM, foi corrigido um problema em que um campo de esquema obrigatório era considerado inválido mesmo se o objeto pai não tivesse valores.

## Versão 2.4.0 - 9 de março de 2021

Contém a versão 2.4.0 da biblioteca de SDK da Web da Adobe Experience Platform.

* Adicionado [&quot;descarga de documentos&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) caixa de seleção para Enviar interface do usuário de ação do evento .
* Suporte adicionado para um `out` opção ao [configuração do consentimento padrão](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) que elimina todos os eventos até que o consentimento seja recebido (o `pending` ). Enfileira eventos e os envia após o recebimento do consentimento.
* Adição de uma dica de ferramenta ao campo de consentimento padrão.
* Suporte adicionado para [Adobe 2.0](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Um erro melhor agora é exibido na interface do usuário do elemento de dados Objeto XDM se o token de acesso do usuário for inválido ou provisionado incorretamente.
* Correção de um erro de origem cruzada (que não afeta a operação da extensão) que era exibido no console do desenvolvedor do navegador ao visualizar um elemento de dados Objeto XDM.

## Versão 2.3.0 - 4 de novembro de 2020

Contém a versão 2.3.0 da biblioteca de SDK da Web da Adobe Experience Platform.

* Adição de suporte para o uso de um elemento de dados ao configurar o consentimento padrão.
* Adição da capacidade de pesquisar esquemas XDM com o tipo de elemento de dados Objeto XDM.
* Adição de clonagem de dados XDM no tipo de ação Enviar evento para garantir que todas as alterações subsequentes no objeto de dados XDM não serão refletidas na solicitação.

## Versão 2.2.0 - 1 de outubro de 2020

* Quando tentavam criar um objeto XDM a partir de esquemas da sandbox, os clientes tinham problemas de autenticação. A API que chama a Platform agora reconhece os ambientes, de modo que os usuários somente são apresentados aos esquemas que eles têm acesso para editar.
* Ao usar a variável `identityMap` elemento de dados, os namespaces agora são preenchidos previamente em uma lista suspensa para que você não precise preenchê-los manualmente.
* A interface do usuário do elemento de dados `xdmObject` foi alterada. Na nova interface do usuário, você pode ver quais campos foram preenchidos sem precisar inserir cada item no objeto.

## Versão 2.1.1 - 26 de agosto de 2020

* Correção de um problema em que as sandboxes da Adobe Experience Platform na visualização de objeto XDM eram exibidas incorretamente. Se, ao usar essa versão da extensão, uma sandbox esperada não for exibida na lista, o usuário deve verificar com o administrador da Adobe Experience Platform se as permissões de acesso estão definidas corretamente.

## Versão 2.1.0 - 5 de agosto de 2020

* Nova alteração: remove a ação `syncIdentity` e oferece suporte à transmissão dessas IDs na ação `sendEvent`. Desative qualquer regra existente que use essa ação antes de atualizar a extensão.
* Atualizar para Alloy v. 2.1.0 ([Notas de versão](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html)).
* Suporte ao Padrão de consentimento IAB 2.0 na ação `setConsent`.
* Suporte à substituição da ID do conjunto de dados na ação `sendEvent`.
* Adiciona um novo Elemento de dados do tipo `IdentityMap`, que pode ser usado para preencher a entrada `identityMap` no Elemento de dados do objeto XDM (agora ativado) e na ação `setConsent`.
* Suporte à transmissão de um mapa de identidade na ação `setConsent`.
* Suporte à escolha de uma sandbox de plataforma no Elemento de dados do objeto XDM.

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
* Ativação da depuração usando `_satellite` agora ativa a depuração no Adobe Experience Platform Web SDK.
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
