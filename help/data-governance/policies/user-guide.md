---
keywords: Experience Platform;página inicial;tópicos populares;governança de dados;política de uso de dados guia do usuário
solution: Experience Platform
title: Gerenciar políticas de uso de dados na interface
description: O Adobe Experience Platform Data Governance fornece uma interface que permite criar e gerenciar políticas de uso de dados. Este documento fornece uma visão geral das ações que você pode executar no espaço de trabalho Políticas na interface do usuário do Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 16%

---

# Gerenciar políticas de uso de dados na interface {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_description"
>title="Integrar e aplicar o consentimento do cliente nos dados do seu perfil"
>abstract="<h2>Descrição</h2><p>A Experience Platform permite integrar os dados de consentimento coletados dos clientes nos seus respectivos perfis. É possível configurar políticas de consentimento para determinar se esses dados podem ser incluídos em segmentos ativados para determinados destinos.</p>"

Este documento aborda como usar o espaço de trabalho **[!UICONTROL Políticas]** na interface do usuário do Adobe Experience Platform para criar e gerenciar políticas de uso de dados.

>[!NOTE]
>
>Para obter informações sobre como gerenciar políticas de controle de acesso na interface, consulte o [guia da interface do usuário do controle de acesso baseado em atributos](../../access-control/abac/ui/policies.md).

>[!IMPORTANT]
>
>Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para aplicação, você deve ativar manualmente essa política. Consulte a seção sobre [habilitação de políticas](#enable) para obter etapas sobre como fazer isso na interface.

## Pré-requisitos

Este guia requer uma compreensão funcional dos [!DNL Experience Platform] conceitos a seguir:

* [Governança de dados](../home.md)
* [Políticas de uso de dados](./overview.md)

## Exibir políticas existentes {#view-policies}

Na interface do usuário do [!DNL Experience Platform], selecione **[!UICONTROL Políticas]** para abrir o espaço de trabalho **[!UICONTROL Políticas]**. Na guia **[!UICONTROL Procurar]**, você pode ver uma lista de políticas disponíveis, incluindo seus rótulos associados, ações de marketing e status.

![](../images/policies/browse-policies.png)

Se você tiver acesso às políticas de consentimento, selecione a opção **[!UICONTROL Políticas de consentimento]** para exibi-las na guia [!UICONTROL Procurar].

![](../images/policies/consent-policy-toggle.png)

Selecione uma política listada para exibir sua descrição e tipo. Se uma política personalizada for selecionada, controles adicionais serão exibidos para editar, excluir ou [habilitar/desabilitar a política](#enable).

![](../images/policies/policy-details.png)

## Criar uma política personalizada {#create-policy}

Para criar uma nova política de uso de dados personalizada, selecione **[!UICONTROL Criar política]** no canto superior direito da guia **[!UICONTROL Procurar]** no espaço de trabalho **[!UICONTROL Políticas]**.

![](../images/policies/create-policy-button.png)

Dependendo de você fazer parte da versão beta para políticas de consentimento, uma das situações a seguir ocorrerá:

* Se você não fizer parte da versão beta, será redirecionado imediatamente para o fluxo de trabalho para [criar uma política de governança de dados](#create-governance-policy).
* Se você fizer parte da versão beta, uma caixa de diálogo fornecerá uma opção extra para [criar uma política de consentimento](#consent-policy).
  ![](../images/policies/choose-policy-type.png)

### Usar políticas de consentimento e governança de dados em conjunto {#combine-policies}

>[!NOTE]
>
>Atualmente, as políticas de consentimento estão disponíveis apenas para organizações que compraram o Adobe Healthcare Shield ou o Adobe Privacy &amp; Security Shield.

As políticas de governança e consentimento podem ser usadas em conjunto para criar regras robustas para governar públicos mapeados para um destino. As políticas de consentimento são de natureza inclusiva, o que significa que elas determinam quais perfis podem ser incluídos em cada experiência de marketing. Por outro lado, as políticas de governança excluem o uso de atributos específicos rotulados de serem configurados para ativação.

Usando esse comportamento, você pode configurar uma combinação de políticas e regras de consentimento que incluam os perfis corretos, mas o impede de incluir dados que vão contra as regras organizacionais definidas. Um exemplo seria quando você deseja excluir dados confidenciais da inclusão, mas ainda pode direcionar usuários consentidos para marketing via redes sociais. As etapas necessárias para esse cenário estão descritas no infográfico abaixo.

![Um infográfico que descreve as etapas para usar as políticas de governança e consentimento em conjunto para criar regras robustas para os públicos-alvo.](../images/policies/governance-and-consent-policies-infographic.png)

### Criar uma política de governança de dados {#create-governance-policy}

O fluxo de trabalho **[!UICONTROL Criar política]** é exibido. Comece fornecendo um nome e uma descrição para a nova política.

![](../images/policies/create-policy-description.png)

Em seguida, selecione os rótulos de uso de dados nos quais a política será baseada. Ao selecionar vários rótulos, você tem a opção de escolher se os dados devem conter todos os rótulos ou apenas um deles para que a política seja aplicada. Selecione **[!UICONTROL Avançar]** quando terminar.

![](../images/policies/add-labels.png)

A etapa **[!UICONTROL Selecionar ações de marketing]** é exibida. Escolha as ações de marketing apropriadas na lista fornecida e selecione **[!UICONTROL Avançar]** para continuar.

>[!NOTE]
>
>Ao selecionar várias ações de marketing, a política as interpreta como uma regra &quot;OR&quot;. Em outras palavras, a política se aplica se **qualquer** das ações de marketing selecionadas for executada.

![](../images/policies/add-marketing-actions.png)

A etapa **[!UICONTROL Revisar]** é exibida, permitindo que você revise os detalhes da nova política antes de criá-la. Quando estiver satisfeito, selecione **[!UICONTROL Concluir]** para criar a política.

![](../images/policies/policy-review.png)

A guia **[!UICONTROL Procurar]** será exibida novamente, listando agora a política recém-criada no status &quot;Rascunho&quot;. Para habilitar a política, consulte a próxima seção.

![](../images/policies/created-policy.png)

### Criar uma política de consentimento {#consent-policy}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_instructions"
>title="Instruções"
>abstract="<ul><li>Certifique-se de que está assimilando dados de preferência em seus esquemas de união por meio do conector de origem do OneTrust ou do esquema XDM padrão para consentimento.</li><li>Selecione <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=pt-BR">Políticas</a> na navegação à esquerda, e depois <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=pt-BR#create-governance-policy">Criar Política</a>.</li><li>Na seção <b>Se</b>, descreva as condições ou ações que acionarão a verificação de política.</li><li>Na seção <b>Então</b>, insira os atributos de consentimento que devem estar presentes para que um perfil seja incluído na ação que acionou a política.</li><li>Selecionar <b>Salvar</b> para criar a política. Para habilitar a política, selecione o botão de alternância <b>Status</b> no painel direito.</li><li>A Experience Platform aplica automaticamente suas políticas de consentimento ativadas quando você ativa segmentos para destinos e fornece detalhes sobre como cada política afeta o tamanho do público-alvo.</li><li>Para obter mais ajuda com esse recurso, consulte o guia em <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=pt-BR#consent-policy">criação de políticas de consentimento</a> na Experience League.</li></ul>"

>[!IMPORTANT]
>
>As políticas de consentimento só estão disponíveis para organizações que compraram o **Adobe Healthcare Shield** ou o **Adobe Privacy &amp; Security Shield**.

Se você optar por criar uma política de consentimento, uma nova tela será exibida, permitindo configurar a nova política.

![](../images/policies/consent-policy-dialog.png)

Para usar as políticas de consentimento, você deve ter atributos de consentimento presentes nos dados do perfil. Consulte o guia sobre [processamento de consentimento no Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md) para obter etapas detalhadas sobre como incluir os atributos necessários no esquema de união.

As políticas de consentimento são compostas de dois componentes lógicos:

* **[!UICONTROL If]**: a condição que acionará a verificação de política. Isso pode ser baseado em uma determinada ação de marketing que está sendo executada, na presença de determinados rótulos de uso de dados ou em uma combinação dos dois.
* **[!UICONTROL Then]**: os atributos de consentimento que devem estar presentes para que um perfil seja incluído na ação que acionou a política.

#### Configurar condições {#consent-conditions}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentif"
>title="Condição “Se”"
>abstract="Comece definindo as condições que acionarão a verificação de política. As condições podem incluir determinadas ações de marketing que estão sendo executadas, determinados rótulos de governança de dados que estão presentes ou uma combinação de ambos."

Na seção **[!UICONTROL If]**, selecione as ações de marketing e/ou os rótulos de uso de dados que devem acionar esta política. Selecione **[!UICONTROL Exibir todos]** e **[!UICONTROL Selecionar rótulos]** para exibir as listas completas de ações de marketing e rótulos disponíveis, respectivamente.

Depois de adicionar pelo menos uma condição, você pode selecionar **[!UICONTROL Adicionar condição]** para continuar adicionando outras condições conforme necessário, escolhendo o tipo de condição apropriado na lista suspensa.

![](../images/policies/add-condition.png)

Se você selecionar mais de uma condição, poderá usar o ícone que aparece entre elas para alternar o relacionamento condicional entre &quot;AND&quot; e &quot;OR&quot;.

![](../images/policies/and-or-selection.png)

#### Selecionar atributos de consentimento {#consent-attributes}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentthen"
>title="Condição “Então”"
>abstract="Depois que a condição “Se” for definida, use a seção “Então” para selecionar pelo menos um atributo de consentimento do esquema de união. Esse é o atributo que deve estar presente para que os perfis sejam incluídos na ação regida por essa política."

Na seção **[!UICONTROL Then]**, selecione pelo menos um atributo de consentimento do esquema de união. Esse é o atributo que deve estar presente para que os perfis sejam incluídos na ação regida por essa política. Você pode escolher uma das opções fornecidas na lista ou selecionar **[!UICONTROL Exibir tudo]** para escolher o atributo diretamente do esquema de união.

Ao selecionar o atributo de consentimento, escolha os valores para o atributo que você deseja que esta política verifique.

![](../images/policies/select-schema-field.png)

Após selecionar pelo menos um atributo de consentimento, o painel **[!UICONTROL Propriedades da política]** será atualizado para mostrar o número estimado de perfis que seriam permitidos sob esta política, incluindo a porcentagem do armazenamento total do Perfil. Essa estimativa é atualizada automaticamente à medida que você ajusta a configuração da política.

![](../images/policies/audience-preview.png)

Para adicionar outros atributos de consentimento à política, selecione **[!UICONTROL Adicionar resultado]**.

![](../images/policies/add-result.png)

Você pode continuar adicionando e ajustando condições e atributos de consentimento à política, conforme necessário. Quando você estiver satisfeito com a configuração, forneça um nome e uma descrição opcional para a política antes de selecionar **[!UICONTROL Salvar]**.

![](../images/policies/name-and-save.png)

A política de consentimento agora é criada e seu status é definido como [!UICONTROL Desabilitado] por padrão. Para habilitar a política imediatamente, selecione a opção **[!UICONTROL Status]** no painel direito.

![](../images/policies/enable-consent-policy.png)

#### Verificar imposição de política

Depois de criar e habilitar uma política de consentimento, você pode visualizar como ela afeta seus públicos-alvo consentidos ao ativar segmentos para destinos. Consulte a seção sobre [avaliação de política de consentimento](../enforcement/auto-enforcement.md#consent-policy-evaluation) para obter mais informações.

## Ativar ou desativar uma política {#enable}

Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para aplicação, é necessário habilitar manualmente essa política por meio da API ou da interface.

Você pode habilitar ou desabilitar políticas da guia **[!UICONTROL Procurar]** no espaço de trabalho **[!UICONTROL Políticas]**. Selecione uma política personalizada na lista para exibir seus detalhes à direita. Em **[!UICONTROL Status]**, selecione o botão de alternância para habilitar ou desabilitar a política.

![](../images/policies/enable-policy.png)

## Exibir ações de marketing {#view-marketing-actions}

No espaço de trabalho **[!UICONTROL Políticas]**, selecione a guia **[!UICONTROL Ações de marketing]** para exibir uma lista de ações de marketing disponíveis definidas pela Adobe e por sua própria organização.

![](../images/policies/marketing-actions.png)

## Criar uma ação de marketing {#create-marketing-action}

Para criar uma nova ação de marketing personalizada, selecione **[!UICONTROL Criar ação de marketing]** no canto superior direito da guia **[!UICONTROL Ações de marketing]** no espaço de trabalho **[!UICONTROL Políticas]**.

![](../images/policies/create-marketing-action.png)

A caixa de diálogo **[!UICONTROL Criar ação de marketing]** é exibida. Insira um nome e uma descrição para a ação de marketing e selecione **[!UICONTROL Criar]**.

![](../images/policies/create-marketing-action-details.png)

A ação recém-criada aparece na guia **[!UICONTROL Ações de marketing]**. Agora você pode usar a ação de marketing ao [criar novas políticas de uso de dados](#create-policy).

![](../images/policies/created-marketing-action.png)

## Editar ou excluir uma ação de marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Somente ações de marketing personalizadas definidas por sua organização podem ser editadas. As ações de marketing definidas pelo Adobe não podem ser alteradas ou excluídas.

No espaço de trabalho **[!UICONTROL Políticas]**, selecione a guia **[!UICONTROL Ações de marketing]** para exibir uma lista de ações de marketing disponíveis definidas pela Adobe e por sua própria organização. Selecione uma ação de marketing personalizada na lista e, em seguida, use os campos fornecidos na seção à direita para editar os detalhes da ação de marketing.

![](../images/policies/edit-marketing-action.png)

Se a ação de marketing não estiver sendo usada por nenhuma política de uso existente, você poderá excluí-la selecionando **[!UICONTROL Excluir ação de marketing]**.

>[!NOTE]
>
>Tentar excluir uma ação de marketing que está sendo usada por uma política existente faz com que uma mensagem de erro seja exibida, indicando que a tentativa de exclusão falhou.

![](../images/policies/delete-marketing-action.png)

## Próximas etapas

Este documento forneceu uma visão geral de como gerenciar as políticas de uso de dados na interface do usuário do [!DNL Experience Platform]. Para obter etapas sobre como gerenciar políticas usando o [!DNL Policy Service API], consulte o [guia do desenvolvedor](../api/getting-started.md). Para obter informações sobre como impor políticas de uso de dados, consulte a [visão geral de imposição de política](../enforcement/overview.md).

O vídeo a seguir fornece uma demonstração de como trabalhar com políticas de uso na interface do usuário do [!DNL Experience Platform]:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
