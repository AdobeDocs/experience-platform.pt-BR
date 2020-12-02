---
keywords: Experience Platform;home;popular topics;update accounts;
description: null
solution: Experience Platform
title: Atualizar detalhes da conta na interface do usuário
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 413687a0d9e790ea3f61a858002e9510216d7c34
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# Atualizar detalhes da conta na interface do usuário

Em algumas circunstâncias, pode ser necessário atualizar os detalhes de uma conta de origem existente. A área de trabalho [!UICONTROL Fontes] fornece a você a capacidade de editar, adicionar e excluir detalhes de uma conta, incluindo valores para seu nome, descrição e credenciais de autenticação.

Este tutorial fornece etapas para atualizar os detalhes e as credenciais de uma conta existente da área de trabalho [!UICONTROL Fontes] .

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

## Atualizar contas

Faça logon na interface do usuário [do](https://platform.adobe.com) Experience Platform e selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar a área de trabalho [!UICONTROL Fontes] . Selecione **[!UICONTROL Contas]** no cabeçalho superior para visualização contas existentes.

![catálogo](../../images/tutorials/update/catalog.png)

A página **[!UICONTROL Contas]** é exibida. Nesta página há uma lista de contas visualizáveis, incluindo informações sobre a origem, o nome de usuário, o número de fluxos de dados e a data de criação.

Selecione o ![filtro](../../images/tutorials/update/filter.png) do ícone de filtro na parte superior esquerda para iniciar o painel de classificação.

![lista de contas](../../images/tutorials/update/accounts-list.png)

O painel de classificação fornece uma lista de todas as fontes. Você pode selecionar mais de uma fonte da lista para acessar uma seleção filtrada de contas associadas a fontes diferentes.

Selecione a fonte com a qual deseja trabalhar para ver uma lista de suas contas existentes. Depois de identificar a conta que deseja atualizar, selecione as elipses (`...`) ao lado do nome da conta.

![classificação de contas](../../images/tutorials/update/accounts-sort.png)

Um menu suspenso é exibido, fornecendo opções para **[!UICONTROL Adicionar dados]**, **[!UICONTROL Editar detalhes]** e **[!UICONTROL Excluir]**. Selecione **[!UICONTROL Editar detalhes]** no menu para atualizar sua conta.

![update](../../images/tutorials/update/update.png)

A caixa de diálogo **[!UICONTROL Editar detalhes]** da conta permite atualizar o nome, a descrição e as credenciais de autenticação de uma conta. Depois de atualizar as informações desejadas, selecione **[!UICONTROL Salvar]**.

![editar detalhes da conta](../../images/tutorials/update/edit-account-details.png)

Após alguns instantes, uma caixa de confirmação verde é exibida na parte inferior da tela para confirmar uma atualização bem-sucedida.

![update-confirm](../../images/tutorials/update/update-confirmed.png)

## Próximas etapas

Ao seguir este tutorial, você usou com êxito a área de trabalho [!UICONTROL Fontes] para atualizar as informações da conta.

Para obter etapas sobre como executar essas operações de forma programática usando a [!DNL Flow Service] API, consulte o tutorial sobre como [atualizar as informações de conexão usando a API](../../tutorials/api/update.md)de Serviço de Fluxo.