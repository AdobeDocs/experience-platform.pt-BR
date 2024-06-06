---
title: Exibição de entrega de borda
description: Este guia detalha informações sobre a exibição de Entrega de borda no Adobe Experience Platform Assurance.
source-git-commit: d6b5894a5c5ba3907a8e6dd0d1864f773dd6325c
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 1%

---

# Exibição de entrega de borda no Assurance

A variável **[!UICONTROL Entrega de borda]** exibir dentro **[!UICONTROL Adobe Experience Platform Assurance]** oferece a capacidade de inspecionar e validar [!UICONTROL Entrada do AJO] entrega de borda de mensagens para seus aplicativos móveis e da web. Essa exibição é particularmente útil para solucionar problemas da entrega de [!UICONTROL Entrada do AJO] Campanhas e jornadas da Web e para dispositivos móveis.

## Introdução

Antes de continuar, verifique se você tem acesso aos seguintes serviços:

- A [Interface da coleção de dados da Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Para saber como instalar o **[!UICONTROL Assurance]** no aplicativo, leia o [guia de implementação do Assurance](../tutorials/implement-assurance.md).

## Usar o Assurance com Entrega de Borda

Depois de abrir uma **[!UICONTROL Assurance]** você pode adicionar a variável **[!UICONTROL Entrega de borda]** exibir para **[!UICONTROL Assurance]**. Na parte inferior do painel esquerdo, selecione **[!UICONTROL Configurar]** para adicionar o **[!UICONTROL Entrega de borda]** exibir e **Salvar** o mesmo.

![Adicione o plug-in selecionando Configurar na parte inferior esquerda](./images/edge-delivery/add-plugin.png)

Depois de adicionado, selecione o **[!UICONTROL Entrega de borda]** exibir no **[!UICONTROL Adobe Journey Optimizer]** seção para validar a entrega da borda de entrada.

![O Edge Delivery pode ser acessado no grupo de exibição do Adobe Journey Optimizer](./images/edge-delivery/ajo-plugins.png)

## Lista de solicitações

No painel principal da exibição, a lista de solicitações de entrega de borda é exibida. Esta lista mostra todas as [!UICONTROL AJO de entrada] solicitações feitas na Experience Edge e processadas pela **[!UICONTROL Serviço de entrega de entrada]**, incluindo solicitações para recuperar decisões de personalização, bem como rastrear interações de apresentação de personalização (como exibição, clique, acionador ou descarte).

As solicitações são ordenadas por carimbo de data e hora, com as solicitações mais recentes na parte superior. Além do carimbo de data e hora, a lista também inclui uma coluna ID de solicitação, bem como Tipo de solicitação, que pode ser uma das seguintes:

- **[!UICONTROL Entrega de experiência]**: uma solicitação para recuperar decisões de personalização
- **[!UICONTROL Interações de experiência]**: uma solicitação para rastrear as interações da apresentação de personalização
- **[!UICONTROL Entrega de experiência e interações]**: uma solicitação para recuperar decisões de personalização, incluindo também interações de apresentação de personalização
- **[!UICONTROL Visualizar entrega]**: uma solicitação para recuperar as decisões de personalização de Pré-visualização

As solicitações também podem ser filtradas inserindo um termo de pesquisa na barra de pesquisa na parte superior da lista. Isso é útil ao filtrar por valores específicos, como IDs.

![A lista de solicitações de entrada é mostrada na visualização principal](./images/edge-delivery/request-list.png)

## Visualizações detalhadas de solicitações

Depois que uma solicitação é selecionada na exibição principal, informações detalhadas sobre a solicitação selecionada são exibidas à direita. Essa exibição inclui as seguintes seções:

### Visão geral da solicitação

Esta seção fornece uma visão geral de alto nível da solicitação selecionada, incluindo [!UICONTROL ID da organização], [!UICONTROL Cluster de borda], [!UICONTROL ID da solicitação] e [!UICONTROL Tipo de solicitação], [!UICONTROL ID de sandbox], [!UICONTROL Nome da sandbox], [!UICONTROL ID da sequência de dados], bem como a lista de superfícies de solicitação em caso de [!UICONTROL Entrega de experiência] solicitações.

![A seção Visão geral da solicitação fornece detalhes da solicitação de alto nível](./images/edge-delivery/request-overview.png)

### Perfil

Esta seção fornece informações sobre os dados de perfil usados ao processar a solicitação, incluindo o mapa de identidade, a associação do segmento e as configurações de consentimento.\
A variável [!UICONTROL Perfil] A seção é muito útil para solucionar problemas como delivery que não estão funcionando como esperado devido à associação ausente ou atrasada do segmento ou às configurações de consentimento de recusa.

![A seção Perfil inclui o mapa de identidade, a associação do segmento e as configurações de consentimento](./images/edge-delivery/profile.png)

### Atividades qualificadas

Esta seção fornece uma lista de atividades que foram qualificadas para a solicitação selecionada, incluindo o tipo de atividade, as IDs, o namespace de identidade, as superfícies, a agenda e os públicos-alvo. Informações mais detalhadas sobre a atividade podem ser encontradas no [seção de rastreamento de execução bruta](#execution).

![A seção Atividades qualificadas contém os detalhes de atividades qualificadas](./images/edge-delivery/qualified-activities.png)

### Atividades não qualificadas

Esta seção fornece uma lista de atividades que foram excluídas de serem qualificadas. Além do tipo de atividade, IDs, namespaces de identidade, superfícies, agendamentos e públicos-alvo, esta seção também inclui uma lista de motivos pelos quais a atividade foi desqualificada.

![A seção Atividades não qualificadas contém detalhes de atividades não qualificadas e motivos de exclusão](./images/edge-delivery/unqualified-activities.png)

### Detalhes da mensagem

Esta seção fornece informações detalhadas sobre as mensagens que foram entregues para a solicitação selecionada. Inclui IDs de mensagem, fragmentos, políticas de decisão, [!UICONTROL Offer decisioning] parâmetros, bem como o contexto de seleção da mensagem.

![Seção que contém detalhes da mensagem entregue, como IDs de mensagem e contexto de seleção, fragmentos, políticas de decisão e parâmetros de decisão](./images/edge-delivery/message-details.png)

### Interações

Esta seção fornece informações detalhadas sobre as interações que foram rastreadas na solicitação selecionada. Inclui o tipo de interação (em `propositionEventType`), bem como metadados de proposta associados, como metadados de atividade (em `scopeDetails.activity`) e o token de evento de apresentação (em `scopeDetails.characteristics.eventToken`).

![As interações são rastreadas por meio de tokens de proposta e metadados de atividade associados](./images/edge-delivery/interactions.png)

### Rastreamentos brutos

Esta seção fornece os rastreamentos brutos da solicitação selecionada. Inclui o rastreamento completo da solicitação, incluindo a solicitação real como foi recebida em **[!UICONTROL Serviço de entrega de entrada]**, rastreamento de execução e rastreamento de resposta. Isso é útil para a solução de problemas avançada, como o não funcionamento esperado do delivery devido à indisponibilidade do Serviço de delivery, dados ausentes ou incorretos, ou para entender o fluxo completo do processamento de solicitações.

#### Solicitação

O rastreamento de solicitação inclui a solicitação completa como foi recebida pelo **[!UICONTROL Serviço de entrega de entrada]** **[!UICONTROL Konductor]** upstream. Inclui os cabeçalhos de solicitação, o corpo e outros metadados. Por exemplo, a carga XDM da solicitação pode ser inspecionada na variável `event.body.xdm` campo.

![Informações detalhadas da solicitação, incluindo cabeçalhos e corpo, podem ser encontradas no rastreamento de solicitação](./images/edge-delivery/request.png)

#### Execução

O rastreamento de execução inclui o rastreamento completo da solicitação conforme foi processada pelo **[!UICONTROL Serviço de entrega de entrada]**. Ela mostra o contexto de execução, a qualificação de atividade, a seleção de mensagens e outras etapas de processamento. Quaisquer erros ou avisos que ocorreram durante o processamento da solicitação podem ser encontrados em `context.messages` e `context.exceptions` campos. Informações detalhadas sobre a qualificação da atividade podem ser encontradas no `context.qualifiedActivitiesDetailed` e `context.unqualifiedActivitiesDetailed` campos.

![O rastreamento de execução inclui contexto de execução, qualificação de atividade, seleção de mensagem e outros detalhes de processamento](./images/edge-delivery/execution.png)

#### Resposta

O rastreamento de resposta inclui a resposta completa conforme retornada por **[!UICONTROL Serviço de entrega de entrada]** downstream para **[!UICONTROL Konductor]**. Ele inclui os cabeçalhos de resposta, o corpo e outros metadados. O corpo completo da resposta pode ser inspecionado copiando a mensagem com a id `1` para a área de transferência usando o **[!UICONTROL Copiar Valor]** e colando-o em um visualizador JSON.

![O rastreamento de resposta contém o corpo de resposta completo retornado downstream](./images/edge-delivery/response.png)
