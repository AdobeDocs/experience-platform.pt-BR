---
keywords: atualizar conta de destino, contas de destino, como atualizar contas, atualizar destino
title: Atualizar contas de destino
type: Tutorial
description: Este tutorial lista as etapas para atualizar contas de destino na interface do usuário do Adobe Experience Platform
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# Atualizar contas de destino

## Visão geral {#overview}

A guia **[!UICONTROL Contas]** mostra detalhes sobre as conexões estabelecidas com vários destinos. Consulte a [Visão geral das contas](../ui/destinations-workspace.md#accounts) para obter todas as informações que você pode obter em cada conta de destino.

Este tutorial aborda as etapas para atualizar detalhes da conta de destino usando a interface do usuário do Experience Platform.

Você pode atualizar os detalhes da conta de destino para atualizar e autenticar novamente as credenciais das contas atuais ou expiradas para os destinos que você está usando no momento. Normalmente, os tokens OAuth e de portador têm uma vida útil limitada, dependendo da plataforma de destino. Quando esses tokens expiram, você pode atualizá-los no workflow descrito mais abaixo. Esse fluxo de trabalho direciona você a passar pelo fluxo de trabalho OAuth ou reinserir um token. Da mesma forma, se uma senha ou acesso de usuário tiver sido alterado na plataforma downstream, você poderá atualizar credenciais.

Para destinos em lote, é possível atualizar a chave de acesso ou secreta, se alguma delas tiver sido alterada. Além disso, se você quiser criptografar seus arquivos daqui em diante, poderá inserir uma chave pública RSA e seus arquivos exportados serão criptografados daqui em diante.

![Guia Contas](../assets/ui/update-accounts/destination-accounts.png)

## Atualizar contas {#update}

Siga as etapas abaixo para atualizar os detalhes da conexão com os destinos existentes.

1. Faça logon na [interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Selecione **[!UICONTROL Contas]** no cabeçalho superior para exibir suas contas existentes.

   ![Guia Contas](../assets/ui/update-accounts/accounts-tab.png)

2. Selecione o ícone de filtro ![Ícone de filtro](../assets/ui/update-accounts/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os seus destinos. É possível selecionar mais de um destino na lista para ver uma seleção filtrada de contas associadas aos destinos selecionados.

   ![Filtrar contas de destino](../assets/ui/update-accounts/filter-accounts.png)

3. Selecione as reticências (`...`) ao lado do nome da conta que você deseja atualizar. Um painel pop-up é exibido, fornecendo opções para **[!UICONTROL Ativar públicos-alvo]**, **[!UICONTROL Editar detalhes]** e **[!UICONTROL Excluir]** a conta. Selecione o botão ![Editar detalhes](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Editar detalhes]** para editar as informações da conta.

   ![Editar conta](../assets/ui/update-accounts/accounts-edit.png)

4. Insira suas credenciais de conta atualizadas.

   * Para contas que usam um tipo de conexão `OAuth1` ou `OAuth2`, selecione **[!UICONTROL Reconectar OAuth]** para renovar suas credenciais de conta. Você também pode atualizar o nome e a descrição da sua conta.

   ![Editar OAuth de detalhes](../assets/ui/update-accounts/edit-details-oauth.png)

   * Para contas que usam um tipo de conexão `Access Key` ou `ConnectionString`, você pode editar as informações de autenticação da conta, incluindo informações como ID de acesso, chaves secretas ou cadeias de conexão. Você também pode atualizar o nome e a descrição da sua conta.

   ![Editar detalhes da Chave de Acesso](../assets/ui/update-accounts/edit-details-key.png)

   * Para contas que usam um tipo de conexão `Bearer token`, você pode inserir um novo token de portador, se necessário. Você também pode atualizar o nome e a descrição da sua conta.

   ![Editar token de portador de detalhes](../assets/ui/update-accounts/edit-details-bearer.png)

   * Para contas que usam um tipo de conexão `Server to server`, você pode atualizar o nome e a descrição da sua conta.

   ![Editar detalhes de servidor para servidor](../assets/ui/update-accounts/edit-details-s2s.png)

5. Selecione **[!UICONTROL Salvar]** para concluir a atualização dos detalhes da conta.

## Próximas etapas

Ao seguir este tutorial, você usou com êxito o espaço de trabalho **[!UICONTROL destinos]** para atualizar contas existentes.

Para obter mais informações sobre destinos, consulte a [visão geral sobre destinos](../catalog/overview.md).