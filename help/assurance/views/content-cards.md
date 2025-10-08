---
title: Exibição de cartões de conteúdo
description: Este guia detalha informações sobre a exibição de Cartões de conteúdo no Adobe Experience Platform Assurance.
source-git-commit: fa5dbbfcc0c178c8886000479f44afd5d63c8c34
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# Exibição de Cartões de conteúdo no Assurance

A exibição de Mensagens no aplicativo no Adobe Experience Platform Assurance fornece a capacidade de validar seu aplicativo, monitorar os cartões de conteúdo entregues ao dispositivo e pré-visualizar cartões.

## Cartões de conteúdo

Na parte superior da guia **[!UICONTROL Cartões de Conteúdo]** está uma lista suspensa de **[!UICONTROL Cartão de Conteúdo]**. Isso lista todos os cartões de conteúdo que foram recebidos na sessão do Assurance. Se um cartão não estiver nessa lista, significa que o aplicativo nunca o recebeu.

![Lista suspensa de Cartão de Conteúdo contendo uma lista de cartões](./images/content-cards/dropdown.png)

Selecionar um cartão de conteúdo mostrará muitas informações sobre ele, conforme descrito nas seções abaixo.

### Visualização do cartão

No painel direito há um painel **[!UICONTROL Visualização do cartão]** que mostra como um cartão é renderizado em modelos comuns — Imagem pequena, Imagem grande e Somente imagem.

![Visualização do Cartão de Conteúdo selecionado](./images/content-cards/preview.png)

Use o botão **[!UICONTROL Tema]** para exibir o cartão no modo claro ou escuro.

![Visualização do Cartão de Conteúdo selecionado no Tema Escuro](./images/content-cards/preview-dark.png)

### Guias disponíveis

Na seção à esquerda, as guias disponíveis dependem do cartão selecionado. Se o cartão incluir regras, você verá três guias: **[!UICONTROL Informações]**, **[!UICONTROL Interações]** e **[!UICONTROL Analisar regras]**.

![Guias disponíveis quando as regras estiverem presentes: Informações, Interações, Analisar Regras](./images/content-cards/tabs-with-rules.png)

Se o cartão não incluir regras, você verá duas guias: **[!UICONTROL Informações]** e **[!UICONTROL Interações]**.

![Guias disponíveis quando sem regras: Informações e Interações](./images/content-cards/tabs-no-rules.png)

### Guia Informações

A guia **[!UICONTROL Informações]** mostra a seção **[!UICONTROL Propriedades do Cartão]** na parte superior, incluindo medalhas para o **[!UICONTROL Estado Atual]** (acionador, exibição, descarte, desqualificação) além de metadados como **[!UICONTROL Modelo]** (Imagem Pequena, Imagem Grande ou Somente Imagem), **[!UICONTROL Superfície]** e qualquer par de valores-chave personalizado.

![Propriedades do cartão mostrando as medalhas do estado atual, o modelo, a superfície e os pares de valor-chave](./images/content-cards/card-properties.png)

Abaixo disso, a seção **[!UICONTROL Propriedades da campanha]** mostra informações carregadas do Adobe Journey Optimizer (AJO).

Você também pode selecionar **[!UICONTROL Exibir campanha]** para abrir o cartão no AJO para inspeção ou edição.

![Seção Propriedades da campanha com botão para exibir a campanha](./images/content-cards/campaign-properties.png)

### Guia Interações

A guia **[!UICONTROL Interações]** resume o ciclo de vida de cada cartão como uma sequência de medalhas: ele sempre começa com **[!UICONTROL acionador]**, seguido por qualquer resultado produzido pelas regras—**[!UICONTROL exibir]**, **[!UICONTROL dispensar]** ou **[!UICONTROL desqualificar]**.

![Tabela de interações que mostra os emblemas de ciclo de vida do acionador para exibição, descarte ou desqualificação](./images/content-cards/interactions-tab.png)

### Guia Analisar regras

A guia **[!UICONTROL Analisar]** mostra uma tabela de eventos com até três colunas de regras —**[!UICONTROL Exibir]**, **[!UICONTROL Dispensar]** e **[!UICONTROL Desqualificar]** — com base nas regras do cartão. Se o cartão definir apenas uma regra, somente essa coluna será exibida.

Cada linha representa um evento de sessão e cada coluna indica se a regra do cartão correspondeu às condições desse evento. Uma pontuação de 0% significa que nenhuma condição foi correspondida; 100% é uma correspondência completa (a regra seria acionada).

Se o evento corresponder a uma condição, ele mostrará uma marca de seleção verde. Se o evento não corresponder, ele mostrará um ícone vermelho.

![Analisar a tabela de eventos da guia com as colunas de regra Exibir, Descartar e Desqualificar](./images/content-cards/rules-tab.png)

Use o controle deslizante **[!UICONTROL Limite de Correspondência]** para filtrar eventos por porcentagem mínima de correspondência.

![Fazer a correspondência do controle deslizante de limite para filtrar eventos pela porcentagem mínima de correspondência](./images/content-cards/match-threshold.png)

Ao selecionar um evento, um painel de detalhes é aberto à direita com uma opção listando as três regras: **[!UICONTROL Exibir]**, **[!UICONTROL Ignorar]** e **[!UICONTROL Desqualificar]**.

![Lista do painel Detalhes do evento Exibir, Ignorar e Desqualificar regras](./images/content-cards/rules-panel.png)

Expanda qualquer seção para ver as condições da regra, quais condições corresponderam e a porcentagem de correspondência calculada para esse resultado.

![Opção de regra expandida mostrando condições correspondentes e porcentagem de correspondência](./images/content-cards/expanded-accordion.png)

## Guia Solicitações

A guia **[!UICONTROL Solicitações]** mostra quais Cartões de Conteúdo foram solicitados e em qual superfície.

![Guia Solicitações mostrando solicitações de Cartão de Conteúdo](./images/content-cards/requests-tab.png)

Use o botão **[!UICONTROL Exibir Cartão]** para voltar para a guia de informações de um cartão de conteúdo específico.

## Guia Lista de eventos

A guia **[!UICONTROL Lista de eventos]** mostra eventos de sessão relevantes para Cartões de conteúdo, incluindo solicitações/respostas de apresentação do AJO, eventos de ciclo de vida do cartão e rastreamento de interação. Pesquise, filtre, classifique e personalize colunas e exporte resultados.

Selecionar um evento abre um painel de detalhes do lado direito com a carga bruta e os atributos principais. Você também pode sinalizar eventos para acompanhamento. Essa exibição é útil para correlacionar solicitações, resultados de regras e interações na sessão.

![Guia Lista de Eventos com eventos de sessão pesquisáveis e filtráveis para Cartões de Conteúdo](./images/content-cards/event-list.png)

## Guia Validação

A guia **[!UICONTROL Validação]** executa validações em relação à sessão atual, verificando se o aplicativo foi configurado corretamente para envio de mensagens:

![Os resultados da guia Validação verificam a configuração de mensagens da sessão atual](./images/content-cards/validation.png)
