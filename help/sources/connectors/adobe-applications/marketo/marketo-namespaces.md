---
title: Namespaces e esquemas B2B
description: Este documento fornece uma visão geral dos namespaces personalizados necessários ao criar um conector de origem B2B.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 923e56098361b4ef42cbbc2395b748033c0e7b94
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 8%

---

# Namespaces e esquemas B2B

>[!AVAILABILITY]
>
>Você deve ter acesso ao [Adobe Real-Time Customer Data Platform B2B edition](../../../../rtcdp/b2b-overview.md) para que seus esquemas B2B sejam qualificados no [Perfil do Cliente em Tempo Real](../../../../profile/home.md).

>[!NOTE]
>
>Você pode usar modelos na interface do usuário do Adobe Experience Platform para agilizar a criação de ativos para dados B2B e B2C. Para obter mais informações, leia o manual sobre [uso de modelos na interface do Experience Platform](../../../tutorials/ui/templates.md).

Leia este documento para obter informações sobre a configuração subjacente dos namespaces e esquemas a serem usados com fontes B2B. Este documento também fornece detalhes sobre a configuração do utilitário de automação do Postman necessário para gerar namespaces B2B e esquemas.

## Configurar namespaces B2B e o utilitário de geração automática de esquema

>[!IMPORTANT]
>
>As credenciais da conta de serviço (JWT) foram substituídas. Você deve garantir a migração do aplicativo ou da integração para a nova credencial OAuth de servidor para servidor antes de 27 de janeiro de 2025. Leia a documentação a seguir para obter as etapas detalhadas sobre [como migrar a credencial JWT para a credencial OAuth Server-to-Server](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Consulte a documentação a seguir para obter as informações de pré-requisito sobre como configurar o ambiente [!DNL Postman] para oferecer suporte ao namespace B2B e ao utilitário de geração automática de esquema.

- Você pode baixar a coleção de utilitários de geração automática de namespace e esquema e o ambiente deste [repositório do GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Para obter informações sobre como usar as APIs do Experience Platform, incluindo detalhes sobre como coletar valores para cabeçalhos necessários e ler chamadas de API de exemplo, consulte o manual em [introdução às APIs do Experience Platform](../../../../landing/api-guide.md).
- Para obter informações sobre como gerar suas credenciais para as APIs do Experience Platform, consulte o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../../landing/api-authentication.md).
- Para obter informações sobre como configurar o [!DNL Postman] para APIs do Experience Platform, consulte o tutorial em [configuração do console do desenvolvedor e [!DNL Postman]](../../../../landing/postman.md).

Com um console de desenvolvedor do Experience Platform e [!DNL Postman] configurados, agora você pode começar a aplicar os valores de ambiente apropriados ao seu ambiente [!DNL Postman].

A tabela a seguir contém valores de exemplo, bem como informações adicionais sobre como preencher o ambiente [!DNL Postman]:

| Variable | Descrição | Exemplo |
| --- | --- | --- |
| `CLIENT_SECRET` | Um identificador exclusivo usado para gerar o `{ACCESS_TOKEN}`. Consulte o tutorial sobre [autenticação e acesso a APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `API_KEY` | Um identificador exclusivo usado para autenticar chamadas para APIs do Experience Platform. Consulte o tutorial sobre [autenticação e acesso a APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | O token de autorização necessário para concluir chamadas para APIs do Experience Platform. Consulte o tutorial sobre [autenticação e acesso a APIs do Experience Platform](../../../../landing/api-authentication.md) para obter informações sobre como recuperar o `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Com relação a [!DNL Marketo], esse valor é fixo e sempre é definido como: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | O container `global` contém todas as classes, grupos de campos de esquema, tipos de dados e esquemas padrão fornecidos pelo parceiro da Adobe e da Experience Platform. Com relação a [!DNL Marketo], esse valor é fixo e sempre é definido como `global`. | `global` |
| `TECHNICAL_ACCOUNT_ID` | Uma credencial usada para integrar ao Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | O Sistema Identity Management (IMS) fornece a estrutura para autenticação de serviços da Adobe. Com relação a [!DNL Marketo], esse valor é fixo e sempre é definido como: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir acesso a seus membros. Consulte o tutorial em [configuração do console do desenvolvedor e [!DNL Postman]](../../../../landing/postman.md) para obter instruções sobre como recuperar as informações de `{ORG_ID}`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | O nome da partição de sandbox virtual que você está usando. | `prod` |
| `TENANT_ID` | Uma ID usada para garantir que os recursos criados tenham o namespace adequado e estejam contidos na organização. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | O endpoint de URL para o qual você está fazendo chamadas de API. Este valor é fixo e está sempre definido como: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### Execução dos scripts

Com a coleção e o ambiente [!DNL Postman] configurados, agora é possível executar o script por meio da interface [!DNL Postman].

Na interface [!DNL Postman], selecione a pasta raiz do utilitário gerador automático e, em seguida, selecione **[!DNL Run]** no cabeçalho superior.

![A pasta raiz do gerador de Namespaces e Esquemas na interface do Postman. &quot;Execuções&quot; está realçado na barra de menu superior.](../images/marketo/root_folder.png)

A interface [!DNL Runner] é exibida. Aqui, verifique se todas as caixas de seleção estão marcadas e selecione **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![A interface Runner da interface do Postman com várias solicitações na coleção Namespaces e Esquemas foi marcada e o botão &quot;Executar Namespaces e Esquemas&quot; foi realçado no lado direito.](../images/marketo/run_generator.png)

Uma solicitação bem-sucedida cria os namespaces e esquemas necessários para o B2B.

## Namespaces B2B

Os namespaces de identidade são um componente de [[!DNL Identity Service]](../../../../identity-service/home.md) que serve para distinguir o contexto de uma identidade. Uma identidade totalmente qualificada inclui um valor de identidade e um namespace. Leia a [visão geral dos namespaces](../../../../identity-service/features/namespaces.md) para obter mais informações.

Os namespaces B2B são usados na identidade principal da entidade.

A tabela a seguir contém informações sobre a configuração subjacente para namespaces B2B.

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Nome de exibição | Símbolo de identidade | Tipo de identidade |
| --- | --- | --- |
| Pessoa B2B | `b2b_person` | `CROSS_DEVICE` |
| Conta B2B | `b2b_account` | `B2B_ACCOUNT` |
| Oportunidade B2B | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| Relação pessoal da oportunidade B2B | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| Campanha B2B | `b2b_campaign` | `B2B_CAMPAIGN` |
| Membro da campanha B2B | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| Lista de marketing B2B | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| Membro da lista de marketing B2B | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| Relação pessoal da conta B2B | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style="table-layout:auto"}

## Esquemas B2B

A Experience Platform usa esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados.

Antes que os dados possam ser assimilados na Experience Platform, um esquema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que podem estar contidos em cada campo. Os esquemas consistem em uma classe base e zero ou mais grupos de campos de esquema.

Para obter mais informações sobre o modelo de composição de esquema, incluindo princípios de design e práticas recomendadas, consulte as [noções básicas da composição de esquema](../../../../xdm/schema/composition.md).

A tabela a seguir contém informações sobre a configuração subjacente de esquemas B2B.

>[!NOTE]
>
>Role a tela para a esquerda/direita para visualizar o conteúdo completo da tabela.

| Nome do esquema | Classe base | Grupos de campos | [!DNL Profile] no esquema | Identidade principal | Namespace de identidade principal | Identidade secundária | Namespace de identidade secundário | Relação | Notas |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Conta B2B | [Conta de negócios XDM](../../../../xdm/classes/b2b/business-account.md) | Detalhes da conta de negócios XDM | Habilitado | `accountKey.sourceKey` na classe base | Conta B2B | `extSourceSystemAudit.externalKey.sourceKey` na classe base | Conta B2B | <ul><li>`accountParentKey.sourceKey` no grupo de campos Detalhes da Conta de Negócios XDM</li><li>Propriedade de destino: `/accountKey/sourceKey`</li><li>Tipo: um para um</li><li>Esquema de referência: Conta B2B</li><li>Namespace: conta B2B</li></ul> |
| Pessoa B2B | [Perfil individual XDM](../../../../xdm/classes/individual-profile.md) | <ul><li>Detalhes de pessoa de negócios XDM</li><li>Componentes de pessoa de negócios XDM</li><li>IdentityMap</li><li>Detalhes sobre consentimento e preferência</li></ul> | Habilitado | `b2b.personKey.sourceKey` no grupo de campos de detalhes de pessoa de negócios XDM | Pessoa B2B | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` do grupo de campos Detalhes de pessoa de negócios XDM</li><li>`workEmail.address` do grupo de campos Detalhes de pessoa de negócios XDM</ol></li> | <ol><li>Pessoa B2B</li><li>Email</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` do grupo de campos Componentes de Pessoa de Negócios XDM</li><li>Tipo: De muitos para um</li><li>Esquema de referência: conta B2B</li><li>Namespace: conta B2B</li><li>Propriedade de destino: accountKey.sourceKey</li><li>Nome do relacionamento do esquema atual: Conta</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> |
| Oportunidade B2B | [Oportunidade de negócios XDM](../../../../xdm/classes/b2b/business-opportunity.md) | Detalhes de oportunidades de negócios XDM | Habilitado | `opportunityKey.sourceKey` na classe base | Oportunidade B2B | `extSourceSystemAudit.externalKey.sourceKey` na classe base | Oportunidade B2B | <ul><li>`accountKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: conta B2B</li><li>Namespace: conta B2B</li><li>Propriedade de destino: `accountKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Conta</li><li>Nome do relacionamento do esquema de referência: Oportunidades</li></ul> |
| Relação pessoal da oportunidade B2B | [Relação pessoal de oportunidade de negócios XDM](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | None | Habilitado | `opportunityPersonKey.sourceKey` na classe base | Relação pessoal da oportunidade B2B | | | **Primeiro relacionamento**<ul><li>`personKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: pessoa B2B</li><li>Namespace: pessoa B2B</li><li>Propriedade de destino: b2b.personKey.sourceKey</li><li>Nome do relacionamento do esquema atual: Pessoa</li><li>Nome do relacionamento do esquema de referência: Oportunidades</li></ul>**Segundo relacionamento**<ul><li>`opportunityKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: Oportunidade B2B </li><li>Namespace: oportunidade B2B </li><li>Propriedade de destino: `opportunityKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Oportunidade</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> |
| Campanha B2B | [Campanha de negócios XDM](../../../../xdm/classes/b2b/business-campaign.md) | Detalhes da campanha de negócios XDM | Habilitado | `campaignKey.sourceKey` na classe base | Campanha B2B | | |
| Membro da campanha B2B | [Membros da campanha de negócios XDM](../../../../xdm/classes/b2b/business-campaign-members.md) | Detalhes do membro da campanha de negócios XDM | Habilitado | `ccampaignMemberKey.sourceKey` na classe base | Membro da campanha B2B | | | **Primeiro relacionamento**<ul><li>`personKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: pessoa B2B</li><li>Namespace: pessoa B2B</li><li>Propriedade de destino: `b2b.personKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Pessoa</li><li>Nome do relacionamento do esquema de referência: Campanhas</li></ul>**Segundo relacionamento**<ul><li>`campaignKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: campanha B2B</li><li>Namespace: campanha B2B</li><li>Propriedade de destino: `campaignKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Campanha</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> |
| Lista de marketing B2B | [Lista de marketing de negócios XDM](../../../../xdm/classes/b2b/business-marketing-list.md) | None | Habilitado | `marketingListKey.sourceKey` na classe base | Lista de marketing B2B | None | None | None | A Lista Estática não está sincronizada a partir de [!DNL Salesforce] e, portanto, não tem uma identidade secundária. |
| Membro da lista de marketing B2B | [Membros da Lista de Marketing Comercial XDM](../../../../xdm/classes/b2b/business-marketing-list-members.md) | None | Habilitado | `marketingListMemberKey.sourceKey` na classe base | Membro da lista de marketing B2B | None | None | **Primeiro relacionamento**<ul><li>`PersonKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: pessoa B2B</li><li>Namespace: pessoa B2B</li><li>Propriedade de destino: `b2b.personKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Pessoa</li><li>Nome do relacionamento do esquema de referência: Listas de marketing</li></ul>**Segundo relacionamento**<ul><li>`marketingListKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: Lista de marketing B2B</li><li>Namespace: lista de marketing B2B</li><li>Propriedade de destino: `marketingListKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Lista de marketing</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> | O membro da lista estática não é sincronizado a partir de [!DNL Salesforce] e, portanto, não tem uma identidade secundária. |
| Relação pessoal da conta B2B | [Relação pessoal da conta comercial XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) | Mapa de identidade | Habilitado | `accountPersonKey.sourceKey` na classe base | Relação pessoal da conta B2B | None | None | **Primeiro relacionamento**<ul><li>`personKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: pessoa B2B</li><li>Namespace: pessoa B2B</li><li>Propriedade de destino: `b2b.personKey.SourceKey`</li><li>Nome do relacionamento do esquema atual: People</li><li>Nome do relacionamento do esquema de referência: Conta</li></ul>**Segundo relacionamento**<ul><li>`accountKey.sourceKey` na classe base</li><li>Tipo: De muitos para um</li><li>Esquema de referência: conta B2B</li><li>Namespace: conta B2B</li><li>Propriedade de destino: `accountKey.sourceKey`</li><li>Nome do relacionamento do esquema atual: Conta</li><li>Nome do relacionamento do esquema de referência: Pessoas</li></ul> |

{style="table-layout:auto"}

## Próximas etapas

Para saber como conectar seus dados do [!DNL Marketo] ao Experience Platform, consulte o tutorial sobre [criação de um conector de origem do Marketo na interface](../../../tutorials/ui/create/adobe-applications/marketo.md).

<!--

| B2B Activity | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>Visit WebPage</li><li>New Lead</li><li>Convert Lead</li><li>Add To List</li><li>Remove From List</li><li>Add To Opportunity</li><li>Remove From Opportunity</li><li>Form Filled Out</li><li>Link Clicks</li><li>Email Delivered</li><li>Email Opened</li><li>Email Clicked</li><li>Email Bounced</li><li>Email Bounced Soft</li><li>Email Unsubscribed</li><li>Score Changed</li><li>Opportunity Updated</li><li>Status in Campaign Progression Changed</li><li>Person Identifier</li><li>Marketo Web URL</li><li>Interesting Moment</li><li>Call Webhook</li><li>Change Campaign Cadence</li><li>Revenue Stage Changed</li><li>Merge Leads</li><li>Email Sent</li><li>Change Campaign Stream</li><li>Add to Campaign</li></ul> | Enabled | `personKey.sourceKey` of Person Identifier field group | B2B Person | None | None | | `ExperienceEvent` is different from entities. The identity of experience event is the person who did the activity. |

-->