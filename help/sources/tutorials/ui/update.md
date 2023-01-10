---
keywords: Experience Platform, home, tópicos populares, atualizar contas
description: Em algumas circunstâncias, pode ser necessário atualizar os detalhes de uma conta de fontes existente. A área de trabalho Fontes oferece a capacidade de adicionar, editar e excluir detalhes de um lote ou conexão de transmissão existente, incluindo o nome, a descrição e as credenciais.
solution: Experience Platform
title: Atualizar detalhes da conta da conexão de origem na interface do usuário
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Atualizar detalhes da conta na interface do usuário

Em algumas circunstâncias, pode ser necessário atualizar os detalhes de uma conta de fontes existente. O [!UICONTROL Fontes] o workspace fornece a capacidade de adicionar, editar e excluir detalhes de uma conexão de lote ou fluxo, incluindo o nome, a descrição e as credenciais.

Este tutorial fornece etapas para atualizar os detalhes e as credenciais de uma conta existente do [!UICONTROL Fontes] espaço de trabalho.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Fontes](../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
- [Sandboxes](../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Atualizar contas

Faça logon no [Interface do usuário do Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. Selecionar **[!UICONTROL Contas]** no cabeçalho superior para exibir as contas existentes.

![catálogo](../../images/tutorials/update/catalog.png)

O **[!UICONTROL Contas]** será exibida. Nesta página, há uma lista de contas visualizáveis, incluindo informações sobre a origem, o nome de usuário, o número de fluxos de dados e a data de criação.

Selecione o ícone de filtro ![filter](../../images/tutorials/update/filter.png) na parte superior esquerda para iniciar o painel de classificação.

![lista de contas](../../images/tutorials/update/accounts-list.png)

O painel de classificação fornece uma lista de todas as fontes. Você pode selecionar mais de uma fonte na lista para acessar uma seleção filtrada de contas associadas a diferentes fontes.

Selecione a fonte com a qual deseja trabalhar para ver uma lista de suas contas existentes. Depois de identificar a conta que deseja atualizar, selecione as reticências (`...`) ao lado do nome da conta.

![classificação de contas](../../images/tutorials/update/accounts-sort.png)

Um menu suspenso é exibido, fornecendo opções para **[!UICONTROL Adicionar dados]**, **[!UICONTROL Editar detalhes]** e **[!UICONTROL Excluir]**. Selecionar **[!UICONTROL Editar detalhes]** no menu para atualizar sua conta.

![atualizar](../../images/tutorials/update/update.png)

O **[!UICONTROL Editar detalhes da conta]** caixa de diálogo permite atualizar o nome de uma conta, a descrição e as credenciais de autenticação. Depois de atualizar as informações desejadas, selecione **[!UICONTROL Salvar]**.

![editar detalhes da conta](../../images/tutorials/update/edit-account-details.png)

Após alguns instantes, uma caixa de confirmação será exibida na parte inferior da tela para confirmar uma atualização bem-sucedida.

![update-confirm](../../images/tutorials/update/update-confirmed.png)

## Próximas etapas

Ao seguir este tutorial, você usou com sucesso a variável [!UICONTROL Fontes] espaço de trabalho para atualizar as informações de uma conta de origem existente.

Para obter etapas sobre como executar essas operações de forma programática usando o [!DNL Flow Service] Consulte o tutorial em [atualização de informações de conexão usando a API do Serviço de Fluxo](../../tutorials/api/update.md).
