---
keywords: atualizar conta de destino, contas de destino, como atualizar contas
title: Atualizar contas de destino
type: Tutorial
description: Este tutorial lista as etapas para atualizar contas de destino na interface do usuário do Adobe Experience Platform
translation-type: tm+mt
source-git-commit: ebe2a35e66b78acf6a9ffa20664877913cd35648
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 1%

---


# Atualizar contas de destino

## Visão geral {#overview}

A guia **[!UICONTROL Accounts]** mostra detalhes sobre as conexões estabelecidas com vários destinos. Consulte a tabela abaixo para obter todas as informações que você pode obter em cada destino:

![Guia Contas](../assets/ui/update-accounts/destination-accounts.png)

| Elemento | Descrição |
|---|---|
| [!UICONTROL Platform] | O destino para o qual você configurou a conexão. |
| [!UICONTROL Connection Type] | Representa o tipo de conexão com seu bucket ou destino de armazenamento. <ul><li>Para destinos de marketing por email: Pode ser S3 ou FTP.</li><li>Para destinos de anúncios em tempo real: Servidor para servidor</li><li>Para destinos de armazenamento em nuvem Amazon S3: Chave de acesso </li><li>Para destinos de armazenamento em nuvem SFTP: Autenticação básica para SFTP</li></ul> |
| [!UICONTROL Username] | O nome de usuário selecionado no [assistente de destino de conexão](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinations] | Representa o número de fluxos de destino únicos bem-sucedidos conectados às informações básicas criadas para um destino. |
| [!UICONTROL Authorized] | A data em que a conexão com esse destino foi autorizada. |

## Atualizar contas {#update}

Siga as etapas abaixo para atualizar os detalhes da conexão com destinos existentes.

1. Faça logon na [interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinations]** na barra de navegação esquerda. Selecione **[!UICONTROL Accounts]** no cabeçalho superior para exibir suas contas existentes.

   ![Guia Contas](../assets/ui/update-accounts/accounts-tab.png)

2. Selecione o ícone de filtro ![Filter-icon](../assets/ui/update-accounts/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de contas associadas aos destinos selecionados.

   ![Filtrar destinos](../assets/ui/update-accounts/filter-accounts.png)

3. Selecione o botão ![Edit account button](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Edit]** na coluna **[!UICONTROL Platform]** para editar as informações da conta.

   ![Guia Contas](../assets/ui/update-accounts/accounts-edit.png)

4. Insira suas credenciais de conta atualizadas.

   * Para contas que usam um tipo de conexão `OAuth2`, selecione **[!UICONTROL Reconnect OAuth]** para renovar suas credenciais de conta.

      ![Editar detalhes OAuth](../assets/ui/update-accounts/edit-details-oauth.png)


   * Para contas que usam um tipo de conexão `Access Key` ou `ConnectionString`, é possível editar as informações de autenticação da conta, incluindo informações como ID de acesso, chaves secretas ou cadeias de conexão.

      ![Editar detalhes da chave de acesso](../assets/ui/update-accounts/edit-details-key.png)

5. Selecione **[!UICONTROL Save]** para concluir a atualização de credenciais.
