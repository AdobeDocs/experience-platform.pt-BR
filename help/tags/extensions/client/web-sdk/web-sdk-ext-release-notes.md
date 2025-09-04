---
title: Notas de versão da extensão para Adobe Experience Platform Web SDK
description: Extensão de tag do Adobe Experience Platform Web SDK
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 1cc62ee8c87ff2c1c1d55db2e462d485289120ed
workflow-type: tm+mt
source-wordcount: '2947'
ht-degree: 26%

---


# Notas de versão da extensão do Web SDK

Este documento aborda as notas de versão da extensão de tag do Adobe Experience Platform Web SDK. Para obter as notas de versão mais recentes do próprio SDK, consulte as [notas de versão do Experience Platform Web SDK](/help/web-sdk/release-notes.md).

## Versão 2.32.0 - 4 de setembro de 2025

**Novos recursos**

- Contém a [versão 2.29.0](../../../../web-sdk/release-notes.md#2-29-0) do Adobe Experience Platform Web SDK.
- Adição de suporte para o Adobe Advertising como um novo componente de build personalizado. Configure na configuração da extensão e em enviar chamadas de evento.
- Adição de suporte para gravar detalhes da assinatura push no Perfil. Isso é feito por meio de uma nova ação, &quot;Detalhes da assinatura por push&quot;

**Correções e melhorias**

- Edição de elemento de dados XDM aprimorada quando esquemas ou sandboxes não estão disponíveis. Agora é possível editar elementos de dados de Objeto e Variável XDM mesmo quando seus esquemas referenciados não puderem ser encontrados ou quando as sandboxes estiverem inacessíveis. Isso soluciona problemas que normalmente ocorrem durante as migrações da organização para novos data centers, em que as IDs de esquema podem mudar e que anteriormente faziam com que as interfaces de edição exibissem erros e se tornassem inutilizáveis.

## Versão 2.31.1 - sexta-feira, 31 de julho de 2025

- Correção de um problema que impedia a execução de compilações personalizadas.
- Contém a [versão 2.28.1](../../../../web-sdk/release-notes.md#2-28-1) do Adobe Experience Platform Web SDK.

## Versão 2.31.0 - sexta-feira, 24 de julho de 2025

**Novos recursos**

- Contém a [versão 2.28.0](../../../../web-sdk/release-notes.md#2-28-0) do Adobe Experience Platform Web SDK.

**Correções e melhorias**

- Correção de um problema em que um erro é lançado quando uma substituição de sequência de dados é ativada por meio de um elemento de dados.
- Correção de um problema em que substituições vazias de `idSyncContainerId` geravam um erro.
- Ao resolver elementos de dados de mídia, o objeto de evento agora é incluído.

**Problemas conhecidos**

- Após o lançamento da v2.31.0, um problema foi identificado com o processo [build de componentes personalizados](/help/web-sdk/install/create-custom-build.md). Enquanto as builds personalizadas continuam a operar, todos os componentes estão incluídos atualmente na build, resultando em um pacote de tamanho normal independentemente da seleção de componentes. Uma correção para esse problema está sendo desenvolvida. Se você depender da seleção de componentes personalizados para minimizar o tamanho da criação, é recomendável aguardar uma versão futura.

## Versão 2.30.1 - quarta-feira, 27 de maio de 2025

**Correções e melhorias**

- Correção de um problema em que a exibição da variável de atualização falhava quando uma organização não tinha uma sandbox padrão definida.

## Versão 2.30.0 - quinta-feira, 21 de maio de 2025

**Novos recursos**

- Agora você pode especificar um elemento de dados ao ativar cookies de terceiros.
- Adição de botões de limpeza nos campos de código.
- Contém a [versão 2.27.0](../../../../web-sdk/release-notes.md#2-27-0) do Adobe Experience Platform Web SDK.

**Correções e melhorias**

- Validação adicionada para impedir a configuração `onBeforeLinkClickSend` quando o agrupamento de eventos está habilitado.

## Versão 2.29.1 - sexta-feira, 8 de maio de 2025

**Correções e melhorias**

- Correção de um problema em que as configurações não eram salvas ao clicar imediatamente em &quot;salvar&quot; após a edição.

## Versão 2.29.0 - 5 de março de 2025

**Novos recursos**

- Agora é possível criar builds personalizadas do Web SDK e escolher os componentes necessários na interface do usuário da extensão de tag. Isso pode resultar em builds menores, excluindo componentes não usados. Consulte a documentação sobre [criação de uma compilação personalizada do Web SDK](web-sdk-extension-configuration.md#custom-build).
- Contém a [versão 2.26.0](../../../../web-sdk/release-notes.md#2-26-0) do Adobe Experience Platform Web SDK.

**Correções e melhorias**

- Foi adicionada uma manipulação adequada de elementos de dados ausentes nas ações [atualizar variável](action-types.md#update-variable). Anteriormente, editar uma ação de atualização de variável com um elemento de dados ausente mostrava uma mensagem de erro. Agora é possível escolher um elemento de dados diferente e todas as configurações da ação de atualização de variável ainda serão aplicadas. Os elementos de dados podem estar ausentes se forem excluídos ou se uma propriedade Tags for duplicada.
- Adicionado suporte para abrir uma nova guia com a ação [redirecionar com identidade](action-types.md#redirect-with-identity). Agora, ao usar a ação, o atributo `target` da marca de âncora é usado ao redirecionar o navegador.
- Correção de um problema em que o Adobe Audience Manager não podia ser desativado nas substituições de configuração.

## Versão 2.28.0 - sexta-feira, 23 de janeiro de 2025

**Correções e melhorias**

- Correção de um problema em que as substituições do Contêiner de sincronização de ID não podiam ser definidas sem a ativação do Audience Manager.
- Correção de um problema em que as substituições de configuração da sequência de dados eram desabilitadas ao atualizar para a versão mais recente.
- Correção de um problema em que os usuários não conseguiam salvar as configurações da coleção de cliques automáticos do Target.

**Novos recursos**

- Adição de um novo recurso para alternar entre nomes técnicos e nomes de exibição no Objeto XDM.
- Contém a [versão 2.25.0](../../../../web-sdk/release-notes.md#2-25-0) do Adobe Experience Platform Web SDK.

## Versão 2.27.0 - sexta-feira, 31 de outubro de 2024

**Novos recursos**

- [Substituições de sequência de dados](../web-sdk/web-sdk-extension-configuration.md#datastream-overrides) agora inclui configurações para desabilitar soluções da Experience Cloud e serviços da Adobe Experience Platform.
- Agora você pode criar [substituições de sequência de dados](../web-sdk/web-sdk-extension-configuration.md) para sessões de mídia.

Contém a versão 2.24.0 do Adobe Experience Platform Web SDK.

## Versão 2.26.1 - 19 de setembro de 2024

**Correções e melhorias**

- Correção de um problema em que os cookies não eram gravados corretamente ao executar o Web SDK localmente.

Contém a versão 2.23.0 do Adobe Experience Platform Web SDK.

## Versão 2.26.0 - 22 de agosto de 2024

**Novos recursos**

- Adição do evento gancho de monitoramento `triggered`.
- [Eventos guiados](action-types.md#instance), [Solicitar personalização padrão](action-types.md#personalization), [Assinar itens do conjunto de regras](event-types.md#subscribe-ruleset-items) e [avaliar conjuntos de regras](action-types.md#evaluate-rulesets) agora estão disponíveis para o público geral.

**Correções e melhorias**

- Correção de um problema em que elementos de dados variáveis duplicados podiam se substituir.
- Ao usar o evento guiado [Solicitar personalização padrão](action-types.md#personalization), as decisões de personalização visual agora são habilitadas automaticamente.

Contém a versão 2.22.0 do Adobe Experience Platform Web SDK.

## Versão 2.25.0 - sexta-feira, 18 de julho de 2024

**Novos recursos**

- Adição de suporte para personalização de rastreamento automático no Adobe Journey Optimizer.
- Introdução de novas configurações para gerenciar a coleção de cliques aprimorada.

Contém a versão 2.21.1 do Adobe Experience Platform Web SDK.

## Versão 2.24.0 - quinta-feira, 5 de junho de 2024

**Correções e melhorias**

- Correção de um erro que ocorria ao modificar a configuração da extensão quando as substituições de configuração eram definidas.
- Permite a configuração de valores vazios para intervalos de ping de coleção de mídia.
- Correção de um erro que ocorria ao modificar uma ação de atualização de variável.
- Permitir a redefinição do contêiner de sincronização de ID nas substituições de configuração.

Contém a versão 2.20.0 do Adobe Experience Platform Web SDK.

## Versão 2.23.1 - quarta-feira, 28 de maio de 2024

**Novos recursos**

- Adicionado suporte para o componente [`Streaming Media Collection`](web-sdk-extension-configuration.md#streaming-media) na configuração de extensão.
- Adição da ação [`Send Media Event`](action-types.md#send-media-event) para a funcionalidade [!DNL Streaming Media Collection].
- Adição do elemento de dados [`Media: Quality of Experience`](data-element-types.md#quality-experience) para a funcionalidade [!DNL Streaming Media Collection].

Contém a versão 2.20.0 do Adobe Experience Platform Web SDK.

**Correções e melhorias**

- Correção de um erro que ocorria ao pesquisar elementos de dados na ação [Atualizar variável](action-types.md#update-variable).
- Removidos os tipos de evento [!UICONTROL Mídia] dos tipos de evento sugeridos para serem usados na ação `sendEvent`.

## Versão 2.22.0 - sábado, 3 de maio de 2024

**Novos recursos**

- Estenda o elemento de dados variável para suportar objetos de dados.
- A ação Atualizar variável agora é compatível com a modificação de dados de passagem do Adobe Analytics, Adobe Audience Manager e Adobe Target.

Contém a versão 2.19.2 do Adobe Experience Platform Web SDK.

## Versão 2.21.4 - quinta-feira, 10 de janeiro de 2024

**Correções e melhorias**

- Correção de um problema em que salvar as Substituições de configuração sem todos os três ambientes definidos travaria a interface do usuário da extensão.
- Correção de um problema em que a caixa de seleção limpar raiz do valor existente não era preenchida ao editar uma ação de atualização de variável.

Contém a versão 2.19.2 do Adobe Experience Platform Web SDK.

## Versão 2.21.3 - sábado, 10 de novembro de 2023

Contém a versão 2.19.1 do Adobe Experience Platform Web SDK.

**Correções e melhorias**

- Correção de um problema em que a matriz de apresentações disponível em `Send event complete` eventos estava sempre vazia.

## Versão 2.21.2 - quinta-feira, 1 de novembro de 2023

**Novos recursos**

- Adicionada a opção `Request default personalization` para enviar ação de evento.
- Adição de suporte para eventos na parte superior e inferior da página na ação enviar evento.
- Adição da ação `Apply propositions`.
- Adição da ação `Evaluate rulesets` e do evento `Subscribe ruleset items` para mensagens no aplicativo.
- Adicionado `Decision context` para enviar ação de evento.

**Correções e melhorias**

- Contém a versão 2.19.0 do Adobe Experience Platform Web SDK.

## Versão 2.20.3 - 8 de agosto de 2023

**Correções e melhorias**

- Correção de um problema em que os elementos de dados não podiam ser salvos no campo de substituição da ID do contêiner de sincronização de ID.

## Versão 2.20.1 - 3 de agosto de 2023

**Correções e melhorias**

- Aprimorada a validação das configurações salvas de substituição de fluxo de dados.

## Versão 2.20.0 - terça-feira, 31 de julho de 2023

**Novos recursos**

- Adicionado suporte para [substituições por comando da ID de sequência de dados](../../../../datastreams/overrides.md).

**Correções e melhorias**

- `edgeConfigId` obsoleto em favor de `datastreamId` na configuração do SDK.
- Várias melhorias na experiência do usuário para a configuração da sequência de dados substitui a interface do usuário.

## Versão 2.19.0 - quinta-feira, 21 de junho de 2023

- O elemento de dados **[!UICONTROL Variável]** e as ações **[!UICONTROL Atualizar Variável]** agora estão disponíveis para o público geral.

## Versão 2.18.0 - sexta-feira, 18 de maio de 2023

- Contém a versão 2.17.0 do Adobe Experience Platform Web SDK.

## Versão 2.17.0 - 25 de abril de 2023

**Novos recursos**

- Contém a versão 2.16.0 do Adobe Experience Platform Web SDK.
- Adicionado suporte para [substituições de configuração de sequência de dados](/help/datastreams/overrides.md).
- Adicione aviso de descontinuação à opção `datasetId` no comando `sendEvent`.

**Correções e melhorias**

- Correção de um problema em que a rolagem no Safari fechava o seletor de sequência de dados.

## Versão 2.16.1 - 14 de abril de 2023

- Correção de um problema com elementos de dados Objeto XDM e Variável, em que não era possível selecionar um esquema de uma sandbox não padrão.

## Versão 2.16.0 - 30 de março de 2023

**Novos recursos**

- (Beta) Adição da ação **[!UICONTROL Atualizar variável]** e do elemento de dados **[!UICONTROL Variável]**.
- Adicionada configuração para a função de retorno de chamada [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md).

**Correções e melhorias**

- Correção de um problema que fazia com que os cliques em elementos em uma tag de âncora não funcionassem quando a ação **[!UICONTROL Redirecionar com identidade]** era usada.
- Correção de um problema em que os elementos de dados do objeto XDM não funcionavam quando havia apenas um esquema presente.
- Contém a versão 2.15.0 do Adobe Experience Platform Web SDK.

## Versão 2.15.1 - sexta-feira, 26 de janeiro de 2023

- Correção de um problema em que os usuários sem acesso a sequências de dados não podiam editar a configuração da extensão.
- Adicionado suporte para superfícies na ação `sendEvent`.

Contém a versão 2.14.0 do Adobe Experience Platform Web SDK.

## Versão 2.14.1 - sexta-feira, 13 de outubro de 2022

- Correção de um problema em que o Web SDK não respeitava a ID do serviço da Experience Cloud ID.

Contém a versão 2.13.1 da Biblioteca Adobe Experience Platform Web SDK.

## Versão 2.14.0 - 28 de setembro de 2022

- Adição de uma nova configuração `targetMigrationEnabled` que permite a migração completa de página por página.
- Adição de uma ação aplicar resposta para ativar implementações híbridas de cliente-servidor.
- Adição da opção de contexto de dicas do cliente de agente do usuário de alta entropia.

Contém a versão 2.13.0 da Biblioteca Adobe Experience Platform Web SDK.

## Versão 2.13.0 - quinta-feira, 29 de junho de 2022

- Correção da ordem de classificação das propriedades numéricas no elemento de dados Objeto XDM, como eVars.

Contém a versão 2.12.0 da Biblioteca Adobe Experience Platform Web SDK.

## Versão 2.12.0 - terça-feira, 13 de junho de 2022

- Elemento de dados `identityMap` atualizado para preencher as opções de namespace com base nas sandboxes definidas pelas configurações de extensão.
- Adição da ação **[!UICONTROL Redirecionar com identidade]** para permitir o compartilhamento de identidade entre domínios.
- Adicionados links de documentação à ação `sendEvent`.
- Atualização da biblioteca da interface do usuário do Espectro React.
- Várias melhorias na interface do usuário.

Contém a versão 2.11.0 da Biblioteca Adobe Experience Platform Web SDK.

## Versão 2.11.2 - quarta-feira, 3 de maio de 2022

Contém a versão 2.10.1 da Biblioteca Adobe Experience Platform Web SDK.

## Versão 2.11.1 - 22 de abril de 2022

- Correção do erro do comando configure na versão 2.11.0.

Contém a versão 2.10.0 da Biblioteca Adobe Experience Platform Web SDK.

## Versão 2.11.0 - 22 de abril de 2022

- Aprimoramento do desempenho da interface do usuário de tags.
- Adicionar seletores de sandbox à configuração da extensão datastreams.

Contém a versão 2.10.0 da Biblioteca Adobe Experience Platform Web SDK.

## Versão 2.10.0 - 10 de março de 2022

- Atualize o trecho pré-ocultação disponível para cópia na página de configuração para funcionar com o editor atualizado do Adobe Target VEC.

Contém a versão 2.9.0 da biblioteca de SDK da Web da Adobe Experience Platform.

## Versão 2.9.0 - quinta-feira, 19 de janeiro de 2022

Contém a versão 2.8.0 da biblioteca de SDK da Web da Adobe Experience Platform.

## Versão 2.8.0 - quarta-feira, 26 de outubro de 2021

Contém a versão 2.7.0 da biblioteca de SDK da Web da Adobe Experience Platform.

- Informações adicionais da Edge Network estão disponíveis no evento Enviar evento Concluído, incluindo `inferences` e `destinations`. O formato dessas propriedades pode mudar, pois esses recursos estão sendo lançados como parte de uma Beta.

## Versão 2.7.3 - 7 de setembro de 2021

Contém a versão 2.6.4 da biblioteca de SDK da Web da Adobe Experience Platform.

- Não há mais um aviso de desativação para `container.buildInfo.environment.`

## Versão 2.7.0 - 16 de agosto de 2021

Contém a versão 2.6.3 da biblioteca de SDK da Web da Adobe Experience Platform.

- Ao usar o tipo de elemento de dados Mapa de identidade, os identificadores cujas IDs resolvem para valores que não são cadeias de caracteres preenchidas agora são removidos automaticamente do mapa de identidade.
- Correção de um erro que ocorria ao tentar salvar um elemento de dados usando o tipo de elemento de dados Objeto XDM e nenhum esquema era selecionado.
- Tipografia da interface do usuário aprimorada.

## Versão 2.6.2 - 4 de agosto de 2021

Contém a versão 2.6.2 da biblioteca de SDK da Web da Adobe Experience Platform.

## Versão 2.6.1 - 29 de julho de 2021

Contém a versão 2.6.1 da biblioteca de SDK da Web da Adobe Experience Platform.

## Versão 2.6.0 - quarta-feira, 27 de julho de 2021

Contém a versão 2.6.0 da biblioteca de SDK da Web da Adobe Experience Platform.

- Rótulos, descrições e mensagens de erro que usam o termo &quot;configuração de borda&quot; foram alterados para usar o termo &quot;sequência de dados&quot; para se alinharem à terminologia mais recente do Adobe Experience Platform.
- Na visualização de configuração de extensão, foi adicionado suporte para lidar com grandes números de datastreams e ambientes de datastream.
- Na visualização do elemento de dados Objeto XDM, foi adicionado suporte para lidar com grandes números de esquemas.
- Um tipo de evento Enviar evento concluído foi adicionado, que pode ser usado para executar uma regra depois que um evento é enviado ao servidor e uma resposta é recebida. Mais documentação estará disponível em breve.
- O tipo de evento Decisões recebidas foi descontinuado. Em vez disso, use o tipo de evento Enviar evento concluído.
- A interface do usuário e o tratamento de erros foram aprimorados.

## Versão 2.5.0 - quarta-feira, 1 de junho de 2021

Contém a versão 2.5.0 da biblioteca de SDK da Web da Adobe Experience Platform.

- Adição de um campo `data` à ação Enviar evento. A documentação futura descreverá como isso pode ser usado em determinados cenários.
- Na visualização do elemento de dados Objeto XDM, um problema foi corrigido em que um erro era lançado se o usuário tivesse acesso às sandboxes da Adobe Experience Platform, mas não à sandbox configurada como padrão para a organização.
- Na visualização do elemento de dados Objeto XDM, um problema foi corrigido em que um campo de esquema obrigatório era considerado inválido mesmo se o objeto pai não contivesse valores.

## Versão 2.4.0 - 9 de março de 2021

Contém a versão 2.4.0 da biblioteca de SDK da Web da Adobe Experience Platform.

- Adicionada a caixa de seleção [&quot;Descarregamento de documento&quot;](/help/web-sdk/commands/sendevent/documentunloading.md) para Enviar interface de ação de evento.
- Adicionado suporte para uma opção `out` ao [configurar o consentimento padrão](/help/web-sdk/commands/configure/defaultconsent.md), que descarta todos os eventos até que o consentimento seja recebido (a opção `pending` existente enfileira eventos e os envia quando o consentimento é recebido).
- Adição de uma dica de ferramenta ao campo de consentimento padrão.
- Adição de suporte para o padrão Consentimento 2.0 da Adobe ao usar o comando [`setConsent`](/help/web-sdk/commands/setconsent.md).
- Um erro melhor agora é exibido na interface do usuário do elemento de dados Objeto XDM se o token de acesso do usuário for inválido ou provisionado incorretamente.
- Correção de um erro entre origens (que não afeta a operação da extensão) que aparecia no console do desenvolvedor do navegador ao visualizar um elemento de dados do Objeto XDM.

## Versão 2.3.0 - quinta-feira, 4 de novembro de 2020

Contém a versão 2.3.0 da biblioteca de SDK da Web da Adobe Experience Platform.

- Adição de suporte para o uso de um elemento de dados ao configurar o consentimento padrão.
- Adição da capacidade de pesquisar esquemas XDM com o tipo de elemento de dados Objeto XDM.
- Adição de clonagem de dados XDM no tipo de ação Enviar evento para garantir que todas as alterações subsequentes no objeto de dados XDM não serão refletidas na solicitação.

## Versão 2.2.0 - sexta-feira, 1 de outubro de 2020

- Quando tentavam criar um objeto XDM a partir de esquemas da sandbox, os clientes tinham problemas de autenticação. A API que chama o Experience Platform agora reconhece os ambientes, de modo que os usuários somente são apresentados aos esquemas que eles têm acesso para editar.
- Ao usar o elemento de dados `identityMap`, os namespaces agora são pré-preenchidos em uma lista suspensa para que você não precise preenchê-los manualmente.
- A interface do usuário do elemento de dados `xdmObject` foi alterada. Na nova interface do usuário, você pode ver quais campos foram preenchidos sem precisar inserir cada item no objeto.

## Versão 2.1.1 - 26 de agosto de 2020

- Correção de um problema em que as sandboxes da Adobe Experience Platform na visualização de objeto XDM eram exibidas incorretamente. Se, ao usar essa versão da extensão, uma sandbox esperada não for exibida na lista, o usuário deve verificar com o administrador da Adobe Experience Platform se as permissões de acesso estão definidas corretamente.

## Versão 2.1.0 - 5 de agosto de 2020

- Nova alteração: remove a ação `syncIdentity` e oferece suporte à transmissão dessas IDs na ação `sendEvent`. Desabilite qualquer regra existente que use essa ação antes de atualizar a extensão.
- Atualizar para Alloy v. 2.1.0 ([Notas de versão](/help/web-sdk/release-notes.md)).
- Suporte ao Padrão de consentimento IAB 2.0 na ação `setConsent`.
- Suporte à substituição da ID do conjunto de dados na ação `sendEvent`.
- Adiciona um novo Elemento de dados do tipo `IdentityMap`, que pode ser usado para preencher a entrada `identityMap` no Elemento de dados do objeto XDM (agora habilitado) e na ação `setConsent`.
- Suporte à transmissão de um mapa de identidade na ação `setConsent`.
- Suporte à escolha de uma sandbox do Experience Platform no Elemento de dados do objeto XDM.

## Versão 1.0.0 - quarta-feira, 26 de maio de 2020

- Suporte à seleção do ambiente no Serviço de configuração.

## Versão 0.1.2 - terça-feira, 4 de maio de 2020

- `configId` renomeado para `edgeConfigId`.
- `viewStart` renomeado para `renderDecisions`, definido como falso por padrão. Se definido como verdadeiro, as ofertas de personalização serão buscadas e renderizadas automaticamente.
- Alterações relacionadas com `Get Decisions`:
   - O comando `getDecisions` foi removido.
   - Adição de uma opção `scopes` ao comando `sendEvent`. As decisões são devolvidas na promessa `sendEvent` resolvida.
   - Adição de um escopo `__view__` integrado que resultará na reversão de ofertas de toda a página/visualização. (Ofertas VEC no Target, por exemplo.)
Essas decisões retornam do comando `sendEvent` somente se `renderDecisions` estiver definido como falso.
   - Adição de um evento `Decisions Received`, que é acionado quando as decisões são disponibilizadas.
- Várias notificações de personalização combinadas em uma única chamada de servidor.
- Correção do problema na ID de mesclagem de evento em que ele era redefinido sempre que o elemento de dados era referenciado.
- A ação `setCustomerIds` foi renomeada para `syncIdentity`.
- Adição de um comando `getIdentity`. Isso pode ser consumido somente por código personalizado por enquanto.
- Habilitar a depuração usando `_satellite` agora habilita a depuração no Adobe Experience Platform Web SDK.
- Adição de suporte para valores digitados no Objeto XDM: Booleanos, números e decimais.

## Versão 0.0.10 - 16 de março de 2020

- Os conceitos de aceitação e recusa foram combinados em `Consent` e foi adicionado um novo comando `setConsent`.
- Adição de um novo Elemento de dados do tipo `XDM Object` que permite o mapeamento de JavaScript/JSON para XDM.

## Versão 0.0.7 - 18 de fevereiro de 2020

- Remoção das opções idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled e cookieDestinationsEnabled.
- Adição de suporte a hifens no valor de opção edgeDomain.
- A solicitação feita durante a migração da ID é enviada para o endpoint demdex para melhorar a identificação entre domínios quando o cookie demdex não está definido.
- A solicitação feita durante a migração de ID sempre espera uma resposta para garantir que o cookie de identidade seja definido.
- Ao executar um comando inválido, uma lista de nomes de comando válidos será registrada no console.
- Adição de uma caixa de seleção para alternar o suporte a cookies de terceiros na extensão de tag. Isso desabilita chamadas com demdex.net

## Versão 0.0.5 - sábado, 20 de dezembro de 2019

- Adicionar configurações do Rastreador de atividade à extensão de tag
- Expor EventType e EventMergeId no comando do evento.
- Adicionar configuração onBeforeEventSend à extensão de tag
- Adicionar configuração edgeBasePath à extensão de tag

## Versão 0.0.3 - terça-feira, 25 de novembro de 2019

- Novos campos ID de Mesclagem e Tipo na ação Enviar evento. O ID de Mesclagem mapeia para o `xdm.eventMergeID` no esquema XDM e o Tipo mapeia para o `xdm.eventType` no esquema XDM.

## Versão 0.0.2 - terça-feira, 18 de novembro de 2019

- Versão inicial
