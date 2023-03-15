---
keywords: atualizar conta de destino, contas de destino, como atualizar contas, atualizar destino
title: Atualizar contas de destino
type: Tutorial
description: Este tutorial lista as etapas para atualizar contas de destino na interface do usuário do Adobe Experience Platform
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: f31b54622c63f96fb8fa727f80dda295a926e2c7
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Atualizar contas de destino

## Visão geral {#overview}

A variável **[!UICONTROL Contas]** A guia mostra detalhes sobre as conexões estabelecidas com vários destinos. Consulte a [Visão geral das contas](../ui/destinations-workspace.md#accounts) para obter todas as informações que você pode obter em cada conta de destino.

Este tutorial aborda as etapas para atualizar detalhes da conta de destino usando a interface do usuário do Experience Platform.

Você pode atualizar os detalhes da conta de destino para atualizar e autenticar novamente as credenciais das contas atuais ou expiradas para os destinos que você está usando no momento. Normalmente, os tokens OAuth e de portador têm uma vida útil limitada, dependendo da plataforma de destino. Quando esses tokens expiram, você pode atualizá-los no workflow descrito mais abaixo. Esse fluxo de trabalho direciona você a passar pelo fluxo de trabalho OAuth ou reinserir um token. Da mesma forma, se uma senha ou acesso de usuário tiver sido alterado na plataforma downstream, você poderá atualizar credenciais.

Para destinos em lote, é possível atualizar a chave de acesso ou secreta, se alguma delas tiver sido alterada. Além disso, se você quiser criptografar seus arquivos daqui em diante, poderá inserir uma chave pública RSA e seus arquivos exportados serão criptografados daqui em diante.

![Guia Contas](../assets/ui/update-accounts/destination-accounts.png)

## Atualizar contas {#update}

Siga as etapas abaixo para atualizar os detalhes da conexão com os destinos existentes.

1. Faça logon no [IU DO EXPERIENCE PLATFORM](https://platform.adobe.com/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Selecionar **[!UICONTROL Contas]** no cabeçalho superior para exibir as contas existentes.

   ![Guia Contas](../assets/ui/update-accounts/accounts-tab.png)

2. Selecione o ícone de filtro ![Ícone de filtro](../assets/ui/update-accounts/filter.png) na parte superior esquerda para iniciar o painel classificar. O painel de classificação fornece uma lista de todos os seus destinos. É possível selecionar mais de um destino na lista para ver uma seleção filtrada de contas associadas aos destinos selecionados.

   ![Filtrar contas de destino](../assets/ui/update-accounts/filter-accounts.png)

3. Selecione as reticências (`...`) ao lado do nome da conta que você pretende atualizar. Um painel pop-up é exibido, fornecendo opções para **[!UICONTROL Ativar segmentos]**, **[!UICONTROL Editar detalhes]**, e **[!UICONTROL Excluir]** a conta. Selecione o ![Botão Editar detalhes](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Editar detalhes]** botão para editar as informações da conta.

   ![Editar conta](../assets/ui/update-accounts/accounts-edit.png)

4. Insira suas credenciais de conta atualizadas.

   * Para contas que usam um `OAuth1` ou `OAuth2` tipo de conexão, selecione **[!UICONTROL Reconectar OAuth]** para renovar as credenciais da conta. Você também pode atualizar o nome e a descrição da sua conta.

   ![Editar OAuth de detalhes](../assets/ui/update-accounts/edit-details-oauth.png)

   * Para contas que usam um `Access Key` ou `ConnectionString` tipo de conexão, você pode editar as informações de autenticação da conta, incluindo informações como ID de acesso, chaves secretas ou cadeias de conexão. Você também pode atualizar o nome e a descrição da sua conta.

   ![Editar detalhes da Chave de acesso](../assets/ui/update-accounts/edit-details-key.png)

   * Para contas que usam um `Bearer token` tipo de conexão, você pode inserir um novo token de portador, se necessário. Você também pode atualizar o nome e a descrição da sua conta.

   ![Editar token de portador de detalhes](../assets/ui/update-accounts/edit-details-bearer.png)

   * Para contas que usam um `Server to server` tipo de conexão, você pode atualizar o nome e a descrição da sua conta.

   ![Editar detalhes de servidor para servidor](../assets/ui/update-accounts/edit-details-s2s.png)

5. Selecionar **[!UICONTROL Salvar]** para concluir a atualização dos detalhes da conta.

## Próximas etapas

Ao seguir este tutorial, você usou com êxito o **[!UICONTROL destinos]** espaço de trabalho para atualizar contas existentes.

Para obter mais informações sobre destinos, consulte o [visão geral dos destinos](../catalog/overview.md).