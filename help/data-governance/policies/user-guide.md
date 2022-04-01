---
keywords: Experience Platform, home, tópicos populares, governança de dados, guia do usuário da política de uso de dados
solution: Experience Platform
title: Gerenciar políticas de uso de dados na interface do usuário
topic-legacy: policies
description: A Governança de dados do Adobe Experience Platform fornece uma interface de usuário que permite criar e gerenciar políticas de uso de dados. Este documento fornece uma visão geral das ações que podem ser executadas no espaço de trabalho Políticas na interface do usuário do Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: 8feb9fbdead75ca7b9ed7e5dcd3a0aab6f328ad5
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 0%

---

# Gerenciar políticas de uso de dados na interface do usuário

A Governança de dados do Adobe Experience Platform fornece uma interface de usuário que permite criar e gerenciar políticas de uso de dados. Este documento fornece uma visão geral das ações que podem ser executadas na **Políticas** na área de trabalho do [!DNL Experience Platform] interface do usuário.

>[!IMPORTANT]
>
>Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para imposição, é necessário habilitar manualmente essa política. Consulte a seção sobre [como ativar políticas](#enable) para obter etapas sobre como fazer isso na interface do usuário do .

## Pré-requisitos

Este guia requer uma compreensão funcional do seguinte [!DNL Experience Platform] conceitos:

* [Governança de dados](../home.md)
* [Políticas de uso de dados](./overview.md)

## Exibir políticas existentes {#view-policies}

No [!DNL Experience Platform] UI, selecione **[!UICONTROL Políticas]** para abrir o **[!UICONTROL Políticas]** espaço de trabalho. No **[!UICONTROL Procurar]** , você pode ver uma lista de políticas disponíveis, incluindo seus rótulos associados, ações de marketing e status.

![](../images/policies/browse-policies.png)

Se você tiver acesso às políticas de consentimento (atualmente em beta), selecione a variável **[!UICONTROL Políticas de consentimento]** alterne para exibi-los na [!UICONTROL Procurar] guia .

![](../images/policies/consent-policy-toggle.png)

Selecione uma política listada para exibir sua descrição e tipo. Se uma política personalizada for selecionada, serão exibidos controles adicionais para editar, excluir ou [ativar/desativar a política](#enable).

![](../images/policies/policy-details.png)

## Criar uma política personalizada {#create-policy}

Para criar uma nova política de uso de dados personalizada, selecione **[!UICONTROL Criar política]** no canto superior direito do **[!UICONTROL Procurar]** na guia no **[!UICONTROL Políticas]** espaço de trabalho.

![](../images/policies/create-policy-button.png)

Dependendo de você fazer parte do beta para políticas de consentimento, uma das seguintes situações ocorre:

* Se você não fizer parte do beta, será direcionado imediatamente para o workflow de [criação de uma política de governança de dados](#create-governance-policy).
* Se você fizer parte do beta, uma caixa de diálogo fornece uma opção extra para [criar uma política de consentimento](#consent-policy).
   ![](../images/policies/choose-policy-type.png)

### Criar uma política de governança de dados {#create-governance-policy}

O **[!UICONTROL Criar política]** workflow é exibido. Comece fornecendo um nome e uma descrição para a nova política.

![](../images/policies/create-policy-description.png)

Em seguida, selecione os rótulos de uso de dados nos quais a política será baseada. Ao selecionar vários rótulos, você tem a opção de escolher se os dados devem conter todos os rótulos ou apenas um deles para que a política seja aplicada. Selecionar **[!UICONTROL Próximo]** quando terminar.

![](../images/policies/add-labels.png)

O **[!UICONTROL Selecionar ações de marketing]** será exibida. Escolha as ações de marketing apropriadas na lista fornecida e selecione **[!UICONTROL Próximo]** para continuar.

>[!NOTE]
>
>Ao selecionar várias ações de marketing, a política as interpreta como uma regra &quot;OU&quot;. Por outras palavras, a política aplica-se se **any** As ações de marketing selecionadas são executadas.

![](../images/policies/add-marketing-actions.png)

O **[!UICONTROL Revisão]** será exibida, permitindo que você revise os detalhes da nova política antes de criá-la. Depois de satisfeito, selecione **[!UICONTROL Concluir]** para criar a política.

![](../images/policies/policy-review.png)

O **[!UICONTROL Procurar]** A guia será exibida novamente, listando agora a política recém-criada no status &quot;Rascunho&quot;. Para ativar a política, consulte a próxima seção.

![](../images/policies/created-policy.png)

### Criar uma política de consentimento (Beta) {#consent-policy}

>[!IMPORTANT]
>
>Atualmente, as políticas de consentimento estão em beta e sua organização pode ainda não ter acesso a elas.

Se você optou por criar uma política de consentimento, será exibida uma nova tela que permite configurar a nova política.

![](../images/policies/consent-policy-dialog.png)

Para usar as políticas de consentimento, você deve ter atributos de consentimento presentes nos dados do perfil. Consulte o guia sobre [processamento de consentimento no Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md) para obter etapas detalhadas sobre como incluir os atributos necessários no esquema de união.

As políticas de consentimento são compostas por dois componentes lógicos:

* **[!UICONTROL If]**: A condição que acionará a verificação de política. Isso pode se basear em uma determinada ação de marketing que está sendo executada, na presença de determinados rótulos de uso de dados ou em uma combinação dos dois.
* **[!UICONTROL Então]**: Os atributos de consentimento que devem estar presentes para um perfil ser incluído na ação que acionou a política.

#### Configurar condições

Em **[!UICONTROL If]** selecione as ações de marketing e/ou rótulos de uso de dados que devem acionar essa política. Selecionar **[!UICONTROL Exibir tudo]** e **[!UICONTROL Selecionar rótulos]** para visualizar as listas completas de ações e rótulos de marketing disponíveis, respectivamente.

Depois de ter adicionado pelo menos uma condição, você pode selecionar **[!UICONTROL Adicionar condição]** para continuar adicionando outras condições conforme necessário, escolha o tipo de condição apropriado na lista suspensa.

![](../images/policies/add-condition.png)

Se você selecionar mais de uma condição, poderá usar o ícone que aparece entre elas para alternar a relação condicional entre &quot;AND&quot; e &quot;OR&quot;.

![](../images/policies/and-or-selection.png)

#### Selecionar atributos de consentimento

Em **[!UICONTROL Então]** selecione pelo menos um atributo de consentimento do schema de união. Esse é o atributo que deve estar presente para que os perfis sejam incluídos na ação regida por essa política. Você pode escolher uma das opções fornecidas na lista ou selecionar **[!UICONTROL Exibir tudo]** para escolher o atributo diretamente do schema de união.

Ao selecionar o atributo de consentimento, escolha os valores para o atributo que deseja que esta política verifique.

![](../images/policies/select-schema-field.png)

Após ter selecionado pelo menos um atributo de consentimento, a variável **[!UICONTROL Propriedades da política]** atualizações do painel para mostrar o número estimado de perfis que seriam permitidos sob esta política, incluindo a porcentagem do armazenamento total de perfis. Essa estimativa é atualizada automaticamente à medida que você ajusta a configuração da política.

![](../images/policies/audience-preview.png)

Para adicionar outros atributos de consentimento à política, selecione **[!UICONTROL Adicionar resultado]**.

![](../images/policies/add-result.png)

Você pode continuar adicionando e ajustando condições e atributos de consentimento à política, conforme necessário. Quando estiver satisfeito com a configuração, forneça um nome e uma descrição opcional para a política antes de selecionar **[!UICONTROL Salvar]**.

![](../images/policies/name-and-save.png)

A política de consentimento foi criada e seu status está definido como [!UICONTROL Desabilitado] por padrão. Para ativar a política imediatamente, selecione o **[!UICONTROL Status]** alternar no painel direito.

![](../images/policies/enable-consent-policy.png)

## Ativar ou desativar uma política {#enable}

Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para imposição, você deve habilitar manualmente essa política por meio da API ou da interface do usuário.

Você pode ativar ou desativar as políticas da **[!UICONTROL Procurar]** na guia no **[!UICONTROL Políticas]** espaço de trabalho. Selecione uma política personalizada na lista para exibir seus detalhes à direita. Em **[!UICONTROL Status]**, selecione o botão de alternância para ativar ou desativar a política.

![](../images/policies/enable-policy.png)

## Exibir ações de marketing {#view-marketing-actions}

No **[!UICONTROL Políticas]** na área de trabalho, selecione o **[!UICONTROL Ações de marketing]** para exibir uma lista das ações de marketing disponíveis definidas pelo Adobe e sua própria organização.

![](../images/policies/marketing-actions.png)

## Criar uma ação de marketing {#create-marketing-action}

Para criar uma nova ação de marketing personalizada, selecione **[!UICONTROL Criar ação de marketing]** no canto superior direito do **[!UICONTROL Ações de marketing]** na guia no **[!UICONTROL Políticas]** espaço de trabalho.

![](../images/policies/create-marketing-action.png)

O **[!UICONTROL Criar ação de marketing]** será exibida. Insira um nome e uma descrição para a ação de marketing e selecione **[!UICONTROL Criar]**.

![](../images/policies/create-marketing-action-details.png)

A ação recém-criada é exibida no **[!UICONTROL Ações de marketing]** guia . Agora você pode usar a ação de marketing ao [criação de novas políticas de uso de dados](#create-policy).

![](../images/policies/created-marketing-action.png)

## Editar ou excluir uma ação de marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Somente as ações de marketing personalizadas definidas pela sua organização podem ser editadas. As ações de marketing definidas pelo Adobe não podem ser alteradas ou excluídas.

No **[!UICONTROL Políticas]** na área de trabalho, selecione o **[!UICONTROL Ações de marketing]** para exibir uma lista das ações de marketing disponíveis definidas pelo Adobe e sua própria organização. Selecione uma ação de marketing personalizada na lista e, em seguida, use os campos fornecidos na seção à direita para editar os detalhes da ação de marketing.

![](../images/policies/edit-marketing-action.png)

Se a ação de marketing não estiver sendo usada por nenhuma política de uso existente, você poderá excluí-la selecionando **[!UICONTROL Excluir ação de marketing]**.

>[!NOTE]
>
>Tentar excluir uma ação de marketing que está sendo usada por uma política existente faz com que uma mensagem de erro seja exibida, indicando que a tentativa de exclusão falhou.

![](../images/policies/delete-marketing-action.png)

## Próximas etapas

Este documento forneceu uma visão geral de como gerenciar políticas de uso de dados no [!DNL Experience Platform] IU. Para obter etapas sobre como gerenciar políticas usando o [!DNL Policy Service API], consulte o [guia do desenvolvedor](../api/getting-started.md). Para obter informações sobre como aplicar políticas de uso de dados, consulte [visão geral da aplicação de políticas](../enforcement/overview.md).

O vídeo a seguir fornece uma demonstração de como trabalhar com políticas de uso no [!DNL Experience Platform] IU:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
