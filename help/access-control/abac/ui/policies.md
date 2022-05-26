---
keywords: Experience Platform, home, tópicos populares, controle de acesso, controle de acesso baseado em atributos, ABAC
title: Controle de acesso baseado em atributo Criar uma política
description: Este documento fornece informações sobre o controle de acesso baseado em atributos no Adobe Experience Platform
hide: true
hidefromtoc: true
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Gerenciar políticas

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos está disponível em uma versão limitada para clientes de assistência médica com base nos EUA. Esse recurso estará disponível para todos os clientes da Real-time Customer Data Platform assim que for totalmente lançado.

Políticas são declarações que reúnem atributos para estabelecer ações admissíveis e não permissíveis. As políticas podem ser locais ou globais e podem substituir outras políticas.

## Criar uma nova política

Para criar uma nova política, selecione a **[!UICONTROL Políticas]** na barra lateral e selecione **[!UICONTROL Criar Política]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

O **[!UICONTROL Criar uma nova política]** for exibida, solicitando a inserção de um nome e uma descrição opcional. Quando terminar, selecione **[!UICONTROL Confirmar]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

Usando a seta suspensa, selecione se desejar **Permitir acesso a** (![flac-allow-access-to](../../images/flac-ui/flac-permit-access-to.png)) um recurso ou **Negar acesso a** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) um recurso.

Em seguida, selecione o recurso que deseja incluir na política usando o menu suspenso e o tipo de acesso de pesquisa, leitura ou gravação.

![lista suspensa flac-flac-policy-resource](../../images/flac-ui/flac-policy-resource-dropdown.png)

Em seguida, usando a seta suspensa, selecione a condição que deseja aplicar a essa política, **Sendo verdadeiro o seguinte** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) ou **Sendo falso** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

Selecione o ícone de mais para **Adicionar expressão de correspondências** ou **Adicionar grupo de expressões** para o recurso .

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

Usando a lista suspensa, selecione o **Recurso**.

![lista suspensa flac-policy-resource](../../images/flac-ui/flac-policy-resource-dropdown.png)

Em seguida, usando a lista suspensa, selecione o **Corresponde**.

![flac-policy-matches-drop-down](../../images/flac-ui/flac-policy-matches-dropdown.png)

Em seguida, usando a lista suspensa, selecione o **Usuário**.

![flac-policy-user-drop-down](../../images/flac-ui/flac-policy-user-dropdown.png)

Finalmente, selecione o **Sandbox** que você gostaria que as condições da política fossem aplicadas usando o menu suspenso.

![lista suspensa flac-policy-sandboxes](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Selecionar **Adicionar recurso** para adicionar mais recursos. Depois de concluído, selecione **[!UICONTROL Salvar e sair]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

A nova política foi criada com êxito e você é redirecionado para a função **[!UICONTROL Políticas]** , onde você verá a política recém-criada na lista.

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## Editar uma política

Para editar uma política existente, selecione a política no **[!UICONTROL Políticas]** guia . Como alternativa, use a opção de filtro para filtrar os resultados e encontrar a política que deseja editar.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Em seguida, selecione as reticências (`…`) ao lado do nome das políticas e uma lista suspensa exibe controles para editar, desativar, excluir ou duplicar a função. Selecione editar na lista suspensa.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

A tela de permissões de política é exibida. Faça as atualizações e selecione **[!UICONTROL Salvar e sair]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

A política foi atualizada com êxito e você é redirecionado para a função **[!UICONTROL Políticas]** guia .

## Duplicar uma política

Para duplicar uma política existente, selecione a política no **[!UICONTROL Políticas]** guia . Como alternativa, use a opção de filtro para filtrar os resultados e encontrar a política que deseja editar.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Em seguida, selecione as reticências (`…`) ao lado de um nome de política e uma lista suspensa exibe controles para editar, desativar, excluir ou duplicar a função. Selecione duplicata na lista suspensa.

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

O **[!UICONTROL Política duplicada]** for exibida, solicitando que você confirme a duplicação.

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

A nova política aparece na lista como uma cópia do original no **[!UICONTROL Políticas]** guia .

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Excluir uma política

Para excluir uma política existente, selecione a política no **[!UICONTROL Políticas]** guia . Como alternativa, use a opção de filtro para filtrar os resultados e encontrar a política que deseja excluir.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Em seguida, selecione as reticências (`…`) ao lado de um nome de política e uma lista suspensa exibe controles para editar, desativar, excluir ou duplicar a função. Selecione excluir na lista suspensa.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

O **[!UICONTROL Excluir política do usuário]** for exibida, solicitando que você confirme a exclusão.

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

Você volta ao **[!UICONTROL políticas]** e uma confirmação do pop-up de exclusão é exibida.

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png)

## Ativar uma política

Para ativar uma política existente, selecione a política no **[!UICONTROL Políticas]** guia . Como alternativa, use a opção de filtro para filtrar os resultados e encontrar a política que deseja excluir.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Em seguida, selecione as reticências (`…`) ao lado de um nome de política e uma lista suspensa exibe controles para editar, ativar, excluir ou duplicar a função. Selecione ativar na lista suspensa.

![flac-policy-ativate](../../images/flac-ui/flac-policy-delete.png)

O **[!UICONTROL Ativar política do usuário]** for exibida, solicitando que você confirme a ativação.

![flac-policy-ativate-confirm](../../images/flac-ui/flac-policy-activate-confirm.png)

Você volta ao **[!UICONTROL políticas]** e uma confirmação do pop-up de ativação é exibida. O status da política é mostrado como ativa.

![flac-policy-enabled](../../images/flac-ui/flac-policy-activated.png)

## Próximas etapas

Com uma nova política criada, você pode prosseguir para a próxima etapa para [gerenciar permissões para uma função](permissions.md).
