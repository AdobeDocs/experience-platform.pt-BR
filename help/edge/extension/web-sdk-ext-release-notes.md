---
title: Notas de versão da extensão do Adobe Experience Platform Web SDK
description: Extensão SDK da Web da Adobe Experience Platform no Adobe Experience Platform Launch
seo-description: Extensão SDK da Web da Adobe Experience Platform no Adobe Experience Platform Launch
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 78%

---

# Notas de versão da extensão do Adobe Experience Platform Web SDK

Este documento aborda as notas de versão da extensão Adobe Experience Platform Web SDK para Adobe Experience Platform Launch. Para obter as notas de versão mais recentes sobre o próprio SDK, consulte as [Notas de versão do SDK da Web da plataforma](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## 9 de março de 2020

### SDK da Web 2.4.0 da Adobe Experience Platform

Contém a versão 2.4.0 da biblioteca de SDK da Web da Adobe Experience Platform.

* Adição da caixa de seleção [&quot;descarregamento de documento&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) para Enviar interface do usuário de ação de evento.
* Adição de suporte para uma opção `out` quando [configurar o consentimento padrão](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), que descarta todos os eventos até que o consentimento seja recebido (a opção `pending` existente enfileira os eventos e os envia depois que o consentimento é recebido).
* Adição de uma dica de ferramenta ao campo de consentimento padrão.
* Adição de suporte para [Adobe Consent 2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Um erro melhor agora é exibido na interface do usuário do elemento de dados Objeto XDM se o token de acesso do usuário for inválido ou provisionado incorretamente.
* Correção de um erro de origem cruzada (que não afeta a operação da extensão) que era exibido no console do desenvolvedor do navegador ao visualizar um elemento de dados Objeto XDM.

## 4 de novembro de 2020

### SDK 2.3.0 da Web da Adobe Experience Platform

Contém a versão 2.3.0 da biblioteca de SDK da Web da Adobe Experience Platform.

#### Recursos

* Adição de suporte para o uso de um elemento de dados ao configurar o consentimento padrão.
* Adição da capacidade de pesquisar esquemas XDM com o tipo de elemento de dados Objeto XDM.
* Adição de clonagem de dados XDM no tipo de ação Enviar evento para garantir que todas as alterações subsequentes no objeto de dados XDM não serão refletidas na solicitação.

## 1 de outubro de 2020

### SDK 2.2.0 da Web da Adobe Experience Platform

#### Correções de erros

* Quando tentavam criar um objeto XDM a partir de esquemas da sandbox, os clientes tinham problemas de autenticação. A API que chama a Platform agora reconhece os ambientes, de modo que os usuários somente são apresentados aos esquemas que eles têm acesso para editar.

#### Recursos

* Ao usar o elemento de dados `identityMap`, os namespaces agora são pré-preenchidos em uma lista suspensa para que você não precise preenchê-los manualmente.
* A interface do usuário do elemento de dados `xdmObject` foi alterada. Na nova interface do usuário, você pode ver quais campos foram preenchidos sem precisar inserir cada item no objeto.


## 26 de agosto de 2020

### SDK 2.1.1 da Web da Adobe Experience Platform

#### Recursos

* Correção de um problema em que as sandboxes da Adobe Experience Platform na visualização de objeto XDM eram exibidas incorretamente. Se, ao usar essa versão da extensão, uma sandbox esperada não for exibida na lista, o usuário deve verificar com o administrador da Adobe Experience Platform se as permissões de acesso estão definidas corretamente.


## 5 de agosto de 2020

### SDK 2.1.0 da Web da Adobe Experience Platform

#### Recursos

* Nova alteração: remove a ação `syncIdentity` e oferece suporte à transmissão dessas IDs na ação `sendEvent`. Desative qualquer regra existente que use essa ação antes de atualizar a extensão.
* Atualizar para Alloy v. 2.1.0 ([Notas de versão](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html)).
* Suporte ao Padrão de consentimento IAB 2.0 na ação `setConsent`.
* Suporte à substituição da ID do conjunto de dados na ação `sendEvent`.
* Adiciona um novo Elemento de dados do tipo `IdentityMap`, que pode ser usado para preencher a entrada `identityMap` no Elemento de dados do objeto XDM (agora ativado) e na ação `setConsent`.
* Suporte à transmissão de um mapa de identidade na ação `setConsent`.
* Suporte à escolha de uma sandbox de plataforma no Elemento de dados do objeto XDM.


## 26 de maio de 2020

### SDK 1.0.0 da Web da Adobe Experience Platform

#### Recursos

* Suporte à seleção do ambiente no Serviço de configuração.


## 4 de maio de 2020

### SDK 0.1.2 da Web da Adobe Experience Platform

#### Recursos

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
* Ativar a depuração usando `_satellite` agora ativa a depuração no SDK da Web da Adobe Experience Platform.
* Adição de suporte para valores digitados no Objeto XDM: Booleanos, números e decimais.

## 16 de março de 2020

### SDK 0.0.10 da Web da Adobe Experience Platform

#### Recursos

* Os conceitos de aceitação e recusa foram combinados em `Consent` e foi adicionado um novo comando `setConsent`.
* Adição de um novo Elemento de dados do tipo `XDM Object` que permite o mapeamento de JavaScript/JSON para XDM.

## 18 de fevereiro de 2020

### SDK 0.0.7 da Web da Adobe Experience Platform

#### Recursos

* Remoção das opções idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled e cookieDestinationsEnabled.
* Adição de suporte a hifens no valor de opção edgeDomain.
* A solicitação feita durante a migração da ID é enviada para o endpoint demdex para melhorar a identificação entre domínios quando o cookie demdex não está definido.
* A solicitação feita durante a migração de ID sempre espera uma resposta para garantir que o cookie de identidade seja definido.
* Ao executar um comando inválido, uma lista de nomes de comando válidos será registrada no console.
* Adição de uma caixa de seleção para alternar o suporte a cookies de terceiros na extensão do Adobe Experience Platform Launch. Isso desativa chamadas com demdex.net.

## 20 de dezembro de 2019

### SDK 0.0.5 da Web da Adobe Experience Platform

#### Recursos

* Adicionar configurações do Rastreador de atividade à extensão do Platform Launch.
* Expor EventType e EventMergeId no comando do evento.
* Adicionar configuração onBeforeEventSend à extensão do Platform Launch.
* Adicionar configuração edgeBasePath à extensão do Platform Launch.

#### Atualização para Alloy v. 0.0.10, que inclui as seguintes alterações:

* Implementar o armazenamento no cliente: Estado e lógica de cookies movidos para o servidor.
* Expor EventType e EventMergeId no comando do evento.
* Usar sendBeacon para rastreamento de links diferentes dos links de saída.
* Trazer de volta as sincronizações de ID menos a verificação de expiração.
* comando setCustomerIds não confundindo ids em páginas não são SSL (http).
* Passar o domínio APEX para o servidor a ser usado ao definir o estado/cookies.
* Pegar o ECID na resposta usando um novo tipo de identificador.
* Remover padrões para configurações de Ativação e identidade.
* Renomear + mover opções de consulta para meta.
* Migração de ECID herdada.

#### Correções de erros

* No caso de um código de status inesperado, analisar e formatar o corpo da resposta para mensagem de erro.
* A execução do comando debug ou uso do alloy_debug é substituído pela configuração.

## 25 de novembro de 2019

### SDK da Web 0.0.3 da Adobe Experience Platform

#### Recursos

* Novos campos ID de Mesclagem e Tipo na ação Enviar evento. O ID de Mesclagem mapeia para o `xdm.eventMergeID` no esquema XDM e o Tipo mapeia para o `xdm.eventType` no esquema XDM.
* Tratamento e relatório de erros aprimorados
* Agora usa `sendBeacon` em todos os links

#### Correções de erros

* Correção de um problema em que a alternância da depuração por meio de um parâmetro de string de consulta ou do comando `debug` não persistia durante a sessão.

## 18 de novembro de 2019

### SDK da Web 0.0.2 da Adobe Experience Platform

#### Recursos

* Extensão iniciada.
* Suporte a ECID sem bibliotecas ou chamadas de rede adicionais.
* Suporte para aceitação.
* Suporte ao envio de XDM para a plataforma
* Suporte a domínio próprio.
* Coletar automaticamente o contexto do navegador.
* Fonte totalmente aberta ([extensão](https://github.com/adobe/reactor-extension-alloy), [SDK](https://github.com/adobe/reactor-extension-alloy)).
* Registro detalhado.
* Capacidade de ocultar erros na produção.
