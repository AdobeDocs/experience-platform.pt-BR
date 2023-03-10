---
keywords: Experience Platform;página inicial;tópicos populares;governança de dados;política de uso de dados guia do usuário
solution: Experience Platform
title: Gerenciar políticas de uso de dados na interface
description: O Adobe Experience Platform Data Governance fornece uma interface que permite criar e gerenciar políticas de uso de dados. Este documento fornece uma visão geral das ações que você pode executar no espaço de trabalho Políticas, na interface do usuário do Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: e539b1e165227d9a888bfe12d8205e285b3ce259
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# Gerenciar políticas de uso de dados na interface {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_description"
>title="Descrição"
>abstract=""

Este documento aborda como usar o **[!UICONTROL Políticas]** na interface do usuário do Adobe Experience Platform para criar e gerenciar políticas de uso de dados.

>[!NOTE]
>
>Para obter informações sobre como gerenciar políticas de controle de acesso na interface, consulte [guia da interface do usuário do controle de acesso baseado em atributos](../../access-control/abac/ui/policies.md) em vez disso.

>[!IMPORTANT]
>
>Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para aplicação, você deve ativar manualmente essa política. Consulte a seção sobre [ativando políticas](#enable) para obter etapas sobre como fazer isso na interface do usuário.

## Pré-requisitos

Este guia requer o entendimento prático do seguinte [!DNL Experience Platform] conceitos:

* [Governança de dados](../home.md)
* [Políticas de uso de dados](./overview.md)

## Exibir políticas existentes {#view-policies}

No [!DNL Experience Platform] Interface, selecione **[!UICONTROL Políticas]** para abrir o **[!UICONTROL Políticas]** espaço de trabalho. No **[!UICONTROL Procurar]** você poderá ver uma lista de políticas disponíveis, incluindo seus rótulos associados, ações de marketing e status.

![](../images/policies/browse-policies.png)

Se você tiver acesso às políticas de consentimento, selecione a **[!UICONTROL Políticas de consentimento]** alternar para visualizá-los no [!UICONTROL Procurar] guia.

![](../images/policies/consent-policy-toggle.png)

Selecione uma política listada para exibir sua descrição e tipo. Se uma política personalizada for selecionada, controles adicionais serão exibidos para editar, excluir ou [ativar/desativar a política](#enable).

![](../images/policies/policy-details.png)

## Criar uma política personalizada {#create-policy}

Para criar uma nova política de uso de dados personalizada, selecione **[!UICONTROL Criar política]** no canto superior direito da **[!UICONTROL Procurar]** na guia **[!UICONTROL Políticas]** espaço de trabalho.

![](../images/policies/create-policy-button.png)

Dependendo de você fazer parte da versão beta para políticas de consentimento, uma das situações a seguir ocorrerá:

* Se você não fizer parte da versão beta, será imediatamente direcionado ao fluxo de trabalho para [criação de uma política de governança de dados](#create-governance-policy).
* Se você fizer parte da versão beta, uma caixa de diálogo fornecerá uma opção extra para [criar uma política de consentimento](#consent-policy).
   ![](../images/policies/choose-policy-type.png)

### Criar uma política de governança de dados {#create-governance-policy}

A variável **[!UICONTROL Criar política]** workflow aparece. Comece fornecendo um nome e uma descrição para a nova política.

![](../images/policies/create-policy-description.png)

Em seguida, selecione os rótulos de uso de dados nos quais a política será baseada. Ao selecionar vários rótulos, você tem a opção de escolher se os dados devem conter todos os rótulos ou apenas um deles para que a política seja aplicada. Selecionar **[!UICONTROL Próxima]** quando terminar.

![](../images/policies/add-labels.png)

A variável **[!UICONTROL Selecionar ações de marketing]** é exibida. Escolha as ações de marketing apropriadas na lista fornecida e selecione **[!UICONTROL Próxima]** para continuar.

>[!NOTE]
>
>Ao selecionar várias ações de marketing, a política as interpreta como uma regra &quot;OR&quot;. Em outras palavras, a política se aplica se **qualquer** das ações de marketing selecionadas são executadas.

![](../images/policies/add-marketing-actions.png)

A variável **[!UICONTROL Revisão]** será exibida, permitindo que você revise os detalhes da nova política antes de criá-la. Quando estiver satisfeito, selecione **[!UICONTROL Concluir]** para criar a política.

![](../images/policies/policy-review.png)

A variável **[!UICONTROL Procurar]** será exibida novamente, listando agora a política recém-criada no status &quot;Rascunho&quot;. Para habilitar a política, consulte a próxima seção.

![](../images/policies/created-policy.png)

### Criar uma política de consentimento {#consent-policy}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_instructions"
>title="Instruções"
>abstract=""

>[!IMPORTANT]
>
>As políticas de consentimento só estão disponíveis para organizações que compraram **Adobe Healthcare Shield** ou **Proteção de segurança e privacidade do Adobe**.

Se você optar por criar uma política de consentimento, uma nova tela será exibida, permitindo configurar a nova política.

![](../images/policies/consent-policy-dialog.png)

Para usar as políticas de consentimento, você deve ter atributos de consentimento presentes nos dados do perfil. Consulte o guia sobre [processamento de consentimento no Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md) para obter etapas detalhadas sobre como incluir os atributos necessários no esquema de união.

As políticas de consentimento são compostas de dois componentes lógicos:

* **[!UICONTROL Se]**: A condição que acionará a verificação de política. Isso pode ser baseado em uma determinada ação de marketing que está sendo executada, na presença de determinados rótulos de uso de dados ou em uma combinação dos dois.
* **[!UICONTROL Depois]**: os atributos de consentimento que devem estar presentes para que um perfil seja incluído na ação que acionou a política.

#### Configurar condições {#consent-conditions}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentif"
>title="Condição If"
>abstract="Comece definindo as condições que acionarão a verificação de política. As condições podem incluir determinadas ações de marketing, a presença de determinados rótulos de governança de dados ou uma combinação de ambos."

No **[!UICONTROL Se]** selecione as ações de marketing e/ou os rótulos de uso de dados que devem acionar essa política. Selecionar **[!UICONTROL Exibir todos]** e **[!UICONTROL Selecionar rótulos]** para visualizar as listas completas de ações e rótulos de marketing disponíveis, respectivamente.

Depois de adicionar pelo menos uma condição, você pode selecionar **[!UICONTROL Adicionar condição]** para continuar adicionando outras condições conforme necessário, escolha o tipo de condição apropriado na lista suspensa.

![](../images/policies/add-condition.png)

Se você selecionar mais de uma condição, poderá usar o ícone que aparece entre elas para alternar o relacionamento condicional entre &quot;AND&quot; e &quot;OR&quot;.

![](../images/policies/and-or-selection.png)

#### Selecionar atributos de consentimento {#consent-attributes}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentthen"
>title="Condição Then"
>abstract="Depois que a condição &quot;If&quot; for definida, use a seção &quot;Then&quot; para selecionar pelo menos um atributo de consentimento do esquema de união. Esse é o atributo que deve estar presente para que os perfis sejam incluídos na ação regida por essa política."

No **[!UICONTROL Depois]** selecione pelo menos um atributo de consentimento do esquema de união. Esse é o atributo que deve estar presente para que os perfis sejam incluídos na ação regida por essa política. Você pode escolher uma das opções fornecidas na lista ou selecionar **[!UICONTROL Exibir todos]** para escolher o atributo diretamente do esquema de união.

Ao selecionar o atributo de consentimento, escolha os valores para o atributo que você deseja que esta política verifique.

![](../images/policies/select-schema-field.png)

Após selecionar pelo menos um atributo de consentimento, a variável **[!UICONTROL Propriedades da política]** atualizações do painel para mostrar o número estimado de perfis que seriam permitidos sob esta política, incluindo a porcentagem do armazenamento total do perfil. Essa estimativa é atualizada automaticamente à medida que você ajusta a configuração da política.

![](../images/policies/audience-preview.png)

Para adicionar mais atributos de consentimento à política, selecione **[!UICONTROL Adicionar resultado]**.

![](../images/policies/add-result.png)

Você pode continuar adicionando e ajustando condições e atributos de consentimento à política, conforme necessário. Quando estiver satisfeito com a configuração, forneça um nome e uma descrição opcional para a política antes de selecionar **[!UICONTROL Salvar]**.

![](../images/policies/name-and-save.png)

A política de consentimento agora é criada e seu status é definido como [!UICONTROL Desabilitado] por padrão. Para ativar a política imediatamente, selecione o **[!UICONTROL Status]** no painel direito.

![](../images/policies/enable-consent-policy.png)

#### Verificar imposição de política

Depois de criar e habilitar uma política de consentimento, você pode visualizar como ela afeta seus públicos-alvo consentidos ao ativar segmentos para destinos. Consulte a seção sobre [avaliação da política de consentimento](../enforcement/auto-enforcement.md#consent-policy-evaluation) para obter mais informações.

## Ativar ou desativar uma política {#enable}

Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para aplicação, é necessário habilitar manualmente essa política por meio da API ou da interface.

Você pode ativar ou desativar políticas na **[!UICONTROL Procurar]** na guia **[!UICONTROL Políticas]** espaço de trabalho. Selecione uma política personalizada na lista para exibir seus detalhes à direita. Em **[!UICONTROL Status]**, selecione o botão de alternância para ativar ou desativar a política.

![](../images/policies/enable-policy.png)

## Exibir ações de marketing {#view-marketing-actions}

No **[!UICONTROL Políticas]** selecione o **[!UICONTROL Ações de marketing]** para ver uma lista de ações de marketing disponíveis definidas pelo Adobe e por sua própria organização.

![](../images/policies/marketing-actions.png)

## Criar uma ação de marketing {#create-marketing-action}

Para criar uma nova ação de marketing personalizada, selecione **[!UICONTROL Criar ação de marketing]** no canto superior direito da **[!UICONTROL Ações de marketing]** na guia **[!UICONTROL Políticas]** espaço de trabalho.

![](../images/policies/create-marketing-action.png)

A variável **[!UICONTROL Criar ação de marketing]** será exibida. Insira um nome e uma descrição para a ação de marketing e selecione **[!UICONTROL Criar]**.

![](../images/policies/create-marketing-action-details.png)

A ação recém-criada aparece na variável **[!UICONTROL Ações de marketing]** guia. Agora você pode usar a ação de marketing quando [criação de novas políticas de uso de dados](#create-policy).

![](../images/policies/created-marketing-action.png)

## Editar ou excluir uma ação de marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Somente ações de marketing personalizadas definidas por sua organização podem ser editadas. As ações de marketing definidas pelo Adobe não podem ser alteradas ou excluídas.

No **[!UICONTROL Políticas]** selecione o **[!UICONTROL Ações de marketing]** para ver uma lista de ações de marketing disponíveis definidas pelo Adobe e por sua própria organização. Selecione uma ação de marketing personalizada na lista e, em seguida, use os campos fornecidos na seção à direita para editar os detalhes da ação de marketing.

![](../images/policies/edit-marketing-action.png)

Se a ação de marketing não estiver sendo usada por nenhuma política de uso existente, é possível excluí-la selecionando **[!UICONTROL Excluir ação de marketing]**.

>[!NOTE]
>
>Tentar excluir uma ação de marketing que está sendo usada por uma política existente faz com que uma mensagem de erro seja exibida, indicando que a tentativa de exclusão falhou.

![](../images/policies/delete-marketing-action.png)

## Próximas etapas

Este documento forneceu uma visão geral de como gerenciar as políticas de uso de dados no [!DNL Experience Platform] IU. Para obter etapas sobre como gerenciar políticas usando o [!DNL Policy Service API], consulte o [guia do desenvolvedor](../api/getting-started.md). Para obter informações sobre como aplicar políticas de uso de dados, consulte a [visão geral da aplicação de políticas](../enforcement/overview.md).

O vídeo a seguir fornece uma demonstração de como trabalhar com políticas de uso no [!DNL Experience Platform] Interface do usuário:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
