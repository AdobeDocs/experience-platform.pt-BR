---
title: Administração Expandida da Conta de Ativação
description: Saiba como executar tarefas administrativas em sua conta de Ativação expandida, como monitorar o uso de licenças e atribuir as permissões corretas.
exl-id: ee0ec4b9-a083-447b-b7a7-e1307e90c646
source-git-commit: 2222e9fbf75f3082d331868f820247e0c0ce3ba2
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Administração de conta

Para assimilar públicos do Audience Manager e ativá-los para destinos sociais e de publicidade, primeiro crie uma conta de usuário de Ativação expandida e atribua a conta à função de permissão correta.

Esta página explica como criar uma conta de usuário no Admin Console e atribuir as permissões corretas para a Ativação expandida.

## Criar contas de usuário {#create-users}

Antes de poder usar [!DNL Audience Manager Expanded Activation], você deve criar uma conta de usuário.

Para criar uma conta de usuário para [!DNL Expanded Activation], siga as instruções sobre como gerenciar usuários na documentação do [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/manage-users-individually.html).

## Adicionar usuários à função de permissão {#permissions}

Após criar uma conta de usuário, você deve adicioná-la à função de permissão [!DNL Expanded Activation], na interface de usuário [!DNL Expanded Activation].

Vá para **[!UICONTROL Administração]** -> **[!UICONTROL Permissões]** -> **[!UICONTROL Funções]** e selecione a **[!UICONTROL Função Padrão de Ativação Expandida]**.

![Imagem da interface de usuário da Ativação expandida mostrando a página Funções.](assets/expanded-activation-role.png)

Vá para a guia **[!UICONTROL Usuários]** e selecione **[!UICONTROL Adicionar usuários]**.

![Imagem da interface de usuário da Ativação expandida mostrando a página Usuários.](assets/add-users.png)

Selecione o usuário recém-criado na lista disponível e selecione **[!UICONTROL Salvar]**.

![Imagem da interface de usuário da Ativação expandida mostrando a página Adicionar Usuários.](assets/add-user.png)

A conta de usuário agora é criada e atribuída à função correta. Agora está pronto para acessar a interface de usuário **[!UICONTROL Ativação Estendida]**.

## Monitorar o uso da licença {#license-usage}

O contrato [!DNL Audience Manager Expanded Activation] especifica o número máximo de emails com hash que você pode assimilar na sua conta.

Você pode encontrar essas informações na página **[!UICONTROL Administração]** -> **[!UICONTROL Uso da Licença]**.

![Imagem da interface de usuário da Ativação expandida mostrando a tela de uso de licença.](assets/license-usage.png)

Nessa página, você pode encontrar as seguintes informações:

* **[!UICONTROL Produto]**: o produto Adobe para o qual você está licenciado. Esta sempre será **[!UICONTROL Ativação Expandida de Audience Manager]**.
* **[!UICONTROL Métrica primária]**: o nome da métrica que está sendo rastreada para uso. Este sempre será **[!UICONTROL Público-alvo endereçável]**.
* **[!UICONTROL Valor da licença]**: o número máximo de emails com hash que você está licenciado a assimilar.

  >[!TIP]
  >
  >Você assimila emails com hash por meio do [conector de origem do Audience Manager](../sources/connectors/adobe-applications/audience-manager.md). Consulte a documentação sobre [como ativar públicos-alvo](activate-audiences.md) para obter mais detalhes.

* **[!UICONTROL Uso]**: o número de emails com hash assimilados.
* **[!UICONTROL Uso %]**: a porcentagem do valor da sua licença que você usou.

Para saber mais sobre o uso da licença no Experience Platform, consulte a [documentação sobre uso da licença](../dashboards/guides/license-usage.md).

## Próximas etapas {#next-steps}

Agora que você configurou pelo menos uma conta de usuário com o acesso correto à Ativação Estendida, é possível começar a usar a conta para [ativar públicos](activate-audiences.md).
