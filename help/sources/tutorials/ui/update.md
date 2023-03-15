---
keywords: Experience Platform;página inicial;tópicos populares;atualizar contas
description: Em algumas circunstâncias, pode ser necessário atualizar os detalhes de uma conta de fontes existente. O espaço de trabalho de Origens fornece a capacidade de adicionar, editar e excluir detalhes de uma conexão de lote ou transmissão existente, incluindo nome, descrição e credenciais.
solution: Experience Platform
title: Atualizar detalhes da conta de conexão de origem na interface
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Atualizar detalhes da conta na interface

Em algumas circunstâncias, pode ser necessário atualizar os detalhes de uma conta de fontes existente. A variável [!UICONTROL Origens] o espaço de trabalho oferece a capacidade de adicionar, editar e excluir detalhes de um lote existente ou conexão de streaming, incluindo nome, descrição e credenciais.

Este tutorial fornece etapas para atualizar os detalhes e as credenciais de uma conta existente do [!UICONTROL Origens] espaço de trabalho.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Origens](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
- [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Atualizar contas

Faça logon no [IU DO EXPERIENCE PLATFORM](https://platform.adobe.com) e selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. Selecionar **[!UICONTROL Contas]** no cabeçalho superior para exibir as contas existentes.

![catálogo](../../images/tutorials/update/catalog.png)

A variável **[!UICONTROL Contas]** é exibida. Nesta página há uma lista de contas visualizáveis, incluindo informações sobre sua origem, nome de usuário, número de fluxos de dados e data de criação.

Selecione o ícone de filtro ![filtro](../../images/tutorials/update/filter.png) na parte superior esquerda para iniciar o painel classificar.

![accounts-list](../../images/tutorials/update/accounts-list.png)

O painel de classificação fornece uma lista de todas as fontes. Você pode selecionar mais de uma origem na lista para acessar uma seleção filtrada de contas associadas a origens diferentes.

Selecione a fonte com a qual deseja trabalhar para ver uma lista de suas contas existentes. Depois de identificar a conta que deseja atualizar, selecione as reticências (`...`) ao lado do nome da conta.

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

Um menu suspenso é exibido, fornecendo opções para **[!UICONTROL Adicionar dados]**, **[!UICONTROL Editar detalhes]**, e **[!UICONTROL Excluir]**. Selecionar **[!UICONTROL Editar detalhes]** no menu para atualizar sua conta.

![atualizar](../../images/tutorials/update/update.png)

A variável **[!UICONTROL Editar detalhes da conta]** permite atualizar o nome, a descrição e as credenciais de autenticação de uma conta. Depois de atualizar as informações desejadas, selecione **[!UICONTROL Salvar]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

Após alguns minutos, uma caixa de confirmação é exibida na parte inferior da tela para confirmar uma atualização bem-sucedida.

![atualização confirmada](../../images/tutorials/update/update-confirmed.png)

## Próximas etapas

Ao seguir este tutorial, você usou com êxito o [!UICONTROL Origens] espaço de trabalho para atualizar as informações de uma conta de origem existente.

Para obter etapas sobre como executar essas operações de forma programática usando o [!DNL Flow Service] , consulte o tutorial em [atualização de informações de conexão usando a API do Serviço de fluxo](../../tutorials/api/update.md).
